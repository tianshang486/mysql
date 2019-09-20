# Set TDE for an RDS for SQL Server instance {#concept_jrp_dw4_ydb .concept}

This topic describes how to set Transparent Data Encryption \(TDE\) for an RDS for SQL Server instance. With TDE enabled, RDS can encrypt and decrypt incoming and outgoing data files in real time. Specifically, RDS encrypts data before the data is written into the disk, and decrypts data when the data is read from the disk to the memory. TDE does not increase the size of data files. Developers can use the TDE function without changing any applications.

## Background information {#section_bws_3w4_ydb .section}

To improve data security, you can use the RDS console or call the [ModifyDBInstanceTDE](../intl.en-US/API Reference/Security management/ModifyDBInstanceTDE.md#) API action to enable TDE, which can encrypt data.

## Precautions {#section_wrx_jw4_ydb .section}

-   Instance-level TDE can be enabled but cannot be disabled. Database-level TDE can be enabled or disabled as needed.
-   The keys used for data encryption are generated and managed by Key Management Service \(KMS\). RDS does not provide the keys or certificates used for data encryption. After TDE is activated, if you want to restore data to your computer, you must first use RDS to [decrypt data](#section_e12_sw4_ydb).
-   TDE increases CPU usage.

## Prerequisites {#section_ttb_lw4_ydb .section}

-   The used DB engine version is RDS for SQL Server.
-   You have logged in to the Alibaba Cloud console by using your Alibaba Cloud account.
-   KMS has been activated. If you have not activated KMS, you can activate it as instructed when activating TDE.

## Enable TDE {#section_azm_mw4_ydb .section}

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  In the upper-left corner, select the region where the target RDS instance is located.

    ![选择地域](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7814/156895983536543_en-US.png)

3.  Find the target RDS instance and click the instance ID.
4.  In the left-side navigation pane, click **Data Security**.
5.  On the **TDE** tab, find **TDE Status** and click the switch next to **Disabled**.

    ![开通TDE](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7950/15689598364151_en-US.png)

6.  In the displayed dialog box, click **Confirm**.
7.  Click the button for setting TDE. In the Database TDE Settings dialog box, select the databases you want to encrypt from the **Unselected Databases** list, click the right arrow to add them to the **Selected Databases** list, and click **OK**.

    ![设置TDE](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41599/156895983642082_en-US.png)


## Decrypt data {#section_e12_sw4_ydb .section}

If you want to decrypt a database that is encrypted by TDE, you can remove the database from the **Selected Databases** list in the Database TDE Settings dialog box.

