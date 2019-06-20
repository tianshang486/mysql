# ST\_boundingDiagonalAsBinary {#reference_mlq_mb4_qfb .reference}

This function returns the well-known binary \(WKB\) value of the bounding box diagonal of a pcpatch object.

## Syntax {#section_ysj_vhn_qfb .section}

```
bytea ST_boundingDiagonalAsBinary(pcpatch pc);
```

## Parameters {#section_gyb_phn_qfb .section}

|Parameter|Description|
|:--------|:----------|
|pc|The pcpatch object.|

## Description {#section_r5z_jb4_qfb .section}

A bounding box is a 2D geometry object.

## Examples {#section_cxp_4jn_qfb .section}

```
SELECT ST_BoundingDiagonalAsBinary( ST_Patch(ARRAY[ ST_MakePoint(1, ARRAY[0.,0.,0.,10.]), ST_MakePoint(1, ARRAY[1.,1.,1.,10.]), ST_MakePoint(1, ARRAY[10.,10.,10.,10.])]));
--------------------------------------------------------
\x01020000a0e610000002000000000000000000000000000000000000000000000000000000000000000000244000000000000024400000000000002440
```

