# RDS for MySQL如何保证数据库字符编码正确 {#concept_x2d_5yt_hhb .concept}

字符集是数据库设计过程中需要详细考虑的一点，您需要根据业务场景、用户数据等方面来综合考虑。

[连接MySQL实例](../cn.zh-CN/RDS for MySQL 快速入门/连接MySQL实例.md#)后，您可以依次执行如下命令查看相应数据库的字符集：

```
use <数据库名>;
```

```
show variables like '%character%';
```

![字符集参数](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8266/155436449043345_zh-CN.jpg)

**说明：** 

-   以上参数必须保证除了**character\_set\_filesystem**外的参数都统一，才不会出现乱码的情况。
-   **character\_set\_client**、**character\_set\_connection**以及**character\_set\_results**是客户端的设置。
-   **character\_set\_system**、**character\_set\_server**以及**character\_set\_database**是服务器端的设置。

    服务器端的参数优先级是：

    **character\_set\_database**\>**character\_set\_server**\>**character\_set\_system**


## 操作步骤 {#section_okt_xb5_hhb .section}

1.  [连接MySQL实例](../cn.zh-CN/RDS for MySQL 快速入门/连接MySQL实例.md#)。
2.  在SQL窗口执行以下命令修改客户端字符集。

    ```
    set names <字符集>;
    ```

3.  在SQL窗口执行以下命令修改**character\_set\_database**。

    ```
    ALTER DATABASE <数据库名> CHARACTER SET = <字符集> COLLATE = <字符集排序规则>;
    ```

4.  登录[RDS管理控制台](https://rds.console.aliyun.com/)。
5.  在页面左上角，选择实例所在地域。

    ![选择地域](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7814/155436449136543_zh-CN.png)

6.  找到目标实例，单击实例ID。
7.  在左侧导航栏中单击**参数设置**。
8.  在可修改参数页签下查找到**character\_set\_server**，单击右侧![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8266/155436449143351_zh-CN.jpg)进行修改并单击**确定**。

    **说明：** 修改参数**character\_set\_server**需要重启实例，建议在业务低峰期进行操作。

    ![修改character_set_server参数](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8266/155436449143352_zh-CN.png)

9.  在右上角单击**提交参数**，在弹出的对话框中单击**确定**，等待实例重启。

    **说明：** 该参数修改后，仅对开启高权限账号的实例后来创建的数据库有效，对当前数据库无效。


**character\_set\_system**暂时不提供更改，但是由于其优先级最低因此影响不大。

做完上述的设置之后基本上可以保证不会出现乱码，在代码中设置客户端字符编码时建议通过`set names <字符集>`来修改客户端的设置。

