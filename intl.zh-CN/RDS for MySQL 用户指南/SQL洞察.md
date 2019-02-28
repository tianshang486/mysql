# SQL洞察 {#concept_msp_gz1_mfb .concept}

为了更好地提供服务，RDS for MySQL的SQL审计功能将升级为**SQL洞察**功能，继续为您的数据库提供安全审计、性能诊断等增值服务，升级过程中不影响实例的正常使用，升级后费用更低，功能更丰富。

## 前提条件 {#d7e21 .section}

实例需要为如下版本：

-   RDS for MySQL 5.5
-   RDS for MySQL 5.6
-   RDS for MySQL 5.7高可用本地SSD盘版

## 升级计划 {#d7e42 .section}

为保证服务质量，全球的RDS for MySQL实例将分批进行升级。

在升级日期后，新购和存量的实例都将支持SQL洞察功能。

|地域|升级日期|
|--|----|
|杭州、上海、青岛、北京、深圳、香港|2018年12月底|
|新加坡、马来西亚、印度尼西亚|2019年1月底|
|日本、澳洲、印度、张北|2019年2月底|
|伦敦|2019年3月底|
|呼和浩特、美国（硅谷、弗尼吉亚）、迪拜|待定|

## 功能说明 {#d7e122 .section}

-   **SQL审计日志**：记录对数据库执行的所有操作。通过审计日志记录，您可以对数据库进行故障分析、行为分析、安全审计等操作。
-   **增强搜索**：可以按照数据库、用户、客户端IP、线程ID、执行时长、扫描行数等进行多维度检索，并支持导出和下载搜索结果。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23711/155132110513817_zh-CN.png)

-   **SQL分析**：新增SQL分析功能，可以对指定时间段的SQL日志进行可视化交互式分析，找出异常SQL，定位性能问题。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23711/155132110513818_zh-CN.png)

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23711/155132110513819_zh-CN.png)

-   **降低成本**：采用新的列式存储和压缩技术，大幅降低了SQL日志存储空间，平均可帮您节省大约60%的成本。SQL洞察功能的单价为US$ 0.0018/GB，按小时扣费。

## 开通SQL洞察 {#d7e154 .section}

1.  登录[RDS管理控制台](https://rds.console.aliyun.com/)。
2.  在页面左上角，选择实例所在地域。

    ![地域截图](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7882/155132110537169_zh-CN.png)

3.  找到目标实例，单击实例ID。
4.  在左侧导航栏中单击**SQL洞察**。
5.  单击**立即开通**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23711/155132110513750_zh-CN.png)

6.  选择SQL审计日志的保存时长，单击**开通服务**。

    -   试用版：审计日志仅保存一天，即只能查询一天范围内的数据；不支持数据导出等高级功能；不保障数据完整性。
    -   30天或以上：按小时扣费，每小时每GB收费US$ 0.0018。
    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23711/155132110513755_zh-CN.png)


## 修改SQL日志的存储时长 {#d7e209 .section}

1.  登录[RDS管理控制台](https://rds.console.aliyun.com/)。
2.  在页面左上角，选择实例所在地域。

    ![地域截图](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7882/155132110537169_zh-CN.png)

3.  找到目标实例，单击实例ID。
4.  在左侧导航栏中单击**SQL洞察**。
5.  单击**服务设置**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23711/155132110613804_zh-CN.png)

6.  修改存储时长。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23711/155132110613805_zh-CN.png)


## 关闭SQL洞察 {#d7e252 .section}

**说明：** 

SQL洞察功能关闭后，SQL审计日志会被清空。请将SQL审计日志导出并保存至本地后，再关闭SQL洞察功能。

1.  登录[RDS管理控制台](https://rds.console.aliyun.com/)。
2.  在页面左上角，选择实例所在地域。

    ![地域截图](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7882/155132110537169_zh-CN.png)

3.  找到目标实例，单击实例ID。
4.  在左侧导航栏中单击**SQL洞察**。
5.  单击**导出**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23711/155132110613823_zh-CN.png)

6.  在弹出的对话框中，单击**确定**。
7.  导出完成后，在**导出列表**中，下载已导出的文件并妥善保存。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23711/155132110613831_zh-CN.png)

8.  单击**服务设置**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23711/155132110613804_zh-CN.png)

9.  关闭SQL洞察的开关。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/23711/155132110613807_zh-CN.png)


