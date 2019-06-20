# S​T\_ExportTo {#reference_lpr_zgn_qfb .reference}

This function exports a raster object as an OSS object.

## Syntax {#section_wkk_wcn_qfb .section}

```
boolean ST_ExportTo(raster source, cstring format, cstring url, integer level = 0);
```

## Parameters {#section_whn_ddn_qfb .section}

|Parameter|Description|
|:--------|:----------|
|source|The raster object.|
|format|The format of the exported data, such as GTiff or BMP.|
|url|The URL of the exported OSS object. For more information, see the description of the url parameter in [ST\_CreateRast](intl.en-US/Spatio-temporal Database/Raster SQL reference/Raster creation/ST_CreateRast.md#).|
|level|The pyramid level.|

## Description {#section_qns_xtn_qfb .section}

If the raster object is successfully exported, the function returns true. If the raster object fails to be exported, the function returns false.

The format parameter specifies the format of the exported data. The following table lists the common formats.

|Format|Full name|
|------|---------|
|BMP|Microsoft Windows Device Independent Bitmap \(.bmp\)|
|ECW|ERDAS Compressed Wavelets \(.ecw\)|
|EHdr|ESRI .hdr Labelled|
|GIF|Graphics Interchange Format \(.gif\)|
|GPKG|GeoPackage|
|GTiff|Tagged Image File Format \(TIFF\), BigTIFF, or GeoTIFF \(.tif\)|
|HDF4|Hierarchical Data Format Release 4|
|PDF|Geospatial PDF|
|PNG|Portable Network Graphics \(.png\)|

## Examples {#section_jtq_jvl_sfb .section}

```
Select ST_ExportTo(raster, 'GTiff', 'OSS://ABCDEFG:1234567890@oss-cn.aliyuncs.com/mybucket/data/4.tif') from raster_table where id=1;
```

