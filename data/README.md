# Data

The raw data files are not included in this repository due to file size.

## How to Download

1. Go to [BTS On-Time: Reporting Carrier On-Time Performance (1987-present)](https://www.transtats.bts.gov/DL_SelectFields.aspx?gnoyr_VQ=FGJ&QO_fu146_anzr=b0-gvzr)
2. Filter by **Geography: New York**
3. Filter by Year 
4. Filter by Period 
5. Select the following fields:
   - FlightDate
   - Tail_Number
   - Flight_Number_Reporting_Airline
   - OriginAirportID
   - Origin
   - DestAirportID
   - Dest
   - CRSDepTime
   - DepTime
   - DepDelay
   - Cancelled
   - Diverted
   - CarrierDelay
   - WeatherDelay
   - NASDelay
   - SecurityDelay
   - LateAircraftDelay

6. Download for the relevant periods:
   - **Train set:** 2022 and 2023 (monthly CSVs)
   - **Test set:** January–October 2025 (monthly CSVs)
7. Place all CSV files in this `/data` folder before running the notebooks

## Sample Data
Two sample files are included for reference:
- `sample_train_Jan2022.csv` — one month from the train set
- `sample_test_Jan2025.csv` — one month from the test set
