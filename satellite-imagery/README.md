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

### Full Datasets (open data, in repo)

| Target | Sensor | Date | Resolution | Preview | GeoTIFF Payload |
|--------|--------|------|-----------|---------|-----------------|
| Luga — wide area | [Sentinel-2](https://dataspace.copernicus.eu/) | 2026-03-21 | 10m | `luga-sentinel2/*.png` | `luga-sentinel2/*-payload.zip` (35MB) |
| Kaliningrad — Chernyakhovsk | [Sentinel-2](https://dataspace.copernicus.eu/) | 2026-03-22 | 10m | `kaliningrad-sentinel2/*.png` | `kaliningrad-sentinel2/*-payload.zip` (26MB) |

### Full Datasets (open data, GitHub Release — too large for repo)

| Target | Sensor | Date | Resolution | Preview | GeoTIFF Payload |
|--------|--------|------|-----------|---------|-----------------|
| Luga — SAR radar | [ICEYE](https://www.iceye.com/) | 2026-01-30 | 2.5m | `luga-iceye-sar/*.png` | See [Releases](../../releases) (7.7GB) |
| Luga — SAR radar | [ICEYE](https://www.iceye.com/) | 2026-02-05 | 2.5m | `luga-iceye-sar/*.png` | See [Releases](../../releases) (7.7GB) |

### Preview Only (commercial imagery — [SkyFi EULA](https://skyfi.com/en/end-user-license-agreement) allows web sharing with attribution, not redistribution of raw data)

| Target | Sensor | Date | Resolution | Preview | Reproduce |
|--------|--------|------|-----------|---------|-----------|
| Pskov — 76th VDV airfield | [Planet](https://www.planet.com/) SkySat | 2026-03-14 | 50cm | `pskov-76vdv/*.jpg` | [SkyFi](https://skyfi.com) archive `4d2b62e5-7edc-4173-9347-c8c7dc7bbe21` |
| Pskov — Cherekha garrison | [Maxar](https://www.maxar.com/) WorldView-3 | 2026-02-05 | 35cm | `pskov-cherekha-vdv/*.jpg` | [SkyFi](https://skyfi.com) archive `cbf8d9ac-25be-4028-aff6-edc43a263cf1` |
| Luga — garrison area | [Planet](https://www.planet.com/) SkySat | 2026-03-07 | 50cm | *pending delivery* | [SkyFi](https://skyfi.com) archive `0390f2c9-32c9-4e32-81b2-aa6842dbb273` |

To reproduce commercial imagery: create a [SkyFi](https://skyfi.com) account, search
the archive IDs above via their [API](https://docs.skyfi.com) or web UI, and purchase.

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
| Finnish OSINT / Yle satellite analysis | Jan 2026 | 50 trucks at Rybka, 2,500–3,000 troops in Karelia | [yle.fi](https://yle.fi/a/74-20113407) |
| Lithuanian VSD annual threat assessment | Mar 2026 | 6–10 years for full NATO conflict readiness | [lrt.lt](https://www.lrt.lt/en/news-in-english/19/2859104/) |
| Lithuanian VSD (Stars and Stripes) | Mar 2026 | Limited Baltic conflict 1–2 years if sanctions lifted | [stripes.com](https://www.stripes.com/theaters/europe/2026-03-09/lithuania-russia-threat-21003306.html) |
| Estonian intelligence annual report | Jan 2026 | "No intention of attacking any NATO state" | [valisluureamet.ee](https://www.valisluureamet.ee/doc/raport/2026-en.pdf) |

## Methodology

1. Identified LVO garrison locations from open sources ([Wikimapia](https://wikimapia.org), [Google Earth](https://earth.google.com))
2. Ordered commercial satellite imagery via [SkyFi API](https://skyfi.com) ([docs](https://docs.skyfi.com))
3. Supplemented with free [Sentinel-2](https://dataspace.copernicus.eu/) and [ICEYE](https://www.iceye.com/) open data
4. Cross-referenced with [ISW daily assessments](https://www.understandingwar.org/backgrounder/russian-offensive-campaign-assessment) and [CDS reports](https://defence.org.ua/)
5. Validated against EstWarden [Earth Engine](https://earthengine.google.com/) monitoring pipeline ([methodology](https://github.com/Estwarden/research))

## Data Files

- `metadata/orders.json` — Full order details, costs, coordinates, findings, source URLs
- `metadata/target_sites.geojson` — GeoJSON with all monitored base locations
- `unit-tracking/lmd_units_march2026.csv` — ISW/CDS unit locations with source URLs

## License

- **Sentinel-2**: [Copernicus open access](https://dataspace.copernicus.eu/terms-and-conditions) — free to use and redistribute
- **ICEYE free tier**: Open data — free to use and redistribute
- **Planet SkySat / Maxar WV3**: [SkyFi EULA](https://skyfi.com/en/end-user-license-agreement) — web sharing with attribution allowed, raw data redistribution prohibited. Preview images included; archive IDs provided for independent purchase.
- **Unit tracking data & metadata**: [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/)

## Attribution

- Imagery marketplace: [SkyFi](https://skyfi.com)
- Satellite providers: [Planet](https://www.planet.com/) / [Maxar](https://www.maxar.com/) / [ESA Copernicus](https://dataspace.copernicus.eu/) / [ICEYE](https://www.iceye.com/)
- Analysis: [EstWarden](https://estwarden.eu) ([GitHub](https://github.com/Estwarden))
- Unit tracking: [ISW](https://www.understandingwar.org/) / [CDS](https://defence.org.ua/)
