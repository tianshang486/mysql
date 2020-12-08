# 设置SSL加密

为了提高链路安全性，您可以启用SSL（Secure Sockets Layer）加密，并安装SSL CA证书到需要的应用服务。SSL在传输层对网络连接进行加密，能提升通信数据的安全性和完整性，但会同时增加网络连接响应时间。

SSL是Netscape公司所提出的安全保密协议，在浏览器和Web服务器之间构造安全通道来进行数据传输，采用RC4、MD5、RSA等加密算法实现安全通讯。国际互联网工程任务组（IETF）对SSL 3.0进行了标准化，标准化后更名为安全传输层协议（TLS）。由于SSL这一术语更为常用，因此本文所述SSL加密实际是指TLS加密。

**说明：** RDS支持的TLS版本为1.0、1.1和1.2。

## 注意事项

-   SSL的证书有效期为1年，请及时更新证书有效期并重新下载配置CA证书，否则使用加密连接的客户端程序将无法正常连接。
-   由于SSL加密的实现原理，启用SSL加密会显著增加CPU使用率，建议您仅在外网链路有加密需求的时候启用SSL加密。内网链路相对较安全，一般无需对链路加密。
-   开启SSL加密后，将无法再关闭，请谨慎操作。
-   读写分离地址不支持SSL加密。

## 开启SSL加密

1.  登录[RDS管理控制台](https://rds.console.aliyun.com/)。

2.  在左侧单击**实例列表**，然后在上方选择实例所在地域。

    ![选择地域](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3074469951/p36543.png)

3.  找到目标实例，单击实例ID。

4.  在左侧菜单栏中单击**数据安全性**。

5.  选择**SSL**标签页。

6.  单击**未开通**前面的滑块开关。

7.  在弹出的对话框中选择要开通SSL加密的地址，单击**确定**，开通SSL加密。

    **说明：** 用户可以根据需要，选择加密内网链路或者外网链路，但只可以加密一条链路。

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/6249259951/p4148.png)

8.  单击**下载证书**，下载SSL CA证书。

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/9236037061/p4149.png)

    下载的文件为压缩包，包含如下三个文件：

    -   p7b文件：用于Windows系统中导入CA证书。
    -   PEM文件：用于其他系统或应用中导入CA证书。
    -   JKS文件：Java中的truststore证书存储文件，密码统一为apsaradb，用于Java程序中导入CA证书链。

        **说明：** 在Java中使用JKS证书文件时，jdk7和jdk8需要修改默认的jdk安全配置，在应用程序所在主机的`jre/lib/security/java.security`文件中，修改如下两项配置：

        ```
        jdk.tls.disabledAlgorithms=SSLv3, RC4, DH keySize < 224
        jdk.certpath.disabledAlgorithms=MD2, RSA keySize < 1024
        ```

        若不修改jdk安全配置，会报如下错误。其它类似报错，一般也都由Java安全配置导致。

        ```
        javax.net.ssl.SSLHandshakeException: DHPublicKey does not comply to algorithm constraints
        ```


## 配置SSL CA证书

开通SSL加密后，应用或者客户端连接RDS时需要配置SSL CA证书。本文以MySQL Workbench为例，介绍SSL CA证书安装方法。其它应用或者客户端请参见对应产品的使用说明。

1.  打开MySQL Workbench。

2.  选择**Database** \> **Manage Connections** 。

3.  启用**Use SSL**，并导入SSL CA证书。

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/7140359951/p4150.png)


## 更新证书有效期

**说明：**

-   **更新有效期**操作将会重启实例，重启前请做好业务安排，谨慎操作。
-   **更新有效期**后需要重新下载及配置CA证书。

![更新证书有效期](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0336037061/p45367.png)

