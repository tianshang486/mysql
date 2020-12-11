# Create a linked server for an ApsaraDB RDS for SQL Server instance

This topic describes how to create a linked server for an ApsaraDB RDS for SQL Server instance that runs SQL Server 2012 or later on RDS High-availability Edition.

You cannot create a linked server in the ApsaraDB RDS console. You can use stored procedures to create a linked server, but the process is complicated. Furthermore, public domain names or IP addresses cannot be used to create a linked server.

The following example provides a simple method to create a linked server:

```
DECLARE
        @linked_server_name sysname = N'my_link_server',
        @data_source sysname = N'***********',   --style: 10.1.10.1,1433
        @user_name sysname = N'****' ,
        @password nvarchar(128) = N'**********',
        @link_server_options xml
        = N'
            <rds_linked_server>
                <config option="data access">true</config>
                <config option="rpc">true</config>
                <config option="rpc out">true</config>
            </rds_linked_server>
        '
        EXEC sp_rds_add_linked_server
            @linked_server_name,
            @data_source,
            @user_name,
            @password,
            @link_server_options
```

After the linked server is created, the following message appears.

![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/5459259951/p4257.jpg)

You can view the following information on the **Messages** tab shown in the preceding figure.

```
The linked server 'my_link_server' has set option 'data access' to 'true'.
The linked server 'my_link_server' has set option 'rpc' to 'true'.
The linked server 'my_link_server' has set option 'rpc out' to 'true'.
create link server 'my_link_server' successfully.
```

