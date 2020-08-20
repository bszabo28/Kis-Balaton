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
