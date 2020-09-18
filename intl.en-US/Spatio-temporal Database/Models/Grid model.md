# Grid model

Grid models are discrete, multi-scale location identification systems that are developed from GeoSOT.

## Overview

A grid model allows you to assign globally unique codes to various objects within the earth space \(from the earth's core to the earth's surface\). The globally unique grid code of an object can be used to associate the object with various data that is collected from the same location as the object.

## Quick start

-   Create an extension.

    ```
    CREATE EXTENSION Ganos_GeomGrid CASCADE;
    ```

-   Create a table with a grid code.

    ```
    CREATE TABLE t_grid(id integer,  
                        geom geometry,  -- A geometry.
                        grid1 geomgrid[], -- A grid code with a precision of 1.
                        grid2 geomgrid[], -- A grid code with a precision of 2.
                        grid3 geomgrid[] -- A grid code with a precision of 3.
                       );
    ```

-   Compute the grid code of the table.

    ```
    --Insert data into the table.
    INSERT INTO t_grid(id, geom)
    VALUES (1, ST_GeomFromText('POINT(116.31522216796875 39.910277777777778)', 4490)),
           (2, ST_GeomFromText('POINT(116.31522217796875 39.910277776777778)', 4490)),
           (3, ST_GeomFromText('POINT(116.31522217797875 39.910277776787778)', 4490)),
           (4, ST_GeomFromText('POINT(116.31522227796875 39.910277776775778)', 4490));
             
    --Create grid codes of different precision levels.
    UPDATE t_grid
    SET grid1 = ST_AsGrid(geom, 10),
        grid2 = ST_AsGrid(geom, 15),
        grid3 = ST_AsGrid(geom, 26);
    ```

-   Create indexes on grid codes.

    ```
    --Create GIN indexes on grid codes of different precision levels.
    CREATE INDEX idx_grid_gin1
    ON t_grid
    USING GIN(grid1);
    
    CREATE INDEX idx_grid_gin2
    ON t_grid
    USING GIN(grid2);
    
    CREATE INDEX idx_grid_gin3
    ON t_grid
    USING GIN(grid3);
    ```

-   Query data.

    ```
    --Query data that resides in a grid.
    SELECT id 
    FROM t_grid
    WHERE grid2 = ARRAY[ST_GridFromText('G001310322230230')];
    
    --Query data that intersects with a grid.
    SELECT id 
    FROM t_grid
    WHERE grid3 @> ARRAY[ST_GridFromText('G00131032223023031031033223')];
    
    --Query data that intersects with more than one grid.
    SELECT id
    FROM t_grid
    WHERE grid3 && ARRAY[ST_GridFromText('G00131032223023031031211001'), 
                             ST_GridFromText('G00131032223023031031211111')];
    
    --Query data that intersects with more than one geometry in a grid.
    SELECT id 
    FROM t_grid
    WHERE grid3 && 
    ST_AsGrid(
      ST_GeomFromText('LINESTRING(116.31522216796875 39.910277777777778, 116.31522217797875 39.910277776787778)', 4490), 26);
    ```

-   Delete the extension that you created.

    ```
    DROP EXTENSION Ganos_GeomGrid CASCADE;
    ```


