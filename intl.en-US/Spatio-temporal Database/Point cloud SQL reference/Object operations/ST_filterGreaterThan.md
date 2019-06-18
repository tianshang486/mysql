# ST\_filterGreaterThan {#reference_d1p_ywn_qfb .reference}

This function filters all pcpoint objects to obtain the pcpoint objects whose values of the specified attribute dimension are greater than a fixed value in a pcpatch object and returns a new pcpatch object that is composed of these pcpoint objects.

## Syntax {#section_ysj_vhn_qfb .section}

```
pcpatch ST_filterGreaterThan(pcpatch pc, text dimname, float8 value);
```

## Parameters {#section_gyb_phn_qfb .section}

|Parameter|Description|
|:--------|:----------|
|pc|The pcpatch object.|
|dimname|The name of the specified attribute dimension.|
|value|The fixed value of the attribute dimension.|

## Examples {#section_cxp_4jn_qfb .section}

```
SELECT ST_AsText(ST_FilterGreaterThan(pa, 'y', 45.57)) FROM patches WHERE id = 7;
------------------------------------------------------------
 {"pcid":1,"pts":[[-126.42,45.58,58,5],[-126.41,45.59,59,5]]}
```

