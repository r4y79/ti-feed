# TI-Collector — CTAC MY Threat Intelligence Feed

Machine-readable indicators of compromise, refreshed automatically. Each publish covers the **last 24 hours** of activity.

**Last updated:** 2026-08-29 22:00 UTC — **1,984 indicators** · TLP:CLEAR

| Type | Count |
|---|---:|
| Malicious SSL Certificates (SHA1) | 507 |
| Malicious Domains | 461 |
| Malware Hashes (MD5) | 323 |
| Malware Hashes (SHA256) | 323 |
| Malicious URLs | 252 |
| Malicious IPs | 118 |

## Consume it

Two ways in: flat files under `feeds/`, or the TAXII 2.1 tree under `taxii2/`. Both are regenerated on every publish and both are overwritten in place, so every URL below is stable.

### Flat files — `feeds/`

```
https://raw.githubusercontent.com/r4y79/ti-feed/main/feeds/ips.txt
https://raw.githubusercontent.com/r4y79/ti-feed/main/feeds/domains.txt
https://raw.githubusercontent.com/r4y79/ti-feed/main/feeds/urls.txt
https://raw.githubusercontent.com/r4y79/ti-feed/main/feeds/hashes.txt
https://raw.githubusercontent.com/r4y79/ti-feed/main/feeds/iocs-latest.csv
https://raw.githubusercontent.com/r4y79/ti-feed/main/feeds/iocs-latest.json
https://raw.githubusercontent.com/r4y79/ti-feed/main/feeds/stellarcyber.tsv
```

The plain-text lists are one indicator per line with `#` comments, ready for a firewall, proxy, or SIEM watchlist:

```bash
curl -s https://raw.githubusercontent.com/r4y79/ti-feed/main/feeds/ips.txt | grep -v '^#' > blocklist.txt
```

`stellarcyber.tsv` is the same 24h window in the Stellar Cyber *Custom Feed / TSV* schema (`TYPE`, `VALUE`, `SOURCE`, `SCORE`, tab-separated, no header).
It carries only the `url`, `ip` and `domain` indicators — that format has no representation for file hashes or SSL certificates.
Stellar Cyber requires a username and password on every custom feed; this host ignores them, so any non-empty pair works.

### TAXII 2.1 — `taxii2/`

The same indicators as STIX 2.1 objects, arranged as a TAXII 2.1 document tree. Walk it the way a client would:

```
discovery    https://raw.githubusercontent.com/r4y79/ti-feed/main/taxii2/index.json
api root     https://raw.githubusercontent.com/r4y79/ti-feed/main/taxii2/api/index.json
collections  https://raw.githubusercontent.com/r4y79/ti-feed/main/taxii2/api/collections/index.json
```

| Collection | Objects | Endpoint |
|---|---:|---|
| IOCs — last 24 hours | 1,985 | [`objects`](https://raw.githubusercontent.com/r4y79/ti-feed/main/taxii2/api/collections/ffbda76d-19e2-5545-a2cc-bbb5d6ee0f14/objects/index.json) |
| CISA KEV (30days) | 30 | [`objects`](https://raw.githubusercontent.com/r4y79/ti-feed/main/taxii2/api/collections/b0959dd1-db13-5431-ba4d-bbc866a2cf22/objects/index.json) |
| CVE (30days) | 16 | [`objects`](https://raw.githubusercontent.com/r4y79/ti-feed/main/taxii2/api/collections/c6715fd0-21b8-50c5-85bd-bfba36bce52f/objects/index.json) |

```bash
curl -s https://raw.githubusercontent.com/r4y79/ti-feed/main/taxii2/api/collections/ffbda76d-19e2-5545-a2cc-bbb5d6ee0f14/objects/index.json \
  | jq -r '.objects[] | select(.type=="indicator") | .pattern'
```

> **This is a static export, not a live TAXII server.** GitHub serves it as `text/plain` rather than `application/taxii+json;version=2.1`, and query parameters (`added_after`, `limit`) are ignored — every fetch returns the full collection. Strict clients will reject it; see [`taxii2/README.md`](taxii2/README.md).

## Archive

`daily/YYYY/MM/` keeps every past run — a dated report and the matching CSV. Newest: [`daily/2026/08/report_20260829.md`](daily/2026/08/report_20260829.md).

## Scope and limitations

- Indicators are republished from upstream feeds; see [`SOURCES.md`](SOURCES.md) for attribution and licensing.
- No third-party enrichment verdicts (VirusTotal, AbuseIPDB, URLScan, Hybrid Analysis) are included — their terms do not permit redistribution.
- `confidence` is TI-Collector's own composite score (0-100), not a vendor score.
- Indicators are **not** independently verified. Validate before blocking; expect false positives on shared hosting and CDN infrastructure.

Released under [CC0 1.0](LICENSE) to the extent the upstream licences allow.
