# TI-Collector — Public Threat Intelligence Feed

Machine-readable indicators of compromise, refreshed automatically. Each publish covers the **last 24 hours** of activity.

**Last updated:** 2026-08-21 02:51 UTC — **1,986 indicators** · TLP:CLEAR

| Type | Count |
|---|---:|
| Malicious SSL Certificates (SHA1) | 518 |
| Malicious Domains | 404 |
| Malicious URLs | 388 |
| Malicious IPs | 226 |
| Malware Hashes (MD5) | 225 |
| Malware Hashes (SHA256) | 225 |

## Consume it

`feeds/` holds rolling files, overwritten on every publish, so these URLs are stable:

```
https://raw.githubusercontent.com/r4y79/ti-feed/main/feeds/ips.txt
https://raw.githubusercontent.com/r4y79/ti-feed/main/feeds/domains.txt
https://raw.githubusercontent.com/r4y79/ti-feed/main/feeds/urls.txt
https://raw.githubusercontent.com/r4y79/ti-feed/main/feeds/hashes.txt
https://raw.githubusercontent.com/r4y79/ti-feed/main/feeds/iocs-latest.csv
https://raw.githubusercontent.com/r4y79/ti-feed/main/feeds/iocs-latest.json
```

The plain-text lists are one indicator per line with `#` comments, ready for a firewall, proxy, or SIEM watchlist:

```bash
curl -s https://raw.githubusercontent.com/r4y79/ti-feed/main/feeds/ips.txt | grep -v '^#' > blocklist.txt
```

## Archive

`daily/YYYY/MM/` keeps every past run — a dated report and the matching CSV. Newest: [`daily/2026/08/report_20260821.md`](daily/2026/08/report_20260821.md).

## Scope and limitations

- Indicators are republished from upstream feeds; see [`SOURCES.md`](SOURCES.md) for attribution and licensing.
- No third-party enrichment verdicts (VirusTotal, AbuseIPDB, URLScan, Hybrid Analysis) are included — their terms do not permit redistribution.
- `confidence` is TI-Collector's own composite score (0-100), not a vendor score.
- Indicators are **not** independently verified. Validate before blocking; expect false positives on shared hosting and CDN infrastructure.

Released under [CC0 1.0](LICENSE) to the extent the upstream licences allow.
