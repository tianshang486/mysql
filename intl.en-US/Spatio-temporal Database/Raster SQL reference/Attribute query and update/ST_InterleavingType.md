# ST\_InterleavingType {#reference_ztn_cb4_qfb .reference}

This function returns the interleaving type of a raster object. The interleaving type can be BSQ, BIL, or BIP.

## Syntax {#section_ysj_vhn_qfb .section}

```
text ST_InterleavingType(rasterraster_obj);
```

## Parameters {#section_gyb_phn_qfb .section}

|Parameter|Description|
|:--------|:----------|
|raster\_obj|The raster object.|

## Examples {#section_cxp_4jn_qfb .section}

```
select ST_InterleavingType(raster_obj) from raster_table;

__________________________________
BSQ
```

