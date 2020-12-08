# Why am I unable to connect to my ApsaraDB RDS for MySQL or ApsaraDB RDS for MariaDB instance from a local server over the Internet?

Before you connect to your ApsaraDB RDS instance from a local server over the Internet, you must add the public IP address of the local server to an IP address whitelist of the RDS instance. This applies if the RDS instance runs MySQL or MariaDB. This topic describes how to obtain the public IP address of the local server.

## Problem description

The public IP address of the local server is obtained by using the `ipconfig` command or a search engine. In addition, the public IP address of the local server is added to an IP address whitelist of the RDS instance.

In this case, the connection may fail because the obtained public IP address is invalid or dynamically changes.

**Note:** The solution that is provided in this topic applies only when the local server is not an Alibaba Cloud Elastic Compute Service \(ECS\) instance. If the local server is an ECS instance, you can view the public and private IP addresses of the ECS instance in the ECS console.

## Precautions

If the public IP address of the local server dynamically changes and the connection is used for a production environment, we recommend that you establish the connection over an internal network. Otherwise, we recommend that you add the public Classless Inter-Domain Routing \(CIDR\) block of the local server to an IP address whitelist of the RDS instance. This way, the RDS instance remains connected even if the public IP address of the local server dynamically changes.

## Obtain the public IP address of the local server

1.  Add the public CIDR block of the local server or the 0.0.0.0/0 entry to an IP address whitelist of the RDS instance. For more information, see [Control access to an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Quick start/Control access to an ApsaraDB RDS for MySQL instance.md).

    **Note:** The 0.0.0.0/0 entry indicates that all devices can access the RDS instance. This may cause potential security risks. Proceed with caution when you add 0.0.0.0/0 to an IP address whitelist. If 0.0.0.0/0 is added, we recommend that you immediately delete the entry when it is no longer needed.

2.  Connect to the RDS instance from the local server by using a database client or the command-line interface \(CLI\).

    ```
    mysql -h<The endpoint that is used to connect to the RDS instance> -u<The username of the used account> -p<The password of the used account> -P3306
    ```

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1750937951/p33319.jpg)

3.  Query information about running processes.

    ```
    show processlist
    ```

    In the command output that is shown in the following figure, the **Host** in the row where **show processlist** resides is the actual public IP address of the local server.

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/1750937951/p33320.jpg)

4.  Remove 0.0.0.0/0 and add the actual public IP address of the local server to the IP address whitelist.

## FAQ

-   I cannot connect to my RDS instance from a local server. How do I determine whether the connection fails because the public IP address of the local server dynamically changes?

    Add 0.0.0.0/0 to an IP address whitelist of your RDS instance and wait for about 1 minute. Then, all devices are granted access to your RDS instance. Connect to your RDS instance from the local server. If your RDS instance can be connected, remove 0.0.0.0/0 and add the public IP address of the local server to the IP address whitelist. Then, connect to your RDS instance from the local server again. If your RDS instance cannot be connected, the public IP address that you added to the IP address whitelist is not the current public IP address of the local server. This indicates that the public IP address of the local server dynamically changes.

-   After I add the public IP address of a local server to an IP address whitelist of my RDS instance, why am I still unable to connect to my RDS instance from the local server?

    If the public IP address of the local server dynamically changes, add the current public IP address of the local server to an IP whitelist of your RDS instance. The IP address whitelist requires about 1 minute to take effect.

    The connection error may be caused by other issues. For more information, see [What do I do if I cannot connect an ECS instance to an ApsaraDB for RDS instance?](/intl.en-US/FAQs/Connections and Networks/Resolve the problem that cannot connect to the RDS instance.md)


