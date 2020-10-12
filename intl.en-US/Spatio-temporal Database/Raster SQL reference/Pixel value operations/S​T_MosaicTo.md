# S​T\_MosaicTo

This topic describes the S​T\_MosaicTo function, which performs a mosaic operation to integrate a raster object or object set into another raster object.

## Syntax

```
raster ST_MosaicTo(raster raster_obj,raster source[]);
```

## Parameters

|Parameter|Description|
|:--------|:----------|
|raster\_obj|The raster object into which you want to integrate another raster object or object set.|
|source|The raster object or object set that you want to integrate it into another raster object or object set.|

## Description

The source and destination raster objects must meet the following requirements:

-   They have the same number of bands.
-   They are all geographically referenced, or none of them is geographically referenced. If all of them are geographically referenced, world coordinates \(geographic coordinates\) are used for the mosaic operation.
-   Although they can have different pixel types, they must have the same spatial reference system identifier \(SRID\) and affine parameters if world coordinates are used for the mosaic operation.

You must configure the following parameter.

|Parameter|Type|Description|
|---------|----|-----------|
|ganos.raster.mosaic\_must\_same\_nodata|boolean|Specifies whether the values of NoData in a data source must be the same during the mosaic operation. Valid values: true and false. The values of NoData are not changed during the mosaic operation. If you set this parameter to false, the semantics of the pixels after the mosaic operation may be changed. Example: ```
Set ganos.raster.mosaic_must_same_nodata = false;
``` |

## Example

```
Update raster_table Set raster_obj = ST_MosaicTo(raster_obj, Array(select raster_obj from raster_table where id < 10)) where id = 11;
```

