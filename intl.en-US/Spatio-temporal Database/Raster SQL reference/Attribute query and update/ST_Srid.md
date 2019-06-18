# ST\_Srid {#reference_gft_xd4_qfb .reference}

This function returns the spatial reference system identifier \(SRID\) of a raster object. The SRID and its definition are stored in the spatial\_ref\_sys table.

## Syntax {#section_ysj_vhn_qfb .section}

```
integer ST_Srid(raster raster_obj);
```

## Parameters {#section_gyb_phn_qfb .section}

|Parameter|Description|
|:--------|:----------|
|raster\_obj|The raster object.|

## Examples {#section_cxp_4jn_qfb .section}

```
select ST_Srid(raster_obj) from raster_table where id=1;

__________________________________
4326
```

