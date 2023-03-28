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

# Tuesday 03/28/23
### Prediction data code (start)
```
P = readtable('SLR_TF U.S. Sea Level Projections.csv');

%create new matrix C that only contains columns of P that have the data 
C = P(:, 14:28);
C(1:12, :) = [];

%create new matrix that only contains the two columns of the lat lon
L = P(:, 6:7);
L(1:27,:) = [];


%call elevation function to get lat lon vectors to use here  
[latitude, longitude] = elevation("USGS_13_n26w_081_20221103.tif");


%index L matrix first column to match latiVec & longVec from elevation
[rowsL,columnsL] = size(L);
for i = 1:rowsL
    for j = 1:columnsL
        if L(i,j) == latiVec(i,:)
            N 
        end 
        if L(i,j) == longVec(i,:)

        end 
    end 
end 
```
