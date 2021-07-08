GeoJSON-Attribute-Cleaner
=========================

Simple web based attribute cleaner for reducing GeoJSON file size.
Removes every attribute from a GeoJSON except country ID and country name. Also removes whitespace.
Input must be a valid JSON.

## Building and reducing a GeoJSON on MacOSX

Quick guide to produce a GeoJSON:

- Install GDAL
```
brew install gdal
```

- Download the shapefile for world countries from NaturalEarthData. [Like this one](http://www.naturalearthdata.com/http//www.naturalearthdata.com/download/50m/cultural/ne_50m_admin_0_map_units.zip)
- Unzip it.
- Navigate to the unzipped folder using the terminal.
- Run `ogr2ogr` to convert the vector shapefile to a GeoJSON.
```
ogr2ogr -f GeoJSON -lco COORDINATE_PRECISION=3 -simplify 0.04 temp.json ne_50m_admin_0_map_units.shp
```
- Using the linked shapefile, this command will create a geoJSON of about 1.1 MB. You can specify lower simplify values to produce better maps but even bigger files. See the [ogr2ogr command line reference](http://www.gdal.org/ogr2ogr.html) for details.
- Open the produced JSON file in a text editor, and paste it in the GeoJSON Attribute Cleaner. Click process.
- Use the resulting JSON for your maps. For the example GeoJSON, size is reduced to 637 KB.

## Example output
Input:
```json
{"type":"FeatureCollection","features":[{"type":"Feature","properties":{"scalerank":1,"featurecla":"Admin-0mapunit","labelrank":5.0,"sovereignt":"Barbados","sov_a3":"BRB","adm0_dif":0.0,"level":2.0,"type":"Sovereigncountry","admin":"Barbados","adm0_a3":"BRB","geou_dif":0.0,"geounit":"Barbados","gu_a3":"BRB","su_dif":0.0,"subunit":"Barbados","su_a3":"BRB","brk_diff":0.0,"name":"Barbados","name_long":"Barbados","brk_a3":"BRB","brk_name":"Barbados","brk_group":null,"abbrev":"Barb.","postal":"BB","formal_en":"Barbados","formal_fr":null,"note_adm0":null,"note_brk":null,"name_sort":"Barbados","name_alt":null,"mapcolor7":4.0,"mapcolor8":1.0,"mapcolor9":5.0,"mapcolor13":3.0,"pop_est":284589.0,"gdp_md_est":5425.0,"pop_year":-99.0,"lastcensus":2010.0,"gdp_year":-99.0,"economy":"6.Developingregion","income_grp":"2.Highincome:nonOECD","wikipedia":-99.0,"fips_10":null,"iso_a2":"BB","iso_a3":"BRB","iso_n3":"052","un_a3":"052","wb_a2":"BB","wb_a3":"BRB","woe_id":-99.0,"adm0_a3_is":"BRB","adm0_a3_us":"BRB","adm0_a3_un":-99.0,"adm0_a3_wb":-99.0,"continent":"NorthAmerica","region_un":"Americas","subregion":"Caribbean","region_wb":"LatinAmerica&Caribbean","name_len":8.0,"long_len":8.0,"abbrev_len":5.0,"tiny":3.0,"homepart":1.0},"geometry":{"type":"Polygon","coordinates":[[[-59.493,13.082],[-59.611,13.102],[-59.647,13.303],[-59.592,13.318],[-59.428,13.153],[-59.493,13.082]]]}}]}
```

Output:
```json
{"type":"FeatureCollection","features":[{"type":"Feature","properties":{"name":"Barbados"},"geometry":{"type":"Polygon","coordinates":[[[-59.493,13.082],[-59.611,13.102],[-59.647,13.303],[-59.592,13.318],[-59.428,13.153],[-59.493,13.082]]]},"id":"BRB"}]}
```

## Revision

Some states, (eg. France) would include lots of other unrelated geographical states. To split those use the same process with [this file](https://www.naturalearthdata.com/http//www.naturalearthdata.com/download/50m/cultural/ne_50m_admin_0_map_subunits.zip50m/cultural/ne_50m_admin_0_map_units.zip)

use the index_sub.html
at last, add the us_states.element at the end of the array.

## References

- http://blog.thematicmapping.org/2012/11/how-to-minify-geojson-files.html
- http://bost.ocks.org/mike/map/