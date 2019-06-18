# Path model {#concept_evl_dll_qfb .concept}

## Overview {#section_g2w_jll_qfb .section}

Path data is a geometric network diagram that consists of edges and nodes. It is used to build road and traffic networks.

Ganos Networking is an extension of PostgreSQL. Ganos Networking provides a series of functions and stored procedures to find the fastest, shortest, and optimal paths based on cost models. If the cost is time, the fastest path is the optimal path. If the cost is distance, the shortest path is the optimal path. The path model can be used for path planning on a road network, path search and planning in GPS navigation on an electronic map, and routing. The path model is fully compatible with pgRouting functions and allows you to smoothly migrate existing applications.

## Quick start {#section_jhl_cwm_qfb .section}

-   Create an extension.

    `Create Extension Ganos_Networking cascade;`

-   Create a table.

    ```
    CREATE TABLE edge_table (
        id BIGSERIAL,
        dir character varying,
        source BIGINT,
        target BIGINT,
        cost FLOAT,
        reverse_cost FLOAT,
        capacity BIGINT,
        reverse_capacity BIGINT,
        category_id INTEGER,
        reverse_category_id INTEGER,
        x1 FLOAT,
        y1 FLOAT,
        x2 FLOAT,
        y2 FLOAT,
        the_geom geometry
    );
    ```

-   Insert records.

    ```
    INSERT INTO edge_table (
        category_id, reverse_category_id,
        cost, reverse_cost,
        capacity, reverse_capacity,
        x1, y1,
        x2, y2) VALUES
    (3, 1,    1,  1,  80, 130,   2,   0,    2, 1),
    (3, 2,   -1,  1,  -1, 100,   2,   1,    3, 1),
    (2, 1,   -1,  1,  -1, 130,   3,   1,    4, 1),
    (2, 4,    1,  1, 100,  50,   2,   1,    2, 2),
    (1, 4,    1, -1, 130,  -1,   3,   1,    3, 2),
    (4, 2,    1,  1,  50, 100,   0,   2,    1, 2),
    (4, 1,    1,  1,  50, 130,   1,   2,    2, 2),
    (2, 1,    1,  1, 100, 130,   2,   2,    3, 2),
    (1, 3,    1,  1, 130,  80,   3,   2,    4, 2),
    (1, 4,    1,  1, 130,  50,   2,   2,    2, 3),
    (1, 2,    1, -1, 130,  -1,   3,   2,    3, 3),
    (2, 3,    1, -1, 100,  -1,   2,   3,    3, 3),
    (2, 4,    1, -1, 100,  -1,   3,   3,    4, 3),
    (3, 1,    1,  1,  80, 130,   2,   3,    2, 4), 
    (3, 4,    1,  1,  80,  50,   4,   2,    4, 3),
    (3, 3,    1,  1,  80,  80,   4,   1,    4, 2),
    (1, 2,    1,  1, 130, 100,   0.5, 3.5,  1.999999999999,3.5),
    (4, 1,    1,  1,  50, 130,   3.5, 2.3,  3.5,4);
    ```

-   Update table attributes.

    ```
    UPDATE edge_table SET the_geom = st_makeline(st_point(x1,y1),st_point(x2,y2)),
    dir = CASE WHEN (cost>0 AND reverse_cost>0) THEN 'B'  
               WHEN (cost>0 AND reverse_cost<0) THEN 'FT'  
               WHEN (cost<0 AND reverse_cost>0) THEN 'TF'  
               ELSE '' END;
    ```

-   Create a topology.

    ```
    SELECT pgr_createTopology('edge_table',0.001);
    ```

-   Query the shortest path.

    ```
    -- Use Dijkstra's algorithm to query the shortest path.
    SELECT * FROM pgr_dijkstra(
        'SELECT id, source, target, cost, reverse_cost FROM edge_table',
        2, 3
    );
    
     seq | path_seq | node | edge | cost | agg_cost
    -----+----------+------+------+------+----------
       1 |        1 |    2 |    4 |    1 |        0
       2 |        2 |    5 |    8 |    1 |        1
       3 |        3 |    6 |    9 |    1 |        2
       4 |        4 |    9 |   16 |    1 |        3
       5 |        5 |    4 |    3 |    1 |        4
       6 |        6 |    3 |   -1 |    0 |        5
    (6 rows)
    
    -- Use the A* algorithm to query the shortest path.
    SELECT * FROM pgr_astar(
        'SELECT id, source, target, cost, reverse_cost, x1, y1, x2, y2 FROM edge_table',
        2, 12,
        directed := false, heuristic := 2);
    
     seq | path_seq | node | edge | cost | agg_cost
    -----+----------+------+------+------+----------
       1 |        1 |    2 |    2 |    1 |        0
       2 |        2 |    3 |    3 |    1 |        1
       3 |        3 |    4 |   16 |    1 |        2
       4 |        4 |    9 |   15 |    1 |        3
       5 |        5 |   12 |   -1 |    0 |        4
    (5 rows)
    
    -- Use the Turn Restricted Shortest Path (TRSP) algorithm to query the shortest path.
    SELECT * FROM pgr_trsp(
            'SELECT id::INTEGER, source::INTEGER, target::INTEGER, cost FROM edge_table',
            2, 7, false, false,
            'SELECT to_cost, target_id::int4,
            from_edge || coalesce('','' || via_path, '''') AS via_path
            FROM restrictions'
        );
    
     seq | id1 | id2 | cost
    -----+-----+-----+------
       0 |   2 |   4 |    1
       1 |   5 |  10 |    1
       2 |  10 |  12 |    1
       3 |  11 |  11 |    1
       4 |   6 |   8 |    1
       5 |   5 |   7 |    1
       6 |   8 |   6 |    1
       7 |   7 |  -1 |    0
    (8 rows)
    ```

-   Delete the extension.

    ```
    Drop Extension Ganos_Networking cascade;
    ```


## SQL reference {#section_ttp_gcm_qfb .section}

For more information, see the [official pgRouting manual](https://docs.pgrouting.org/latest/en/index.html).

