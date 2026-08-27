# Router default passwords and login IPs

<!-- generated:headline -->
An open dataset of **391 router, gateway, mesh and access-point models** with, for each one: the
default login IP, the default admin username, the default password (or an explicit reason there is
no universal one), the credential type, factory-reset steps, and the manufacturer URL the values
came from.
<!-- /generated:headline -->

Published by [ssid.ai](https://ssid.ai). Licensed **CC BY 4.0** — use it commercially, redistribute
it, build on it. Just credit ssid.ai.

<!-- generated:generated-at -->
Generated 2026-08-27 from the live directory at <https://ssid.ai/routers>.
<!-- /generated:generated-at -->

## Files

<!-- generated:files-table -->
| File | What it holds |
| --- | --- |
| `routers.csv` | 391 rows, 18 columns, RFC 4180, LF line endings |
| `routers.json` | The same 391 rows, with a licence and provenance header |
| `compliance.json` | The Router Default-Credential Compliance Index: share of models with no universal default password, by brand |
| `SCHEMA.md` | Every field defined, including the four `credential_type` values |
| `LICENSE` | CC BY 4.0, and what attribution means here |
<!-- /generated:files-table -->

## What is the default password for a router?

For most models sold today there isn't one. That single fact is what the old default-password lists
get wrong, and it is why this dataset has a `credential_type` column instead of filling every
password cell with `admin`.

<!-- generated:cred-mix -->
Of the 391 models here, **286 have no universal default password**:

- 120 are `set-on-setup` — the router makes you create the password the first time you configure it.
- 118 are `label-unique` — every unit ships with a different password, printed on a sticker on the device.
- 48 are `app-only` — there is no web admin at all; you sign in to a phone app or a cloud account.

The other **105 models do ship a universal default**, and this dataset gives it to you. 99 of them
have a documented password string. 6 have a documented blank password: the field is empty out of
the box, which still counts as a universal default, of nothing.
<!-- /generated:cred-mix -->

### By brand

<!-- generated:brand-table -->
| Brand | Models | The answer |
| --- | --- | --- |
| TP-Link | 40 | 4 of 40 still ship a universal default; the other 36 do not (22 `set-on-setup`, 13 `app-only`, 1 `label-unique`). |
| Netgear | 37 | 15 of 37 still ship a universal default; the other 22 do not (21 `set-on-setup`, 1 `label-unique`). |
| ASUS | 27 | 1 of 27 still ships a universal default; the other 26 do not (26 `set-on-setup`). |
| Linksys | 15 | 9 of 15 still ship a universal default; the other 6 do not (6 `app-only`). |
| D-Link | 13 | 8 of 13 still ship a universal default; the other 5 do not (3 `label-unique`, 2 `set-on-setup`). |
| Ubiquiti | 13 | 6 of 13 still ship a universal default; the other 7 do not (4 `app-only`, 3 `set-on-setup`). |
| AVM | 12 | No universal default on any of the 12: 11 `label-unique`, 1 `set-on-setup`. |
| MikroTik | 10 | 1 of 10 still ships a universal default; the other 9 do not (7 `label-unique`, 2 `set-on-setup`). |
| Zyxel | 10 | 5 of 10 still ship a universal default; the other 5 do not (2 `set-on-setup`, 2 `label-unique`, 1 `app-only`). |
| Peplink | 9 | All 9 ship a universal default password. |
| Grandstream | 8 | No universal default on any of the 8: 8 `label-unique`. |
| Tenda | 7 | No universal default on any of the 7: 4 `label-unique`, 2 `set-on-setup`, 1 `app-only`. |
| DrayTek | 6 | All 6 ship a universal default password. |
| Keenetic | 6 | No universal default on any of the 6: 6 `set-on-setup`. |
<!-- /generated:brand-table -->

Full per-model rows are in `routers.csv` / `routers.json`. Each has a human-readable
`credential_note` explaining that model's specific behaviour, and a `source_url` you can check.

## What is the default login IP for a router?

<!-- generated:gateway-ips -->
Across the 391 models, 34 distinct default gateway IPs. The distribution:

| Default gateway IP | Models | Common on |
| --- | --- | --- |
| 192.168.1.1 | 129 | Netgear, Linksys, Ubiquiti, Keenetic |
| 192.168.0.1 | 73 | TP-Link, D-Link, Tenda, Claro Brasil |
| 192.168.50.1 | 27 | ASUS, Peplink |
| 192.168.1.254 | 11 | AT&T, EE, Plusnet, BT |
| 192.168.178.1 | 10 | AVM |
| 192.168.88.1 | 10 | MikroTik |
| 192.168.100.1 | 9 | Netgear, ARRIS, H3C, Motorola |
| 192.168.2.1 | 9 | Deutsche Telekom, Belkin, Bell, Edimax |

218 models also answer on a hostname (`tplinkwifi.net`, `routerlogin.net`, `router.asus.com`,
`fritz.box`), which is in the `default_login_host` column and usually more reliable than typing the
IP.

53 models have **no** admin IP at all. 33 of those are `app-only`: an eero or a Google Nest Wifi
has no web interface to log into, so a list that prints an IP for them is guessing. The other 20
are models whose manufacturer publishes a hostname or a DHCP-assigned address instead.
<!-- /generated:gateway-ips -->

## Which routers still ship a universal default password?

<!-- generated:compliance -->
**105 of 391 models (27%).** Put the other way: 73% no longer do, as of 2026-08-27. That number is
the Router Default-Credential Compliance Index, and `compliance.json` carries the full breakdown
plus every one of the 105 models with its username, password and source.

Brands with the most models still shipping a universal default:

| Brand | Models tracked | Still universal-default |
| --- | --- | --- |
| Netgear | 37 | 15 |
| Linksys | 15 | 9 |
| Peplink | 9 | 9 |
| D-Link | 13 | 8 |
| Ubiquiti | 13 | 6 |
| DrayTek | 6 | 6 |
| Netgate | 6 | 6 |
| Zyxel | 10 | 5 |

77 of the 114 brands tracked have no model here that ships a universal default.
<!-- /generated:compliance -->

Why this is measurable at all: the UK's Product Security and Telecommunications Infrastructure Act
has banned universal default passwords on consumer connectable products supplied in the UK since
April 2024, and the EU Cyber Resilience Act and the RED delegated act push the same way. `static`
is the pattern those regimes target. A `static` row here is a statement about what the
manufacturer documents for that model, not a legal finding about that product. Plenty of the static
rows are older hardware that predates the rules or is sold outside their scope.

The live version of this index, updated as the directory grows, is at
<https://ssid.ai/compliance> and <https://ssid.ai/compliance/data.json>.

## How the data is sourced

Every row comes from the manufacturer's own documentation: their domain, their support KB, or
their official manual PDF. Never a forum, never an aggregator, never another password list.

<!-- generated:sourcing -->
- All 391 rows carry an `https` `source_url`, drawn from 131 distinct manufacturer and ISP domains.
- A model that cannot be verified against an official source is excluded from the directory
  rather than guessed at. That is why the count is 391 and not 30,000.
- 292 rows are marked `confidence: high` (the source states the behaviour directly). 99 are
  `medium`, usually because the manufacturer documents a family rather than that exact SKU, or
  because hardware revisions of the same model differ. The `credential_note` says which.
<!-- /generated:sourcing -->
<!-- generated:archive-sourcing -->
- 156 rows also carry `source_archive_url`, a Wayback Machine copy of the cited page, so the
  claim stays checkable after the manufacturer reorganises their site. A daily job works
  through the rest, so the other 235 are queued rather than skipped. All 391 are sourced
  either way — the archive is a second copy of the evidence, never the only one.
<!-- /generated:archive-sourcing -->
- A null password is a real answer. Writing `admin` / `admin` for a router that forces a password
  at setup is worse than writing nothing, because someone acts on it, fails, and factory-resets a
  working router for no reason.

## How to use it

Download the file:

```bash
curl -O https://raw.githubusercontent.com/Drumworks/router-default-passwords/main/routers.csv
curl -O https://raw.githubusercontent.com/Drumworks/router-default-passwords/main/routers.json
```

Look up one model in the shell:

```bash
jq '.routers[] | select(.slug == "netgear-nighthawk-r7000")' routers.json
```

Which returns, with the longer text fields left out here for width:

```json
{
  "slug": "netgear-nighthawk-r7000",
  "brand": "Netgear",
  "model": "Nighthawk R7000 (AC1900)",
  "category": "router",
  "default_gateway_ip": "192.168.1.1",
  "default_login_host": "routerlogin.net",
  "default_username": "admin",
  "default_password": "password",
  "default_password_blank": false,
  "credential_type": "static",
  "source_url": "https://kb.netgear.com/24340/What-are-the-factory-default-settings-on-my-Nighthawk-R7000-router-and-how-do-I-reset-to-default",
  "confidence": "high",
  "last_verified": "2026-08-08",
  "ssid_url": "https://ssid.ai/routers/netgear-nighthawk-r7000"
}
```

Find every model that still ships a universal default:

```bash
jq -r '.routers[] | select(.credential_type == "static") | [.brand, .model, .default_username, .default_password] | @tsv' routers.json
```

Load the CSV in pandas:

```python
import pandas as pd
df = pd.read_csv("routers.csv")
df[df.credential_type == "static"][["brand", "model", "default_username", "default_password"]]
```

Other ways to reach the same data:

- **Per-model web page**, with the source cited inline: `https://ssid.ai/routers/{slug}` — e.g.
  <https://ssid.ai/routers/netgear-nighthawk-r7000>
- **Per-brand hub**: `https://ssid.ai/routers/brand/{brand}`
- **Per-gateway-IP hub**: `https://ssid.ai/routers/ip/{ip}` — every model that defaults to, say,
  <https://ssid.ai/routers/ip/192.168.1.1>
- **REST API**, free tier, no key required: <https://ssid.ai/api-docs>
- **MCP server** for assistants and agents: [`ssid-mcp`](https://www.npmjs.com/package/ssid-mcp) —
  `npx -y ssid-mcp`
- **Live compliance feed**: <https://ssid.ai/compliance/data.json>

## Fields

<!-- generated:fields-count -->
18 columns. `SCHEMA.md` defines each one. The two that matter most:
<!-- /generated:fields-count -->

`credential_type` is one of four values, and it is how you read a null password:

| Value | Meaning |
| --- | --- |
| `static` | A universal default that is the same on every unit. `default_password` holds it, or `default_password_blank` is `true` when the documented default is an empty field. |
| `set-on-setup` | No universal default. The owner creates the password during first-time setup. |
| `label-unique` | No universal default. Each unit ships with its own password, printed on the device. |
| `app-only` | No web admin login. Access is through a vendor app or cloud account. |

<!-- generated:blank-password -->
`default_password_blank` exists because `null` alone cannot distinguish "there is no universal
default" from "the universal default is an empty password". 6 models are the latter: the
documented login is a username with the password field left empty, or the admin dashboard ships
unlocked.
<!-- /generated:blank-password -->

## Known gaps

Where the data is thin, here is where:

<!-- generated:gaps -->
- **53 models have no `default_gateway_ip`.** 33 are `app-only` and genuinely have no admin IP.
  The remaining 20 are models whose manufacturer documents a hostname or DHCP-assigned address
  instead.
- **173 models have no `default_login_host`.** Most manufacturers publish only an IP.
<!-- /generated:gaps -->
<!-- generated:archive-gap -->
- **235 of 391 rows have no `source_archive_url` yet.** A daily job archives a batch at a
  time, so this shrinks steadily. Some never will: a handful of manufacturers block the
  Wayback crawler outright, and those rows keep their live `source_url` as the only citation.
<!-- /generated:archive-gap -->
- **A few sources can never be archived.** Some manufacturers and ISPs serve a bot-block
  page to any automated client — cox.com returns the same short "NOINDEX, NOFOLLOW" stub for
  every request, including one for its own homepage. Those pages are fine in a browser but
  cannot be captured, so those rows keep their live `source_url` as the only citation.
<!-- generated:gaps-tail -->
- **99 rows are `confidence: medium`.** Read the `credential_note` before relying on those.
  Hardware revisions of one model name can differ, and the note says so where it applies.
- **Coverage is 391 models, not exhaustive.** It grows by roughly 12 to 18 verified models a week.
  A model gets added only once an official source for it has been found, which caps the rate.
<!-- /generated:gaps-tail -->

<!-- generated:companion-dataset -->
ssid.ai publishes one other open dataset, built the same way: the **OUI change
history** at <https://github.com/Drumworks/oui-change-history>. The IEEE registry that
maps a MAC prefix to a manufacturer is published as current state only, so nobody knows
what a prefix resolved to five years ago. That repository is the diff, reconstructed from
dated captures going back to 2016, and it is why a MAC prefix is not a permanent vendor
identifier. Same licence, same sourcing rule.
<!-- /generated:companion-dataset -->

## Corrections

If a row is wrong, the fix needs a source. Three ways to send one:

- Open an issue or a pull request here with the manufacturer URL that supports the correct value.
- Call `submit_correction` on the [ssid-mcp](https://www.npmjs.com/package/ssid-mcp) server.
- Post it directly:

```bash
curl -X POST https://ssid.ai/api/corrections \
  -H 'content-type: application/json' \
  -d '{
    "slug": "netgear-nighthawk-r7000",
    "field": "defaultPassword",
    "proposedValue": "password",
    "sourceUrl": "https://kb.netgear.com/24340/"
  }'
```

`field` takes the API's name for the column, one of `defaultGatewayIp`, `defaultUsername`,
`defaultPassword`, `credType`, `resetSteps`. `sourceUrl` must be `https` and must not be a known
aggregator; submissions citing one are rejected at the endpoint.

Corrections are never applied automatically. Each one is checked against its cited source under
the same rule the rest of the directory follows: official manufacturer documentation, or it does
not ship. Agents may submit on the same terms as people.

## Licence

**CC BY 4.0.** Copy it, change it, sell it, feed it to a model. Credit ssid.ai and link back to
<https://ssid.ai/routers>. `LICENSE` is the full legal code; `NOTICE.md` explains what it means
here, including what counts as attribution in a model-generated answer.

The underlying facts are not owned by anyone. A given router's default IP and login are facts about
that product, stated by its manufacturer. What is licensed here is the compilation: the selection,
the verification, the credential-type classification and the per-row provenance.
