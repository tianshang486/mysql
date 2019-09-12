# 切换专有网络VPC和虚拟交换机 {#task_2134447 .task}

您可以直接切换部分实例的专有网络VPC和虚拟交换机。

实例版本如下：

-   MySQL 8.0高可用版（本地SSD盘）
-   MySQL 5.7高可用版（本地SSD盘）
-   MySQL 5.6高可用版
-   MySQL 5.5

## 影响 {#section_xyy_xzz_x0j .section}

-   切换过程会有30秒闪断，请确保应用程序具有重连机制。
-   切换专有网络VPC和虚拟交换机会造成虚拟IP（VIP）的变更，请您在应用程序中尽量使用[连接地址](cn.zh-CN/RDS for MySQL 用户指南/数据库连接/设置连接地址.md#)进行连接，不要使用IP地址。
-   VIP的变更会短暂影响到[DRDS](https://help.aliyun.com/document_detail/117729.html)的可用性，请及时在DRDS控制台刷新并查看连接信息。
-   VIP的变更会短暂影响到[DMS](https://help.aliyun.com/document_detail/47550.html)、[DTS](https://help.aliyun.com/document_detail/26592.html)的使用，变更结束后会自动恢复正常。
-   客户端缓存会导致只能读取数据，无法写入数据，请及时清理缓存。

## 操作步骤 {#section_61o_50t_wlh .section}

1.  登录[RDS管理控制台](https://rds.console.aliyun.com/)。
2.  在页面左上角，选择实例所在地域。 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/62164/156825288549697_zh-CN.png)

3.  找到目标实例，单击实例ID。
4.  在左侧导航栏选择**数据库连接**。
5.  在右侧单击**切换交换机**。 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1693774/156825288559957_zh-CN.png)

6.  选择VPC和虚拟交换机，并单击**确定**。 

    **说明：** 如需新建VPC或虚拟交换机请单击**到控制台创建**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/1693774/156825288559958_zh-CN.png)

7.  在弹出的风险提示框中单击**确定切换**。

## 相关文档 {#section_5p1_i2t_xsp .section}

对于不支持直接切换专有网络VPC和虚拟交换机的实例，请您参见[RDS实例如何变更VPC](../cn.zh-CN/常见问题/网络__IP/RDS实例如何变更VPC.md#)。

