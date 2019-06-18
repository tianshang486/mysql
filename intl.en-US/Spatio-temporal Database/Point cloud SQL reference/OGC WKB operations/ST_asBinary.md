# ST\_asBinary {#reference_l35_514_qfb .reference}

This function returns the well-known binary \(WKB\) value of a pcpoint object.

## Syntax {#section_ysj_vhn_qfb .section}

```
bytea ST_asBinary(pcpoint pt);
```

## Parameters {#section_gyb_phn_qfb .section}

|Parameter|Description|
|:--------|:----------|
|pt|The pcpoint object.|

## Examples {#section_cxp_4jn_qfb .section}

```
SELECT ST_AsBinary('010100000064CEFFFF94110000703000000400'::pcpoint);
---------------------------------------------
\x01010000800000000000c05fc000000000008046400000000000005f40
```

