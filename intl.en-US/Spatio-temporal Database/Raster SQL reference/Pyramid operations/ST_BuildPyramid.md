# ST\_BuildPyramid

The ST\_BuildPyramid function creates pyramids for a raster dataset.

## Syntax

```
raster ST_BuildPyramid(raster source);
raster ST_BuildPyramid(raster source,  cstring chunkTableName);
raster ST_BuildPyramid(raster source,  integer pyramidLevel,ResampleAlgorthim algorhim,
                       cstring chunkTableName, cstring storageOption);
```

## Parameters

|Parameter|Description|
|:--------|:----------|
|source|The name of the raster dataset.|
|chunkTableName|The name of the chunk table that is stored in the pyramids.|
|pyramidLevel|The number of pyramid levels. The value -1 indicates that the largest number of pyramid levels are created.|
|algorhim|The resampling algorithm that is used to create the pyramids. Valid values:-   Near
-   Average
-   Bilinear
-   Cubic |
|storageOption|The options that specify the storage settings. This parameter is valid only on raster datasets that are stored in Alibaba Cloud Object Storage Service \(OSS\) buckets.|

The value of the storageOption parameter is a JSON-formatted string that describes the chunk storage information of the pyramids. The following table describes the fields in this parameter.

|Field|Type|Description|
|-----|----|-----------|
|chunkdim|string|The dimensions from which the raster data is chunked. The value of this field follows the `(w, h, b)` format. The chunk size is obtained from the original raster data by default.|
|interleaving|string|The method that is used to interleave the raster data.-   bip: band interleaved by pixel \(BIP\)
-   bil: band interleaved by line \(BIL\)
-   bsq: band sequential \(BSQ\) \(This is the default value.\)
-   auto: an interleaving method that is specified by this function |
|compression|string|The algorithm that is used to compress the raster data. Valid values:-   none
-   jpeg
-   zlib
-   png
-   lzo
-   lz 4\(default\)
-   zstd
-   snappy
-   jp2k |
|quality|integer|The quality of compression. This parameter is valid only for JPEG and JP2K compression algorithms. Default value: 75.|

## Description

This function supports GPU-accelerated computing. In a running environment with GPUs, Ganos enables GPU-accelerated computing by default.

## Examples

```
Update raster_table set raster_obj = ST_BuildPyramid(raster_obj) where id = 1;

Update raster_table set raster_obj = ST_BuildPyramid(raster_obj, 'chunk_table') where id = 2;

--Specify to use the JP2K compression algorithm, which ensures that all bands are in the same chunk.
Update raster_table set raster_obj = ST_BuildPyramid(
    raster_obj, 
    -1, 
    'Near', 
    'chunk_table', 
    '{"compression":"jp2k", 
        "quality": 75, 
        "chunkdim":"(256,256,4)",
        "interleaving":"auto"}'
 ) 
where id = 3;
```

