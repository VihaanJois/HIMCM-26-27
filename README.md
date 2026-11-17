# HIMCM-26-27
Aarit Das, Teja, August, Vihaan

## Best Place to Live: model

A three-tier funnel. Every tier uses the same scoring method:

1. Cap each indicator at the 5th and 95th percentiles.
2. Rescale it from 0 to 1, where 1 is best.
3. Weight the indicators with the entropy method.
4. Score each place as the weighted average of the indicators it has data for.

| Tier | Ranks | Criteria | Passes on |
|---|---|---|---|
| 1 | Countries (World Bank) | Healthcare, water, sanitation, internet, road safety, test scores, income equality | Top 30 countries |
| 2 | OECD regions inside those countries | Homicide, vehicle theft, air quality (PM2.5), green space, public transport access | Top 20 regions |
| 3 | OECD cities inside those regions | Demographic diversity (% born abroad), entertainment (venues within 5 km) | Top 10 cities |

No criterion is used in more than one tier.

## Folders

- `tier1/`, `tier2/`, `tier3/`: data download and model scripts for each tier
- `results/`: rankings (CSV), charts (`fig_tier1/2/3`), the Tier 1 report and the data sources table
- `figures_code/`: scripts that draw the charts
- `himcm26_simple.py`, `HiMCM26_simple.ipynb`: the Tier 1 model, with comments

## Run

```
python tier2/tier2_regions.py <oecd_raw dir> tier1/countryInfo.txt results/tier1_country_ranking.csv <out dir> <oecd_city dir> tier3/fua_located.csv
python tier3/tier3_cities.py <oecd_city dir> tier3/fua_located.csv <out dir>/tier2_regions_to_tier3.csv <out dir> tier3/wd_venues.csv tier3/city_foreign_born.csv <DSD_REG_MIGRANT@DF_MIGR_STOCK.csv>
```

The OECD files are downloaded from `https://sdmx.oecd.org/public/rest/data/OECD.CFE.EDS,<dataflow>/all?format=csvfile`. See `results/data_sources_tier2_tier3.png` for every dataset used.
