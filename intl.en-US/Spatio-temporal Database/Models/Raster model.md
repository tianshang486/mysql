# Raster model {#concept_v3y_q3l_qfb .concept}

## Overview {#section_mdw_53l_qfb .section}

Raster data consists of a matrix of cells \(or pixels\) organized into rows and columns \(or a grid\) where each cell contains a value that represents information, such as temperature.

Raster data can be digital aerial photographs, imagery from satellites, digital pictures, or even scanned maps.

By implementing the raster model in ApsaraDB for PostgreSQL, Ganos Raster can efficiently store and analyze raster data with the help of database technologies and methods.

## Quick start {#section_zhc_c5m_qfb .section}

-   Create an extension.

    ``` {#codeblock_ypv_h7n_7qz}
    Create Extension Ganos_Raster cascade;
    ```

-   Create a raster table.

    ``` {#codeblock_5ll_3co_f4c}
    Create Table raster_table(id integer, raster_obj raster);
    ```

-   Import raster data from OSS.

    ``` {#codeblock_hys_rfn_oc7}
    Insert into raster_table Values(1, ST_ImportFrom('chunk_table','OSS://ABCDEFG:1234567890@oss-cn.aliyuncs.com/mybucket/data/4.tif'))
    ```

-   Query raster object information.

    ``` {#codeblock_l79_3y6_p2o}
    Select ST_Height(raster_obj),ST_Width(raster_obj) From raster_table Where id = 1;
    ```

-   Create a pyramid.

    ``` {#codeblock_7pd_ssm_72r}
    Update raster_table Set raster_obj = ST_BuildPyramid(raster_obj) Where id = 1;
    ```

-   Compute the best pyramid level based on the world space, width, and height of a viewport.

    ``` {#codeblock_jti_9ak_gqm}
    Select ST_BestPyramidLevel(raster_obj, '((128.0, 30.0),(128.5, 30.5))', 800, 600) from raster_table where id = 10;
    
    ---------------------
    3
    ```

-   Obtain a pixel matrix from the specified space of a raster object.

    ``` {#codeblock_7hs_3kn_r72}
    Select ST_Clip(raster_obj, 0, '((128.980,30.0),(129.0,30.2))', 'World') From raster_table Where id = 1;
    ```

-   Compute the raster space of a clipped area.

    ``` {#codeblock_rgn_0bq_odk}
    Select ST_ClipDimension(raster_obj, 2, '((128.0, 30.0),(128.5, 30.5))') from raster_table where id = 10;
    
    ------------------------------------
    '((600, 720),(200, 300))'
    ```

-   Use GPU-accelerated computing.

    If you purchase an ApsaraDB for RDS instance and have a GPU in the runtime environment, GPU-accelerated computing is automatically enabled. You do not need to set any parameters. For example, use the ST\_BuildPyramid function that supports GPU-accelerated computing to create a pyramid.

    ``` {#codeblock_v8a_722_l7g}
    
    -- Resampling during pyramid creation supports GPU-accelerated computing. The resampling type can be set to Near, Average, Cubic, or Bilinear.
    Update raster_table set rast = ST_BuildPyramid(rast) where id = 1;
    Update raster_table set rast = ST_BuildPyramid(rast, 6, 'Bilinear') where id = 1;
    Update raster_table set rast = ST_BuildPyramid(rast, 6, 'Bilinear', 'chunk_table') where id = 1;
    ```

    For more information about GPU-accelerated computing, see [Enable GPU-accelerated computing](intl.en-US/Spatio-temporal Database/Advanced usage/Enable GPU-accelerated computing.md#).

-   Delete the extension.

    ​

    ``` {#codeblock_3ax_ft1_tjn}
    Drop Extension Ganos_raster cascade;
    ```


## SQL reference {#section_kp4_5kl_qfb .section}

For more information, see [Raster SQL reference](intl.en-US/Spatio-temporal Database/Raster SQL reference/Basic concepts.md#).

