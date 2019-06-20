# ST\_ImportFrom {#reference_lpr_zgn_qfb .reference}

This function imports an OSS object into a raster object in ApsaraDB for PostgreSQL that uses Ganos.

## Syntax {#section_wkk_wcn_qfb .section}

``` {#codeblock_wz6_olx_ed5}
raster ST_ImportFrom(cstring chunkTableName, cstring url);
```

## Parameters {#section_whn_ddn_qfb .section}

|Parameter|Description|
|:--------|:----------|
|chunkTableName|The chunk table name, which must comply with the table naming rules of ApsaraDB for PostgreSQL.|
|u​rl|The URL of the external OSS object. For more information, see the description of the url parameter in [ST\_CreateRast](intl.en-US/Spatio-temporal Database/Raster SQL reference/Raster creation/ST_CreateRast.md#).|

## Description {#section_f2z_ctn_qfb .section}

This function creates a raster object and imports an external OSS object into the raster object.

## Examples {#section_xhh_zfn_qfb .section}

``` {#codeblock_gkv_uf1_p0g}
Select ST_ImportFrom('chunk_table','OSS://ABCDEFG:1234567890@oss-cn.aliyuncs.com/mybucket/data/4.tif');
```

