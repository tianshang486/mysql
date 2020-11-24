# 设置独享代理连接地址SSL加密

RDS提供数据库独享代理服务，基于独享代理提供例如读写分离、连接池、事务拆分等高级功能，您可以对独享代理连接地址进行SSL加密，保证数据的传输安全。

-   实例版本如下：

    -   MySQL 8.0高可用版本地SSD盘（内核小版本20200831或以上）
    -   MySQL 5.7高可用版本地SSD盘（内核小版本20200831或以上）
    -   MySQL 5.6高可用版本地SSD盘（内核小版本20200831或以上）
    **说明：** 如果实例有只读实例，只读实例也需要满足[内核小版本](/cn.zh-CN/RDS MySQL 数据库/升级版本/升级内核小版本.md)要求。

-   [独享代理内核小版本](/cn.zh-CN/RDS MySQL 数据库/数据库代理（读写分离）/数据库独享代理.md)为1.12.8或以上。
-   需要开通SSL加密的代理连接地址总长度不能超过64个字符。
-   当前仅在新版控制台支持此功能，您可以在控制台右下角单击**体验新版**切换到新版控制台。

    ![体验新版](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6384325061/p182014.png)


## 注意事项

-   每个实例仅支持对一个代理连接地址设置SSL加密。
-   开通SSL加密、关闭SSL加密、修改SSL加密、更新证书有效期都会重启实例，请谨慎操作。

## 开通SSL加密

**说明：** 开通SSL加密会重启实例，请谨慎操作。

1.  登录[RDS管理控制台](https://rds.console.aliyun.com/)。

2.  在左侧单击**实例列表**，然后在上方选择实例所在地域。

    ![选择地域](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3074469951/p36543.png)

3.  找到目标实例，单击实例ID。

4.  在左侧导航栏中单击**数据库代理**。

5.  单击**SSL**页签。

6.  单击**未开通**左侧开关，选择需要加密的地址，然后单击**确定**。

    ![开通SSL](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5427824061/p176828.png)


## 修改SSL加密地址

**说明：** 修改SSL加密地址会更新证书有效期，同时重启实例，请谨慎操作。

1.  登录[RDS管理控制台](https://rds.console.aliyun.com/)。

2.  在左侧单击**实例列表**，然后在上方选择实例所在地域。

    ![选择地域](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3074469951/p36543.png)

3.  找到目标实例，单击实例ID。

4.  在左侧导航栏中单击**数据库代理**。

5.  单击**SSL**页签。

6.  单击**设置SSL**，选择需要新的加密地址，然后单击**确定**。

    ![修改SSL](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/5427824061/p176830.png)


## 更新证书有效期

**说明：** 更新证书有效期会重启实例，请谨慎操作。

1.  登录[RDS管理控制台](https://rds.console.aliyun.com/)。

2.  在左侧单击**实例列表**，然后在上方选择实例所在地域。

    ![选择地域](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3074469951/p36543.png)

3.  找到目标实例，单击实例ID。

4.  在左侧导航栏中单击**数据库代理**。

5.  单击**SSL**页签。

6.  单击**更新有效期**，在弹出的重启提示对话框中单击**确定**。


## 关闭SSL加密

**说明：** 关闭SSL加密会重启实例，请谨慎操作。

1.  登录[RDS管理控制台](https://rds.console.aliyun.com/)。

2.  在左侧单击**实例列表**，然后在上方选择实例所在地域。

    ![选择地域](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3074469951/p36543.png)

3.  找到目标实例，单击实例ID。

4.  在左侧导航栏中单击**数据库代理**。

5.  单击**SSL**页签。

6.  单击**已开通**左侧开关，在弹出的对话框中单击**确定**。


