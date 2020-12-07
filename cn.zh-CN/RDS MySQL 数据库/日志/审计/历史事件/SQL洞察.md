# SQL洞察

RDS MySQL的SQL审计功能已升级为SQL洞察功能，继续为您的数据库提供安全审计、性能诊断等增值服务，升级过程中不影响实例的正常使用，升级后费用更低，功能更丰富。

实例需要为如下版本：

-   MySQL 8.0高可用版
-   MySQL 5.7高可用版
-   MySQL 5.6
-   MySQL 5.5

开启SQL洞察功能可以记录所有DML和DDL操作信息，这些信息是系统通过网络协议分析所得，对系统CPU消耗极低。试用版支持免费保留最近一天的日志，更长的日志保留时间需要额外付费。

## 计费

-   试用版：自2020年8月20日开始，各地域将陆续对SQL洞察试用版进行调整：

    SQL洞察试用版将增加15天的使用期限，即使用时间超过15天后，会自动关闭SQL洞察试用版，如果你需要持续使用，请提前修改为非试用版。

    **说明：** 每个实例的SQL洞察试用版只能开启一次。

-   非试用版：可以保存审计日志30天、6个月、1年、3年或5年。按小时扣费，0.008元/（GB\*小时）。

## 使用场景

-   对数据安全有严格要求的行业，如金融行业、安全行业、证券行业、政务行业、保险行业等。
-   需要详细排查数据库运行情况的场景，如极端场景的问题排查、SQL语句性能排查。
-   极端情况保护数据的场景，可以通过SQL洞察记录的SQL语句恢复数据。

## SQL洞察与Binlog日志的区别

RDS MySQL版的增量数据可以通过SQL洞察或Binlog日志来查看，但是两者又有区别：

-   SQL洞察：类似于MySQL的审计日志，会统计所有DML和DDL操作信息，这些信息是系统通过网络协议分析所得。SQL洞察不解析实际的参数值，在SQL查询量较大的时候会丢失少量记录。因此通过这种方式来统计增量数据可能会出现不准确的情况。
-   Binlog日志：准确记录数据库所有的增、删、改操作信息以及恢复用户的增量数据。Binlog日志先暂存在实例中，系统定期将实例中已经写完数据的Binlog日志转移至OSS保存7天。无法保存正在写入数据的Binlog文件，所以单击一键上传Binlog后仍有部分Binlog日志没有被上传。这种方式可以准确记录数据库的增量数据，但是无法获取实时日志。

## 注意事项

-   在线查询时间范围最多为24小时。这是因为SQL洞察记录所有数据库行为，会记录大量SQL语句，在线查询选择时间范围过大，会导致长时间没有返回查询结果，甚至查询超时。

    **说明：** 如果需要查询更大时间范围的SQL记录，请您导出后进行查询。导出功能会异步导出日志， 适合大时间范围内的查询。

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6223729951/p56771.png)

-   在线查询支持组合查询。例如在关键字搜索栏输入test1 test2可以查询包含test1或test2的SQL日志。
-   在线查询不支持模糊查询。
-   SQL语句长度限制为2000字节，超过的部分无法记录。

## 功能说明

-   SQL审计日志

    记录对数据库执行的所有操作。通过审计日志记录，您可以对数据库进行故障分析、行为分析、安全审计等操作。

-   增强搜索

    可以按照数据库、用户、客户端IP、线程ID、执行时长、扫描行数等进行多维度检索，并支持导出和下载搜索结果。

    **说明：**

    -   单维度查询时，维度内设置多个查询条件，查询时执行or操作。例如**用户**栏查询user1和user2，会查询出user1和user2的所有SQL语句。
    -   多维度查询时，维度之间执行and操作。例如**用户**栏查询user1，**操作类型**栏查询select，会查询出user1执行的select语句。
    -   暂不支持模糊查询。
    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6223729951/p13817.png)

-   SQL分析

    新增SQL分析功能，可以对指定时间段的SQL日志进行可视化交互式分析，找出异常SQL，定位性能问题。

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6223729951/p13818.png)

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7223729951/p13819.png)

-   降低成本

    采用新的列式存储和压缩技术，大幅降低了SQL日志存储空间，平均可帮您节省大约60%的成本。


## 开通SQL洞察

1.  登录[RDS管理控制台](https://rds.console.aliyun.com/)。

2.  在左侧单击**实例列表**，然后在上方选择实例所在地域。

    ![选择地域](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3074469951/p36543.png)

3.  找到目标实例，单击实例ID。

4.  在左侧导航栏中单击**SQL洞察**。

5.  单击**立即开通**。

6.  选择SQL审计日志的保存时长，单击**开通服务**。

    **说明：** 超过保存时长的SQL日志将被删除。

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7223729951/p13755.png)


## 修改SQL日志的存储时长

1.  登录[RDS管理控制台](https://rds.console.aliyun.com/)。

2.  在左侧单击**实例列表**，然后在上方选择实例所在地域。

    ![选择地域](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3074469951/p36543.png)

3.  找到目标实例，单击实例ID。

4.  在左侧导航栏中单击**SQL洞察**。

5.  单击**服务设置**。

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2636037061/p13804.png)

6.  修改存储时长并单击**确认**。

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7223729951/p13805.png)


## 关闭SQL洞察

**说明：** SQL洞察功能关闭后，SQL审计日志会被清空。请将SQL审计日志导出并保存至本地后，再关闭SQL洞察功能。

1.  登录[RDS管理控制台](https://rds.console.aliyun.com/)。

2.  在左侧单击**实例列表**，然后在上方选择实例所在地域。

    ![选择地域](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3074469951/p36543.png)

3.  找到目标实例，单击实例ID。

4.  在左侧导航栏中单击**SQL洞察**。

5.  单击**导出**。

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2636037061/p13823.png)

6.  在弹出的对话框中，单击**确认**。

7.  导出完成后，在**查看导出列表**中，下载已导出的文件并妥善保存。

8.  单击**服务设置**。

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/2636037061/p13804.png)

9.  关闭SQL洞察的开关，然后单击**确认**。

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8223729951/p13807.png)


## 常见问题

开通SQL洞察后，如何确认SQL洞察生成的日志大小？

答：您可以在**基本信息**页面的**使用量统计**区域查看实例的SQL洞察日志大小。

![SQL洞察日志大小](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8223729951/p67321.png)

