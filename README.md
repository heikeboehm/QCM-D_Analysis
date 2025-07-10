# QCMD_Analysis

QCM-D Analysis Tools for Processing QSense-Analyzer Data

## Overview

QCMD_Analysis is a collection of Python programs designed to process and analyze data recorded on a QSense-Analyzer. These programs help break down the data into independent, unified datasets for each sensor position and save the data in a "brick-style" format for easier comparison between experiments. The analysis pipeline differs depending on the QCM-D module used: (1) flow modules or (2) open modules can be analyzed separetly. The resulting brick struckture of either can be compared to one another afterwards.

Example graph for one measurement with different overtones in brick-style presentation:

![Plot_CBP-GS_BGI-CG_3926427_20231107_S2_QCMD_bricks](https://github.com/heikeboehm/QCMD_Analysis/assets/134604887/42d480e7-c105-4778-98e9-ab9a07ccbfe4)



## Features of Flow Module Analysis

### 1. QCMD_flow_to_adj_folder
- Separates data for each of the possible four sensors with the respective, corrected timeline. For each sensor two csv files are saved:
    - adj_qcmd_data: 
        Adjusted QCM-D dataset with time in seconds, normalized Δf/n, and normalized D for all overtones. 
          Normalization is achieved by subtracting the averaged value of the first 100 data points for each measured frequency and dissipation overtone.
          All normalized frequency values have been divided by the overtone number to represent Δf/n.
    - adj_timeline_data: 
        Timeline given in the text file for the respective sensor, including the time in seconds adjusted with respective lag time, 
        the flow speed in µm/min, and information on the solution change. 

### 2. QCMD_flow_adj_to_bricks_folder
- Reads in the csv files created by QCMD_flow_to_adj_folder
    (1) plots 7th overtone of complete experiment (saves this plot) and asks user to specify the dynamic brick(s)
    (2) plots the bricks with all overtones (saves this plot) and asks user to specify brick pairs to calculate Sauerbrey mass -> saves a plot of the sauerbrey mass for each brick-pair for each overtone and calculates the average value saved in the plot as well.

### 3. QCMD_flow_bricks_to_plots
- Reads in adj_qcmd_bricks_data.csv; adj_timeline_bricks; and a csv file called "plotting" which outlines which Data to plot into which graph and which brick
- returns the resepective plots as pdfs

## Features of Open Module Analysis

### 1. QCMD_raw_to_adj
- Separates data for each of the possible four sensors with the respective, corrected timeline. For each sensor two csv files are saved:
    - adj_qcmd_data: 
        Adjusted QCM-D dataset with time in seconds, normalized Δf/n, and normalized D for all overtones. 
          Normalization is achieved by subtracting the averaged value of the first 100 data points for each measured frequency and dissipation overtone.
          All normalized frequency values have been divided by the overtone number to represent Δf/n.
    - adj_timeline: 
        Timeline given in the text file for the respective sensor, including the time in seconds originally recorded and the adjusted time as determined by a min or max within 
        the 4min time window of the original time indicating the exchange of liquids in open modules and the information given on the solution change,
        the flow speed in µm/min, and information on the solution change. including changes of solutions

### 2. QCMD_open_adj_to_bricks_folder
- Reads in the csv files created by QCMD_open_to_adj_folder
    (1) plots 7th overtone of complete experiment (saves this plot) and asks user to specify the dynamic brick(s)
    (2) plots the bricks with all overtones (saves this plot) and asks user to specify brick pairs to calculate Sauerbrey mass -> saves a plot of the sauerbrey mass for each              brick-pair for each overtone and calculates the average value saved in the plot as well.

### 3. QCMD_open_bricks_to_plots
- Reads in adj_qcmd_bricks_data.csv; adj_timeline_bricks; and a csv file called "plotting" which outlines which Data brick to plot into which graph 
- returns the resepective plots as pdfs      


## Example Plots

Here are some example plots generated using QCMD_Analysis:

(1) Full experiment with points for change of solutions indicated - only 7th overtone shown:
    ![Plot_CBP-GS_BGI-CG_3926427_20231107_S2_QCMD_n7](https://github.com/heikeboehm/QCMD_Analysis/assets/134604887/f1435254-328c-4e2a-ac9b-9bfbc3719256)

(2) Comparing two datasets:
    ![Plot_10](https://github.com/heikeboehm/QCMD_Analysis/assets/134604887/38ad0930-b456-40a6-9eab-a922e2b1f0be)

(3) Overview of calculated values using the Sauerbrey mass calculation for each overtone:
    ![Plot_CBP-GS_BGI-CG_3926427_20231107_S2_QCMD_sauerbrey](https://github.com/heikeboehm/QCMD_Analysis/assets/134604887/09012127-04b1-4b54-a4e0-74e7bd6b87c7)
