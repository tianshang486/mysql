# ST\_AddZ

This topic describes the ST\_AddZ function, which specifies the Z coordinate of a geometry based on the band of the raster converted from the geometry.

## Syntax

```
geometry ST_AddZ(raster source,
                 geometry geom,
                 integer pyramid,
                 integer band);
```

## Parameters

|Parameter|Description|
|:--------|:----------|
|source|The raster from which the geometry is converted.|
|geom|The geometry whose Z coordinate you want to specify.|
|pyramid|The pyramid level at which the raster resides. Valid values start from 0. Default value: 0.|
|band|The band of the raster. Valid values start from 0. Default value: 0.|

## Description

This function specifies the Z coordinate of a geometry based on the band of the raster converted from the geometry. If the raster is georeferenced, this function returns a geographic coordinate of the geometry. Otherwise, this function returns a pixel coordinate of the geometry.

**Note:** All of the points on the geometry must fall within the raster.

## Example

```
SELECT ST_AddZ(rast_object, ST_GeomFromText('POINT(120.5 30.6)', 4326), 0, 0)
FROM raster_table;

------------------------
POINT Z(120.5 30.6 27)

SELECT ST_AddZ(rast_object, ST_GeomFromText('POINT(120.5 30.6)', 4326), 1, 1)
FROM raster_table;

------------------------
POINT Z(120.5 30.6 115)
```

