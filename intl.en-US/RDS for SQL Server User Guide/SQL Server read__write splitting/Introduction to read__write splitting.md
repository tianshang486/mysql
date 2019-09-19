# Introduction to read/write splitting {#concept_ptl_fl4_wdb .concept}

This topic introduces the read/write splitting function of SQL Server. This function enables RDS to distribute read and write requests through a read-only splitting address.

If your application initiates a small number of write requests but a large number of read requests, a single instance may not be able to resist the read pressure. As a result, services may be affected. To achieve the elastic expansion of the read ability and share the pressure of the database, you can create one or more [read-only instances](../../../../intl.en-US/Quick Start for SQL Server/Read-only instances/Introduction to SQL Server read-only instances.md#) in a region. The read-only instances can handle massive read requests and increase the application throughput.

After read-only instances are created, you can enable the cluster management function, and then configure the connection information of the master instance and the automatically generated read-only splitting address in your application. All read and write requests are sent to the read-only splitting address. Then the system distributes the write requests to the master instance and the read requests to the read-only instances based on the read weights of the read-only instances.

![](images/34382_en-US.png)

## Differences between the read-only address and internal and public endpoints {#section_gdt_tmq_dgb .section}

After you enable the read/splitting function for an RDS master instance, a read-only splitting address is generated. You must configure the read-only splitting address in your application. The read requests from the application are sent to the read-only splitting address and then are distributed to the read-only instances of the master instance based on the read weights of the read-only instances.

If the connection address you have configured in your application is the internal or public endpoint of the master instance, all requests are sent to the master instance. Therefore, if you want to use read/write splitting, you must add the connection information and read-weights of the master and read-only instances to your application.

## Benefits {#section_tn1_jl4_wdb .section}

-   Facilitates maintenance with a single read-only splitting address.

    The read/write splitting function provides an additional address called read-only splitting address. You can connect to this address to perform read operations on the read-only instances, with read requests automatically distributed. Therefore, maintenance costs are reduced.

    Additionally, you can increase the processing capability of your DB system by adding read-only instances without making any changes to your application.

-   Improves performance with support for the highly secure link.

    For users who build a proxy layer to implement read/write splitting on the cloud, data has to go through multiple components for statement parsing and forwarding before it reaches the database, significantly increasing the response latency. RDS read/write splitting can be directly set in the existing highly secure link without time consumption by any other components, which reduces the latency and improves the processing rate.

-   Applies to various scenarios with customizable read weights.

    You can customize the read weights of read-only instances as needed.

-   Enhances database availability with instance health checks.

    RDS read/write splitting performs health check automatically for all instances in the distribution system. If any instance fails or its latency exceeds the threshold, RDS automatically removes the instance out of the distribution system \(while marking it as unavailable and stopping allocating read requests to it\) and allocates read and write requests to the remaining healthy instances by the predefined weights. In this way, applications still run properly even if any single-node read-only instance fails. After the instance resumes, RDS automatically reclaims it into the request distribution system.

    **Note:** To prevent single node failures, we recommend that you create at least two read-only instances for each master instance if you are using read/write splitting.

-   Reduces resource and maintenance costs with free services.

    The read/write splitting function is free of charge.

    **Note:** You only need to pay for the [read-only instances](../../../../intl.en-US/Quick Start for SQL Server/Read-only instances/Introduction to SQL Server read-only instances.md#) you use.


