# MySQL设置本地Binlog {#task_hsm_ycn_42b .task}

RDS for MySQL支持您手动设置本地Binlog日志的清理规则，您可以根据需求灵活设置Binlog。在设置Binlog之前请先了解MySQL Binlog日志生成和清理规则。

相关API，请参见[DescribeBinlogFiles](../cn.zh-CN/API参考/日志管理/DescribeBinlogFiles.md#)。

**MySQL实例空间内生成Binlog日志的规则如下：**

-   通常情况下，当Binlog大小超过500MB时会切换到下一序号文件继续写入，即写满500MB就会生成新的Binlog日志文件。新的Binlog文件继续写入，老的Binlog文件并不会立刻上传，而是异步上传。
-   有些情况下，Binlog日志不满500MB就不再写入，比如由于命令的执行、系统重启等原因。
-   有些情况下，会出现Binlog文件尺寸超过500MB的情况，比如当时在执行大事务，不断写入Binlog导致当前Binlog文件尺寸超过500MB。

**MySQL实例的空间内默认清理binlog日志的规则如下：**

-   实例空间内默认会保存最近18个小时内的Binlog文件。
-   当实例使用空间小于购买空间的80%时，系统会保存购买空间的30%的Binlog（即使该Binlog文件已经上传到OSS内）。
-   当实例使用空间超过购买空间的80%时，Binlog会在上传到OSS后，发起删除本地数据的请求，但本地删除会有任务调度，有一定延迟。

1.  登录[RDS管理控制台](https://rds.console.aliyun.com/)。
2.  选择目标实例所在地域。![选择地域](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7814/156774133336543_zh-CN.png)


3.  在左侧导航栏中，选择备份恢复，进入备份恢复页面。
4.  切换至本地日志设置页签，显示实例当前的本地Binlog设置。 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16164/15677413347410_zh-CN.png)

5.  在本地Binlog设置页面单击**编辑**进入本地Binlog设置窗口。 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/16164/15677413347413_zh-CN.png)

6.  设置本地Binlog的**保留时长**、**空间使用率不超过**的范围值以及是否开启**可用空间保护**。 参数说明：
    -   **保留时长**：默认值为18，表示实例空间内默认保存最近18个小时内的Binlog文件，18个小时之前的日志将在备份后（需要开启日志备份）清理。**保留时长**可选范围值为0~7\*24小时。
    -   **空间使用率不超过**：默认值为30%，表示本地Binlog空间使用率大于30%时，系统会从最早的Binlog开始清理，直到空间使用率低于30%。**空间使用率不超过**可选范围值为0 - 50% 。
    -   **可用空间保护**，默认开启该功能，表示当实例总空间使用率超过80%或实例剩余可用空间不足5GB时，会强制从最早的Binlog开始清理，直到总空间使用率降到80%以下且实例剩余可用空间大于5GB。
7.  设置好各项参数后单击**确定**完成设置。

