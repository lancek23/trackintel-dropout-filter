# trackintel-dropout-filter

## Table of Contents
1. Introduction
2. Setup Guide
3. Code Files Usage

## Introduction
TODO

## Setup Guide
##### Downloading the data
The T-drive dataset sample is available for download [here](https://www.microsoft.com/en-us/research/publication/t-drive-trajectory-data-sample/). After downloading and unzipping the data, the highest folder (called 'release') should be placed in the same folder as the code, which should allow the code in this project to run normally and interact with the data with the expected behavior

The Geolife dataset is available for download [here](https://www.microsoft.com/en-us/research/publication/geolife-gps-trajectory-dataset-user-guide/). After downloading and unzipping the data, the highest folder (called 'Geolife Trajectories 1.3') should be placed in the same folder as the code, which should allow the code in this project to run normally and interact with the data with the expected behavior

##### Dependencies
This project was run with Python version 3.13.2

The following are the primary python libraries which must be installed to run all the files in this project:
- numpy
- pandas
- geopandas
- trackintel

See requirements.txt for versions and other requirements.

##### Running the code
All code for this project is in ipynb files. You can simply run them using "Run All," but the code blocks are separated so you may only run parts of it if you desire.

## Code Files Usage
##### t-drive_sps_final.ipynb
This file will:
- Read in the data from the downloaded T-drive dataset sample
- Generate initial staypoints for this data using the trackintel library
- Add data dropout randomly to the trajectories in this dataset
- Generate staypoints a second time, now using the data with dropouts
- Run a function which filters out the staypoints known to be spurious as a result of this dropout
- Generate some resultant data based on the filter function to demonstrate the filter's functionality

##### geolife_sps_final.ipynb
This file will:
- Read in the data from the downloaded Geolife dataset
- Generate initial staypoints for this data using the trackintel library
- Add data dropout randomly to the trajectories in this dataset
- Generate staypoints a second time, now using the data with dropouts
- Run a function which filters out the staypoints known to be spurious as a result of this dropout
- Generate some resultant data based on the filter function to demonstrate the filter's functionality
