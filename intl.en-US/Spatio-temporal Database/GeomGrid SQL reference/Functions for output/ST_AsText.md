# ST\_AsText

This topic describes the ST\_AsText function, which converts a grid into a text that is encoded in a specified format.

## Syntax

```
text ST_AsText(geomgrid    grid,
               integer precision,
               text standard default 'GGER')
text[] ST_AsText(geomgrid[]    grid,
               integer precision,
               text standard default 'GGER')
```

## Parameters

|Parameter|Description|
|:--------|:----------|
|grid|The grid that you want to convert.|
|precision|The precision level based on which you want to convert the grid. Valid values: 0 to 31. The value -1 specifies the default precision level.|
|standard|The specifications based on which you want to convert the grid. Set the value to GGER. Geospatial Grid Encoding Rule \(GGER\) is developed by the Ministry of Natural Resources of the People's Republic of China. Default value: GGER.|

## Description

This function converts a grid into a text based on the specified layer, precision level, and encoding format. If the specified precision level is higher than the precision level of the grid, the system does not fill 0s in the return result.

## Examples

```
--Retain the default layer that you want to convert.
with g as (
  select unnest(st_asgrid(
    ST_geomfromtext('POINT(116.31522216796875 39.910277777777778)',4490), 15)) as grid) 
select ST_asText(grid) from g;

    st_astext     
------------------
 G001310322230230

--Specify the layer that you want to convert.
with g as (
  select unnest(st_asgrid(
    ST_geomfromtext('POINT(116.31522216796875 39.910277777777778)',4490), 15)) as grid) 
select ST_asText(grid, 8) from g;

  st_astext  
-------------
 G01310322
```

