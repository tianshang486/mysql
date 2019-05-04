# High security {#concept_rvl_gy5_tdb .concept}

## DDoS protection {#section_phx_ly5_tdb .section}

If DDoS attacks are detected, the security system of RDS enables traffic cleaning first. If traffic cleaning fails or the attacks reach the blackhole threshold, blackhole filtering is triggered.

**Note:** We recommend accessing RDS instances through the intranet to prevent DDoS attacks.

## Access control {#section_qhx_ly5_tdb .section}

-   IP addresses can access RDS only after you add them to the whitelist. IP addresses that are not in the whitelist cannot access RDS.
-   Each account can only view and operate its own databases.

For more information, see [access control](https://www.alibabacloud.com/help/doc-detail/53617.htm).

## System security {#section_shx_ly5_tdb .section}

-   RDS is protected by multiple firewall layers that block various network attacks and ensure data security.
-   Direct logon to the RDS server is not allowed. Only the ports required by certain database services are open.
-   RDS servers cannot initiate an external connection. It can only accept access requests.

For more information, see [Network isolation](https://www.alibabacloud.com/help/doc-detail/53618.htm).

## Professional security team {#section_gcq_o0l_uvv .section}

Aliabab Cloud security team is responsible for ensuring the security of RDS.

## Get started {#section_oh2_idp_2it .section}

-   [Quick start](../../../../intl.en-US/User Guide/Quick start.md#)
-   [Learning path](https://www.alibabacloud.com/getting-started/learningpath/rds)

**Related topics**

-   [Low costs and easy-to-use](intl.en-US/Product Introduction/Benefits/Low costs and easy-to-use.md#)
-   [High performance](intl.en-US/Product Introduction/Benefits/High performance.md#)
-   [Disaster tolerance](intl.en-US/Product Introduction/Benefits/Disaster tolerance.md#)
-   [Comparison between ApsaraDB for RDS and local databases](intl.en-US/Product Introduction/Benefits/Comparisons between ApsaraDB for RDS and self-hosted databases.md#)

