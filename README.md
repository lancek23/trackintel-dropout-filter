# trackintel-dropout-filter

## Table of Contents
1. Introduction
2. Setup Guide
3. Code Files Usage

## Introduction
This repository first presents a weakness of the Sliding Window Staypoint Detection algorithm (see the original paper [here](https://dl.acm.org/doi/abs/10.1145/1463434.1463477)), specifically using the implementation in the Trackintel library for trajectory analysis (see Trackintel [repository](https://github.com/mie-lab/trackintel) and [documentation](https://trackintel.readthedocs.io/en/latest/)). Second, it provides a function for a solution to this issue.

The weakness is as follows: GPS trajectory data often experiences data dropout- times in which the user being tracked does not transmit any data. This may be caused by device malfunction, user error, device batteries dying, or environmental factors such as tunnels. The staypoint detection algorithm therefore provides functionality to handle this data dropout. In the Trackintel library, this is handled with the "gap_threshold" parameter, which is a time delta. Any amount of data dropout taking place during a staypoint which lasts for less than the gap_threshold can be ignored and simply included in the staypoint.

However, if there is an amount of data dropout during the trajectory which is (1) long enough to constitute a staypoint, but (2) short enough to be under the gap threshold, the algorithm will identify a staypoint at this time, even if the user is in the middle of a tripleg, creating spurious staypoints.

The solution we provide then, is as follows: simply identify the sufficiently long dropouts in the trajectory, then compare their start times with those of the identified staypoints. We demonstrate this on two datasets- T-drive, a collection of trajectories from taxis, and Geolife, a collection of trajectories from volunteers over different modalities.

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
