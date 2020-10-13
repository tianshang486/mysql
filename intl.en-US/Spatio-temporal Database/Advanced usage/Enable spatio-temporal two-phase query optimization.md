# Enable spatio-temporal two-phase query optimization

This topic describes the spatio-temporal two-phase query optimization method that is provided by Ganos. This method optimizes a query in two phases based on the spatio-temporal index framework. This allows you to reduce extra data I/O and computing overheads.

A conventional spatio-temporal query runs in two phases: coarse filtering and precise filtering. In the coarse filtering phase, the database system coarsely filters data records based on multi-dimensional spatio-temporal indexes to obtain an intermediate result set. In the precise filtering phase, the database system invokes an appropriate function to further filter data records from the intermediate result set. This allows the database system to obtain the final result set.

## Example

The database system coarsely filters data records from the test table based on the spatial index on the test table and based on the query object. This allows the database system to obtain an intermediate result set. Then, the database system invokes the \_st\_intersects function to precisely filter data records from the intermediate result set. This allows the database system to obtain the final result set that consists of qualified data records.

In this example, the intermediate result set that you obtain in the coarse filtering phase still contains a large number of irrelevant data records. These irrelevant data records increase data I/O and computing overheads in the precise filtering phase.

```
select id from test where st_intersects(ST_GeomFromText('POLYGON((250000 -268000, 250000 270000, 280000 270000,280000 -268000, 250000 -268000))', 3857),geom)=true;
```

## Two-phase query optimization

The two-phase query optimization method is suitable for spatio-temporal range queries and point in polygon \(PIP\) queries. This method is controlled by using the guc parameter. However, this parameter is invisible to users. This parameter is set to off by default.

You can run the following command to enable or disable the two-phase query optimization method for a session on your RDS instance:

```
# Enable the two-phase query optimization method.
set polar_enable_gist_refine = true;
# Disable the two-phase query optimization method.
set polar_enable_gist_refine = false;
```

