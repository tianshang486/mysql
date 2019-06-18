# S​T\_UpdateOverview {#reference_p3y_wc4_qfb .reference}

This function uses raster objects to update an overview.

## Syntax {#section_og1_4hn_qfb .section}

```
raster ST_UpdateOverview(raster raster_obj, raster source[]);
```

## Parameters {#section_cxv_qhn_qfb .section}

|Parameter|Description|
|---------|-----------|
|raster\_obj|The destination raster object.|
|source|The source raster objects.|

## Description {#section_lkb_rtd_5gb .section}

All the specified raster objects must meet the following requirements:

-   They have the same number of bands.
-   Either all of them are geographically referenced, or none of them is geographically referenced. If all of them are geographically referenced, world coordinates \(geographic coordinates\) are used for the mosaic operation.
-   Their pixel types can be different. If world coordinates are used for the mosaic operation, they must have the same spatial reference system identifier \(SRID\) and pixel resolution.

## Examples {#section_lmw_qhn_qfb .section}

```
Update raster_table set raster_obj = ST_UpdateOverview(raster_obj, Array(select raster_obj from raster_table_new)) where id = 1;
```

