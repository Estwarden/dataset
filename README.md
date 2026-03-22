# EstWarden Baltic Security Dataset

Open OSINT dataset from [EstWarden](https://estwarden.eu) — a Baltic Security Monitor tracking military posture, disinformation, influence operations, and economic indicators in the Baltic region.

**27,487 signals** from 21 source types, collected Jan–Mar 2026.  
**NEW**: Satellite imagery dataset — 55 Sentinel-2 analyses of 35 military sites with spectral indices.

## Download

| File | Signals | Size | Description |
|------|---------|------|-------------|
| `media_signals.jsonl` | 17,358 | 27MB | RSS articles, Telegram, YouTube, GDELT military news, milwatch |
| `economic_signals.jsonl` | 6,561 | 5MB | Energy prices, sanctions entities, business registry, embassy advisories |
| `military_signals.jsonl` | 2,748 | 2MB | ADS-B flights, FIRMS thermal, GPS jamming, satellite analysis, OSINT |
| `environmental_signals.jsonl` | 765 | 429KB | Weather balloons, space weather, internet outages, NOTAMs |
| `satellite_signals.jsonl` | 55 | 48KB | Earth Engine satellite imagery analyses with spectral indices |
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
| `satellite_analysis` | 405 | Gemini-analyzed Sentinel-2 imagery + spectral indices |
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

## Satellite Imagery Dataset (NEW)

`satellite_signals.jsonl` contains 55 Sentinel-2 analyses of **35 Russian and Belarusian military installations** near the Baltic states, with:

- **LLM imagery analysis** (Gemini 2.0 Flash) — activity level, vehicle concentration, aircraft count, runway status
- **Spectral indices** (computed server-side in Google Earth Engine):
  - NDVI, NDBI, BSI (Bare Soil Index)
  - Fuel signature %, metal reflectance %, active infrastructure %
  - Year-over-year deltas (same month last year baseline)
- **SAR change detection** — Sentinel-1 VV backscatter change vs 30-day baseline
- **Thumbnail URLs** — 2048px Sentinel-2 RGB at `storage.googleapis.com/estwarden-satellite/`

### Satellite Signal Schema

```json
{
  "source_type": "satellite_analysis",
  "source_id": "ee:pskov-76th-vdv:2026-03-15",
  "title": "EE: Pskov-76th-VDV — MODERATE",
  "latitude": 57.78,
  "longitude": 28.39,
  "metadata": {
    "site": "Pskov-76th-VDV",
    "country": "RU",
    "site_type": "airborne",
    "scene_date": "2026-03-15",
    "gcs_url": "gs://estwarden-satellite/thumbnails/Pskov-76th-VDV/2026-03-15.jpg",
    "analysis": {
      "activity_level": "MODERATE",
      "vehicles": "LOW",
      "aircraft_count": 0,
      "runway": "CLEAR",
      "summary": "...",
      "confidence": "MEDIUM"
    },
    "spectral_indices": {
      "ndvi": 0.4249,
      "ndbi": 0.0514,
      "bsi": 0.1035,
      "fuel_pct": 3.28,
      "metal_pct": 0.12,
      "active_pct": 72.98,
      "yoy_ndvi": 0.0228,
      "yoy_ndbi": -0.028,
      "yoy_bsi": -0.008
    },
    "sar_change": {
      "mean_change_db": 1.62,
      "std_change_db": 2.07
    }
  }
}
```

### Monitored Sites (35 sites with imagery)

| Region | Sites | Examples |
|--------|------:|---------|
| Kaliningrad | 5 | Chkalovsk (airbase), Baltiysk (naval), Donskoye (missiles) |
| Pskov/Novgorod | 4 | 76th VDV, Ostrov (airbase), Strugi-Krasnye |
| St. Petersburg | 3 | Kronstadt (naval), Levashovo (airbase), Kamenka (brigade) |
| Belarus | 5 | Machulishchy (airbase), Baranovichi, Grodno, Brest, Osipovichi |
| Central Russia | 8 | Alabino, Tver-Migalovo, Shaykovka, Yelnya, Smolensk |
| Southern Russia | 5 | Millerovo, Morozovsk, Kursk-Khalino, Voronezh, Pogonovo |
| Arctic/North | 3 | Severomorsk, Olenya, Nizhny-Tagil |
| Other | 2 | Sevastopol, Saki-Novofedorovka |

### Thumbnail Access

All thumbnails are publicly accessible. Example:
```
https://storage.googleapis.com/estwarden-satellite/thumbnails/Pskov-76th-VDV/2026-03-15.jpg
```

List all available thumbnails:
```
https://storage.googleapis.com/storage/v1/b/estwarden-satellite/o?prefix=thumbnails/
```

### Satellite Research Use Cases

- **Change detection model training** — bitemporal Sentinel-2 pairs with spectral indices
- **Activity classification** — correlate spectral indices with LLM activity labels
- **Anomaly detection** — Isolation Forest on 6-band multispectral data
- **Seasonal baseline construction** — year-over-year same-month comparison
- **Multi-sensor fusion** — combine FIRMS thermal + SAR + optical for base monitoring
- **Super-resolution benchmarking** — 10m Sentinel-2 vs 0.3m ESRI reference

See [Estwarden/research](https://github.com/Estwarden/research) experiments 08–15 for validated techniques.

## Use Cases

- **Narrative detection model training** — 17K labeled media signals + 1.1K narrative tags
- **Threat index calibration** — 41 days of CTI scores with component breakdowns
- **Military activity analysis** — ADS-B, FIRMS, GPS jamming, satellite data
- **Satellite imagery analysis** — spectral indices, change detection, anomaly detection
- **Maritime OSINT** — 300K+ vessel positions for shadow fleet research
- **Influence campaign detection** — temporal patterns across media sources
- **Multi-source fusion research** — how to combine 21 heterogeneous sources

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

## Region Tags

Signals in production are tagged with geographic regions:
`estonia`, `latvia`, `lithuania`, `finland`, `poland`, `baltic` (composite),
plus adversary zones: `kaliningrad`, `pskov`, `stpetersburg`, `belarus_north`, `murmansk`.

This dataset was exported **before** region tagging was deployed, so signals
do not include a `region` field. A future release will include region-tagged data
for per-country analysis.

The CTI is computed separately for three regions:
- **Baltic** (estwarden, latwarden, litwarden, balticwarden)
- **Finland** (finwarden)
- **Poland** (polwarden)
