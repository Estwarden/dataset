# Satellite Imagery — LVO Force Posture Verification

Commercial and open-source satellite imagery of Russian military bases in the
Leningrad Military District (LVO), collected January–March 2026.

Cross-referenced with ISW/CDS order of battle data to verify whether LVO combat
units are at their home garrisons or deployed elsewhere.

## Key Finding

**Every major LVO combat unit is confirmed deployed to Ukraine** as of March 2026.
Satellite imagery of home bases shows low vehicle concentration and empty airfield
aprons, consistent with unit absence.

## Imagery

| Target | Sensor | Date | Resolution | File |
|--------|--------|------|-----------|------|
| Pskov — 76th VDV airfield | Planet SkySat | 2026-03-14 | 50cm | `pskov-76vdv/` |
| Pskov — Cherekha garrison | Maxar WorldView-3 | 2026-02-05 | 35cm | `pskov-cherekha-vdv/` |
| Luga — garrison area | Planet SkySat | 2026-03-07 | 50cm | `luga-garrison/` *(pending)* |
| Luga — wide area | Sentinel-2 | 2026-03-21 | 10m | `luga-sentinel2/` |
| Luga — SAR radar | ICEYE | 2026-01-30 | 2.5m | `luga-iceye-sar/` |
| Luga — SAR radar | ICEYE | 2026-02-05 | 2.5m | `luga-iceye-sar/` |
| Kaliningrad — Chernyakhovsk | Sentinel-2 | 2026-03-22 | 10m | `kaliningrad-sentinel2/` |

Imagery acquired via [SkyFi](https://skyfi.com) satellite marketplace API.

## Unit Tracking (ISW/CDS)

All LVO combat units confirmed in Ukraine as of March 2026:

| Unit | Home Base | Current Location | Source | Link |
|------|-----------|-----------------|--------|------|
| 76th Guards VDV Division | Pskov | Zaporizhia/Orikhiv | ISW Mar 7 | [source](https://www.understandingwar.org/backgrounder/russian-offensive-campaign-assessment-march-7-2026) |
| 69th Guards MR Division | Kamenka | Kharkiv/Sumy | ISW Mar 22 | [source](https://www.understandingwar.org/backgrounder/russian-offensive-campaign-assessment-march-22-2026) |
| 68th MR Division | Vladimirsky Lager | Kupyansk | ISW Mar 22 | [source](https://www.understandingwar.org/backgrounder/russian-offensive-campaign-assessment-march-22-2026) |
| 80th Arctic Brigade | Alakurtti | Sumy Oblast | ISW Mar 22 | [source](https://www.understandingwar.org/backgrounder/russian-offensive-campaign-assessment-march-22-2026) |
| 44th Army Corps | Petrozavodsk | Kharkiv Oblast | ISW Jan 15 | [source](https://www.understandingwar.org/backgrounder/russian-offensive-campaign-assessment-january-15-2026) |
| 11th Army Corps elements | Kaliningrad | Kupyansk | ISW Mar 22 | [source](https://www.understandingwar.org/backgrounder/russian-offensive-campaign-assessment-march-22-2026) |
| 26th Rocket Brigade | Luga | Equipment sent to Ukraine | Yle Oct 2025 | [source](https://yle.fi/a/74-20113407) |

Full CSV with coordinates: [`unit-tracking/lmd_units_march2026.csv`](unit-tracking/lmd_units_march2026.csv)

## EstWarden Automated Monitoring

[EstWarden](https://estwarden.eu) monitors 38 military sites daily via
[Google Earth Engine](https://earthengine.google.com/) (Sentinel-2 + SAR).
Latest assessments for LVO bases:

- **Pskov-76th-VDV**: LOW — clear runway, low vehicle concentration
- **Kamenka-138th-MRB**: MODERATE — vehicle concentration LOW
- **Luga-6th-CAA**: MODERATE — vehicle concentration LOW, no aircraft
- **Strugi-Krasnye**: LOW — no visible vehicles or aircraft

Methodology: [Estwarden/research](https://github.com/Estwarden/research)

## Corroborating Intelligence Sources

| Source | Date | Finding | Link |
|--------|------|---------|------|
| Finnish OSINT / Yle satellite analysis | Jan 2026 | 50 trucks at Rybka (Petrozavodsk), 2,500–3,000 troops in Karelia | [yle.fi](https://yle.fi/a/74-20113407) |
| Lithuanian VSD annual threat assessment | Mar 2026 | 6–10 years for full NATO conflict readiness; 15,000 troops in Karelia (was 3,000) | [lrt.lt](https://www.lrt.lt/en/news-in-english/19/2859104/) |
| Lithuanian VSD (Stars and Stripes) | Mar 2026 | Russia needs 6–10 years; limited Baltic conflict 1–2 years if sanctions lifted | [stripes.com](https://www.stripes.com/theaters/europe/2026-03-09/lithuania-russia-threat-21003306.html) |
| Estonian intelligence annual report | Jan 2026 | "Russia has no intention of attacking any NATO state this year or next" | [valisluureamet.ee](https://www.valisluureamet.ee/doc/raport/2026-en.pdf) |
| BISI (Baltic Institute for Security and Innovation) | Mar 2026 | 80,000 troops is the PLAN, unlikely until after Ukraine war | [bisi.lv](https://bisi.lv/en/publications/) |

## Methodology

1. Identified LVO garrison locations from open sources ([Wikimapia](https://wikimapia.org), [Google Earth](https://earth.google.com))
2. Ordered commercial satellite imagery via [SkyFi API](https://skyfi.com)
3. Supplemented with free [Sentinel-2](https://dataspace.copernicus.eu/) multispectral and [ICEYE](https://www.iceye.com/) SAR radar imagery
4. Cross-referenced with [ISW daily assessments](https://www.understandingwar.org/backgrounder/russian-offensive-campaign-assessment) and [CDS reports](https://defence.org.ua/)
5. Validated against EstWarden automated [Earth Engine](https://earthengine.google.com/) monitoring pipeline

All imagery preview files are included. Full-resolution GeoTIFF payloads available
on request (multi-GB files, too large for GitHub).

## Data Files

- `metadata/orders.json` — Full order details, costs, coordinates, findings
- `metadata/target_sites.geojson` — GeoJSON with all monitored base locations
- `unit-tracking/lmd_units_march2026.csv` — ISW/CDS unit location data with source URLs

## License

Satellite imagery: subject to provider licensing terms ([Planet](https://www.planet.com/), [Maxar](https://www.maxar.com/), [ESA Copernicus](https://dataspace.copernicus.eu/), [ICEYE](https://www.iceye.com/)).
Preview images included under fair use for research and public interest reporting.
Unit tracking data and metadata: [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).

## Attribution

- Imagery marketplace: [SkyFi](https://skyfi.com)
- Satellite providers: [Planet](https://www.planet.com/) / [Maxar](https://www.maxar.com/) / [ESA Copernicus](https://dataspace.copernicus.eu/) / [ICEYE](https://www.iceye.com/)
- Analysis: [EstWarden](https://estwarden.eu) ([GitHub](https://github.com/Estwarden))
- Unit tracking: [ISW](https://www.understandingwar.org/) / [CDS](https://defence.org.ua/)
