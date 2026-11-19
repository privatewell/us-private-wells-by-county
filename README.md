# US private well statistics by county, 2026

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.24377826.svg)](https://doi.org/10.5281/zenodo.24377826)

County-level statistics on household (domestic) wells in the United States, plus county-level groundwater quality results. Published by PrivateWell (https://privatewell.org), an independent US private-well data site.

- Version: 2026.11.1 (updated 2026-11-20)
- Author: Rohit S, Editor and data lead, PrivateWell
- Licence: CC BY 4.0
- Browse the county pages: https://privatewell.org/counties/
- Dataset landing page: https://privatewell.org/statistics/

## What this data is

The package has two county tables and one source list.

1. **Well records.** 6,820,947 household (domestic) well records taken from official state databases in 39 states (AK, AL, AR, AZ, CA, CO, DE, FL, IA, ID, IL, IN, KS, KY, MA, ME, MI, MN, MO, MS, MT, ND, NE, NH, NM, NV, NY, OH, OK, OR, PA, SC, SD, TX, VA, VT, WA, WI, WY). 2,270 counties have at least 30 records, and 1,830 counties have 200 or more records (these have a page on privatewell.org).
2. **Groundwater quality.** County summaries of Water Quality Portal results for groundwater wells since 1990: 97,424 wells and 1,055,679 sample results.
3. **Sources.** One row per state database, with the link, the filter used and the record count.

## Files

| File | Rows | What it holds |
|---|---|---|
| `us_private_wells_by_county_2026.csv` | 3,137 | One row per county. Depth, water level, yield, depth bands and the USGS arsenic population estimate. |
| `us_county_groundwater_quality_2026.csv` | 7,853 | One row per county and characteristic (11 characteristics). |
| `sources.csv` | 40 | Source database, URL, filter and record count for each state, plus the USGS arsenic model. |

All files are UTF-8 CSV with a header row. Empty cells mean the value was not available or did not meet the minimum sample rule. FIPS codes are text and keep their leading zero, so read them as strings.

## Data dictionary: `us_private_wells_by_county_2026.csv`

| Column | Unit | Description |
|---|---|---|
| `fips` | text, 5 digits | County FIPS code. |
| `state` | text | Two-letter state code. |
| `county` | text | County name without the word "County". |
| `household_well_records` | count | Domestic well records after the state filter. Empty where the state has no record source here. |
| `records_with_depth` | count | Records that have a usable depth. |
| `median_depth_ft` | feet | Median well depth. Only given where the county has 30 or more records. |
| `p10_depth_ft` | feet | 10th percentile depth. |
| `p25_depth_ft` | feet | 25th percentile depth. |
| `p75_depth_ft` | feet | 75th percentile depth. |
| `p90_depth_ft` | feet | 90th percentile depth. |
| `median_static_water_level_ft` | feet below ground | Median static water level. Empty where the state source does not carry it. |
| `median_yield_gpm` | gallons per minute | Median driller-reported yield. Empty where the state source does not carry it. |
| `median_depth_pre1990_ft` | feet | Median depth of wells completed before 1990. Needs 30 or more wells in that period. |
| `median_depth_2010on_ft` | feet | Median depth of wells completed in 2010 or later. Needs 30 or more wells in that period. |
| `share_lt100ft` | fraction, 0 to 1 | Share of wells shallower than 100 ft. |
| `share_100to300ft` | fraction, 0 to 1 | Share of wells from 100 ft up to 300 ft. |
| `share_300to500ft` | fraction, 0 to 1 | Share of wells from 300 ft up to 500 ft. |
| `share_ge500ft` | fraction, 0 to 1 | Share of wells 500 ft or deeper. |
| `usgs_arsenic_pop_est` | people | Modelled number of people using domestic wells with arsenic above 10 µg/L (USGS county model, 2010 population). |
| `usgs_arsenic_pop_lo` | people | Lower bound of the USGS estimate. |
| `usgs_arsenic_pop_hi` | people | Upper bound of the USGS estimate. |
| `page_url` | URL | The county page on privatewell.org. Given for the 1,830 counties with 200 or more records. |

The four depth-band shares add up to about 1 (rounding aside).

## Data dictionary: `us_county_groundwater_quality_2026.csv`

| Column | Unit | Description |
|---|---|---|
| `fips` | text, 5 digits | County FIPS code. |
| `state` | text | Two-letter state code. |
| `county` | text | County name, including "County" or the local equivalent. |
| `characteristic` | text | One of arsenic, fluoride, hardness, iron, lead, manganese, nitrate, radon, uranium, pfoa, pfos. |
| `n_wells` | count | Wells with a result. At least 10 per row. |
| `n_samples` | count | Sample results behind those wells. |
| `median_value` | see `unit` | Median of the per-well values (most recent result per well). |
| `p90_value` | see `unit` | 90th percentile of the per-well values. |
| `unit` | text | µg/L, mg/L, mg/L as N, mg/L as CaCO3, pCi/L or ng/L, depending on the characteristic. |
| `limit_value` | see `unit` | Reference limit used for the exceedance count. Empty for hardness, which has no limit. |
| `limit_name` | text | What the limit is: EPA MCL, EPA SMCL, EPA action level, EPA lifetime health advisory or EPA AMCL. |
| `n_wells_over_limit` | count | Wells above `limit_value`. |
| `pct_wells_over_limit` | percent | `n_wells_over_limit` as a percentage of `n_wells`. |
| `secondary_limit_value` | see `unit` | A second, lower reference level, where one is used (fluoride, manganese, radon). |
| `pct_wells_over_secondary` | percent | Percentage of wells above the secondary level. |
| `first_year` | year | Earliest sample year in the county row. |
| `last_year` | year | Latest sample year in the county row. |
| `top_providers` | text | Main data providers for the row, separated by ` \| `. |

Reference limits used: arsenic 10 µg/L (EPA MCL), nitrate 10 mg/L as N (EPA MCL), uranium 30 µg/L (EPA MCL), manganese 0.3 mg/L (EPA health advisory), radon 4,000 pCi/L (EPA AMCL), PFOA 4 ng/L and PFOS 4 ng/L (EPA MCL), fluoride 4.0 mg/L, iron 0.3 mg/L (EPA SMCL), lead 15 µg/L (EPA action level). Read the limit columns in the file for the exact values and names.

## Data dictionary: `sources.csv`

| Column | Description |
|---|---|
| `state` | Two-letter state code, or `ALL` for the national USGS arsenic model. |
| `dataset` | Name of the database and the agency that runs it. |
| `url` | Where the data comes from. |
| `filter` | The rule used to keep household wells. |
| `records` | Records kept after the filter. |

## Sources

Every state database and its link is in `sources.csv`. The 39 state well databases are published by the state agencies named in that file (for example the Minnesota County Well Index, Michigan EGLE Wellogic, California DWR Well Completion Reports and the Kansas Geological Survey WWC5 records). Two other sources:

- USGS county model of domestic well population with arsenic above 10 µg/L (Ayotte, Medalie and Qi, 2017): https://doi.org/10.5066/F7CN724V
- Water Quality Portal (USGS, EPA and state agencies): https://www.waterqualitydata.us/

Full list with links and per-state filters: https://privatewell.org/sources/ and https://privatewell.org/methodology/

## Method

- **Domestic-use filters.** Each state database is filtered to household wells with that state's own use field (for example `USE_C = 'DO'` in Minnesota or `WELL_TYPE = 'HOSHLD'` in Michigan). The exact filter for each state is in `sources.csv`.
- **Medians.** County figures are medians, not means, so a few very deep or very shallow records do not move them.
- **30-record minimum.** Depth statistics are given only for counties with 30 or more records. Pre-1990 and 2010-on medians each need 30 or more wells in that period. Pages are made only for counties with 200 or more records.
- **Depth bands.** Wells are grouped into under 100 ft, 100 to 300 ft, 300 to 500 ft and 500 ft or more.
- **Water quality.** From the Water Quality Portal we use groundwater wells with results since 1990. Each well counts once, using its most recent result for each characteristic. A county row needs at least 10 wells. Nitrate medians over 30 mg/L are held back.
- **Arsenic population estimate.** Taken from the USGS model, not measured.

## Caveats

- State coverage differs. 39 states have well records. Records per state, depth fields, static levels, yields and completion dates differ by state, and some states only have part of their wells (see the caveats in `sources.csv` and on the methodology page).
- Indiana has no well-use field. Its domestic wells are inferred from owner, casing diameter and pump rate, so the Indiana medians describe small-diameter wells that look like household wells.
- Deeper new wells do not prove water tables fell, because drilling practice, rules and well types changed too. In 905 of 1,083 counties (84%) with 30 or more wells in both periods, wells completed since 2010 have a deeper median than wells completed before 1990. That is a statement about completed wells, not about aquifers.
- The Water Quality Portal is not a random sample of private wells. It includes monitoring and public-supply wells, and sampling is often done where a problem is already suspected.
- USGS data after January 2024 is missing from the Water Quality Portal service used.
- Arsenic population figures are a model, not a test of any single well.
- County statistics say nothing about a specific well. Test your own water.

## Licence

Creative Commons Attribution 4.0 International (CC BY 4.0). You may share and adapt the data, including commercially, if you credit the source. See `LICENSE.md`. Underlying state and federal records stay under their own terms; see the links in `sources.csv`.

## How to cite

Rohit S (2026). *US private well statistics by county, 2026* (version 2026.11.1) [Data set]. PrivateWell. https://doi.org/10.5281/zenodo.24377826

BibTeX:

```bibtex
@dataset{s_2026_privatewell,
  author    = {S, Rohit},
  title     = {US private well statistics by county, 2026},
  year      = {2026},
  version   = {2026.11.1},
  publisher = {PrivateWell},
  doi       = {10.5281/zenodo.24377826},
  url       = {https://doi.org/10.5281/zenodo.24377826},
  license   = {CC-BY-4.0}
}
```

The DOI above always points to the newest version. Each version also has its own DOI on Zenodo (2026.11: https://doi.org/10.5281/zenodo.24377827).

## Changes

- 2026.11.1 (2026-11-20): corrected `median_depth_pre1990_ft` and `median_depth_2010on_ft`. For some states loaded from summary files, these medians were filled even when the period had fewer than 30 wells. They are now blank unless the period has 30 or more wells, as the method says. 589 county rows changed; no other column or file changed. The headline comparison (905 of 1,083 counties, 84%) already used the 30-well rule and is unchanged.
- 2026.11 (2026-11-19): first release.

## Contact

info@privatewell.org

## Decade file: us_private_wells_by_county_decade_2026.csv

| Column | Description |
|---|---|
| fips | 5-digit county FIPS code |
| state | 2-letter state code |
| county | County name |
| decade | Decade the wells were completed (1950 means 1950 to 1959) |
| wells_completed | Household well records completed in that decade with a recorded depth |
| median_depth_ft | Median depth of those wells, in feet |

The file covers 1,644 counties. A decade is listed only when it has 30 or more wells. Use it for decade trend charts.
