# data-512-Wildfire-Analysis
## Wildland Fire Analysis of Rialto, California

## Project Overview  
The goal of this project is to study the wildfire data and analyse the factors that affect the smoke released into the atmosphere. Next step is to come up with a smoke estimate and see how closely they match with the Air Quality Index. Further, we model the available data to forecast the smoke estimate of the next 25 years. 

As part of the extended analysis, this project aims to answer the research questions: 
1.	How wildfires contribute to fluctuations in the AQI.
2.	How does smoke affect the people in the city?
3.	How can these health impacts be tackled by the city council?

By addressing these questions, this study aims to contribute to the existing body of knowledge while providing practical recommendations tailored to the needs of Rialto. Building upon the predictive model of smoke estimate, the extension plan aimed to refine and adapt the model to estimate a respiratory health impacts in the city of Rialto, understanding the healthcare implications of wildfire smoke is critical, as it directly affects the well-being of residents and the capacity of healthcare systems.

## License  
### Data License  
Data pertaining to Wildland Fires, provided by the USGS, are publicly available and not subject to copyright restrictions.


AQI data is accessed through the EPA API.

### Code Attribution
Snippets of the code were taken from a code example developed by Dr. David W. McDonald for use in DATA 512, a course in the UW MS Data Science degree program. This code is provided under the Creative Commons CC-BY license.

Rest of the code is licensed under standard MIT licence.

## Access Key
To use AQI related API we need to request a key using a valid email address. The EPA then sends a confirmation email link and a 'key' that we use for all other requests. We only need to sign-up once, unless we want to invalidate the current key (by getting a new key) or we lose the key. Refer to the notebook 2_aqi_data_acquisition.ipynb for additional information.

## Wildfire Data
The input data file is too large to be uploaded to the git repository. FInd the zipped data here: https://www.sciencebase.gov/catalog/item/61aa537dd34eb622f699df81 

## Raw Data Files
`all_records.csv` which is a the wildfire dataframe which was obtained after processing the wildfire geoJson dataset.

### Schema Description

| Column Name        | Description                                                               | Data Type   |
|--------------------|---------------------------------------------------------------------------|-------------|
| `name`             | The name or identifier of the wildfire event.                             | `string`    |
| `year`             | The year in which the wildfire occurred.                                  | `integer`   |
| `shortest_distance`| The shortest distance from the wildfire's location to a reference point (e.g., city, area). | `float`     |
| `size`             | The size of the wildfire area (e.g., in acres, square miles).             | `float`     |
| `type`             | The type of the wildfire event (e.g., "Wildfire").                        | `string`    |
| `avg_distance`     | The average distance from the wildfire's location to other key points.   | `float`     |
| `perimeter_start`  | The coordinates of the starting point of the wildfire's perimeter.       | `string`    |

`aqi.csv` contains the gaseous and particulate csv data returned from the AQI API calls. This csv is a result of data processing from the API responses. 

### Schema Description

| Column Name        | Description                                                            | Data Type   |
|--------------------|------------------------------------------------------------------------|-------------|
| `state_code`       | The state code identifying the location of the measurement site.      | `integer`   |
| `county_code`      | The county code identifying the location of the measurement site.     | `integer`   |
| `site_number`      | The site number representing the specific monitoring station.         | `integer`   |
| `latitude`         | The latitude coordinate of the monitoring station.                    | `float`     |
| `longitude`        | The longitude coordinate of the monitoring station.                   | `float`     |
| `parameter_code`   | The code representing the type of pollutant being measured (e.g., carbon monoxide). | `integer`   |
| `parameter`        | The name or description of the pollutant being measured.              | `string`    |
| `sample_duration`  | The duration of the sampling period for pollutant measurement.         | `string`    |
| `arithmetic_mean`  | The arithmetic mean value of pollutant concentration over the sampling period. | `float`   |
| `units_of_measure` | The units of measurement for the pollutant concentration.              | `string`    |
| `date_local`       | The local date when the measurement was taken.                        | `date`      |
| `aqi`              | The Air Quality Index value calculated based on pollutant concentration. | `float`   |
| `year`             | The year in which the measurement was taken.                          | `integer`   |

`filtered_records.json` file contains the wildfire dataset for my city Rialto and fires within 650 miles of the city. 

### Schema Description

| Column Name        | Description                                                             | Data Type     |
|--------------------|-------------------------------------------------------------------------|---------------|
| `name`             | The name or identifier of the wildfire event.                           | `string`      |
| `year`             | The year in which the wildfire occurred.                                | `integer`     |
| `shortest_distance`| The shortest distance from the wildfire's location to a reference point (e.g., city, area). | `float`       |
| `size`             | The size of the wildfire area (e.g., in acres, square miles).           | `float`       |
| `type`             | The type of the wildfire event (e.g., "Wildfire").                      | `string`      |
| `avg_distance`     | The average distance from the wildfire's location to other key points. | `float`       |
| `perimeter_start`  | The coordinates (latitude, longitude) of the starting point of the wildfire's perimeter. | `array of floats` |

## Csv Files 
I am documenting the final csvs that were used in the plotting and analysis. All other files are considered intermediary so that while data processing, data is not lost. This is to handle the scenario of losing connections, network issues and memory issues  while the code runs. 

`aqi_1964_2024.csv` contains the AQI csv data for the year 1064 to 2024. 
This dataset contains annual air quality index (AQI) values measured over several years. The AQI indicates the level of air pollution and its potential impact on health. Each row in the dataset represents the AQI value for a specific year.

### Schema Description

| Column Name | Description                                              | Data Type      |
|-------------|----------------------------------------------------------|----------------|
| `year`      | The year the AQI measurement was recorded.              | `integer`      |
| `aqi`       | The average Air Quality Index for the given year.       | `float`        |

`fire_distance_info.csv` dataset contains information about wildfires recorded over different years. Each row represents a specific wildfire, including its name, distance from a reference point, size, type, and geographical coordinates.

### Schema Description

| Column Name        | Description                                                                      | Data Type                  |
|--------------------|----------------------------------------------------------------------------------|----------------------------|
| `name`             | The name and identifier of the wildfire.                                        | `string`                   |
| `year`             | The year the wildfire occurred.                                                  | `integer`                  |
| `shortest_distance`| The shortest distance from a specified reference point (in meters).             | `float`                    |
| `size`             | The size of the wildfire (in acres).                                            | `float`                    |
| `type`             | The type of event (e.g., "Wildfire").                                          | `string`                   |
| `avg_distance`     | The average distance from a reference point to the wildfire (in meters).        | `float`                    |
| `perimeter_start`  | The starting geographical coordinates of the wildfire's perimeter.              | `string` (Array of floats) |

`smoke_estimate_per_year.csv` contains estimates of smoke levels measured over different years. Each row represents the estimated amount of smoke present in the atmosphere for a specific year.

### Schema Description

| Column Name       | Description                                         | Data Type   |
|-------------------|-----------------------------------------------------|-------------|
| `year`            | The year when the smoke estimate was recorded.     | `integer`   |
| `smoke_estimate`  | The estimated amount of smoke (arbitrary units).   | `float`     |

`gaseous_aqi_1964_2024.csv` dataset contains air quality measurements recorded at specific monitoring sites. Each row represents an observation for gaseous air quality parameter on a given day, along with site and geographic details.

### Schema Description

| Column Name        | Description                                                                 | Data Type                  |
|--------------------|-----------------------------------------------------------------------------|----------------------------|
| `state_code`       | The code representing the U.S. state where the monitoring site is located. | `string`                   |
| `county_code`      | The code representing the county within the state where the site is located.| `string`                   |
| `site_number`      | The unique identifier for the monitoring site within the county.            | `string`                   |
| `latitude`         | The latitude of the monitoring site in decimal degrees.                    | `float`                    |
| `longitude`        | The longitude of the monitoring site in decimal degrees.                   | `float`                    |
| `parameter_code`   | The numeric code representing the air quality parameter being measured.    | `integer`                  |
| `parameter`        | The name of the air quality parameter being measured.                      | `string`                   |
| `sample_duration`  | The duration of the sampling period for the measurement.                   | `string`                   |
| `arithmetic_mean`  | The arithmetic mean value of the measured parameter during the sampling period. | `float`                |
| `units_of_measure` | The units in which the parameter is measured.                               | `string`                   |
| `date_local`       | The date of the measurement in `YYYY-MM-DD` format.                        | `date`                     |
| `aqi`              | The Air Quality Index (AQI) value for the measured parameter (may be null).| `float` or `null`          |

`particulate_aqi_1964_2024.csv` contains AQI data based on particulate matter measurements. Each row represents the air quality index and related details recorded at a specific monitoring site on a particular date.

### Schema Description

| Column Name        | Description                                                                 | Data Type   |
|--------------------|-----------------------------------------------------------------------------|-------------|
| `state_code`       | The state code identifying the location of the measurement site.           | `integer`   |
| `county_code`      | The county code identifying the location of the measurement site.          | `integer`   |
| `site_number`      | The site number representing the specific monitoring station.              | `integer`   |
| `latitude`         | The latitude coordinate of the monitoring station.                        | `float`     |
| `longitude`        | The longitude coordinate of the monitoring station.                       | `float`     |
| `parameter_code`   | The code representing the type of pollutant being measured.               | `integer`   |
| `parameter`        | The name or description of the pollutant being measured.                  | `string`    |
| `sample_duration`  | The duration of the sampling period for pollutant measurement.            | `string`    |
| `arithmetic_mean`  | The arithmetic mean value of pollutant concentration over the sampling period. | `float`  |
| `units_of_measure` | The units of measurement for the pollutant concentration.                 | `string`    |
| `date_local`       | The local date when the measurement was taken.                            | `date`      |
| `aqi`              | The Air Quality Index value calculated based on pollutant concentration.  | `integer`   |

## Extended Analysis Dataset

`COPD-Emergency-Dept-Visits-Asthma.csv` contains health-related data indicating the number of cases of COPD, asthma-related emergency department (ED) visits, and hospitalizations over different years. Each row represents the reported cases for a specific year. This data was obtained from the tracking california data explorer system.  

### Schema Description

| Column Name          | Description                                                      | Data Type   |
|----------------------|------------------------------------------------------------------|-------------|
| `Year`               | The year for which the health impact data is recorded.          | `integer`   |
| `COPD Cases`         | The number of COPD related emergency department (ED) visits. | `integer` |
| `Asthma ED Visit`    | The number of asthma-related emergency department (ED) visits.  | `integer`   |
| `Hospitalization`    | The number of Asthma related hospitalizations | `integer`   |

`future_smoke_estimate_predictions.csv` contains estimated smoke levels based on ARIMA model predictions for different years. Each row represents the estimated smoke level for a specific year.

### Schema Description

| Column Name            | Description                                           | Data Type   |
|------------------------|-------------------------------------------------------|-------------|
| `year`                 | The year for which the smoke estimate was recorded.  | `integer`   |
| `smoke_estimate_arima` | The estimated smoke level (in arbitrary units) based on ARIMA model predictions. | `float`     |

`smoke_breathing_data.csv` contains smoke estimates and the respiratory data that includes COPD cases, asthma-related emergency department visits, and hospitalizations for different years. Each row represents the data for a specific year.

### Schema Description

| Column Name              | Description                                                           | Data Type   |
|--------------------------|-----------------------------------------------------------------------|-------------|
| `year`                   | The year for which the data is recorded.                              | `integer`   |
| `smoke_estimate`         | The estimated amount of smoke present in the atmosphere (arbitrary units). | `float`     |
| `COPD Cases`             | The number of reported cases of Chronic Obstructive Pulmonary Disease (COPD). | `integer` |
| `Asthma ED Visit`        | The number of asthma-related emergency department (ED) visits.       | `integer`   |
| `Asthma-related-hospitalization` | The number of asthma-related hospitalizations.                   | `integer`   |


## Plots  
The plots generated as part of the visual analysis are stored in the folder Visulaizations. This folder contains 3 images in the PNG format. 

## Repository usage and code to replicate the results  
In order to reproduce the results, Clone this repository and execute the notebooks in the order in which they are named.  
Step 1: Run 1_wildfire_data_Acquisition.ipynb  
Step 2: Run 2_AQI_Data_Acquisition.ipynb  
Step 3: Run 3_Data_Analysis.ipynb  
Step 4: Run 4_Modelling.ipynb  
Step 5: Run 5_DataVisualization.ipynb  
Step 6: Run Extended_Analysis.ipynb  

While running Wildfire Data Acquisition code, make sure to keep the combined dataset json file in the same directory. This file is not uploaded to github because of the size. Refer the link mentioned in the section wildfire Data. Additionally, place the compute_distance script in the same directory as this notebook and import it in this script. 

Note that the data files required for each notebook is mentioned in the code comments.  Each cell in the notebook has to be run one by one in the same order. Do not execute all the cells at once because data aqusition and processing steps will take long time. 



## Limitations and Considerations  
Missing AQI records - for the responses that did not have any AQI data, I simply dropped those rows. 
In order to calculate yearly AQI value, I took an average value. 

For the calculation of smoke esitmate, The formula is explained in the Data Analysis notebook. However there are some limitations to this calculation since all factors that affect the smoke are not present in the data. For example the kind of vegetation, wind speed and the duration of the fire and how soon it was controlled.   

Public health data, such as hospitalizations and emergency visits, may be incomplete or inconsistently reported, affecting the accuracy of conclusions drawn from it. For example, healthcare facilities may not consistently record asthma-related visits or categorize them uniformly.

## Conclusion
This study sought to address critical questions about the impact of wildfire smoke on respiratory health in Rialto, CA. Specifically, it investigated:
1.	How do wildfires contribute to fluctuations in the Air Quality Index (AQI) and hence smoke estimate?
2.	How does smoke affect the health of people in the city?
3.	What measures can the city council take to mitigate these health impacts?

The findings reveal that wildfire smoke significantly exacerbates respiratory conditions, as evidenced by strong correlations between smoke estimate and increased cases of COPD, asthma-related emergency visits, and hospitalizations. Regression analyses quantified these impacts, demonstrating the severity of the problem, while predictive models highlighted persistent health burdens in the coming decades. These results emphasize the urgent need for targeted interventions to reduce smoke exposure and its associated health risks.
This research advances our understanding of human-centered data science by demonstrating how data-driven insights can directly inform public health strategies. The project integrates statistical rigor with geospatial analysis and predictive modeling. It underscores the importance of designing studies that prioritize the well-being of communities and provide actionable insights for decision-makers.
By bridging environmental and health data, this study offers a model for leveraging data science to tackle real-world challenges, empowering cities like Rialto to build resilience against climate-driven health risks. It is a call to action for policymakers to adopt evidence-based strategies that address immediate needs while planning for a sustainable future.
