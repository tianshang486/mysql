# Enable read/write splitting {#concept_mkx_gt4_wdb .concept}

In the business scenario that needs a small number of write requests but a large number of read requests to the database, you can enable the read/write splitting function to share the read pressure on the master instance. This article introduces how to enable read/write splitting.

**Note:** Currently the read/write splitting function does not support the instances located in Asia Pacific NE 1 \(Japan\), Germany 1 \(Frankfurt\), Asia Pacific SE 2 \(Sydney\), Middle East 1 \(Dubai\) or Singapore.

## Prerequisites {#section_lsg_nh4_fhb .section}

-   The instance is MySQL 5.6 High-Availability Edition or Finance Edition, or MySQL 5.7 High-Availability Edition and is a master instance.
-   The instance has at least one read-only instances. To create a read-only instance, see [Create read-only instance](https://www.alibabacloud.com/help/doc-detail/56991.htm).

## Attention {#section_e2s_4h4_fhb .section}

-   When you first enable the read/write splitting function, the system automatically upgrades the backend control system of the master instance and all the associated read-only instances to the latest version to make sure that your service works properly. Therefore, the master instance and read-only instances automatically restart once during the enabling process. The master instance is subject to a transient disconnection of up to 30 seconds, and the read-only instances cannot be accessed during the whole restart process. To avoid the influence of transient disconnection, we recommend that you enable read/write splitting during off-peak hours and make sure that automatic reconnection is available for your application.
-   If you have restarted or made configuration changes to the master instance and read-only instances for which to enable read/write splitting for at least once since March 8, 2017, then the backend control system of these instances has automatically updated to the latest version. The system does not restart the instances again during the enabling process.

## Procedure {#section_vbs_qh4_fhb .section}

1.  Log on to the [RDS console](https://rdsnew.console.aliyun.com/console/index#/rdsList/).
2.  Select the region where the target instance is located.
3.  Click the target instance ID to enter the **Basic Information** page.
4.  Select **Connection Options** in the left-side navigation pane to enter the **Connection Options** page.
5.  Select **Read/Write Splitting** tab.
6.  Click **Enable now** to enter the **Configure Read/Write Splitting** page.

    **Note:** If the instance was created before March 8, 2017, and it has not been restarted or its specifications have remained unchanged since March 8, 2017, the master and read-only instances will be restarted once after you enable read/write splitting. On the displayed confirmation dialog box, click **OK** to enable read/write splitting.

7.  Enter the setup information, as shown in the following figure.

    -   Network Type: Read/write splitting address, which can be an intranet address or an Internet address. If the intranet address is selected, the intranet type of the read/write splitting address automatically matches with that of the master instance. For example, if the intranet type of the master instance is VPC \(Virtual Private Cloud\), then the intranet type of the read/write splitting is VPC as well.
    -   Latency Threshold: This refers to the latency threshold of read-only instances with a value range of 0 to 7,200s. If the latency of a read-only instance exceeds this threshold, read requests are not forwarded to this instance regardless of its weight. Depending on the running of SQLs, latencies may occur in read-only instances. We recommend that you set the value to no less than 30s.
    -   Read Weight Distribution: This refers to the read request weights of different instances. An instance with a higher weight ratio processes more read requests. For example, if a read/write splitting address is associated with one master instance and three read-only instances with a read weight of 0, 100, 200, and 200, respectively, it means that the master instance does not process read requests \(write requests are automatically forwarded to the master instance\), and the three read-only instances process read requests by a ratio of 1:2:2. To set the weights, you can use either of the following modes:
        -   Automatic Distribution: The system automatically distributes weights for instances according to their configurations. The new read-only instances under the master instance later is automatically added to the read/write splitting link according to the set weights without manual configuration. For the read weights of instances with different specifications, see [Rules of weight distribution by system](https://www.alibabacloud.com/help/doc-detail/51225.htm#concept_oqf_j5p_wdb).

        -   Customized Distribution: You can customize the read request processing weights of different instances with a value range of 0 to 10,000. If you select this mode, the weight of new read-only instances added to the master instance defaults to 0, and you have to set this parameter manually.

**Note:** To obtain real-time data with certain query statements, you can forcibly forward these statements to the master instance for execution using the Hint format. For the Hint format supported by RDS read/write splitting, see “Specify whether an SQL is sent to the master instance or a read-only instance by using Hint” in the [Rules of weight distribution by system](https://www.alibabacloud.com/help/doc-detail/51225.htm#concept_oqf_j5p_wdb).

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7915/15536564403097_en-US.png)

8.  Click **OK**.

    **Note:** The instance status changes to **Creating Network Connection**. Wait for a while patiently.


