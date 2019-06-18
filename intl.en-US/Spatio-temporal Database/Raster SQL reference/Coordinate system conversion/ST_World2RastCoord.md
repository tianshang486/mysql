# S​T\_World2RastCoord {#reference_lpr_zgn_qfb .reference}

This function computes the pixel coordinates of a cell by using an inverse affine transformation formula based on the world coordinates and pyramid level of the cell.

## Syntax {#section_wkk_wcn_qfb .section}

```
point ST_World2RastCoord(raster raster_obj, integer pyramidLevel, point coord);
```

## Parameters {#section_whn_ddn_qfb .section}

|Parameter|Description|
|:--------|:----------|
|raster\_obj|The raster object.|
|pyramidLevel|The pyramid level.|
|coord|The world space.|

## Description {#section_f2z_ctn_qfb .section}

The raster object must have a valid spatial reference system identifier \(SRID\).

## Examples {#section_xhh_zfn_qfb .section}

```
Select ST_World2RastCoord(raster_obj, 0, '(27.9,128.6)') from raster_table;
```

