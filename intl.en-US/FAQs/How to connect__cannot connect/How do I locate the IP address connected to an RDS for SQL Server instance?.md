# How do I locate the IP address connected to an RDS for SQL Server instance? {#concept_58941_zh .concept}

## Obtain the IP address of your computer connected to an RDS instance {#section_2xq_eid_hd7 .section}

**Problem description**

The public IP address of your computer dynamically changes, therefore the IP address you obtain by using a local IP address query tool may be incorrect. As a result, RDS reports connection errors even after you add the obtained public IP address to the IP address whitelist of the RDS instance. You can access the RDS instance only after you obtain the correct IP address of your computer.

**Precautions**

If the public IP address of your computer changes and the established connection to the RDS instance is used in a production environment, we recommend that you use a private network connection instead or add an appropriate CIDR block to the IP address whitelist of the RDS instance. This helps to guarantee a stable connection despite changes to the public IP address of your computer.

**Procedure**

1.  Add the IP address 0.0.0.0/0 to the IP address whitelist of the RDS instance. For more information, see [Configure a whitelist](../../../../intl.en-US/Quick Start for SQL Server/Initial configuration/Configure a whitelist.md#).

    **Note:** The IP address 0.0.0.0/0 indicates that all IP addresses are allowed to access the RDS instance.

2.  Use a client to connect your computer to the RDS instance. For more information, see [Connect to an RDS for SQL Server instance](../../../../intl.en-US/Quick Start for SQL Server/Connect to an RDS for SQL Server instance.md#).
3.  Run the following commands to query the IP address of your computer:

    ``` {#codeblock_ti5_zct_8m4 .language-sql}
    SELECT  CONNECTIONPROPERTY('PROTOCOL_TYPE') AS PROTOCOL_TYPE,
            CONNECTIONPROPERTY('CLIENT_NET_ADDRESS') AS CLIENT_NET_ADDRESS
    					
    ```

4.  Delete the IP address 0.0.0.0/0 that you added to the IP address whitelist in Step **1**, and add the real outbound IP address of your computer to the IP address whitelist.

## Obtain all IP addresses connected to an RDS instance {#section_vsk_1ym_1gb .section}

**Problem description**

You want to obtain all IP addresses that are connected to the RDS instance, or you want to locate security issues such as link leakage.

**Procedure**

1.  Add the IP address 0.0.0.0/0 to the IP address whitelist of the RDS instance. For more information, see[Configure a whitelist](../../../../intl.en-US/Quick Start for SQL Server/Initial configuration/Configure a whitelist.md#).
2.  Use a client to connect your computer to the RDS instance.
3.  Run the following commands to query all IP addresses that are connected to the RDS instance.

    ``` {#codeblock_5dn_gpk_dzw .language-sql}
    SELECT
    SP.SPID,
    SP.LOGINAME,
    SP.LOGIN_TIME,
    SP.HOSTNAME,
    SP.PROGRAM_NAME,
    DC.CLIENT_TCP_PORT,
    DC.CLIENT_NET_ADDRESS
    FROM SYS.SYSPROCESSES AS SP
    INNER JOIN SYS.DM_EXEC_CONNECTIONS AS DC
    ON SP.SPID = DC.SESSION_ID
    WHERE SP.SPID > 50
    AND DC.AUTH_SCHEME='SQL'
    					
    ```

4.  Delete the IP address 0.0.0.0/0 or the CIDR block containing your company's IP address segment that you added to the IP address whitelist in Step **1**.

## View the parameter settings of a connection {#section_a0p_jsz_ncn .section}

After you obtain all IP addresses that are connected to the RDS instance, you can run the following command to view the parameter settings of a specific connection:

``` {#codeblock_29e_lh7_eu3 .language-sql}
SELECT * FROM SYS.DM_EXEC_SESSIONS WHERE SESSION_ID=<The obtained SPID>
			
```

