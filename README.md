# EstWarden Baltic Security Dataset

Open OSINT dataset from [EstWarden](https://estwarden.eu) — a Baltic Security Monitor tracking military posture, disinformation, influence operations, and economic indicators in the Baltic region.

**27,432 signals** from 20 source types, collected Jan–Mar 2026.

## Download

| File | Signals | Size | Description |
|------|---------|------|-------------|
| `media_signals.jsonl` | 17,358 | 27MB | RSS articles, Telegram, YouTube, GDELT military news, milwatch |
| `economic_signals.jsonl` | 6,561 | 5MB | Energy prices, sanctions entities, business registry, embassy advisories |
| `military_signals.jsonl` | 2,748 | 2MB | ADS-B flights, FIRMS thermal, GPS jamming, satellite analysis, OSINT |
| `environmental_signals.jsonl` | 765 | 429KB | Weather balloons, space weather, internet outages, NOTAMs |
| `ais_signals.jsonl.gz` | 301,855 | 11MB | Baltic Sea vessel positions (compressed, separate) |
| `narrative_tags.jsonl` | 1,109 | 142KB | LLM narrative classifications (N1–N5) |
| `daily_reports.jsonl` | 41 | 6KB | Daily threat assessments with CTI scores |
| `campaigns.jsonl` | 31 | 16KB | Detected influence campaigns |
| `indicators.jsonl` | 497 | 81KB | Per-report threat indicators |

## Signal Schema

```json
{
  "source_type": "rss",
  "source_id": "propastop:a1b2c3d4e5f6",
  "title": "Article title",
  "content": "Article text (truncated to 3000 chars)...",
  "url": "https://source-url.com/article",
  "published_at": "2026-03-15T08:30:00+00:00",
  "severity": "HIGH",
  "latitude": 59.43,
  "longitude": 24.75,
  "source_category": "counter_disinfo",
  "metadata": {
    "feed_handle": "propastop",
    "category": "counter_disinfo",
    "tier": "T1"
  }
}
```

## Source Types

### Media (17,358 signals)
| Source | Count | What |
|--------|-------|------|
| `rss` | 14K+ | 54 RSS feeds — Baltic media, Russian state, independent, defense think tanks |
| `rss_security` | 1K+ | Security-focused feeds (CEPA, ICDS, War on the Rocks, FPRI) |
| `telegram` | 1K+ | Public Telegram channel messages |
| `milwatch` | 956 | Military watch RSS feeds (25 defense news sources) |
| `gdelt` | 1K+ | GDELT Global Knowledge Graph — military news near monitored sites |
| `youtube` | 122 | YouTube video metadata from tracked channels |
| `deepstate` | 65 | Ukraine frontline data |

### Military (2,748 signals)
| Source | Count | What |
|--------|-------|------|
| `firms` | 887 | NASA VIIRS thermal anomalies at military bases |
| `satellite_analysis` | 350 | Gemini-analyzed Sentinel-2 imagery |
| `adsb` | 316 | Military aircraft positions (Baltic airspace) |
| `gpsjam` | 133 | GPS interference zones (H3 hex aggregation) |
| `osint_perplexity` | 123 | AI-powered OSINT research queries |
| `osint_milbase` | 28 | Military base deep research |

### Economic (6,561 signals)
| Source | Count | What |
|--------|-------|------|
| `sanctions` | 5,890 | OpenSanctions entity database (RU/BY related) |
| `energy` | 43 | Estonian electricity prices (Elering) |
| `business` | 73 | Estonian business registry liquidations |
| `ru_legislation` | 15 | Russian legislation changes |
| `embassy` | 11 | Travel advisories (US, UK, DE, FI, SE) |

### Environmental (765 signals)
| Source | Count | What |
|--------|-------|------|
| `balloon` | 643 | Weather radiosonde positions (SondeHub, Baltic region) |
| `space_weather` | 60+ | NOAA Kp geomagnetic index |

### Maritime (301,855 signals — separate file)
| Source | Count | What |
|--------|-------|------|
| `ais` | 301K+ | Baltic Sea vessel positions, including shadow fleet detection |

## Narrative Taxonomy

Signals are classified into five Baltic-targeted disinformation categories:

| Code | Narrative | Description |
|------|-----------|-------------|
| N1 | Russophobia / Persecution | "Estonia persecutes Russian speakers" |
| N2 | War Escalation Panic | "Baltic politicians drag civilians into war" |
| N3 | Aid = Theft | "Ukraine support wastes taxpayer money" |
| N4 | Delegitimization | "EU/Estonian leaders are corrupt" |
| N5 | Isolation / Victimhood | "Nobody listens to the Russian community" |

## Composite Threat Index

Daily reports include a CTI score (0–100):

| Level | Score | Meaning |
|-------|-------|---------|
| 🟢 GREEN | 0–24 | Normal baseline |
| 🟡 YELLOW | 25–49 | Elevated activity |
| 🟠 ORANGE | 50–74 | Significant concern |
| 🔴 RED | 75–100 | Critical threat |

## Use Cases

- **Narrative detection model training** — 17K labeled media signals + 1.1K narrative tags
- **Threat index calibration** — 41 days of CTI scores with component breakdowns
- **Military activity analysis** — ADS-B, FIRMS, GPS jamming, satellite data
- **Maritime OSINT** — 300K+ vessel positions for shadow fleet research
- **Influence campaign detection** — temporal patterns across media sources
- **Multi-source fusion research** — how to combine 20 heterogeneous sources

## Provenance

All data collected from **public APIs and open sources**:
- RSS feeds (direct XML), Wayback Machine archives
- NASA FIRMS, NOAA SWPC, EASA CZIB
- OpenSky/adsb.lol, Digitraffic.fi (Finnish maritime)
- GDELT, ACLED, OpenSanctions
- SondeHub, GPSJam.org

No private data, no scraped personal content, no classified information.

## Citation

```bibtex
@dataset{estwarden2026,
  title={EstWarden Baltic Security Dataset},
  author={EstWarden},
  year={2026},
  url={https://github.com/Estwarden/dataset},
  note={27K+ OSINT signals from 20 sources, Jan-Mar 2026}
}
```

## License

[Open Data Commons Attribution License (ODC-By)](https://opendatacommons.org/licenses/by/1-0/)

You are free to share and adapt this dataset. Please credit EstWarden.

## Related

- [estwarden.eu](https://estwarden.eu) — Live dashboard
- [Estwarden/collectors](https://github.com/Estwarden/collectors) — Data collection pipelines
- [Estwarden/research](https://github.com/Estwarden/research) — CTI methodology + autoresearch
- [Estwarden/integrations](https://github.com/Estwarden/integrations) — MCP server, Home Assistant, CLI
