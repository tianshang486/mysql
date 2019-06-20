# ST\_CreateRast {#reference_lpr_zgn_qfb .reference}

This function creates a raster object based on Alibaba Cloud OSS.

## Syntax {#section_wkk_wcn_qfb .section}

``` {#codeblock_9fi_ei4_6wx}
raster ST_CreateRast(cstring url);
```

## Parameters {#section_whn_ddn_qfb .section}

|Parameter|Description|
|:--------|:----------|
|url|The path of OSS raster files.|

## Description {#section_f2z_ctn_qfb .section}

The path of OSS files is in the following format: oss://access\_id:secrect\_key@endpoint/path\_to/file. The parameter *endpoint* can be omitted, and the system will automatically find the corresponding endpoint. If the endpoint is omitted, the path must start with the forward slash \(/\).

The endpoint is the address used to access OSS from the intranet. To ensure that data is imported at the fastest speed, make sure that the ApsaraDB RDS for PostgreSQL instance is in the same region as the OSS bucket. For more information, see [Endpoints](../../../../intl.en-US/Developer Guide/Endpoint/Endpoints.md#).

## Examples {#section_xhh_zfn_qfb .section}

``` {#codeblock_cz0_wnv_7tm}
-- Specify the AccessKey ID, AccessKey Secret, and endpoint.
Select ST_CreateRast('OSS://ABCDEFG:1234567890@oss-cn.aliyuncs.com/mybucket/data/4.tif');

-- Specify the AccessKey ID and AccessKey Secret.
Select ST_CreateRast('OSS://ABCDEFG:1234567890@/mybucket/data/4.tif');

-- Specify the URL in https format. AccessKey-based access has better performance than URL-based access.
Select ST_CreateRast('https://mybuckets.oss-cn.aliyuncs.com/data/4.tif');
```

