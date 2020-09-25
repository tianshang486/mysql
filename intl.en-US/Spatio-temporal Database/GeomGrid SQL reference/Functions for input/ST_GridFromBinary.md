# ST\_GridFromBinary

This topic describes the ST\_GridFromBinary function, which converts a grid from a binary structure into a GeomGrid structure.

## Syntax

```
geomgrid ST_GridFromBinary(bytea   binary)
```

## Parameters

|Parameter|Description|
|:--------|:----------|
|binary|The binary structure of the grid that you want to convert.|

## Examples

```
select st_astext(
  st_gridfrombinary('\x01010c0f74271236'));
  
    st_astext     
------------------
 G001310322230230
```

