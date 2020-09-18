# Vector pyramid

Vector pyramids are structures that are designed to display more than tens of millions spatial geometry data records.

## Overview

Vector pyramids allow you to create sparse indexes on spatial geometry data records and to preprocess data-intensive areas based on the specified rules. This way, you can obtain standard data records in the MVT and PBF formats.

Ganos-provided vector pyramids allow you to preprocess hundreds of millions of spatial geometry data records within minutes and to display the preprocessing results within seconds.

## Quick start

-   Create an extension.

    ```
    CREATE EXTENSION ganos_geometry_pyramid CASCADE;
    ```

-   Build a pyramid for a spatial table.

    ```
    --Build a pyramid for the table named test and specify the names of element ID fields. The names must be of the int4 or int8 data type.
    --Specify the names of spatial fields in the test table. Before you specify the name of a spatial field, you must create a spatial index for the field. The EPSG: 4326 and EPSG: 4490 coordinate systems are supported.
    SELECT ST_BuildPyramid('test', 'geom', 'id', '');
    ```

-   Read MVT-formatted data records from the pyramid that you built.

    ```
    --Read the data record with the tile ID 0_0_0 from the pyramid. You can specify any tile ID. The system returns a data record regardless of whether the specified tile ID exists in the pyramid.
    --Make sure that the specified tile ID follows the z_x_y format and the EPSG:3857 coordinate system.
    SELECT ST_Tile('test', '0_0_0');
    ```

-   Delete the pyramid that you built.

    ```
    --Delete the pyramid named test.
    SELECT ST_DeletePyramid('test');
    ```

-   Delete the extension that you created.

    ```
    DROP EXTENSION ganos_geometry_pyramid CASCADE;
    ```


## Parameter settings

-   Pyramid name

    By default, the pyramid that you want to build has the same name as the table to which the pyramid belongs. You can also specify another name for the pyramid. This allows you to map one table to multiple pyramids.

    ```
    --Build a pyramid named hello for the table named test.
    SELECT ST_BuildPyramid('test', 'geom', 'id', '{"name": "hello"}');
    ```

-   Number of parallel tasks

    You can specify the maximum number of parallel tasks that can run in parallel to build pyramids. The default value is 0, which indicates that the number is not limited. The value cannot exceed four times the number of CPUs that are configured.

    ```
    --Allow four CPUs to be occupied by tasks that run in parallel to build pyramids.
    SELECT ST_BuildPyramid('test', 'geom', 'id','{"parallel": 4}');
    ```

-   Tile parameters

    You can specify the tile size and the tile extension size.

    -   Valid tile sizes are multiples of 256 within the range of 0 to 4096.
    -   Valid tile extension sizes are within the range of 0 to 256.
    ```
    --Set the tile size to 512 and the tile extension size to 8.
    SELECT ST_BuildPyramid('test', 'geom', 'id','{
                            "tileSize": 512,
                            "tileExtend": 8
                           }');
    ```

-   Maximum number of pyramid layers

    You can specify the maximum number of pyramid layers. The default value is 16. If the number of zoom levels is greater than the maximum number of pyramid layers, the layers beyond the maximum number are no longer included in the pyramid. If you do not set this parameter, the system specifies an appropriate maximum number based on data density.

    ```
    --Set the maximum number of pyramid layers to 12. If the number of zoom levels exceeds 12, the system reads data in real time to generate data records in the MVT format.
    SELECT ST_BuildPyramid('test', 'geom', 'id', '{"maxLevel": 12}');
    ```

-   Layered processing

    You can specify unique criteria that are used to process each pyramid layer. These criteria include the fields to display and the filter conditions.

    You can specify these criteria by using the `buildRules` element.

    ```
    --Enable layered processing.
    --Specify only the "1!=1" filter condition for layers 0 through 5. The system generates empty data records in the MVT format and does not display the data of layers 0 through 5.
    -- Specify the name field to display and the "code = 1" filter condition for layers 6 through 9.
    -- Specify only the name and width fields to display for layers 10 through 15.
    SELECT ST_BuildPyramid('test', 'geom', 'id', '{
                            "buildRules":[
                              {
                                "level":[0,1,2,3,4,5],
                                "value": {
                                  "filter": "1 ! = 1"
                                }
                              },
                              {
                                "level":[6,7,8,9],
                                "value": {
                                  "filter": "code = 1",
                                  "attrFields": ["name"]
                                }
                              },
                              {
                                "level":[10,11,12,13,14,15],
                                "value": {
                                  "attrFields": ["name", "width"]
                                }
                              }                       
                            ]
                           }');
    ```


## Advanced functions

-   Merge data records based on attributes.

    You can merge the data records within a specified tile based on attributes to reduce the total number of data records.

    ```
    --Merge the data records whose codes are 1 and those whose codes are 2 separately.
    SELECT ST_BuildPyramid('test', 'geom', 'id', '{
                            "buildRules":[
                              {
                                "level":[0,1,2,3,4,5],
                                "value": {
                                  "merge": ["code=1","code=2"]
                                }
                              }
                            ]
                           }');
    ```

-   Filter out data records based on attributes.

    You can filter out the data records within a specified tile based on attributes. Make sure that only one geometry element is retained on each pixel.

    ```
    --Filter out the data records whose codes are 1 and those whose codes are 2 separately.
    SELECT ST_BuildPyramid('test', 'geom', 'id', '{
                            "buildRules":[
                              {
                                "level":[0,1,2,3,4,5],
                                "value": {
                                  "cull": ["code=1","code=2"]
                                }
                              }
                            ]
                           }');
    ```


