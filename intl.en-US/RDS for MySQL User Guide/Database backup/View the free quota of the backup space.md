# View the free quota of the backup space {#concept_ipg_lm4_ydb .concept}

This topic describes how to view the quota of free backup space and calculate the quota for an RDS instance. Backup files occupy backup space. Each RDS instance has a specific quota of free backup space. If the total size of backup files exceeds the quota, additional fees are incurred.

## Calculate the quota of free backup space for an RDS instance {#section_n1i_4b4_yjl .section}

Quota of free backup space = Round up \(50% × Storage space purchased for the RDS instance\) \(Unit: GB\)

Backup space beyond the quota = Backup data size + Backup log size - Round up \(50% × Storage space purchased for the RDS instance\) \(Unit: GB\)

For example, the backup data size is 30 GB, the backup log size is 10 GB, and the storage space is 60 GB, then you must pay for 10-GB storage space every hour:

``` {#codeblock_4m6_z5w_56t}
Hourly fees = 30 + 10 - 50% × 60 = 10 (GB)
```

**Note:** 

-   For more information about the hourly fees for the backup space beyond the quota, see [ApsaraDB RDS for MySQL pricing](https://www.alibabacloud.com/product/apsaradb-for-rds?spm=a3c0i.7938564.220486.8.4nCrkf#pricing).
-   The Basic Editions of some DB engines store backup files generated within the last seven days for free. For more information, log on to the RDS console.

    ![基础版截图](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7805/156686860437301_en-US.png)


## View the quota of free backup space in the RDS console {#section_lyn_fm4_ydb .section}

1.  Log on to the [RDS console](https://rds.console.aliyun.com/).
2.  In the upper-left corner, select the region where the target RDS instance is located.

    ![选择地域](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7814/156686860436543_en-US.png)

3.  Find the target RDS instance and click its ID.
4.  In the **Usage Statistics** section of the Basic Information page, view the data size next to **Space Used for Backup**. The data size is the quota of free backup space.

    **Note:** The quota of free backup space varies depending on the instance type. The following figure is only an example.

    ![使用量统计](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7965/15668686044106_en-US.png)


