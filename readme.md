# simplify-geojson

Apply douglas-peucker line simplification to [GeoJSON](http://www.geojson.org/) features or feature collections in JS or on the CLI. This module uses https://github.com/seabre/simplify-geometry for the simplification and wraps it in a interface for easily simplifying GeoJSON.

[![NPM](https://nodei.co/npm/simplify-geojson.png)](https://nodei.co/npm/simplify-geojson/)

### CLI

```sh
npm install simplify-geojson -g
cat data.geojson | simplify-geojson -t 0.01
```

tolerance is specified by either `-t` or `--tolerance` and is a number in degrees (e.g. lat/lon distance). 1 degree is roughly equivalent to 69 miles. the default is 0.001, which is around a city block long

#### example

simplify alaska and count the number of lines of the simplified geojson output (tweak `-t` to see how it affects length):

```sh
curl https://raw.github.com/johan/world.geo.json/master/countries/USA/AK.geo.json | simplify-geojson -t 0.01 | wc -l
```

### JS

```js
var simplify = require('simplify-geojson')
var simplified = simplify(geojson, tolerance)
```

`geojson` can be any of the following:

- Feature with a LineString
- Feature with a MultiLineString
- Feature with a Polygon
- Feature with a MultiPolygon
- FeatureCollection with any of the above

All segments in any of the supported types will be simplified (including holes in polygons, for instance)
