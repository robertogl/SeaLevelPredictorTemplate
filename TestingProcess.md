
## Thur 11/10/2022

Readding and displaying TIFF:
```
t = Tiff('USGS_13_n43w071_20220713.tif','r');
imageData = read(t);

imshow(imageData);
```
Result:

<img src="https://user-images.githubusercontent.com/86635895/202313140-e0ee46f0-790e-426a-b8e1-04c5dac42c63.png" width="500" height="500" />
