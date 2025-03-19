# NOAA ISD Data Processor

A project to download, process, and analyze NOAA Integrated Surface Database (ISD) weather data for eight major US cities from 2018-2024.

## Project Structure
- `data/raw`: Downloaded raw data files
- `data/processed`: Cleaned and processed data files
- `scripts`: Python scripts for data downloading and processing
- `notebooks`: Jupyter notebooks for analysis
- `docs`: Project documentation

## Setup
1. Clone this repository
2. Create virtual environment: `python3 -m venv venv`
3. Activate virtual environment: `source venv/bin/activate`
4. Install dependencies: `pip install -r requirements.txt`

## Usage
1. Run `scripts/download_stations.py` to identify and download station data
2. Run `scripts/download_data.py` to download weather data
3. Run `scripts/process_data.py` to parse and clean the data
4. Run `scripts/upload_bigquery.py` to upload to BigQuery
