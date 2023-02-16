# Tues 02/14/2023
### Display Basemap of Boston
```
% Code for Basemap of Boston (zoomed out)
[~,R] = readgeoraster("USGS_13_n26w081_20221103.tif","OutputType","double");
latlim1 = R.LatitudeLimits;
lonlim1 = R.LongitudeLimits;

latlim = [24,28];
lonlim = [-82,-78];

[A,RA] = readBasemapImage("colorterrain",latlim,lonlim,25);

[xGrid,yGrid] = worldGrid(RA);
[latGrid,lonGrid] = projinv(RA.ProjectedCRS,xGrid,yGrid);

figure
h = worldmap(latlim,lonlim);
getm(h,"mapprojection")
geoshow(latGrid,lonGrid,A)
geoshow(lat,lon,DisplayType="point",Marker="pentagram")
title("Boston")
subtitle("Basemap")
```
### Result: 

# Thurs 02/16/2023
### Display Basemap of Miami
```
% Code for Basemap of Miami (zoomed out)

[~,R] = readgeoraster("USGS_13_n26w081_20221103.tif","OutputType","double");
latlim1 = R.LatitudeLimits;
lonlim1 = R.LongitudeLimits;

latlim = [24,28]; 
lonlim = [-82,-78]; 

[A,RA] = readBasemapImage("colorterrain",latlim,lonlim,25);

[xGrid,yGrid] = worldGrid(RA);
[latGrid,lonGrid] = projinv(RA.ProjectedCRS,xGrid,yGrid);

figure
h = worldmap(latlim,lonlim);
getm(h,"mapprojection")
geoshow(latGrid,lonGrid,A)
geoshow(lat,lon,DisplayType="point",Marker="pentagram")
title("Miami")
subtitle("Basemap")
```
