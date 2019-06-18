# ST\_length {#reference_qbj_5zp_3gb .reference}

This function returns the total length of a trajectory object, in meters.

## Syntax {#section_og1_4hn_qfb .section}

```
float8 ST_length(trajectory traj, integer srid default 0);
```

## Parameters {#section_cxv_qhn_qfb .section}

|Parameter|Description|
|---------|-----------|
|traj|The trajectory object.|
|srid|The spatial reference system identifier \(SRID\) for the coordinates of trajectory points in the trajectory object. Default value: 0.|

## Examples {#section_lmw_qhn_qfb .section}

```
select st_length(traj) from traj where id = 2;
    st_length     
------------------
 13494.6660605311
(1 row)
```

