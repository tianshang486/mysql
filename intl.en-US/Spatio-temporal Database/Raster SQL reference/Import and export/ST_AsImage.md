# ST\_AsImage

This topic describes the ST\_AsImage function, which converts a raster into a BYTEA-type image.

## Syntax

```
bytea ST_AsImage(raster raster_obj,
        box extent,
        integer pyramidLevel default 0,
        cstring bands default '',
        cstring format default 'PNG',
        cstring option default '');
```

## Parameters

|Parameter|Description|
|:--------|:----------|
|raster\_obj|The raster that you want to convert.|
|extent|The extent of the image. The geographic coordinate system is used by default.|
|pyramidLevel|The pyramid layer at which the image resides. Valid values start from 0. Default value: 0.|
|bands|The list of bands based on which you want to obtain the image. Valid values start from 0. Examples: `'0-2'` and `'1,2,3'`. This parameter is empty by default. If the image is in the JPEG format, set this parameter to 1 or 3. If the image is in the PNG format, set this parameter to 1, 2, 3, or 4. The first three bands are used by default.|
|format|The format of the image. Valid values:-   PNG
-   JPEG |
|option|The options that are used to convert JSON-formatted strings.|

The following table describes the fields in the option parameter.

|Field|Description|Type|Default value|Setting notes|
|-----|-----------|----|-------------|-------------|
|nodata|Specifies whether to use NoData values.|bool|false|-   true: NoData values are processed.
-   false: NoData values are processed as normal values. |
|nodataValue|The NoData value of the raster.|integer|0|If the nodata parameter is set to true, you must specify the NoData value.|
|rast\_coord|Specifies whether the input box is specified by using pixel coordinates.|bool|false|If pixel coordinates are used, x indicates the column No. of the pixel and y indicates the row No. of the pixel. Both the column No. and the row No. start from 0.|
|strength|Specifies whether to implement enhancement in the display.|string|none|Valid values:-   none: Enhancement is not implemented.
-   stats: Enhancement is implemented by using stretching based on statistical values. |
|quality|The quality of compression.|integer|75|Valid values: 1 to 100.|

## Description

-   This function returns a BYTEA-type image.
-   Up to 100 MB of cropped data can be cached by default, which indicates that up to 100 MB of data can be returned. To adjust the limit on the image size, you can specify the cache size by using the **ganos.raster.clip\_max\_buffer\_size** parameter.
-   The following values are valid for this parameter:
    -   1: The raster has a single band based on which the raster can be converted into a grayscale image.
    -   2: The raster has a single band, based on which the raster can be converted into a grayscale image, and the Alpha band.
    -   3: The raster has three bands, which are the R band, G band, and B band.
    -   4: The raster has four bands, which are the R band, G band, B band, and Alpha band.

## Examples

```
--Specify the size of cropped data that can be cached.
SELECT ST_AsImage(raster_obj, 
                  '(-180,-90), (0,0)'::Box) 
FROM raster_table    
WHERE id=1;

--Specify the pyramid layer at which the image resides.
SELECT ST_AsImage(raster_obj, 
                  '(-180,-90), (0,0)'::Box,
                 1) 
FROM raster_table    
WHERE id=1;

--Specify the cropping range of a band.
SELECT ST_AsImage(raster_obj, 
                  '(-180,-90), (0,0)'::Box,
                 1,
                 '0-2') 
FROM raster_table    
WHERE id=1;

--Specify the compression format.
SELECT ST_AsImage(raster_obj, 
                  '(-180,-90), (0,0)'::Box,
                 1,
                 '0-2',
                 'PNG') 
FROM raster_table    
WHERE id=1;

--Specify to implement enhancement by using stretching based on statistical values.
SELECT ST_AsImage(rast, 
                  '(-180,-90), (0,0)'::Box, 
                  0, 
                  '',
                  'PNG', 
                  '{"nodata":"false", "nodatavalue":"0","rast_coord":"false", "strength":"stats", "quality":"75"}')
FROM raster_table    
WHERE id=1;

--Specify the pixel coordinates based on which you want to crop the image and implement enhancement by using stretching based statistical values.
SELECT ST_AsImage(rast, 
                  '(0,0), (200,100)'::Box, 
                  0, 
                  '',
                  'PNG', 
                  '{"nodata":"false", "nodatavalue":"0","rast_coord":"true", "strength":"stats", "quality":"75"}')
FROM raster_table    
WHERE id=1;
```

