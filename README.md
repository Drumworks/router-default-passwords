# Router default passwords and login IPs

An open dataset of **335 router, gateway, mesh and access-point models** with, for each one: the
default login IP, the default admin username, the default password (or an explicit reason there is
no universal one), the credential type, factory-reset steps, and the manufacturer URL the values
came from.

Published by [ssid.ai](https://ssid.ai). Licensed **CC BY 4.0** — use it commercially, redistribute
it, build on it. Just credit ssid.ai.

Generated 2026-08-12 from the live directory at <https://ssid.ai/routers>.

## Files

| File | What it holds |
| --- | --- |
| `routers.csv` | 335 rows, 18 columns, RFC 4180, LF line endings |
| `routers.json` | The same 335 rows, with a licence and provenance header |
| `compliance.json` | The Router Default-Credential Compliance Index: share of models with no universal default password, by brand |
| `SCHEMA.md` | Every field defined, including the four `credential_type` values |
| `LICENSE` | CC BY 4.0, and what attribution means here |

## What is the default password for a router?

For most models sold today there isn't one. That single fact is what the old default-password lists
get wrong, and it is why this dataset has a `credential_type` column instead of filling every
password cell with `admin`.

Of the 335 models here, **241 have no universal default password**:

- 107 are `set-on-setup` — the router makes you create the password the first time you configure it.
- 92 are `label-unique` — every unit ships with a different password, printed on a sticker on the device.
- 42 are `app-only` — there is no web admin at all; you sign in to a phone app or a cloud account.

The other **94 models do ship a universal default**, and this dataset gives it to you. 88 of them
have a documented password string. Six have a documented blank password: the field is empty out of
the box, which still counts as a universal default, of nothing.

### By brand

| Brand | Models | The answer |
| --- | --- | --- |
| TP-Link | 34 | No universal default on 30 of 34. You create the password at first setup, at `tplinkwifi.net` (192.168.0.1). Four models still ship `admin` / `admin`: the TL-WR841N and three Omada access points. |
| Netgear | 32 | Split. 18 models force a password at setup and one cable modem is unique-per-device; **13 still ship `admin` / `password`** at 192.168.1.1 (`routerlogin.net`). Per-model rows say which. |
| ASUS | 25 | No universal default on 24 of 25. Username is `admin`, password is created during setup, at 192.168.50.1 (`router.asus.com`). The older RT-AC68U ships `admin` / `admin`. |
| Ubiquiti | 13 | Mixed: 4 app or cloud-account, 3 set-on-setup, 6 EdgeRouters on `ubnt` / `ubnt`. |
| Linksys | 13 | **9 of 13 ship a universal default password of `admin`**, mostly at 192.168.1.1 (`myrouter.local`). Six have no username field; three are `admin` / `admin`. Four are app-only. |
| AVM (FRITZ!Box) | 10 | Unique per device, printed on the label. Login at `fritz.box` / 192.168.178.1. |
| Peplink | 9 | All 9 ship a universal default. |
| Zyxel | 10 | Mixed; 5 ship a universal default, all `admin` / `1234`. |
| D-Link | 10 | **8 of 10 ship a universal default**, mostly at 192.168.0.1: three are `admin` with a blank password, four are password-only `password`, and the DSL series is `admin` / `admin` at 192.168.1.1. |
| MikroTik | 10 | Username `admin`, at 192.168.88.1. Six models print a unique password on the case sticker, two make you set one on first login, and the Chateau 5G ax ships with the field blank. |
| Tenda | 7 | No universal default. Four print a unique password on the label, two are set at first access via `tendawifi.com` (192.168.0.1), one is app-only. |
| Verizon, AT&T, BT, Sky, Virgin Media | 13 | ISP gateways: unique per device, printed on the label. Never `admin` / `admin`. |
| eero, Google Nest Wifi | 3 | App-only. No web admin, no default password. |

Full per-model rows are in `routers.csv` / `routers.json`. Each has a human-readable
`credential_note` explaining that model's specific behaviour, and a `source_url` you can check.

## What is the default login IP for a router?

Across the 335 models, 31 distinct default gateway IPs. The distribution:

| Default gateway IP | Models | Common on |
| --- | --- | --- |
| 192.168.1.1 | 113 | Netgear, Linksys, Ubiquiti, many ISP gateways |
| 192.168.0.1 | 60 | TP-Link, D-Link, Tenda, Sky, Virgin Media |
| 192.168.50.1 | 25 | ASUS, Peplink |
| 192.168.178.1 | 10 | AVM FRITZ!Box |
| 192.168.1.254 | 9 | AT&T, BT, EE, Plusnet, TELUS gateways |
| 192.168.2.1 | 9 | Belkin, Bell, Deutsche Telekom |
| 192.168.88.1 | 10 | MikroTik |
| 192.168.100.1 | 9 | ARRIS, Motorola and Netgear cable modems |

186 models also answer on a hostname (`tplinkwifi.net`, `routerlogin.net`, `router.asus.com`,
`fritz.box`), which is in the `default_login_host` column and usually more reliable than typing the
IP.

39 models have **no** admin IP at all. 29 of those are `app-only`: an eero or a Google Nest Wifi
has no web interface to log into, so a list that prints an IP for them is guessing. The other 9
are models whose manufacturer publishes a hostname or a DHCP-assigned address instead.

## Which routers still ship a universal default password?

**94 of 335 models (28%).** Put the other way: 72% no longer do, as of 2026-08-12. That number is
the Router Default-Credential Compliance Index, and `compliance.json` carries the full breakdown
plus every one of the 94 models with its username, password and source.

Brands with the most models still shipping a universal default:

| Brand | Models tracked | Still universal-default |
| --- | --- | --- |
| Netgear | 32 | 13 |
| Linksys | 13 | 9 |
| Peplink | 9 | 9 |
| D-Link | 10 | 8 |
| DrayTek | 6 | 6 |
| Ubiquiti | 13 | 6 |
| Netgate | 6 | 6 |
| Zyxel | 10 | 5 |

66 of the 97 brands tracked have no model here that ships a universal default. Among those with
three or more models: AVM, Tenda, Keenetic, Deutsche Telekom, Synology, GL.iNet,
Mercusys, Firewalla, Grandstream, eero, Verizon, AT&T and Virgin Media.

Why this is measurable at all: the UK's Product Security and Telecommunications Infrastructure Act
has banned universal default passwords on consumer connectable products supplied in the UK since
April 2024, and the EU Cyber Resilience Act and the RED delegated act push the same way. `static`
is the pattern those regimes target. A `static` row here is a statement about what the
manufacturer documents for that model, not a legal finding about that product — plenty of the 94
are older hardware that predates the rules or is sold outside their scope.

The live version of this index, updated as the directory grows, is at
<https://ssid.ai/compliance> and <https://ssid.ai/compliance/data.json>.

## How the data is sourced

Every row comes from the manufacturer's own documentation: their domain, their support KB, or
their official manual PDF. Never a forum, never an aggregator, never another password list.

- All 335 rows carry an `https` `source_url`, drawn from 116 distinct manufacturer and ISP domains.
- A model that cannot be verified against an official source is excluded from the directory
  rather than guessed at. That is why the count is 335 and not 30,000.
- 239 rows are marked `confidence: high` (the source states the behaviour directly). 96 are
  `medium`, usually because the manufacturer documents a family rather than that exact SKU, or
  because hardware revisions of the same model differ. The `credential_note` says which.
<!-- generated:archive-sourcing -->
- 102 rows also carry `source_archive_url`, a Wayback Machine copy of the cited page, so the
  claim stays checkable after the manufacturer reorganises their site. A daily job works
  through the rest, so the other 233 are queued rather than skipped. All 335 are sourced
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

18 columns. `SCHEMA.md` defines each one. The two that matter most:

`credential_type` is one of four values, and it is how you read a null password:

| Value | Meaning |
| --- | --- |
| `static` | A universal default that is the same on every unit. `default_password` holds it, or `default_password_blank` is `true` when the documented default is an empty field. |
| `set-on-setup` | No universal default. The owner creates the password during first-time setup. |
| `label-unique` | No universal default. Each unit ships with its own password, printed on the device. |
| `app-only` | No web admin login. Access is through a vendor app or cloud account. |

`default_password_blank` exists because `null` alone cannot distinguish "there is no universal
default" from "the universal default is an empty password". Six models are the latter: three
D-Link models and the MikroTik Chateau 5G ax, where the documented login is `admin` with the
password field left empty, and two Belkin families that ship with the admin dashboard unlocked.

## Known gaps

Where the data is thin, here is where:

- **39 models have no `default_gateway_ip`.** 29 are `app-only` and genuinely have no admin IP.
  The remaining 10 are models whose manufacturer documents a hostname or DHCP-assigned address
  instead. One of them, `ruckus-r350`, has a static credential but neither an IP nor a hostname —
  it is a controller-managed access point.
- **149 models have no `default_login_host`.** Most manufacturers publish only an IP.
<!-- generated:archive-gap -->
- **233 of 335 rows have no `source_archive_url` yet.** A daily job archives a batch at a
  time, so this shrinks steadily. Some never will: a handful of manufacturers block the
  Wayback crawler outright, and those rows keep their live `source_url` as the only citation.
<!-- /generated:archive-gap -->
- **96 rows are `confidence: medium`.** Read the `credential_note` before relying on those.
  Hardware revisions of one model name can differ, and the note says so where it applies.
- **Coverage is 335 models, not exhaustive.** It grows by roughly 12 to 18 verified models a week.
  A model gets added only once an official source for it has been found, which caps the rate.

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
