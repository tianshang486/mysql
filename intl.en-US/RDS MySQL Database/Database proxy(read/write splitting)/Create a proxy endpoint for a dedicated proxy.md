# Create a proxy endpoint for a dedicated proxy

A dedicated proxy provides a default proxy endpoint. This is the proxy endpoint to which the read/write splitting function is bound. You can create, modify, or delete a proxy endpoint for the dedicated proxy.

The dedicated proxy feature is enabled. For more information, see [Dedicated proxy](/intl.en-US/RDS MySQL Database/Database proxy(read/write splitting)/Dedicated proxy.md).

## Network types for proxy endpoints

ApsaraDB for RDS supports the following network types for proxy endpoints: **Internal \(VPC\)**, **Internal \(Classic Network\)**, and **Public**.

When you enable the dedicated proxy feature for an RDS instance, you can use the default network type. After the default proxy endpoint is created, you can create another proxy endpoint. Different instance configurations support different network types for proxy endpoints.

|Instance configuration|Network type of the default proxy endpoint|Network type of a new proxy endpoint|
|----------------------|------------------------------------------|------------------------------------|
|Standard or enhanced SSDs \(VPC\)|**Internal \(VPC\)**|**Public**|
|Enhanced SSDs \(VPC\)|
|Local SSDs \(VPC\)|**Internal \(VPC\)**

**Public**

|**Internal \(VPC\)**

**Internal \(Classic Network\)**

**Public** |
|Local SSDs \(classic network\)|**Internal \(Classic Network\)**

**Public**

|**Internal \(Classic Network\)**

**Public** |

**Note:** Each proxy endpoint of an RDS instance must have a unique **Network Type**. For example, an RDS instance cannot have more than one proxy endpoint of the **Internal \(VPC\)** type.

## Create a proxy endpoint

The default proxy endpoint is created when you enable the dedicated proxy feature. For more information, see [Dedicated proxy](/intl.en-US/RDS MySQL Database/Database proxy(read/write splitting)/Dedicated proxy.md). After the default proxy endpoint is created, you can create another proxy endpoint.

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).

2.  In the left-side navigation pane, click **Instances**. In the top navigation bar, select the region where your RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find your RDS instance and click its ID.

4.  In the left-side navigation pane, click **Database Proxy**.

5.  Click **Create Endpoint**.

    ![Create Endpoint](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/2302703061/p169747.png)

6.  Specify the prefix, port, and network type of the new proxy endpoint. Then, click **OK**.

    **Note:**

    -   Each proxy endpoint of an RDS instance must have a unique **Network Type**.
    -   The prefix of a proxy endpoint must be 1 to 40 characters in length, and can contain letters, digits, and hyphens \(-\). It must start with a lowercase letter.
    -   The port number of a proxy endpoint must be within the range of 1000 to 5999.
    -   For more information about how to connect to an RDS instance, see [Connect to an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Quick start/Connect to an ApsaraDB RDS for MySQL instance.md).
    ![Set the new proxy endpoint](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/2302703061/p169748.png)


## Change a proxy endpoint or port

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).

2.  In the left-side navigation pane, click **Instances**. In the top navigation bar, select the region where your RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find your RDS instance and click its ID.

4.  In the left-side navigation pane, click **Database Proxy**.

5.  Find the proxy endpoint that you want to change. Click **Change Endpoint** or **Change Port**. After you change the proxy endpoint or port, click **OK**.

    **Note:**

    -   The prefix of a proxy endpoint must be 1 to 40 characters in length, and can contain letters, digits, and hyphens \(-\). It must start with a lowercase letter.
    -   The port number of a proxy endpoint must be within the range of 1000 to 5999.
    -   For more information about how to connect to an RDS instance, see [Connect to an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Quick start/Connect to an ApsaraDB RDS for MySQL instance.md).
    ![Change Endpoint](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/2302703061/p169756.png)


## Delete a proxy endpoint

**Note:**

-   If an RDS instance uses standard or enhanced SSDs, you cannot delete the proxy endpoint of the **Internal \(VPC\)** type.
-   If an RDS instance uses local SSDs, you must reserve at least one proxy endpoint for the RDS instance.

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).

2.  In the left-side navigation pane, click **Instances**. In the top navigation bar, select the region where your RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find your RDS instance and click its ID.

4.  In the left-side navigation pane, click **Database Proxy**.

5.  Find the proxy endpoint that you want to delete and click **Delete**. In the dialog box that appears, click **OK**.

    ![Delete](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/2302703061/p169758.png)


