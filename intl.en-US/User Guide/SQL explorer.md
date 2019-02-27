# SQL explorer {#concept_msp_gz1_mfb .concept}

ApsaraDB RDS for MySQL has upgraded the SQL audit function as **SQL explorer**, which continues to provide security audit and performance diagnosis, but has more diverse features and costs much less. The upgrade process does not affect the RDS for MySQL instances.

## Applicable scope {#section_ccm_hp5_xgb .section}

-   RDS for MySQL 5.5
-   RDS for MySQL 5.6
-   RDS for MySQL 5.7 High-Availability Edition based on local SSDs

## Upgrade plan {#section_pnw_5rp_xgb .section}

To ensure the quality of our services, all RDS for MySQL instances across the globe will be upgraded in several batches.

After the upgrade time, new and existing instances will both support the SQL explorer function.

|Regions|Upgrade time|
|-------|------------|
|China \(Hangzhou, Shanghai, Qingdao, Beijing, Shenzhen, Hong Kong\)|By of end of December, 2018|
|Singapore, Malaysia, and Indonesia|By the end of January, 2019|
|Japan, Australia, India, and China \(Zhangjiakou\)|By the end of February, 2019|
|London|By the end of March, 2019|
|China \(Hohhot\), US \(Silicon Valley, Virginia\), and UAE \(Dubai\)|To be determined|

## Features {#section_ovx_hcv_lfb .section}

-   **SQL log**: SQL log records all operations that have been performed on databases. With SQL log, you can do database troubleshooting, action analysis, and security audit.
-   **Enhanced search**: You can search data by database, user, client ID, thread ID, execution time, or the number of scanned rows. You can also export and download the search results.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23711/155129404313817_en-US.png)

-   **SQL analysis**: This new feature provides visualized interactive analysis of SQL log of a specified time period. You can use this feature to locate abnormal SQL statements and performance issues.
-   **Cost reduction**: SQL explorer adopts the column-based storage and compression technology to reduce the SQL log size and reduce storage costs by about 60%. The hourly fee is US$ 0.0018 per GB.

## Activate SQL explorer {#section_g4n_21b_mfb .section}

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  In the upper-left corner, select the region of the target instance.
3.  Locate the target instance, and click the instance ID.
4.  In the left-side navigation pane, select **SQL Explorer**.
5.  Click **Activate Now**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23711/155129404313750_en-US.png)

6.  Specify the SQL log storage duration \(for how long you want to keep the SQL log\), and click **Activate**. The system then automatically starts charging an hourly fee of US$ 0.0018 per GB.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23711/155129404313755_en-US.png)


## Modify the SQL log storage duration {#section_sgz_q13_mfb .section}

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  In the upper-left corner, select the region of the target instance.
3.  Locate the target instance, and then click the instance ID.
4.  In the left-side navigation pane, select **SQL Explorer**.
5.  Click **Service Settings**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23711/155129404313804_en-US.png)

6.  Modify the storage duration.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23711/155129404313805_en-US.png)


## Disable SQL explorer {#section_f4b_sb3_mfb .section}

**Note:** 

If you disable the SQL explorer function, the existing SQL log will be deleted. Export and save the SQL log to your local disks before you disable the function.

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  In the upper-left corner, select the region of the target instance.
3.  Locate the target instance, and then click the instance ID.
4.  In the left-side navigation pane, select **SQL Explorer**.
5.  Click **Export**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23711/155129404313823_en-US.png)

6.  Click **OK** in the dialog box.
7.  After the export process is complete, click **View Exported List** and then download the log file.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23711/155129404313831_en-US.png)

8.  Click **Service Settings**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23711/155129404313804_en-US.png)

9.  Click the toggle to disable the SQL explorer function.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23711/155129404313807_en-US.png)


