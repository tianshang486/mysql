# ST\_AsBox

This topic describes the ST\_AsBox function, which obtains the box-represented range of a grid.

## Syntax

```
box ST_AsBox(geomgrid grid);
box[] ST_AsBox(geomgrid[] grid);
```

## Parameters

|Parameter|Description|
|:--------|:----------|
|grid|The grid whose range you want to obtain.|

## Examples

```
select st_asbox(
   st_gridfromtext('G0013103220310313'));
   
                                   st_asbox                                   
------------------------------------------------------------------------------
 (116.46666666666667,39.31666666666667),(116.4588888888889,39.30888888888889)
```

