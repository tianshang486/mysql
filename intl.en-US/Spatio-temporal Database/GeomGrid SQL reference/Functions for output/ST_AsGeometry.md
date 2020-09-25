# ST\_AsGeometry

This topic describes the ST\_AsGeometry function, which obtains the geometry-represented range of a grid.

## Syntax

```
geometry ST_AsGeometry(geomgrid grid);
geometry[] ST_AsGeometry(geomgrid[] grid);
```

## Parameters

|Parameter|Description|
|:--------|:----------|
|grid|The grid whose range you want to obtain.|

## Examples

```
select st_astext(
   st_asgeometry(st_gridfromtext('G0013103220310313')));
                                                                                
      st_astext                                                                 
                      
--------------------------------------------------------------------------------
 POLYGON((116.458888888889 39.3088888888889,116.458888888889 39.3166666666667,11
6.466666666667 39.3166666666667,116.466666666667 39.3088888888889,116.4588888888
89 39.3088888888889))
```

