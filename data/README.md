# Wildfire Smoke Impact Analysis and Forecasting: Data Dictionary

## **Overview**
This document provides a detailed description of the raw, intermediate, and final datasets used in this project, including their structure, variables, and purpose. Each dataset serves a specific role in the pipeline to analyze and forecast the relationship between wildfire smoke, air quality, and real estate trends in Hartford, CT.

## **1. Final Data**
### `enhanced_data.csv`
This file contains the final dataset used for regression and forecasting analyses.

| **Column**               | **Description**                                                                 |
|---------------------------|---------------------------------------------------------------------------------|
| `year`                   | The year of observation.                                                       |
| `median_sale_amount`     | Median sale amount (USD) for real estate transactions in Hartford.              |
| `median_assessed_value`  | Median assessed value of properties in Hartford for tax purposes.               |
| `count_sales`            | Total number of real estate transactions recorded in the year.                  |
| `smoke_impact`           | Annual cumulative smoke impact estimate based on wildfire data.                 |
| `avg_daily_max_aqi`      | Average daily maximum Air Quality Index (AQI) for Hartford over the year.       |
| `max_daily_aqi`          | Maximum daily AQI recorded in Hartford during the year.                         |
| `smoke_impact_lag_1`     | Smoke impact from the previous year (1-month lag).                               |
| `smoke_impact_lag_3`     | Smoke impact from three years prior (3-month lag).                               |
| `max_daily_aqi_lag_1`    | Maximum AQI from the previous year (1-month lag).                                |
| `max_daily_aqi_aqi_lag_3`| Maximum AQI from three years prior (3-month lag).                                |
| `transaction_volume`     | Total volume of real estate transactions during the year.                       |
| `transaction_volume_lag` | Real estate transaction volume from the previous year.                          |

## **2. Intermediate Data**
### `aqi_data.csv`
This dataset contains daily air quality data for Hartford, CT.

| **Column**     | **Description**                                      |
|-----------------|------------------------------------------------------|
| `date`         | Date of the AQI observation.                         |
| `daily_max_aqi`| Daily maximum Air Quality Index (AQI) recorded.       |

### `filtered_real_estate_df.csv`
This dataset includes preprocessed real estate transaction data for Hartford, CT.

| **Column**          | **Description**                                                                 |
|----------------------|---------------------------------------------------------------------------------|
| `Serial Number`      | Unique identifier for each real estate transaction.                            |
| `List Year`          | Year the property was listed for sale.                                         |
| `Date Recorded`      | Date when the transaction was officially recorded.                             |
| `Town`               | Town where the property is located (Hartford, CT in this case).                |
| `Address`            | Address of the property.                                                       |
| `Assessed Value`     | Assessed tax value of the property.                                            |
| `Sale Amount`        | Sale price of the property.                                                    |
| `Sales Ratio`        | Ratio of sale price to assessed value.                                          |
| `Property Type`      | Type of property (e.g., Residential, Commercial, Industrial).                  |
| `Residential Type`   | Specifies whether the property is single or multi-family residential.          |
| `Non Use Code`       | Indicates unreliable sale data (e.g., sale price anomalies).                   |
| `Assessor Remarks`   | Remarks or notes provided by the assessor.                                     |
| `OPM remarks`        | Notes provided by the Office of Policy and Management (OPM).                  |
| `Location`           | Latitude and longitude coordinates of the property.                           |
| `coords`             | Processed geospatial coordinates.                                              |
| `distance_to_hartford`| Distance from the property to Hartford’s city center.                         |

### `selected_processed_wildfires2.csv`
This dataset includes preprocessed wildfire data relevant to Hartford.

| **Column**              | **Description**                                                                 |
|--------------------------|---------------------------------------------------------------------------------|
| `year`                  | Year of the wildfire.                                                          |
| `discovery_date`        | Date the wildfire was discovered.                                              |
| `fire_name`             | Name of the wildfire.                                                          |
| `fire_size_acres`       | Size of the wildfire in acres burned.                                          |
| `fire_type`             | Type of fire (wildfire in this project).                                       |
| `average_distance_miles`| Average distance of the wildfire from Hartford, CT.                            |
| `listed_dates`          | Key dates (discovery, start, and end) associated with the wildfire.            |
| `days_burning`          | Total number of days the wildfire burned.                                      |
| `smoke_impact`          | Calculated annual smoke impact based on wildfire size, duration, and distance. |
| `normalized_smoke_impact`| Smoke impact normalized to a standard scale for comparison.                   |

## **3. Raw Data**
### `Real_Estate_Sales_2001-2022_GL_20241117.csv`
This raw dataset includes real estate sales data for Connecticut from 2001 to 2022. This data is too large to be stored in Github, please visit the [Connecticut Real Estate Sales Database](https://aqs.epa.gov/aqsweb/documents/data_api.html) to download this data.

| **Column**          | **Description**                                                                 |
|----------------------|---------------------------------------------------------------------------------|
| `Serial Number`      | Serial number of the sale.                                                     |
| `List Year`          | Year the property was listed for sale.                                         |
| `Date Recorded`      | Date the sale was recorded locally.                                            |
| `Town`               | Name of the town.                                                             |
| `Address`            | Address of the sale.                                                          |
| `Assessed Value`     | Value of the property used for local tax assessment.                          |
| `Sale Amount`        | Amount the property was sold for.                                              |
| `Sales Ratio`        | Ratio of the sale price to the assessed value.                                 |
| `Property Type`      | Type of property (e.g., Residential, Commercial, Industrial, Vacant).          |
| `Residential Type`   | Indicates whether the property is single or multi-family residential.          |
| `Non-Use Code`       | Indicates unreliable sale price data.                                          |
| `Assessor Remarks`   | Notes provided by the assessor.                                               |
| `OPM remarks`        | Notes from the Office of Policy and Management.                               |
| `Location`           | Latitude and longitude coordinates.                                           |


### `USGS_Wildland_Fire_Combined_Dataset.json`
This raw dataset includes wildfire data for the U.S. and its territories from 1961 to 2021. This data is also too large to be stored in Github, please visit the [USGS Combined wildland fire datasets](https://www.sciencebase.gov/catalog/item/61aa537dd34eb622f699df81), to download this data. The dataset includes:
- Fire size, type, and name
- Geographic location (latitude, longitude)
- Discovery, start, and end dates of wildfires
