# ST\_setPcid {#reference_u3q_szn_qfb .reference}

This function sets a new schema for a pcpatch object and returns a new pcpatch object.

## Syntax {#section_ysj_vhn_qfb .section}

```
pcpatch ST_setPcid(pcpatch pc, integer pcid, float8 def default 0.0);
```

## Parameters {#section_gyb_phn_qfb .section}

|Parameter|Description|
|:--------|:----------|
|pc|The pcpatch object.|
|pcid|The ID of the new schema, which comes from the pointcloud\_formats table.|
|def|The specified value. Attribute dimensions that exist in the new schema but not in the old schema are set to this value. The default value is 0.0.|

## Description {#section_v4p_wzn_qfb .section}

Attribute dimensions that exist in the old schema but not in the new schema are discarded.

## Examples {#section_cxp_4jn_qfb .section}

```
update patches set pa=ST_setPcid(pa, 2, 0.0);
--------------------------------------
(1 rows)
```

