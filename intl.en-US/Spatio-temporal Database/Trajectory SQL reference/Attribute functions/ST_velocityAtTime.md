# ST\_velocityAtTime {#reference_t53_3sn_qfb .reference}

This function returns the value of the velocity attribute field at the specified time point.

## Syntax {#section_og1_4hn_qfb .section}

``` {#codeblock_lzq_a9j_flx}
float8 ST_velocityAtTime (trajectory traj, timestamp t);
```

## Parameters {#section_cxv_qhn_qfb .section}

|Parameter|Description|
|---------|-----------|
|traj|The trajectory object.|
|t|The time point.|

## Examples {#section_lmw_qhn_qfb .section}

``` {#codeblock_yfg_88s_pmi}
Select ST_velocityAtTime(traj) From traj_table;
```

