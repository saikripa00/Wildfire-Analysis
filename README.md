# data-512-Wildfire-Analysis
## Wildland Fire Analysis of Rialto, California

## Project Overview  
The goal of this project is to study the wildfire data and analyse the factors that affect the smoke released into the atmosphere. Next step is to come up with a smoke estimate and see how closely they match with the Air Quality Index. Further, we model the available data to forecast the smoke estimate of the next 25 years.  

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
This folder contains all_records.csv which is a the wildfire dataframe which was obtained after processing the wildfire geoJson dataset.
aqi.csv contains the gaseous and particulate csv data returned from the AQI API calls. This csv is a result of data processing from the API responses. 
filtered_records.json file contains the wildfire dataset for my city Rialto and fires within 650 miles of the city. 

## Csv Files 
I am documenting the final csvs that were used in the plotting and analysis. All other files are considered intermediary so that while data processing, data is not lost. This is to handle the scenario of losing connections, network issues and memory issues  while the code runs. 

aqi_1964_2024.csv contains the AQI csv data for the year 1064 to 2024. 
This dataset contains annual air quality index (AQI) values measured over several years. The AQI indicates the level of air pollution and its potential impact on health. Each row in the dataset represents the AQI value for a specific year.

### Schema Description

| Column Name | Description                                              | Data Type      |
|-------------|----------------------------------------------------------|----------------|
| `year`      | The year the AQI measurement was recorded.              | `integer`      |
| `aqi`       | The average Air Quality Index for the given year.       | `float`        |

fire_distance_info.csv dataset contains information about wildfires recorded over different years. Each row represents a specific wildfire, including its name, distance from a reference point, size, type, and geographical coordinates.

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

smoke_estimate_per_year.csv contains estimates of smoke levels measured over different years. Each row represents the estimated amount of smoke present in the atmosphere for a specific year.

### Schema Description

| Column Name       | Description                                         | Data Type   |
|-------------------|-----------------------------------------------------|-------------|
| `year`            | The year when the smoke estimate was recorded.     | `integer`   |
| `smoke_estimate`  | The estimated amount of smoke (arbitrary units).   | `float`     |


## Plots  
The plots generated as part of the visual analysis are stored in the folder Visulaizations. This folder contains 3 images in the PNG format. 

## Repository usage and code   
In order to reproduce the results, Clone this repository and execute the notebooks in the order in which they are named. they are named by number_name.  
 
While running Wildfire Data Acquisition code, make sure to keep the combined dataset json file in the same directory. This file is not uploaded to github because of the size. Refer the link mentioned in the section wildfire Data. Additionally, place the compute_distance script in the same directory as this notebook and import it in this script. 

## Limitations and Considerations  
Missing AQI records - for the responses that did not have any AQI data, I simply dropped those rows. 
In order to calculate yearly AQI value, I took an average value. 

For the calculation of smoke esitmate, The formula is explained in the Data Analysis notebook. However there are some limitations to this calculation since all factors that affect the smoke are not present in the data. For example the kind of vegetation, wind speed and the duration of the fire and how soon it was controlled. 

