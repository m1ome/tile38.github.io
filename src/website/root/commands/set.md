<!--
layout:  index.html
title:   SET - Tile38
class:   command
command: set
-->

Set the value of an id. If a value is already associated to that key/id, it'll be overwritten.

## Examples

Set a simple point in latitude, longitude. 

```tile38
SET fleet truck1 POINT 33.5123 -112.2693
```

A point with **Z** data. This is application specific such as elevation, or a timestamp, etc.

```tile38
SET fleet truck1 POINT 33.5123 -112.2693 245.0
```

A [minimum bounding rectangle](https://en.wikipedia.org/wiki/Minimum_bounding_rectangle). The values are (southwest latitude, southwest longitude, northeast latitude, northeast longitude).

```tile38
SET props house1 BOUNDS 33.7840 -112.1520 33.7848 -112.1512 
```

A [Geohash](https://en.wikipedia.org/wiki/Geohash). A geohash is a convenient way of expressing a location (anywhere in the world) using a short alphanumeric string, with greater precision obtained with longer strings.

```tile38
SET props area1 HASH 9tbnwg
```

A [GeoJSON](http://geojson.org/) object. GeoJSON is an industry standard format for representing a variety of object types including a point, multipoint, linestring, multilinestring, polygon, multipolygon, geometrycollection, feature, and featurecollection. Tile38 supports all of the standards with these exceptions.

1. The **crs** member is not supported and will be ignored. The CRS84/WGS84 projection is assumed.
2. Any member that is not recognized (including **crs**) will be ignored.
3. All coordinates can be 2 or 3 axes. Less than 2 axes or more than 3 will result in a parsing error.

<i>* All ignored members will not persist.</i>

**Important to note that all GeoJSON coordinates are in Longitude, Latitude order.**

```tile38
SET cities tempe OBJECT {"type":"Polygon","coordinates":[[[-111.9787,33.4411],[-111.8902,33.4377],[-111.8950,33.2892],[-111.9739,33.2932],[-111.9787,33.4411]]]}
```


<a name="fields"></a>
## Fields

Fields are extra data which belongs to an object. A field is always a [double precision floating point](https://en.wikipedia.org/wiki/Double-precision_floating-point_format). There is no limit to the number of fields that an object can have.

To set a field when setting an object.

```tile38
SET fleet truck1 FIELD speed 90 POINT 33.5123 -112.2693             
SET fleet truck1 FIELD speed 90 FIELD age 21 POINT 33.5123 -112.2693
```

It's also possible to set a field when an object already exists. See [FSET](/commands/fset).