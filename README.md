# Wildfire Smoke Impact Analysis and Forecasting in Hartford, CT

## **Project Overview**
This project investigates the relationship between wildfire smoke and its impacts on air quality, property values, and economic behavior in Hartford, CT. Using wildfire data, smoke impact estimates, air quality metrics from the US EPA, and real estate transaction records, the study employs regression and time series modeling to quantify these effects and forecast future trends over the next 50 years. The findings aim to inform policymakers, city managers, and residents about the long-term implications of wildfire smoke and provide actionable insights for resilience planning.

## **Key Objectives**
1. Analyze historical smoke impacts on Hartford’s air quality and economy.
2. Quantify the relationships between smoke exposure, air quality, and property values.
3. Use SARIMAX models to forecast future smoke impacts and property value trends.
4. Provide actionable recommendations for mitigating wildfire impacts.

## **Data Sources**
The three following data sources were used during this project. These datasets were manipulated, cleaned and filterd muliple times during this project. If you would like to view all of these datasets along with their corresponding data dictionaries, please navigate to the `/data` folder of this repository.

### **1. Wildfire Data**
Wildfire data was obtained from the [Combined Wildland Fire](https://www.sciencebase.gov/catalog/item/61aa537dd34eb622f699df81) datasets, focusing on wildfires that:
- Occurred within 650 miles of Hartford, CT.
- Were recorded between 1961 and 2021.
- Took place during the wildfire season (May 1st – October 31st).

This data is processed and stored in `selected_processed_wildfires2.csv`, located in the `data/intermediate` folder of this repository. Some key fields include:
- `year`: The year of the wildfire.
- `discovery_date`: The date the wildfire was reported.
- `fire_name`: The name of the wildfire.
- `fire_size_acres`: The acreage burned by the wildfire.
- `fire_type`: Type of fire (wildfire in this case).
- `average_distance_miles`: Average distance of the wildfire from Hartford, CT.
- `listed_dates`: Key dates (discovery, start, and end) associated with the wildfire.

### **2. Air Quality Data (EPA AQS API)**
Air quality data was collected from the [US EPA AQS API](https://aqs.epa.gov/aqsweb/documents/data_api.html). The dataset, stored as `aqi_df`, provides daily AQI values for Hartford, CT. Key parameters include:
- **Pollutants Monitored**: Ozone (O3), Particulate Matter (PM2.5, PM10).
- **Frequency**: Daily AQI summaries by county.
- **Format**: Tabular data with date, pollutant type, and AQI values.

To access this data, an EPA AQS API key is required. The processed AQI dataset is stored in `aqi_data.csv` located in the `data/intermediate` folder.

### **3. Real Estate Data**
Real estate data was sourced from **Connecticut Real Estate Sales Data** and includes information about the:
  - `transaction_volume`: Total sales volume per year.
  - `median_sale_amount`: Median property sale price.
  - `sale_date`: Date of the transaction.

The raw real estate dataset is too large to be stored in Github. Please visit the [Connecticut Real Estate Sales Database](https://aqs.epa.gov/aqsweb/documents/data_api.html) to download this data.

## **Notebooks Used**
The data processing and cleaning steps are outlined in the following notebooks:
   - **`wildfire_common_analysis.ipynb`:**  
   Preprocesses wildfire and AQI datasets, calculates smoke impact using a weighted formula, and generates lag variables to account for delayed effects.

   - **`wildfire_real_estate_processing.ipynb`:**  
   Merges the processed wildfire and AQI datasets with real estate data, calculates cumulative smoke impact estimates, and generates yearly transaction volumes.

   - **`finished_analysis.ipynb`:**  
   Conducts regression analysis and time series forecasting to evaluate the relationship between wildfire smoke, air quality, and real estate metrics. Visualizations and final insights are generated in this notebook.

Intermediate datasets produced from these notebooks (`aqi_data.csv`, `filtered_real_estate_df.csv`, and `selected_processed_wildfires2.csv`) are saved in the `data/intermediate` folder for further analysis. The final dataset used for the model : `enhanced_data.csv` is stored in the `data/final` folder.  

## **Methodology**
The analysis follows these steps:
1. **Exploratory Data Analysis**:
   - Visualized historical smoke impacts, AQI trends, and real estate metrics.
   - Assessed correlations between smoke impacts and property values.
2. **Regression Modeling**:
   - Quantified relationships between smoke exposure, AQI, transaction volumes, and property values using OLS regression.
   - Incorporated lagged variables to capture delayed effects.
3. **Time Series Forecasting**:
   - Applied SARIMAX models to predict future smoke impacts and property value trends over 50 years.
   - Integrated uncertainty intervals to account for forecast variability.

## **Results**
- **Historical Trends**:
  - Significant year-over-year fluctuations in smoke impact, with increasing trends in recent decades.
  - Negative correlation between air quality (worse AQI) and property values.
- **Forecasts**:
  - Projected cumulative smoke impacts show high variability, emphasizing the need for adaptive planning.
  - Property value forecasts reveal periodic dips during years of high smoke exposure.
- To read more about my results please the `docs/` folder with writeups about my exploratory analysis (`common_analysis_visualizations_reflections.pdf`) and my final report (`DATA 512_ Final Written Report.pdf`)

## **Visualizations**
Key figures are stored in the `visuals/` folder. They include:
1. **Annual Cumulative Smoke Impact**: Historical trends in smoke exposure over time.
2. **Relationship Between Smoke Impact and Property Values**: Scatterplot showing weak correlations but notable patterns.
3. **10-Year Forecast of Smoke Impacts**: Forecasted trends with confidence intervals.

## **Reproducibility**
To reproduce the analysis:
1. Clone the repository:  
   ```
   git clone <repo-url>
   ```
2. Install dependencies:  
   ```
   pip install -r requirements.txt
   ```
3. Run the notebooks in sequence (make sure to update the relevant fields, as prompted in the directions with your desired information):
   - `wildfire_common_analysis.ipynb`
   - `wildfire_real_estate_processing.ipynb`
   - `finished_analysis.ipynb`

## **License**
This code example was developed by Trisha Prasant for use in DATA 512, a course in the UW MS Data Science degree program. The code is available under the MIT License. See the `LICENSE` file for more details. 

The datasets used in this project partly derived from the EPA AQS API which is subject to the EPA Terms of Use. The data retrieved through the API is available for reuse under the terms of use of this license, provided attribution is given.

## **Acknowledgments**
- **Wildfire Data**: [USGS Combined Wildland Fire Dataset](https://www.sciencebase.gov/catalog/item/61aa537dd34eb622f699df81).
- **Air Quality Data**: [EPA AQS API](https://aqs.epa.gov/aqsweb/documents/data_api.html).
- **Real Estate Data**: [Connecticut Real Estate Sales Database](https://aqs.epa.gov/aqsweb/documents/data_api.html).
- To the Instructors of the UW MSDS DATA 512 Course! Thank you for a great quarter :)