# TI-Collector — Public Threat Intelligence Feed

Machine-readable indicators of compromise, refreshed automatically. Each publish covers the **last 24 hours** of activity.

**Last updated:** 2026-08-20 09:36 UTC — **2,002 indicators** · TLP:CLEAR

| Type | Count |
|---|---:|
| Malicious SSL Certificates (SHA1) | 503 |
| Malicious URLs | 350 |
| Malware Hashes (MD5) | 309 |
| Malware Hashes (SHA256) | 309 |
| Malicious Domains | 302 |
| Malicious IPs | 229 |

## Consume it

`feeds/` holds rolling files, overwritten on every publish, so these URLs are stable:

```
<add a GitHub remote to populate these URLs>/feeds/ips.txt
<add a GitHub remote to populate these URLs>/feeds/domains.txt
<add a GitHub remote to populate these URLs>/feeds/urls.txt
<add a GitHub remote to populate these URLs>/feeds/hashes.txt
<add a GitHub remote to populate these URLs>/feeds/iocs-latest.csv
<add a GitHub remote to populate these URLs>/feeds/iocs-latest.json
```

The plain-text lists are one indicator per line with `#` comments, ready for a firewall, proxy, or SIEM watchlist:

```bash
curl -s <add a GitHub remote to populate these URLs>/feeds/ips.txt | grep -v '^#' > blocklist.txt
```

## Archive

`daily/YYYY/MM/` keeps every past run — a dated report and the matching CSV. Newest: [`daily/2026/08/report_20260820.md`](daily/2026/08/report_20260820.md).

## Scope and limitations

- Indicators are republished from upstream feeds; see [`SOURCES.md`](SOURCES.md) for attribution and licensing.
- No third-party enrichment verdicts (VirusTotal, AbuseIPDB, URLScan, Hybrid Analysis) are included — their terms do not permit redistribution.
- `confidence` is TI-Collector's own composite score (0-100), not a vendor score.
- Indicators are **not** independently verified. Validate before blocking; expect false positives on shared hosting and CDN infrastructure.

Released under [CC0 1.0](LICENSE) to the extent the upstream licences allow.
