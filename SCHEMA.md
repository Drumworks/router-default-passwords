# Schema

Two generated data files share one row shape:

- `routers.csv` — 312 rows, 18 columns, header row first, RFC 4180 quoting, LF line endings, UTF-8.
- `routers.json` — an object with licence and provenance keys plus `routers`, an array of the same
  312 objects in the same order and with the same key order as the CSV columns.

Rows are sorted by `brand`, then `model`, then `slug`, using an `en` collation with
case-insensitive comparison. The sort is fixed so that a diff between two exports shows only what
changed in the data.

## Null

In `routers.json`, a field with no value is `null`. In `routers.csv`, it is an empty cell. Empty
string and null are the same thing here; there is no field where an empty string carries meaning
of its own.

A null is never a placeholder for a value that exists and is unknown. If a model's default
password could not be established from the manufacturer's own documentation, the model is not in
this dataset at all.

## Fields

### `slug`
String, always present, unique. The stable identifier for the model, and the last path segment of
its page: `https://ssid.ai/routers/{slug}`. Lowercase, hyphenated. Example: `netgear-nighthawk-r7000`.

### `brand`
String, always present. The manufacturer or ISP as ssid.ai records it: `TP-Link`, `Netgear`, `AVM`,
`Virgin Media`. 83 distinct values.

### `model`
String, always present. The model name without the brand prefix. Example: `Nighthawk R7000
(AC1900)`. May name a family rather than a single SKU where the manufacturer documents them
together, in which case `credential_note` says so.

### `category`
String, always present. One of:

| Value | Count | Meaning |
| --- | --- | --- |
| `router` | 153 | Standalone consumer or prosumer router |
| `gateway` | 83 | ISP-supplied or combined modem-router |
| `mesh` | 46 | Multi-node mesh system |
| `ap` | 11 | Access point |

### `default_gateway_ip`
String or null. The IPv4 address the admin interface answers on out of the box, e.g.
`192.168.1.1`. Present on 275 of 312 rows. Null means the model has no documented default admin
IP, which is normal for `app-only` models: they have no web interface.

### `default_login_host`
String or null. A hostname the admin interface also answers on, e.g. `tplinkwifi.net`,
`routerlogin.net`, `fritz.box`. Present on 161 rows. Usually more reliable than the IP, because it
keeps working after the LAN subnet is changed. Null means the manufacturer publishes no such
hostname.

### `default_username`
String or null. The factory admin username. Present on 153 rows. Null means one of two things,
and `credential_note` says which: the login screen has no username field at all (common on
password-only interfaces such as TP-Link and Linksys), or the model has no web login.

### `default_password`
String or null. The factory admin password, **only ever populated when `credential_type` is
`static`** — that is, when the same password is documented for every unit shipped. Present on 78
rows.

Null on the other 215, and the null is itself the answer. For 210 of those, there is no universal
default password to publish; `credential_type` says why. For the remaining 5, the universal default
is an empty password, and `default_password_blank` is `true`.

### `default_password_blank`
Boolean, always present. `true` on 5 rows. It exists because `null` alone cannot distinguish "there
is no universal default password" from "the universal default password is an empty field".

`true` means the manufacturer documents an empty password field as the shipped factory state: you
log in by leaving the box blank. Those five are three D-Link models where the documented login is
`admin` with no password, and two Belkin families that ship with the admin dashboard unlocked.

Invariant, enforced at export: when `credential_type` is `static`, either `default_password` is
non-null or `default_password_blank` is `true`. Never both, never neither. When `credential_type`
is anything else, `default_password` is null and `default_password_blank` is `false`.

### `credential_type`
String, always present, one of four values. This is the field that tells you how to read a null
password.

| Value | Count | Meaning |
| --- | --- | --- |
| `static` | 83 | A universal default: the same credential on every unit of that model. `default_password` holds it, or `default_password_blank` is `true`. |
| `set-on-setup` | 96 | No universal default. The router requires the owner to create an admin password during first-time setup, and after every factory reset. |
| `label-unique` | 76 | No universal default. Each unit ships with its own password, printed on a sticker or card that comes with the device. |
| `app-only` | 38 | No web admin login exists. Administration goes through a vendor mobile app or a cloud account. |

The enum matches the `credType` field returned by the ssid.ai API and the `ssid-mcp` server, so a
consumer can move between this file and the live feed without remapping.

`unknown` is a fifth value defined in the ssid.ai codebase for rows whose type has not been
classified. It appears in `compliance.json`'s `by_credential_type` histogram as a zero. No row in
this dataset carries it, and the exporter fails rather than publishing one.

### `credential_note`
String, always present. A model-specific explanation in plain language: why there is no default
password, what the label looks like, which hardware revisions differ, what the common wrong answer
is. This is the field to read before acting on a `medium`-confidence row.

### `reset_steps`
String, always present. How to factory-reset that specific model, and what the login state is
afterwards. Written per model, not templated.

### `source_url`
String, always present, always `https`. The manufacturer's own page, support article or manual PDF
that establishes the credential values in this row. 99 distinct domains across the dataset. Never
a forum, an aggregator or another password list.

### `source_name`
String, always present. A human-readable name for the source, e.g. `NETGEAR official KB 24340
(R7000 factory defaults)`.

### `source_archive_url`
String or null. A Wayback Machine copy of `source_url`, captured at verification time, so the claim
stays checkable after the manufacturer reorganises their site. Present on 81 rows. Archiving began
after the directory did and runs only on new or changed rows, so a null here means "not archived
yet", not "unsourced".

### `confidence`
String, always present. `high` on 201 rows, `medium` on 92.

`high` means the cited source states the login behaviour for that model directly. `medium` means
the source covers the model family rather than that exact SKU, or hardware revisions of the same
model name are known to differ. `credential_note` explains the specific reservation.

### `last_verified`
Date, `YYYY-MM-DD`, always present. The date of the most recent ssid.ai ingest run that recorded
this row's credential fields against the cited source.

Precisely: ssid.ai keeps an append-only observation log (`device_versions`). Every run appends one
observation per model, typed `added`, `changed` or `verified_unchanged`. `last_verified` is the
date of the latest such observation for this slug. It tells you when the row was last confirmed to
hold these values, and a `changed` observation in that log is what a corrected credential looks
like historically.

### `ssid_url`
String, always present. The model's page on ssid.ai, where the same values are shown with the
source cited inline: `https://ssid.ai/routers/{slug}`.

## `compliance.json`

An aggregation of the same 312 rows. It makes no claim that is not already in `routers.json`.

| Key | Type | Meaning |
| --- | --- | --- |
| `generated_at` | date | When this snapshot was computed |
| `model_count` | int | Models in the index (312) |
| `by_credential_type` | object | Histogram over the enum above, including a zero `unknown` bucket |
| `no_universal_default_pct` | int | Percentage of models that are not `static`, rounded (72) |
| `universal_default_pct` | int | Percentage that are `static`, rounded (28) |
| `by_brand` | array | Per brand: `brand`, `models`, `universal_default_models`, `no_universal_default` (true when zero of that brand's models are `static`). Sorted by `universal_default_models` descending, then `models` descending. |
| `still_shipping_universal_default` | array | Every `static` model, with `brand`, `model`, `slug`, `default_username`, `default_password`, `source_url`, `source_name`, `ssid_url`. Sorted by brand. |

The always-current version of this index is <https://ssid.ai/compliance/data.json>. Its key names
follow the ssid.ai API's camelCase convention; this file uses snake_case to match the CSV columns.

## Regenerating

These files are generated from the ssid.ai spine, which is the same store behind the website, the
REST API and the MCP server. The generator sorts deterministically and runs an integrity gate that
aborts the export if any row breaks the rules above: a non-`https` source, a duplicate slug, an
`unknown` credential type, a password on a non-`static` row, a `static` row with neither a password
nor a blank flag, or a row with no verification observation.
