# Software Installation & Code Importation
## Installation Process

The software required to run this code is MATLAB_R2022b or any newer version of MatLab. First, you will have to download the correct prediction data file which is linked in this repository under the folder named "data". This file should be named "SLR_TF U.S. Sea Level Projections.csv". Then, you will need to download every code file under the folder named "insert name".

Once all the MatLab (*.m*) files are downloaded to your device and opened in your MatLab window, you will need to also import the prediction data file (that you have already downloaded to your device) into your MatLab folder where you are going to run the files for this project. The specific folder in your MatLab window is not important - the only requirement is that you have all the data files and script files in the same folder when you run the final function script. 

## Code Importation & Script Run Process

The code files that should be imported into MatLab are of the following: 
1. finalFunction.m
2. predictionTable.m
3. elevationDataFunction.m
4. Region.m 
5. rangeparse.m
6. fetchregion.m
7. ElevationData.m
8. dispelev.m

Note: Files #4, #5, #6, #7, #8 are referenced from the open source MatLab code “terrain-elevation” posted by “spfrommer” on GitHub.
https://github.com/spfrommer/terrain-elevation


These files can be found in the folder named 'Final Code Files' in this repository. Once these are all open in your MatLab window, the only file you will need to run in order to see the final output maps of the two figures (original elevation data & predicted new coastline) is the script named "finalFunction.m". 

Once you run this script, there will be three prompts that you will need to answer in order to run the script. The three prompts are: "Choose which city you would like to view the new coastline for: " , "Choose which scenario you would like to view the new coastline for: " , and "Choose which year you would like to view the new coastline for: ". 

Once the prompts are answered by pressing the enter key, wait for the two figures to show up on your screen. The figure named "Elevation Data" is of the original elevatoin data in the present day. The figure named "Prediction Data" is of the new predicted coastline for the year chosen. 


### Overview of Each Software Module

#### *finalFunction.m* - Script file:

Get Prediction Data

  1. The finalFunction is a script where the three user inputs are prompted and saved as the three variables named *'wantedRegion'*, *'wantedYear'* and *'wantedScenario'*. 
  2. The script calls the *predictionTable* function to get the prediction data and stores it in a table with variable name *'newPTable'*. 
  3. The code indexes through *'newPTable'* to find and extract the data that match the *'wantedRegion'* and *'wantedYear'*.
      - A "_for_ loop" nested with an "_if_ statement" is used to find the index of the desired rows.
        - Looks to match the *'wantedRegion'* name to the 'NOAAName' column.
      - A new table with variable name *'predictionRegion'* is created and copies the data of: Latitude; Longitude; Scenario; 2020; 'wantedYear', based on the row index. 
  4. The code indexes through *'predictionRegion'* to find and extract the data that match the *'wantedScenario'*.
      - A similar "_for_ loop and "_if_ statement" is used.
        - Looks to match the *'wantedScenario'* to the 'Scenario' column.

Get Elevation Data

  5. The script calls the *elevationDataFunction* function to get the elevation data of the desired region based on the latitude and longitude geographical coordinates extracted from the prediction data.
      - The elevation values are stored in a matrix with variable name *'regionMat'*.
      - Other information including geographical area (e.g. North/West for Boston), raster size, units, etc. are stored in a matrix with variable name *'R'*.
      
Analysis of Data
      
  6. The script subtracts the prediction value of the 'wantedYear' by that of the year 2020 and divides the value by 100, then stores the value as a variable named *'seaLevelRise'*.
       - The elevation data are of 2020 and the prediction data are of 2005.
       - Division by 100 is to convert the unit from centimeter (prediction data unit) to meter (elevation data unit).
  7. The script subtracts the whole *'regionMat'* matrix by the *'seaLevelRise'* value to create the predicted elevation matrix named *'predictedCoastline'*.
  8. The script displays the predicted map based on the elevation matrix *'predictedCoastline'* and the information matrix *'R'*.


#### *predictionTable.m* - Function file: 

- This function's main purpose is to import the prediction data file and extract the data needed for the final function.
1. The function reads the _.csv_ data file into a table starting at line 17.
     - This is to exclude the notes and explinations in the first few rows of the file.
     - Those notes and explinations are useful for better understanding the file, but pose problems when the file is used.
2. The function renames the 'year' headers from _"RSL[year]_cm_"_ to just the [year] numbers.


#### *elevationDataFunction.m* - Function file: 

- The main purpose of this function is the display the current elevation data on a map. The output of this function is a figure map of the current elevatoin for the given region that the user inputs. This function calls the fetchregion function to get the raw elevatoin data for the wanted region, and then also calls the readelevation function to get the correct latitude and longitude values in a new matrix. 
- There is a for loop that fixes the map's color scheme - originally the map showed green where the water was supposed to be and also green where the land was. This for loop sets the elevation equal to 0 for the display and sets any water as negative numbers so that the map registers negative numbers as under sea level turning it a blue color. 

#### *Region.m* - Function file: 

- This script's main purpose is to define the function called 'readelevation'. 
- This file is from the open source MatLab code “terrain-elevation” posted by “spfrommer” on GitHub.
- The function readelevation pulls the elevation from the existing elevation data files in the data server and copies the longitude and latitude values to create a new elevation matrix. 

#### *rangeparse.m* - Function file: 

- This function's main purpose is to find the latitude and longitude values of the top left corner to cover the given range of the region. 
- Uses bulit in functions from MATLAB.
- This file is from the open source MatLab code “terrain-elevation” posted by “spfrommer” on GitHub.


#### *fetchregion.m* - Function file: 

- This file is from the open source MatLab code “terrain-elevation” posted by “spfrommer” on GitHub.
- The function is called in elevationDataFunction.m 
- The purpose of this function is to find the exact location and data of a given region from the USGS elevation data. In doing so, it calls the rangepars function and uses two for loops to download the zipped files of the specified region, extract the zip file from the area, and then copies the path into a new region array for the raw data. 

#### *ElevationData.m* - Function file: 


#### *dispelev.m* - Function file: 



