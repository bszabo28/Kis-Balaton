
# [Kapcsolódó blog poszt](https://szabo-balazs.hu/blog/2020/fentrol-hu-legifoto-feldolgozasa)

## Docker gdal telepítése és bejelentkezés
```
docker pull osgeo/gdal:alpine-ultrasmall-latest

docker run --rm -v ${PWD}:/fentrol-hu -it osgeo/gdal:alpine-ultrasmall-latest
```

## Docker-ben lefuttatandó parancsok
```
mkdir fentrol-hu/hasznos-teruletre-vagott

cd fentrol-hu/geoshop
for kep in *.tif;do
        gdalwarp -s_srs 'EPSG:23700' -t_srs 'EPSG:3857' -dstalpha -dstnodata 0 -multi -overwrite -cutline ../vektoros-allomanyok/hasznos-terulet.shp -cwhere "name='$kep'" -crop_to_cutline -of GTiff  $kep  ../hasznos-teruletre-vagott/$kep;
done
```

```
cd ../hasznos-teruletre-vagott
for kep in *.tif;do
        gdalwarp -s_srs 'EPSG:3857' -t_srs 'EPSG:3857' -dstalpha -dstnodata 0 -multi -overwrite -cutline ../vektoros-allomanyok/hidvegi-to-3857.shp -crop_to_cutline -of GTiff  $kep  ../hidvegi-to-teruletere-vagott/$kep;
done
```

```
cd ../hidvegi-to-teruletere-vagott
gdalbuildvrt -hidenodata index.vrt *.tif
```
