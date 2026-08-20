# Sources and Licensing

Every indicator in this repository is republished from a feed whose licence
permits redistribution. Sources are listed per-indicator in the `source`
column of the CSV/JSON.

| Source | Upstream | Licence |
|---|---|---|
| `urlhaus` | [URLhaus](https://urlhaus.abuse.ch) — abuse.ch | CC0 1.0 |
| `malwarebazaar` | [MalwareBazaar](https://bazaar.abuse.ch) — abuse.ch | CC0 1.0 |
| `threatfox` | [ThreatFox](https://threatfox.abuse.ch) — abuse.ch | CC0 1.0 |
| `feodotracker` | [Feodo Tracker](https://feodotracker.abuse.ch) — abuse.ch | CC0 1.0 |
| `sslbl` | [SSL Blacklist](https://sslbl.abuse.ch) — abuse.ch | CC0 1.0 |

CISA KEV entries in the reports come from the
[Known Exploited Vulnerabilities Catalog](https://www.cisa.gov/known-exploited-vulnerabilities-catalog),
a US Government work in the public domain.

## Deliberately excluded

These feeds are collected internally but **not** republished here:

- **OpenPhish** — the free Community Feed prohibits redistribution.
- **AlienVault OTX** — user-contributed pulse content; bulk republication is
  not covered by the API terms.
- **Community Zeek intel feeds** — mixed and often unstated upstream licences.
- **blocklist.de** — free to use, but redistribution is not expressly granted.
- **VirusTotal, AbuseIPDB, URLScan.io, Hybrid Analysis, GreyNoise** — per-indicator
  verdicts and scores are never exported, in line with their terms.

## Corrections

If an indicator here is a false positive, or you hold rights to content you
believe is republished in error, open an issue and it will be removed.
