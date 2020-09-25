# Load raster data

This topic describes how to load a raster data file from your computer or an Alibaba Cloud Object Storage Service \(OSS\) to Ganos by using the ST\_ImportFrom function.

## Precautions

Your RDS instance is authorized to access the raster data file. If the raster data file is stored in an OSS bucket, your RDS instance resides in the same region as the OSS bucket. For more information, see [OSS domain names](/intl.en-US/Developer Guide/Endpoint/OSS domain names.md).

## Introduction to the ST\_ImportFrom function

The ST\_ImportFrom function is used to load a raster data file from your computer or an OSS bucket to Ganos.

**Note:**

-   In addition to the ST\_ImportFrom function, Ganos provides other raster-related functions. For more information, see Raster SQL Reference.
-   For more information about the parameters in the ST\_ImportFrom function, see [ST\_ImportFrom]().

## Syntax

```
INSERT INTO <raster_table_name>(<raster_column_name>) VALUES (ST_IMPORTFROM('<chunk_table_name>','<path_to_raster_file>'))
```

## Examples

1.  Create the ganos\_raster extension.

    ```
    CREATE EXTENSION Ganos_Raster CASCADE
    ```

2.  Load a raster data file from your computer to Ganos.

    ```
    INSERT INTO raster_table(name, rast) VALUES ('local_file', ST_ImportFrom('chunk_table', '/home/beijing.tif'));
    ```

3.  Load a raster data file from an OSS bucket to Ganos.

    ```
    INSERT INTO raster_table(name, rast) VALUES ('oss_file', ST_ImportFrom('chunk_table', 'oss://ak:as@bucket/data/beijing.tif'));
    ```


