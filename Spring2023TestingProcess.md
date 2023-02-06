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
<img src="https://user-images.githubusercontent.com/86635895/217102375-cefd937b-8202-444d-bfa6-e1ad6529ba4f.png" width="500" height="500" />
<img src="https://user-images.githubusercontent.com/86635895/217102909-debe4311-1450-456e-9bc7-d29985726ca8.png" width="500" height="500" />
<img src="" width="500" height="500" />

<img src="" width="500" height="500" />
<img src="" width="500" height="500" />
<img src="" width="500" height="500" />



