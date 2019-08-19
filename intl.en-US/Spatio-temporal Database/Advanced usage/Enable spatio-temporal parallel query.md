# Enable spatio-temporal parallel query {#concept_vwd_cgd_5gb .concept}

## Parallel query principles {#section_or5_2gd_5gb .section}

Ganos can use the table-level parallel query capability of PostgreSQL to accelerate complex spatio-temporal data queries that involve a large amount of data. The following figure shows the PostgreSQL parallel query process.

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/124712/156620864038834_en-US.png)

## Precautions {#section_fwy_nhd_5gb .section}

-   A larger number of workers used for parallel query means a higher CPU load. If the CPU load is already high in some scenarios, we recommend that you set the number of workers to 2, that is, set the value of max\_parallel\_workers\_per\_gather to 2.
-   When enabling parallel query for highly concurrent access requests on a server with limited memory, you need to properly set the work\_mem parameter \(minimum value: 64 KB\). You must ensure that the number of concurrent access requests multiplied by the number of parallel workers multiplied by the value of the work\_mem parameter does not exceed 60% of the server memory.

## Procedure {#section_vzp_qgd_5gb .section}

To enable Ganos parallel query, perform the following operations:

1.  Set parallel query parameters in the PostgreSQL configuration file postgresql.conf.
    -   Set the max\_parallel\_workers parameter to specify the total number of parallel workers that can be enabled, in the range of 8 to 32. The value of this parameter must be smaller than that of the max\_worker\_processes parameter.
    -   Set the max\_parallel\_workers\_per\_gather parameter to specify the maximum number of parallel workers for a single query gather, in the range of 2 to 4. The value of this parameter must be smaller than that of the max\_parallel\_workers parameter.
    -   To forcibly enable parallel query, set the force\_parallel\_mode parameter to on.
    -   To set the number of parallel workers for a single table, execute the following SQL statement: alter table table\_name set \(parallel\_workers=n\).

        **Note:** In the preceding SQL statement, n indicates the number of parallel workers. For more information about how to set an appropriate value for n, see the description of the max\_parallel\_workers\_per\_gather parameter.

2.  Increase the cost of Ganos functions.

    After a Ganos module extension is created, functions have a default cost. If the data size of the table for the module extension is small, parallel query is disabled by default. If a function is computing-intensive and parallel query is suitable for the function, you must increase the cost of the function before you can enable parallel query.


