# Tuesday 03/28/23
### Elevation code as a function

```
function [latiVec, longVec] = elevation(in)

[A,R] = readgeoraster(in,"OutputType","single");
latlim1 = R.LatitudeLimits;
lonlim1 = R.LongitudeLimits;

figure
usamap(latlim1,lonlim1)
geoshow(A,R,"DisplayType","texturemap")
demcmap(A)
colorbar
title("Elevation Data of Florida")

% Creating latitude (vertical) and longitude (horizontal) vectors
latiVec = zeros(R.RasterSize(1), 1);
longVec = zeros(1, R.RasterSize(2));

latiUnit = (abs(latlim1(1) - latlim1(2)))/R.RasterSize(1);
longUnit = (abs(lonlim1(1) - lonlim1(2)))/R.RasterSize(2);

% inputing values for latitude vector
for i = 1:R.RasterSize(1)
    latiVec(i,1) = latlim1(1) + (latiUnit * (i-1));
end

% inputing values for longitude vector
for j = 1:R.RasterSize(2)
    longVec(j,1) = lonlim1(1) + (longUnit * (j-1));
end

%creating new map of coastline with "fake data" 
figure
C = (A - 1.99876);
usamap(latlim1,lonlim1)
geoshow(C,R,"DisplayType","texturemap")
demcmap(C)
colorbar
title("New Coastline of Florida - (Elevation - 1.99876)")

end 
```

### Prediction data code (start)
```
function [] = predictionData(dataIn)

P = readmatrix(dataIn);

%create new matrix C that only contains columns of P that have the data 
C = P(:, 14:28);
C(1:12, :) = [];

%create new matrix that only contains the two columns of the lat lon
L = P(:, 6:7);
L(1:27,:) = [];


%call elevation function to get lat lon vectors to use here  
[latlim1, lonlim1] = elevationData("TitusvilleFlorida.tif");


%index L matrix first column to match latiVec & longVec from elevation
[rowsL,columnsL] = size(L);

newLatindex = [];
newLonindex = [];

%index into latitude colomn
z = 1;
for i = 1:rowsL
    if (L(i,1) >= latlim1(1)) && (L(i,1) <= latlim1(2))
        newLatindex(z) = i;
        z = z+1;
    end 
end

%index into longitude column
a = 1;
for j = 1:rowsL
    if (L(j,2) >= lonlim1(1)) && (L(j,2) <= lonlim1(2))
        newLonindex(a) = j;
        a = a+1;
    end
end
end

```

# Wednesday 03/29/23
### Start of final function code 

```
function [] = finalFunction()

%user input to get which city to run the code for 
    prompt = "Choose which city you would like to view the new coastline for: Boston, Titusville, San Francisco, or New Orleans - ";
    city = input(prompt, "s");

%user input to get which year to output new coastline for 
    prompt = "What year would you like to see the new coastline for: " ;
    year = str2double(input(prompt, "s"));

%pulling the data for which city the user chose and creating the new matrix of that corresponding data for that region
    if city == "Titusville"
        [latlim1, lonlim1] = elevationData("TitusvilleFlorida.tif");
        [newLatindex, newLonindex] = predictionData("PredictionData.csv");
       
        last = length(newLatindex);
        lastLon = length(newLonindex);

        [columnsL, P] = predictionData("PredictionData.csv");

       % need help with this for loop (matrix vs. table dilemma) and
       % extracting the single column depending on what year the user wants
       % to see
        for c = 1: columnsL
            if P(:,c) == year
                NewMatrix = P(newLatindex(1):newLatindex(last), c);
                NewMatrix2 = P(newLonindex(1):newLonindex(lastLon), c);            
            end
        end 

%creating the final output map of the elevation minus the new matrix of data
        [A,R] = elevationData("TitusvilleFlorida.tif");
        figure
        Final = (A - ([NewMatrix2 NewMatrix]));
        usamap(latlim1,lonlim1)
        geoshow(Final,R,"DisplayType","texturemap")
        demcmap(Final)
        colorbar
        title("Coastline of Titusville, Florida in year ", year)

 
%     elseif city == "Boston"
%         elevationData("Boston.tif");
%         predictionData("PredictionData.csv");
%          
%     elseif city == "San Francisco"
%         elevationData("SanFrancisco.tif");
%         predictionData("PredictionData.csv");
%     elseif city == "New Orleans"
%         elevationData("NewOrleans.tif");
%         predictionData("PredictionData.csv");
    end 

end 
```

### Prediction Data Function
```
function [newLatindex, newLonindex] = predictionData(dataIn)

P = readmatrix(dataIn);

%create new matrix C that only contains columns of P that have the data 
C = P(:, 14:28);
C(1:12, :) = [];

%create new matrix that only contains the two columns of the lat lon
L = P(:, 6:7);
L(1:27,:) = [];


%call elevation function to get lat lon vectors to use here  
[latlim1, lonlim1] = elevationData("TitusvilleFlorida.tif");


%index L matrix first column to match latiVec & longVec from elevation
[rowsL, columnsL] = size(L);

newLatindex = zeros();
newLonindex = zeros();

%index into latitude colomn
z = 1;
for i = 1:rowsL
    if (L(i,1) >= latlim1(1)) && (L(i,1) <= latlim1(2))
        newLatindex(z) = i;
        z = z+1;
    end 
end

%index into longitude column
a = 1;
for j = 1:rowsL
    if (L(j,2) >= lonlim1(1)) && (L(j,2) <= lonlim1(2))
        newLonindex(a) = j;
        a = a+1;
    end
end
end
```

### Elevation Data Function
```
function [latiVec, longVec] = elevationData(in)

[A,R] = readgeoraster(in,"OutputType","single");
latlim1 = R.LatitudeLimits;
lonlim1 = R.LongitudeLimits;

% figure;
% usamap(latlim1,lonlim1);
% geoshow(A,R,"DisplayType","texturemap");
% demcmap(A);
% colorbar;
% title("Elevation Data of Florida");

% Creating latitude (vertical) and longitude (horizontal) vectors
latiVec = zeros(R.RasterSize(1), 1);
longVec = zeros(1, R.RasterSize(2));

latiUnit = (abs(latlim1(1) - latlim1(2)))/R.RasterSize(1);
longUnit = (abs(lonlim1(1) - lonlim1(2)))/R.RasterSize(2);

% inputing values for latitude vector
for i = 1:R.RasterSize(1)
    latiVec(i,1) = latlim1(1) + (latiUnit * (i-1));
end

% inputing values for longitude vector
for j = 1:R.RasterSize(2)
    longVec(j,1) = lonlim1(1) + (longUnit * (j-1));
end

end 
```

# Thursday 03/30/23
### Debuging predictionData function

We were getting errors in the prediction data values we wanted, so I checked table P. I realized that table P was not being read correctly. The prediction data file had a lot of blank cells in the first few rows as they were used for explinations and citations. For now, we are hard coding MatLab to start reading the .csv file at line 18, so that we have the correct headers, using this line of code:
```
predictTable = readtable('SLR_TF U.S. Sea Level Projections.csv', 'NumHeaderLines', 17);
```
Relevent links:
<br />https://www.mathworks.com/matlabcentral/answers/593539-problem-to-read-csv-file-with-a-blank-line
<br />https://www.mathworks.com/help/matlab/ref/readtable.html#bvghccx
<br />Answer that worked: https://www.mathworks.com/matlabcentral/answers/1705655-reading-csv-file-with-header-and-other-data

### Changing the prediction data table header

Relevant links:
<br />https://www.mathworks.com/help/matlab/ref/table.renamevars.html
<br />
<br />
<br />
<br />
<br />
<br />
<br />


### Updated prediction data function 

```
function [newLatindex, newLonindex, columnsC, Pdata, L] = predictionData(dataIn)

predictTable = readtable(dataIn, 'NumHeaderLines', 17);

% %create new matrix C that only contains columns of P that have the data 
C = predictTable(:, 14:28);

[~, columnsC] = size(C);
    
Pdata = renamevars(C, ["RSL2005_cm_", "RSL2020_cm_", "RSL2030_cm_", "RSL2040_cm_", ...
    "RSL2050_cm_", "RSL2060_cm_", "RSL2070_cm_", "RSL2080_cm_", "RSL2090_cm_", ...
    "RSL2100_cm_", "RSL2110_cm_", "RSL2120_cm_", "RSL2130_cm_", "RSL2140_cm_", ...
    "RSL2150_cm_"], [2005, 2020, 2030, 2040, 2050, 2060, 2070, 2080, 2090, ...
    2100, 2110, 2120, 2130, 2140, 2150]);

%create new matrix that only contains the two columns of the lat lon
L = predictTable(:, 6:7);
L(1:15,:) = [];


%call elevation function to get lat lon vectors to use here  
% [latlim1, lonlim1, latiVec, longVec] = elevationData("Newport.tif");
N = zeros(size(L));

%index L matrix first column to match latiVec & longVec from elevation
[rowsL,columnsL] = size(N);

% latitude - 1st colomn
for x = 1:rowsL 
    N(x,1) = L.('Lat')(x);
end

% longitude - 2nd colomn
for y = 1:rowsL
    N(y,2) = L.('Long')(y);
end

newLatindex = zeros();
newLonindex = zeros();

%index into latitude colomn
a = 1;
for i = 1:rowsL
    if (N(i,1) >= latlim1(1)) && (N(i,1) <= latlim1(2))
        newLatindex(a) = i;
        a = a+1;
    end
end

b = 1;
for j = 1:rowsL
    if (N(j,2) >= lonlim1(1)) && (N(j,2) <= lonlim1(2))
        newLonindex(b) = j;
        b = b+1;
    end
end

predictionIndex = intersect(newLonindex,newLatindex);

end
```

### Updated final function
```
function [] = finalFunction()

%user input to get which city to run the code for 
    prompt = "Choose which city you would like to view the new coastline for (Newport): ";
    city = input(prompt, "s");

%user input to get which year to output new coastline for 
    prompt = "What year would you like to see the new coastline for: " ;
    wantedYear = str2double(input(prompt, "s"));

%pulling the data for which city the user chose and creating the new matrix of corresponding data
    if city == "Newport"
        [latlim1, lonlim1, latiVec, longVec, A, R] = elevationData("Newport.tif");
        [newLatindex, newLonindex, columnsC, Pdata, L] = predictionData("PredictionData.csv");
       
%matching columns of the data matrix to the correct data rows for that year
%[columnsL, C] = predictionData("PredictionData.csv");   
    last = length(newLatindex);
    lastLon = length(newLonindex);
    for year = 1:columnsC
        if Pdata(:,year) == wantedYear
                data = Pdata(newLatindex(1):newLatindex(last), c);
                data2 = Pdata(newLonindex(1):newLonindex(lastLon), c);            
        end
    end 

%creating the final output map of the elevation minus the new matrix of data
%[A,R] = elevationData("Honolulu1.tif");
        figure
        Final = (A - ([data data2]));
        usamap(latlim1,lonlim1)
        geoshow(Final,R,"DisplayType","texturemap")
        demcmap(Final)
        colorbar
        title("Coastline of Newport, RI in year ", wantedYear)
        
    end  
end 
```




