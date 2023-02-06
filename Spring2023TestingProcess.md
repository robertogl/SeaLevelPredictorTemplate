# Mon 02/06/2023
### Display Map with GeoCoordinates
```
[A,R] = readgeoraster("USGS_13_n42w071_20230117.tif","OutputType","double");
latlim = R.LatitudeLimits;
lonlim = R.LongitudeLimits;
usamap(latlim,lonlim)
geoshow(A,R,"DisplayType","surface")
demcmap(A)
```
Result:
Units: degree, meter
<img src="https://user-images.githubusercontent.com/86635895/217102375-cefd937b-8202-444d-bfa6-e1ad6529ba4f.png" width="300" height="300" />
<img src="https://user-images.githubusercontent.com/86635895/217102909-debe4311-1450-456e-9bc7-d29985726ca8.png" width="500" height="250" />
<img src="https://user-images.githubusercontent.com/86635895/217103149-4ac0afe5-ac17-49db-b8f2-5ebc93b60963.png" width="500" height="250" />
<img src="https://user-images.githubusercontent.com/86635895/217103231-cf96d16c-afd9-4271-b120-c795b59d3f5c.png" width="500" height="250" />

<img src="" width="500" height="500" />
<img src="" width="500" height="500" />



