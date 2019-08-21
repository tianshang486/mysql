# SQL洞察 {#concept_msp_gz1_mfb .concept}

为了更好地提供服务，RDS for MySQL的SQL审计功能将升级为**SQL洞察**功能，继续为您的数据库提供安全审计、性能诊断等增值服务，升级过程中不影响实例的正常使用，升级后费用更低，功能更丰富。

## SQL洞察与Binlog日志的区别 {#section_mqd_z9j_wsr .section}

RDS for MySQL版的增量数据可以通过SQL洞察或Binlog日志来查看，但是两者又有区别：

-   SQL洞察：类似于MySQL的审计日志，会统计所有DML和DDL操作信息，这些信息是系统通过网络协议分析所得。SQL洞察不解析实际的参数值，在SQL查询量较大的时候会丢失少量记录。因此通过这种方式来统计增量数据可能会出现不准确的情况。
-   Binlog日志：准确记录数据库所有的增、删、改操作信息以及恢复用户的增量数据。Binlog日志先暂存在实例中，系统定期将实例中已经写完数据的Binlog日志转移至OSS保存7天。无法保存正在写入数据的Binlog文件，所以单击**一键上传Binlog**后仍有部分Binlog日志没有被上传。这种方式可以准确记录数据库的增量数据，但是无法获取实时日志。

## 前提条件 {#section_ccm_hp5_xgb .section}

实例需要为如下版本：

-   MySQL 8.0高可用版（本地SSD盘）
-   MySQL 5.7高可用版
-   MySQL 5.6
-   MySQL 5.5

## 注意事项 {#section_vxz_4ft_kfu .section}

在线查询时间范围最多为24小时。这是因为SQL洞察记录所有数据库行为，会记录大量SQL语句，在线查询选择时间范围过大，会导致长时间没有返回查询结果，甚至查询超时。

**说明：** 如果需要查询更大时间范围的SQL记录，请您导出后进行查询。导出功能会异步导出日志， 适合大时间范围内的查询。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41829/156635463056771_zh-CN.png)

## 功能说明 {#section_ovx_hcv_lfb .section}

-   **SQL审计日志**：记录对数据库执行的所有操作。通过审计日志记录，您可以对数据库进行故障分析、行为分析、安全审计等操作。
-   **增强搜索**：可以按照数据库、用户、客户端IP、线程ID、执行时长、扫描行数等进行多维度检索，并支持导出和下载搜索结果。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23711/156635463013817_zh-CN.png)

-   **SQL分析**：新增SQL分析功能，可以对指定时间段的SQL日志进行可视化交互式分析，找出异常SQL，定位性能问题。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23711/156635463013818_zh-CN.png)

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23711/156635463113819_zh-CN.png)

-   **降低成本**：采用新的列式存储和压缩技术，大幅降低了SQL日志存储空间，平均可帮您节省大约60%的成本。SQL洞察功能的单价为¥0.008/GB，按小时扣费。

## 开通SQL洞察 {#section_g4n_21b_mfb .section}

1.  登录[RDS管理控制台](https://rds.console.aliyun.com/)。
2.  在页面左上角，选择实例所在地域。

    ![地域截图](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7882/156635463137169_zh-CN.png)

3.  找到目标实例，单击实例ID。
4.  在左侧导航栏中单击**SQL洞察**。
5.  单击**立即开通**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23711/156635463113750_zh-CN.png)

6.  选择SQL审计日志的保存时长，单击**开通服务**。

    -   试用版：审计日志仅保存一天，即只能查询一天范围内的数据；不支持数据导出等高级功能；不保障数据完整性。
    -   30天或以上：按小时扣费，0.008元/\(GB\*小时\)。
    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23711/156635463113755_zh-CN.png)


## 修改SQL日志的存储时长 {#section_sgz_q13_mfb .section}

1.  登录[RDS管理控制台](https://rds.console.aliyun.com/)。
2.  在页面左上角，选择实例所在地域。

    ![地域截图](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7882/156635463137169_zh-CN.png)

3.  找到目标实例，单击实例ID。
4.  在左侧导航栏中单击**SQL洞察**。
5.  单击**服务设置**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23711/156635463213804_zh-CN.png)

6.  修改存储时长。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23711/156635463213805_zh-CN.png)


## 关闭SQL洞察 {#section_f4b_sb3_mfb .section}

**说明：** 

SQL洞察功能关闭后，SQL审计日志会被清空。请将SQL审计日志导出并保存至本地后，再关闭SQL洞察功能。

1.  登录[RDS管理控制台](https://rds.console.aliyun.com/)。
2.  在页面左上角，选择实例所在地域。

    ![地域截图](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7882/156635463137169_zh-CN.png)

3.  找到目标实例，单击实例ID。
4.  在左侧导航栏中单击**SQL洞察**。
5.  单击**导出**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23711/156635463213823_zh-CN.png)

6.  在弹出的对话框中，单击**确定**。
7.  导出完成后，在**导出列表**中，下载已导出的文件并妥善保存。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23711/156635463213831_zh-CN.png)

8.  单击**服务设置**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23711/156635463213804_zh-CN.png)

9.  关闭SQL洞察的开关。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23711/156635463313807_zh-CN.png)


## 常见问题 {#section_fgw_4hl_zgb .section}

开通SQL洞察后，如何确认SQL洞察生成的日志大小？

答：您可以在右上角选择**费用** \> **进入费用中心**，然后在左侧菜单栏的**消费记录** \> **消费明细**里查询相应实例的SQL日志大小。

![SQL洞察日志大小](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23711/156635463339928_zh-CN.png)

**说明：** **SQL审计**即SQL洞察的日志大小。

