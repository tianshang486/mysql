# What do I do if I cannot connect an ECS instance to an ApsaraDB for RDS instance? {#concept_cqq_x1d_sfb .concept}

This topic describes what you can do if you cannot connect an ECS instance to an RDS instance in various situations.

If you fail to connect ECS to RDS, one common reason is that the network type of the ECS instance differs from that of the RDS instance. Another common reason is that the IP address whitelist for the RDS instance does not contain the required IP addresses. The most common reasons and corresponding solutions are as follows:

## ECS and RDS belong to different network types {#section_i2s_5pc_sfb .section}

**The ECS instance runs in a VPC while the RDS instance runs in a classic network.**

-   Solution 1 \(recommended\): Switch the RDS instance from its classic network to the VPC where the ECS instance resides. For detailed steps, see [Set network type](../../../../intl.en-US/User Guide/Instance management/Set network type.md#).

    **Note:** The RDS instance must run in the same VPC as the ECS instance after the switching so that they can communicate with each other through the intranet.

-   Solution 2: Purchase another ECS instance that runs in the classic network because ECS instances cannot be switched from a VPC to the classic network. A VPC is safer than the classic network. Therefore, we recommend that you use a VPC.
-   Solution 3: Connect the ECS instance to the RDS instance through the Internet by using the public address of the RDS instance. This solution is inferior to solutions 1 and 2 in terms of performance, security, and stability.

**The ECS instance runs in the classic network while the RDS instance runs in a VPC.**

-   Solution 1 \(recommended\): Switch the ECS instance from the classic network to the VPC where the RDS instance resides.

    **Note:** The ECS instance must run in the same VPC as the RDS instance after the switching so that they can communicate with each other through the intranet.

-   Solution 2: Switch the RDS instance from its VPC to the classic network. However, a VPC is safer than the classic network. Therefore, we recommend that you use a VPC.
-   Solution 3: Use the [ClassicLink](https://www.alibabacloud.com/help/doc-detail/65412.htm) function. This function allows the ECS instances in the classic network to communicate with the resources in a VPC through the intranet.
-   Solution 4: Connect the ECS instance to the RDS instance through the Internet by using the public address of the RDS instance. This solution is inferior to solutions 1, 2, and 3 in terms of performance, security, and stability.

## ECS and RDS are in different VPCs {#section_dbb_stc_sfb .section}

Each VPC is a logically isolated network on Alibaba Cloud. If the ECS instance and RDS instance both run in VPCs, they must be in the same VPC so that they can communicate with each other through the intranet.

-   Solution 1 \(recommended\): Switch the RDS instance to the VPC where the ECS instance is located.

    Specifically, switch the RDS instance from its VPC to the classic network and then switch from the classic network to the VPC where the ECS instance resides. For detailed steps, see [Set network type](../../../../intl.en-US/User Guide/Instance management/Set network type.md#).

-   Solution 2: Establish an Express Connect channel between the two VPCs. For detailed steps, see [Interconnect two VPCs under the same account](https://www.alibabacloud.com/help/doc-detail/44843.htm).
-   Solution 3: Connect the ECS instance to the RDS instance through the Internet. This solution is inferior to solutions 1 and 2 in terms of performance, security, and stability.

## ECS and RDS are in different regions {#section_v4b_r5c_sfb .section}

If the ECS instance is located in a region different from the RDS instance, they cannot communicate with each other through the intranet.

-   Solution 1: Release the ECS or RDS instance and purchase instances again.
-   Solution 2: Set the network types of the ECS instance and RDS instance to VPCs, and establish an Express Connect channel between the two VPCs. For detailed steps, see [Set network type](../../../../intl.en-US/User Guide/Instance management/Set network type.md#) and [Interconnect two VPCs under the same account](../../../../intl.en-US/Peering connections/Interconnect two VPCs under the same account.md#).
-   Solution 3: Connect the ECS instance to the RDS instance through the Internet. This solution is inferior to solutions 1 and 2 in terms of performance, security, and stability.

## Incorrect IP address whitelist settings {#section_ank_fyc_sfb .section}

-   The whitelist contains only the default IP address 127.0.0.1, which indicates that no devices are allowed to access the RDS instance. You need to add the IP address of the ECS instance to the whitelist. For detailed steps, see [Set the whitelist](../../../../intl.en-US/User Guide/Security/Set the whitelist.md#).
-   The IP address in the whitelist is 0.0.0.0. However, the correct format is 0.0.0.0/0.

    **Note:** 0.0.0.0/0 indicates that all devices are allowed to access the RDS instance. Please use it with caution.

-   The whitelist is set to the [enhanced security mode](../../../../intl.en-US/User Guide/Security/Switch the IP whitelist to enhanced security mode.md#). In this case, you need to check the following:
    -   If you want the ECS instance to connect to the RDS instance through the VPC address, ensure that the private IP address of the ECS instance is added to the VPC whitelist of the RDS instance.
    -   If you want the ECS instance to connect to the RDS instance through the classic network address, ensure that the private IP address of the ECS instance is added to the classic network whitelist of the RDS instance.
    -   If you want the ECS instance to connect to the RDS instance through the Internet address, ensure that the public IP address of the ECS instance is added to the classic network whitelist of the RDS instance. The VPC whitelist does not restrict access from the Internet.
-   The public IP address that you add to the whitelist is not the real outbound IP address of the ECS instance. Possible reasons are as follows:

    -   The public IP address is not fixed and may change.
    -   The IP address query tool or website may provide inaccurate IP addresses.
    To find out the real IP address, see [Locate the real IP address](https://www.alibabacloud.com/help/doc-detail/41754.htm).


## Domain name resolution failures {#section_p2n_lyw_pgb .section}

If your Domain Name Server \(DNS\) fails or its network interface card \(NIC\) configuration is changed, domain name resolution may fail. You can run the `ping` and `telnet` commands to check whether you can properly connect to the RDS instance.

``` {#codeblock_zci_9q0_jn3}
ping <domain name>
telnet <domain name><port number>        
```

 **Example:** 

If the communication is abnormal, you can modify the NIC configuration file of your DNS to resolve the problem by completing the following steps:

1.  Modify the NIC configuration file.

    ``` {#codeblock_5jc_8w3_mvh}
    vi /etc/sysconfig/network-scripts/<name of the NIC configuration file>
    ```

    **Note:** Fill the name of the NIC used by the ECS server in the <name of the NIC configuration file\> field. You can run the `ifconfig` command to check the suffix. The default suffix is ifcfg-eth0.

2.  Add the following information to the end of the NIC configuration file:

    ``` {#codeblock_jma_kkq_50c}
    DNS1=100.100.2.136
    DNS2=100.100.2.138
    ```

    **Note:** If the DNS1 and DNS2 parameters are set, you need to change their settings to the IP addresses shown above.

    ![Modify the configuration of your DNS.](images/38364_en-US.png)

3.  Run the following command to restart your network service:

    ``` {#codeblock_aci_h8h_oew}
    systemctl restart network
    ```

4.  Run the following command to check whether the modification is successful:

    ``` {#codeblock_2jp_efl_lg4}
     cat  /etc/resolv.conf
    ```

    ![The configuration of your DNS is modified.](images/38363_en-US.png)


Common connection failures and solutions 

|Database type|Error message|Cause|Solution|
|-------------|-------------|-----|--------|
|MySQL or MariaDB TX| -   ERROR 2003 \(HY000\): Can’t connect to MySQL server on ‘XXX’ \(10038, 10060, or 110\)
-   Cannot connect to the database: XXX

 |The network connection is abnormal.|[Click here.](https://help.aliyun.com/knowledge_detail/91274.html)|
| -   ERROR 1045 \(HY000\): \#28000ip not in whitelist
-   ERROR 2801 \(HY000\): \#RDS00ip not in whitelist, client ip is XXX

 |The IP address whitelist is set improperly.|[Click here.](https://help.aliyun.com/knowledge_detail/91275.html)|
| -   ERROR 1045 \(28000\): Access denied for user ‘XXX’@’XXX’ \(using password: YES or NO\)

 |The user name or password is incorrect.|[Click here.](https://help.aliyun.com/knowledge_detail/91277.html)|
| -   ERROR 2005 \(HY000\): Unknown MySQL server host ‘xxxxxxx’ \(110 or 11004\)
-   SQLSTATE\[HY000\] \[2002\] php\_network\_getaddresses: getaddrinfo failed: Name or service not known
-   Name or service not known

 |The DNS cannot parse IP addresses properly.|[Click here.](https://help.aliyun.com/knowledge_detail/92120.html)|
|SQL Server| Cannot connect to XXX.

 A network-related or instance-specific error occurs when a connection is being established with SQL Server. The server cannot be found or accessed. Check whether the instance name is correct. Also check whether the SQL Server is configured and allows remote access. \(provider: TCP Provider, error: 0 - The receiver fails to respond correctly within the specified period or the host to be connected does not respond.\) \(Microsoft SQL Server, error: 10060 or 258\)

 |The network connection is abnormal.|[Click here.](https://help.aliyun.com/knowledge_detail/91689.html)|
| Cannot connect to XXX.

 A connection is established with the server, but an error occurs during the login. provider: TCP Provider, error: 0 - The specified network name is no longer available.\)\( Microsoft SQL Server, error: 64\)

 |The IP address whitelist is set improperly.|[Click here.](https://help.aliyun.com/document_detail/26198.html)|
|PostgreSQL/PPAS| Unable to connect to server:

 could not connect to server: Connection timed out \(0x0000274C/10060\)Is the server running on host “XXX.rds.aliyuncs.com” and acceptingTCP/IP connections on port XXX?

 |The network connection is abnormal.|[Click here.](https://help.aliyun.com/knowledge_detail/91707.html)|
| -   server closed the connection unexpectedly This probably means the server terminated abnormally before or while processing the request.
-   Error connecting to the server: FATAL: no pg\_hba.conf entry

 |The IP address whitelist is set improperly.|[Click here.](https://www.alibabacloud.com/help/doc-detail/91697.htm)|

