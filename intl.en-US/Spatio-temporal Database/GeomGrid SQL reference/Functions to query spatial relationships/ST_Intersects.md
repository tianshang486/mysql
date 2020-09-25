# ST\_Intersects

This topic describes the ST\_Intersects function, which queries whether a grid intersects with a geometry.

## Syntax

```
boolean ST_Intersects(geomgrid grid, geometry geom);
boolean ST_Intersects(geometry geom, geomgrid grid);
```

## Parameters

|Parameter|Description|
|:--------|:----------|
|grid|The grid whose spatial relationship you want to query.|
|geom|The geometry whose spatial relationship you want to query.|

## Description

This function returns the spatial relationship between a grid and a geometry. The geometry must use the CGC2000 spatial reference system. In addition, the spatial reference system identifier \(SRID\) of the geometry must be 4490.

## Examples

```
select st_intersects(ST_gridfromtext('G001331032213300013'), 
      ST_geomfromtext('LINESTRING(122.48077 51.72814, 122.47416 51.73714)',4490));

 st_intersects 
---------------
 t
```

