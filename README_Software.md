# Software Installation & Code Importation
## Installation Process

The software required to run this code is MATLAB_R2022b or any newer version of MatLab. First, you will have to download the correct prediction data file which is linked in this repository under the folder named "data". This file should be named "SLR_TF U.S. Sea Level Projections.csv". Then, you will need to download every code file under the folder named "insert name".

Once all the MatLab ".m" files are downloaded to your device and opened in your MatLab window, you will need to also import the prediction data file (that you have already downloaded to your device) into your MatLab folder where you are going to run the files for this project. The specific folder in your MatLab window is not important - the only requirement is that you have all the data files and script files in the same folder when you run the final function script. 

## Code Importation & Script Run Process

The code files you will need to import into your MatLab window are of the following file names: 
1. Region.m 
2. rangeparse.m
3. predictionTable.m
4. finalFunction.m
5. fetchregion.m
6. elevationDataFunction.m
7. ElevationData.m
8. dispelev.m

These files can be found in the folder named 'Final Code Files' in this repository. Once these are all open in your MatLab window, the only file you will need to run in order to see the final output maps of the two figures (original elevation data & predicted new coastline) is the script named "finalFunction.m". 

Once you run this script, there will be three prompts that you will need to answer in order to run the script. The three prompts are: "Choose which city you would like to view the new coastline for: " , "Choose which scenario you would like to view the new coastline for: " , and "Choose which year you would like to view the new coastline for: ". 

Once the prompts are answered by pressing the enter key, wait for the two figures to show up on your screen. The figure named "Elevation Data" is of the original elevatoin data in the present day. The figure named "Prediction Data" is of the new predicted coastline for the year chosen. 


### Overview of Each Software Module

1. Region.m file: 

- This script's main purpose is to define the function called 'readelevation'. 


2. rangeparse.m file: 

- This function's main purpose is to 

3. predictionTable.m file: 

- This function's main purpose is to import the prediction data file and extract the data needed for the final function. First, the function reads the data into a table 

4. finalFunction.m file: 

- The final function script is where the three user prompts are set up and stores the user input as three variables named 'wantedRegion', 'wantedYear' and 'wantedScenario'. Then, the script calls the 'predictionTable' function to get the data and stores it in the variable called 'newPTable'. 

5. fetchregion.m file: 

- called in elevationDataFunction.m 
- The purpose of this function is to 

6. elevationDataFunction.m file: 


7. ElevationData.m file: 


8. dispelev.m file: 



