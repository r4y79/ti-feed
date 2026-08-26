# TAXII 2.1 (static export)

A TAXII 2.1-**shaped** set of JSON documents, regenerated on every publish.
The structure, object ids and declared media types follow the spec, so the
normal client walk works:

```
discovery    https://raw.githubusercontent.com/r4y79/ti-feed/main/taxii2/index.json
api root     https://raw.githubusercontent.com/r4y79/ti-feed/main/taxii2/api/index.json
collections  https://raw.githubusercontent.com/r4y79/ti-feed/main/taxii2/api/collections/index.json
```

## Collections

### IOCs — last 24 hours

`ffbda76d-19e2-5545-a2cc-bbb5d6ee0f14`

Indicators observed in the last 24 hours, republished from abuse.ch (CC0). Refreshed on every publish.

```
metadata  https://raw.githubusercontent.com/r4y79/ti-feed/main/taxii2/api/collections/ffbda76d-19e2-5545-a2cc-bbb5d6ee0f14/index.json
objects   https://raw.githubusercontent.com/r4y79/ti-feed/main/taxii2/api/collections/ffbda76d-19e2-5545-a2cc-bbb5d6ee0f14/objects/index.json
```

### CISA Known Exploited Vulnerabilities

`b0959dd1-db13-5431-ba4d-bbc866a2cf22`

Vulnerability objects for CVEs added to the CISA KEV catalog in the window. US Government public domain.

```
metadata  https://raw.githubusercontent.com/r4y79/ti-feed/main/taxii2/api/collections/b0959dd1-db13-5431-ba4d-bbc866a2cf22/index.json
objects   https://raw.githubusercontent.com/r4y79/ti-feed/main/taxii2/api/collections/b0959dd1-db13-5431-ba4d-bbc866a2cf22/objects/index.json
```

### CISA KEV — actively discussed

`c6715fd0-21b8-50c5-85bd-bfba36bce52f`

Known-exploited CVEs (CISA KEV) that also appear in AlienVault OTX pulses seen in the last 30 days. Every field is CISA KEV data, US Government public domain; OTX is used only to select which KEV entries are listed, and no OTX-authored content is republished.

```
metadata  https://raw.githubusercontent.com/r4y79/ti-feed/main/taxii2/api/collections/c6715fd0-21b8-50c5-85bd-bfba36bce52f/index.json
objects   https://raw.githubusercontent.com/r4y79/ti-feed/main/taxii2/api/collections/c6715fd0-21b8-50c5-85bd-bfba36bce52f/objects/index.json
```

## What this is not

This is static hosting, so it is **not** a conformant TAXII server:

- **Content-Type is wrong.** The spec requires `application/taxii+json;version=2.1`; raw.githubusercontent.com sends
  `text/plain`. Strict clients (including some `taxii2-client` configurations) will refuse the response.
- **No query parameters.** `?added_after=`, `?limit=`, `?next=` and `?match[...]` are ignored — every fetch returns the full current
  collection. Diff against your own last copy rather than relying on `added_after`.
- **No `/status/` endpoint, no write access, no authentication.**

Point a static file server that resolves directories to `index.json` (nginx: `index index.json;`) at this tree and it becomes a working
read-only TAXII 2.1 endpoint, provided the server also sets the media type.

## Fetching it directly

```bash
curl -s https://raw.githubusercontent.com/r4y79/ti-feed/main/taxii2/api/collections/index.json | jq '.collections[].title'
curl -s https://raw.githubusercontent.com/r4y79/ti-feed/main/taxii2/api/collections/ffbda76d-19e2-5545-a2cc-bbb5d6ee0f14/objects/index.json \
  | jq '.objects[] | select(.type=="indicator") | .pattern' | head
```
