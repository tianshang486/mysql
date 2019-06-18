# S​T\_nearestApproachDistance {#reference_uww_3zn_qfb .reference}

This function returns the nearest distance between a trajectory object and the specified geometry object within the specified time range.

## Syntax {#section_og1_4hn_qfb .section}

```
float8 S​T_nearestApproachDistance(trajectory traj, tsrange range, geometry g);
float8 S​T_nearestApproachDistance(trajectory traj, timestamp t1, timestamp t2, geometry g);
```

## Parameters {#section_cxv_qhn_qfb .section}

|Parameter|Description|
|---------|-----------|
|traj|The trajectory object.|
|t1|The start time.|
|t2|The end time.|
|range|The time range.|
|g|The specified geometry object.|

## Examples {#section_lmw_qhn_qfb .section}

```
Select ST​_nearestApproachDistance(traj, '2010-1-1 13:00:00', '2010-1-1 14:00:00', 'LINESTRING(0 0, 5 5, 9 9)'::geometry) from traj_table; 
```

