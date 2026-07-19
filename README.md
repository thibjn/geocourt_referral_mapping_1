# Replicating GEOCOURT: Mapping Legal Integration in the EU

A cartographic replication of the two main exhibits in:

> Dyevre, A. and Lampach, N., *"Subnational Disparities in EU Law Use: Exploring the
> GEOCOURT Dataset."*

using the GEOCOURT dataset — courts that submitted Article 267 preliminary references
to the Court of Justice of the European Union, 1961–2017.

## Contents

| File | Description |
|---|---|
| `GEOCOURT_Replication.ipynb` | Main notebook: data cleaning and all three figures |
| `figure1_courts_map.png` | Court-level referral map (peak vs. non-peak courts) |
| `figure2_referral_choropleth.png` | NUTS2-level choropleth of regional referral intensity |
| `figureA2_courts_by_period.png` | Figure 1 broken down into three sub-periods |
| `requirements.txt` | Python package dependencies |

## Data

The underlying data is available on this repository. There are two files: 

- `GEOCOURT_NUTS_2.csv` — court-level referral data available from the [GEOCOURT
  Dataset's](https://euthority.eu/?page_id=795) original distribution
- `NUTS_RG_20M_2013_3035.gpkg` — Eurostat NUTS2 (2013) region boundaries
  ([Eurostat GISCO](https://ec.europa.eu/eurostat/web/gisco/geodata/statistical-units/territorial-units-statistics))

## Setup

```
pip install -r requirements.txt
```

See `requirements.txt` for the full package list (geopandas, pandas, numpy,
matplotlib, shapely, mapclassify). If running in Google Colab, most of these are
already installed; `geopandas` and `mapclassify` typically still need the line above.

## Notes on methodology

A few departures from a literal transcription of the paper's figures, documented in
full in the notebook itself:

- **Court aggregation** is done on the court identifier (`court_ID`), not on court name,
  since the same physical court is recorded under multiple name variants across its
  history.
- **Referral volume** is encoded using four discrete size tiers (matching the paper's
  own legend breakpoints).
- **Regional referral intensity** (Figure 2) is classified using Natural Breaks
  rather than a linear scale, given the strongly skewed distribution of referral counts
  across regions, and separates confirmed zero-referral regions from the colour ramp
  used for regions with at least one referral.
- **Court tier** distinguishes First Instance, Second Instance (Court of Appeal), and Peak Court, using the two binary flags available in the released data (`peak_court` and `int_court`). Where the two flags conflict (157 courts flagged as both peak and intermediate — chiefly UK/Scottish courts and administrative supreme courts that are apex-level for only part of their function), peak status takes priority, consistent with the paper's footnote 4 definition of peak court as an institutional category (supreme or constitutional court) rather than a per-case designation.
