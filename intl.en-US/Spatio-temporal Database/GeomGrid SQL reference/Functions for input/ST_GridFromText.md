# ST\_GridFromText

This topic describes the ST\_GridFromText function, which converts a grid from a string into a GeomGrid structure.

## Syntax

```
geomgrid ST_GridFromText(text   Code)
```

## Parameters

|Parameter|Description|
|:--------|:----------|
|Code|The string of the grid that you want to convert.|

## Examples

```
select st_gridfromtext('G0013103220310313');

   st_gridfromtext    
----------------------
 01011C1074271B120101
```

