# ST\_intersection {#reference_qjy_ryn_qfb .reference}

This function returns a new trajectory object that indicates the intersection of a trajectory object and the specified geometry object within the specified time range.

## Syntax {#section_og1_4hn_qfb .section}

```
trajectory[] ST_intersection(trajectory traj, tsrange range, geometry g);
trajectory[] ST_intersection(trajectory traj, timestamp t1, timestamp t2, geometry g);
```

## Parameters {#section_cxv_qhn_qfb .section}

|Parameter|Description|
|---------|-----------|
|traj|The trajectory object.|
|t1|The start time.|
|t2|The end time.|
|range|The time range.|
|g|The specified geometry object.|

If the trajectory object and the geometry object intersect at multiple spatial points, this function returns multiple sub-trajectories.

## Examples {#section_lmw_qhn_qfb .section}

```
Select ST_intersection(traj, '2010-1-1 13:00:00', '2010-1-1 14:00:00', 'LINESTRING(0 0, 5 5, 9 9)'::geometry) from traj_table;
```

