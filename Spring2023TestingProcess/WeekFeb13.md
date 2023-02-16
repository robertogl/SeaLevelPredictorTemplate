# Tues 02/14/2023
### Display Basemap of Boston
```
% Code for Basemap of Boston (zoomed out)

%Use latitude and longitude limits from elevation data
[~,R] = readgeoraster("USGS_13_n43w071_20220713.tif","OutputType","double");
latlim1 = R.LatitudeLimits;
lonlim1 = R.LongitudeLimits;

%Specify latitude and longitude limits for the basemap image from elevation
%[latlim,lonlim] = [latlim1,lonlim1];
latlim = [41,43]; %latlim1;
lonlim = [-72, -69]; %lonlim1;

%[latlim,lonlim] = geoquadline(lat,lon);
%[latlim,lonlim] = bufgeoquad(latlim,lonlim,10,10);

%Read an image for the region from the "bluegreen" basemap
[A,RA] = readBasemapImage("colorterrain",latlim,lonlim,25);

%Extract the Web Mercator coordinates of the basemap image from the reference object.
[xGrid,yGrid] = worldGrid(RA);
[latGrid,lonGrid] = projinv(RA.ProjectedCRS,xGrid,yGrid);

%Create map
figure
h = worldmap(latlim,lonlim);
getm(h,"mapprojection")
geoshow(latGrid,lonGrid,A)
geoshow(lat,lon,DisplayType="point",Marker="pentagram")
title("Boston")
subtitle("Basemap")


# Thurs 02/16/2023
### Display Basemap of Miami
```
% Code for Basemap of Miami (zoomed out)

%Use latitude and longitude limits from elevation data
[~,R] = readgeoraster("USGS_13_n26w081_20221103.tif","OutputType","double");
latlim1 = R.LatitudeLimits;
lonlim1 = R.LongitudeLimits;

%Specify latitude and longitude limits for the basemap image from elevation
%[latlim,lonlim] = [latlim1,lonlim1];
latlim = [24,28]; %latlim1;
lonlim = [-82,-78]; %lonlim1;

%[latlim,lonlim] = geoquadline(lat,lon);
%[latlim,lonlim] = bufgeoquad(latlim,lonlim,10,10);

%Read an image for the region from the "bluegreen" basemap
[A,RA] = readBasemapImage("colorterrain",latlim,lonlim,25);

%Extract the Web Mercator coordinates of the basemap image from the reference object.
[xGrid,yGrid] = worldGrid(RA);
[latGrid,lonGrid] = projinv(RA.ProjectedCRS,xGrid,yGrid);

%Create map
figure
h = worldmap(latlim,lonlim);
getm(h,"mapprojection")
geoshow(latGrid,lonGrid,A)
geoshow(lat,lon,DisplayType="point",Marker="pentagram")
title("Boston")
subtitle("Basemap")
