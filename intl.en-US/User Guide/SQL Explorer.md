# SQL Explorer {#concept_msp_gz1_mfb .concept}

ApsaraDB RDS for MySQL has upgraded the SQL audit function as **SQL explorer**, which continues to provide security audit and performance diagnosis, but has more diverse features and costs much less. The upgrade process does not affect the RDS for MySQL instances.

## Upgrade plan {#section_ktf_nhn_mfb .section}

To ensure the quality of our services, all the RDS for MySQL instances across the globe will be upgraded in several batches.

-   After the upgrade date, all newly purchased RDS for MySQL instances support the SQL explorer function.
-   For existing instances, the SQL explorer function will become available before March 1, 2019.

|Regions|Upgrade date for newly purchased instances|Upgrade date for existing instances|
|-------|------------------------------------------|-----------------------------------|
|China \(Beijing\), China \(Shanghai\), Alibaba Finance Cloud Hangzhou, and Alibaba Finance Cloud Shanghai|October 23, 2018|From October 23, 2018 to March 1, 2019|
|China \(Qingdao\), China \(Hangzhou\), China \(Shenzhen\), Finance Cloud Shenzhen|November 1, 2018|
|Other regions|The upgrade for other regions starts from November 15, 2018.|

## Features {#section_ovx_hcv_lfb .section}

-   **SQL log**: SQL log records all operations that have been performed on databases. With SQL log, you can do database troubleshooting, action analysis, and security audit.
-   **Enhanced search**: You can search data by database, user, client ID, thread ID, execution time, or the number of scanned rows. You can also export and download the search results.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23711/155120109413817_en-US.png)

-   **SQL analysis**: This new feature provides visualized interactive analysis of SQL log of a specified time period. You can use this feature to locate abnormal SQL statements and performance issues.

    ![](images/13818_en-US.png)

    ![](images/13819_en-US.png)

-   **Cost reduction**: SQL explorer adopts the column-based storage and compression technology to reduce the SQL log space usage and reduce storage costs by about 60%. The hourly fee for SQL explorer is RMB 0.008/GB.

## Activate SQL explorer {#section_g4n_21b_mfb .section}

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  In the upper-left corner, select the region of the target instance.
3.  Locate the target instance, and click the instance ID.
4.  In the left-side navigation pane, select **SQL Explorer**.
5.  Click **Activate Now**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23711/155120109413750_en-US.png)

6.  Specify the SQL log storage duration \(for how long you want to keep the SQL log\), and click **Activate**. The system then automatically starts charging an hourly fee of RMB 0.008/GB.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23711/155120109413755_en-US.png)


## Modify the SQL log storage duration {#section_sgz_q13_mfb .section}

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  In the upper-left corner, select the region of the target instance.
3.  Locate the target instance, and then click the instance ID.
4.  In the left-side navigation pane, select **SQL Explorer**.
5.  Click **Service Settings**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23711/155120109413804_en-US.png)

6.  Modify the storage duration.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23711/155120109413805_en-US.png)


## Disable SQL explorer {#section_f4b_sb3_mfb .section}

**Note:** 

If you disable the SQL explorer function, the existing SQL log will be deleted. Export and save the SQL log to your local disks before you disable the function.

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  In the upper-left corner, select the region of the target instance.
3.  Locate the target instance, and then click the instance ID.
4.  In the left-side navigation pane, select **SQL Explorer**.
5.  Click **Export**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23711/155120109413823_en-US.png)

6.  Click **OK** in the dialog box.
7.  After the export process is complete, click **View Exported List** and then download the log file.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23711/155120109413831_en-US.png)

8.  Click **Service Settings**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23711/155120109413804_en-US.png)

9.  Click the toggle to disable the SQL explorer function.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23711/155120109413807_en-US.png)


