# MySQL设置本地Binlog

RDS MySQL支持您手动设置本地Binlog日志的清理规则，您可以根据需求灵活设置Binlog。在设置Binlog之前请先了解MySQL Binlog日志生成和清理规则。

-   MySQL实例空间内生成Binlog日志的规则

    -   通常情况下，当Binlog大小超过500MB时会切换到下一序号文件继续写入，即写满500MB就会生成新的Binlog日志文件。新的Binlog文件继续写入，老的Binlog文件并不会立刻上传，而是异步上传。
    -   有些情况下，Binlog日志不满500MB就不再写入，例如由于命令的执行、系统重启等原因。
    -   有些情况下，会出现Binlog文件尺寸超过500MB的情况，例如当时在执行大事务，不断写入Binlog导致当前Binlog文件尺寸超过500MB。
    **说明：** MySQL 5.7和8.0的企业版实例，固定为500MB时进行切换。

-   MySQL实例空间内默认清理binlog日志的规则
    -   实例空间内默认会保存最近18个小时内的Binlog文件。
    -   当实例使用空间小于购买空间的80%时，系统会保存购买空间的30%的Binlog（即使该Binlog文件已经上传到OSS内）。
    -   当实例使用空间超过购买空间的80%时，Binlog会在上传到OSS后，发起删除本地数据的请求，但本地删除会有任务调度，有一定延迟。
    -   当Binlog本地使用量超过设定值仍未清理，可能是客户端故障或DTS任务阻塞，请查看日志管理中的错误日志里是否有出现如下日志：

        ```
        [Warning] file /home/mysql/data3001/mysql/mysql-bin.069435 was not purged because it was being readby thread number 17126285
        ```

        然后将相应的任务终止即可。


1.  登录[RDS管理控制台](https://rds.console.aliyun.com/)。

2.  选择目标实例所在地域。

    ![选择地域](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/3074469951/p36543.png)

3.  在左侧导航栏中，选择备份恢复，进入备份恢复页面。

4.  单击本地日志设置页签。

5.  单击**编辑**设置本地Binlog设置，参数说明如下。

    |参数|说明|
    |--|--|
    |**保留时长**|默认值为18，表示实例空间内默认保存最近18个小时内的Binlog文件，18个小时之前的日志将在备份后（需要开启日志备份）清理。取值为0~168。|
    |**空间使用率不超过**|默认值为30%，表示本地Binlog空间使用率大于30%时，系统会从最早的Binlog开始清理。取值为0~50 。|
    |**保留个数**|默认值为60。Binlog文件的保留个数，超出限制后会从最早的Binlog开始清理。取值6~100。|
    |**可用空间保护**|默认开启该功能，表示当实例总空间使用率超过80%或实例剩余可用空间不足5GB时，会强制从最早的Binlog开始清理，直到总空间使用率降到80%以下且实例剩余可用空间大于5GB。|

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/0323729951/p7413.png)

6.  单击**确定**。


