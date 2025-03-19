# NOAA ISD Weather Data Processor

This project downloads, processes, and analyzes hourly weather data from the NOAA Integrated Surface Database (ISD) for eight major US cities from 2019-2024. It will be an essential source of data for the analysis of rideshare data.

## Project Overview

The NOAA Integrated Surface Database (ISD) contains global hourly weather observations from airports and other weather stations. This project focuses on extracting, cleaning, and analyzing weather data for major US cities to support various analyses including potential correlation with taxi demand patterns.

## Features

- Downloads weather station data from NOAA's public AWS S3 bucket
- Identifies the most reliable weather stations for each target city
- Downloads and processes hourly weather observations
- Extracts key weather metrics (temperature, precipitation, wind speed)
- Handles data cleaning, deduplication, and filling missing values
- Creates visualizations for data analysis

## Target Cities

- New York City
- Los Angeles
- Chicago
- Miami
- Houston
- Boston
- Minneapolis
- Seattle

## Directory Structure

```
weather_noaa/
├── data/
│   ├── raw/            # Downloaded raw data
│   │   └── isd_data/   # Raw weather station files
│   └── processed/      # Cleaned and transformed data
├── notebooks/          # Jupyter notebooks for each processing step
├── scripts/            # Python scripts (converted from notebooks)
└── venv/               # Virtual environment
```

## Setup and Installation

1. Clone this repository
2. Create a virtual environment:
   ```bash
   python3 -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```
3. Install dependencies:
   ```bash
   pip install pandas numpy matplotlib jupyter boto3 google-cloud-bigquery tqdm
   ```

## Processing Steps

### 1. Exploring the AWS Data Source

- `01_explore_aws_data.ipynb`: Examines the NOAA ISD data available in the public AWS S3 bucket
- Identifies the data structure, file format, and available years
- Provides insights into the source data organization

### 2. Finding Stations for Target Cities

- `02_find_city_stations.ipynb`: Identifies the most suitable weather stations for each target city
- Uses station history data to find airports or other reliable stations
- Ensures stations have data available for the entire period of interest (2018-2024)
- Creates a mapping between stations and their respective cities

### 3. Downloading Weather Data

- `03_download_weather_data.ipynb`: Downloads hourly weather data files from AWS S3
- Efficiently handles file retrieval with progress tracking
- Validates downloaded files
- Generates reports on download success and file availability

### 4. Processing Weather Data

- `04_process_weather_data.ipynb`: Extracts, transforms, and cleans the weather data
- Parses the fixed-width format of ISD files
- Extracts key weather metrics (temperature, wind speed, precipitation)
- Handles data issues including:
  - Duplicate entries for the same hour
  - Missing hours in the dataset
  - Scaling factors for units
  - Special handling for precipitation data

### 5. Data Analysis and Visualization

The processed data includes several visualizations:
- Records by city
- Temperature trends over time
- Precipitation patterns
- Data completeness analysis

## Data Format and Features

The processed weather data includes:
- `city`: Target city name
- `datetime`: Timestamp in ISO format
- `date`: Date component (YYYY-MM-DD)
- `hour`: Hour of the day (0-23)
- `temperature`: Temperature in Celsius
- `wind_speed`: Wind speed in meters per second
- `precipitation`: Precipitation in millimeters
- `latitude`, `longitude`: Geographic coordinates for each station

## Challenges and Solutions

### Data Format Complexity
- The ISD data uses a complex fixed-width format with mandatory and optional sections
- Solution: Carefully implemented parser following NOAA documentation

### Missing Data
- Weather stations occasionally have missing observations
- Solution: Forward-fill missing hours with data from the previous hour

### Duplicate Records
- Some hours have multiple observations
- Solution: Group by city, date, and hour, and aggregate numeric values

### Precipitation Data Issues
- Precipitation data can represent different time periods
- Solution: Special handling of precipitation codes, normalization for longer periods

## Data Source

This project uses the NOAA Integrated Surface Database (ISD) available as a public dataset on AWS:
`s3://noaa-isd-pds/`

