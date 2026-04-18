# The Impact of Weather on Flight Delays

## The Problem
Flight delays are not just an inconvenience — they represent 
a multi-billion-dollar operational challenge for the aviation 
industry. In the U.S. alone, delays have been estimated to cost 
around $33 billion yearly.

Whilst weather-related delays cannot be fully prevented, predicting 
them creates real operational value. Explicit cost data, as 
extracted from University of Westminster study and adjusted to 
2022 prices, indicates that a single 15 minute delay at the gate 
for an A321 aircraft could cost an airline €689 as a base tactical 
cost, disregarding the chain reaction effect. If we are able 
to create a model that would predict five 15 minute delays a week 
for this type of aircraft, the avoided tactical cost alone could 
be approximately €180,000 annually — excluding downstream network effects.

Early warning enables airlines to act: substituting aircraft, 
engaging reserve crew, repositioning staff, optimising fuel 
planning, and managing passenger expectations before compensation 
claims arise.

## Business Question
To what extent do weather conditions influence the likelihood of 
flight departure delays — and can a predictive model support earlier 
operational decision-making across crew planning, aircraft routing, 
gate allocation, and passenger reaccommodation?

## Approach
- Scope limited to JFK Airport departures (one origin = cleaner 
  weather signal)
- Target variable: `delayed_15` — 1 if departure delay ≥ 15 mins 
  (aligned with FAA definition)
- Evaluated on **recall** (catching delays) and **average precision** 
  (managing false positives, which also carry cost)

## Data
Sourced from the US Department of Transportation, Bureau of 
Transportation Statistics — On-Time Reporting Carrier Performance.

- **Train set:** 2022–2023 JFK departures (~250,000 observations)  
- **Test set:** January–October 2025 JFK departures  
- **Delay rate:** 24.4% (train) | 20.3% (test)

To reproduce: download data filtered to New York state from 
[BTS](https://www.transtats.bts.gov/DL_SelectFields.aspx?gnoyr_VQ=FGJ&QO_fu146_anzr=b0-gvzr), select fields listed in 
`data/README.md`, and place CSVs in the `/data` folder.

## Key Findings

- **Temperature is the dominant predictor**, accounting for ~22% of 
  feature importance (MDI) and confirmed as the largest single 
  contributor in permutation testing on the test set. Rather than 
  acting as a simple weather variable, temperature likely functions 
  as a seasonal proxy — the model is sensing broader weather regimes 
  (coastal systems, storms, nor’easters) rather than isolated 
  conditions.

- **Five features capture ~80% of predictive power**: temperature, 
  atmospheric pressure, wind speed, wind direction, and humidity. 
  This combination is characteristic of storm system signatures, 
  suggesting the model has learned to detect high-risk meteorological 
  patterns rather than individual thresholds.

- **Precipitation ranks lower than expected** — appearing 8th in MDI 
  importance — which reflects that delays are often driven by 
  conditions preceding or surrounding precipitation events, not 
  rainfall alone.

- The model achieves **60% recall** on unseen 2025 data, trained 
  entirely on 2022–2023 flights — demonstrating reasonable 
  generalisation across time.

## Results
Our Random Forest model correctly predicts **60% of flight delays** 
based on weather conditions at scheduled departure time.

This does not capture every event — many disruptions stem from 
factors beyond weather (inbound aircraft delays, carrier constraints) 
which were outside scope. But within the weather signal alone, the 
model provides actionable lead time for operational planning.

## Notebooks
| Notebook | Description |
|---|---|
| `01_EDA_2022-2023.ipynb` | Exploratory analysis — train dataset |
| `02_EDA_2025.ipynb` | Exploratory analysis — test dataset |
| `03_Model_2022_2025.ipynb` | Modelling, evaluation |

## Tech Stack
Python, Pandas, Scikit-learn, Matplotlib, Jupyter

## Documents
- 📄 [Full Capstone Report](docs/AS_Capstone_Project_Document.pdf)
- 📊 [Presentation](docs/AS_Capstone_Project_Presentation.pdf)