# 设置透明数据加密TDE

透明数据加密TDE（Transparent Data Encryption）可对数据文件执行实时I/O加密和解密，数据在写入磁盘之前进行加密，从磁盘读入内存时进行解密。TDE不会增加数据文件的大小，开发人员无需更改任何应用程序，即可使用TDE功能。

-   实例类型如下：
    -   RDS MySQL 8.0高可用版（本地盘）
    -   RDS MySQL 5.7高可用版（本地盘）
    -   RDS MySQL 5.6
-   已开通KMS。如果您未开通KMS，可在开通TDE过程中根据引导开通KMS。

加密使用的密钥由密钥管理服务（KMS）产生和管理，RDS不提供加密所需的密钥和证书。部分可用区不仅可以使用阿里云自动生成的密钥，也可以使用自带的密钥材料生成数据密钥，然后授权RDS使用。

**说明：** 开通后使用的加密算法为AES\_128\_ECB。

## 注意事项

-   TDE开通过程中会重启实例造成连接中断，请做好业务安排，谨慎操作。
-   TDE开通后无法关闭。
-   TDE开通后无法修改密钥。
-   TDE开通后，用户如果要恢复数据到本地，需要先通过RDS[解密数据](#section_0nx_bpi_ef8)。
-   TDE开通后，会显著增加CPU使用率。
-   使用已有自定义密钥时，需要注意：

    -   禁用密钥、设置密钥删除计划或者删除密钥材料都会造成密钥不可用。
    -   撤销授权关系后，重启RDS实例会导致RDS实例不可用。
    -   需要使用主账号或者具有AliyunSTSAssumeRoleAccess权限的账号。
    **说明：** 关于密钥的相关操作请参见[密钥管理服务](https://help.aliyun.com/document_detail/28935.html)。


## 使用由阿里云自动生成的密钥

1.  登录[RDS管理控制台](https://rds.console.aliyun.com/)。

2.  在左侧单击**实例列表**，然后在上方选择实例所在地域。

    ![选择地域](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3074469951/p36543.png)

3.  找到目标实例，单击实例ID。

4.  在左侧菜单栏中单击**数据安全性**。

5.  在**TDE**页签单击**未开通**左边的滑块。

6.  选择**使用由阿里云自动生成的密钥**，单击**确定**，开通TDE。

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8123729951/p57154.png)


## 使用已有自定义密钥

1.  登录[RDS管理控制台](https://rds.console.aliyun.com/)。

2.  在左侧单击**实例列表**，然后在上方选择实例所在地域。

    ![选择地域](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3074469951/p36543.png)

3.  找到目标实例，单击实例ID。

4.  在左侧菜单栏中单击**数据安全性**。

5.  在**TDE**页签单击**未开通**左边的滑块。

6.  选择**使用已有自定义密钥**，选择密钥，单击**确定**，开通TDE。

    **说明：** 如果没有自定义密钥，需要单击**前往创建**，在密钥管理服务控制台创建密钥并导入自带的密钥材料。详情请参见[管理密钥](https://help.aliyun.com/document_detail/108805.html)。

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/8123729951/p57190.png)


## 加密操作

登录数据库，执行如下命令，对要加密的表进行加密。

-   MySQL 5.6

    ```
    alter table <tablename> engine=innodb,block_format=encrypted;
    ```

-   MySQL 5.7或8.0

    ```
    alter table <tablename> encryption='Y';
    ```


## 解密操作

如果您要对TDE加密的表解密，请执行如下命令：

-   MySQL 5.6

    ```
    alter table <tablename> engine=innodb,block_format=default;
    ```

-   MySQL 5.7或8.0

    ```
    alter table <tablename> encryption='N';
    ```


## 常见问题

-   开启TDE后，常用数据库工具（Navicat等）还能正常使用吗？

    可以正常使用。

-   加密后查看数据为什么还是明文的？

    查询数据时会解密并读取到内存，所以是明文显示。开启TDE可以防止备份泄露导致数据泄露，备份文件是加密的，无法用于恢复到本地，如果要恢复数据到本地，需要先[解密数据](#section_0nx_bpi_ef8)。


## 相关文档

[RDS SQL Server设置透明数据加密](/cn.zh-CN/RDS SQL Server 数据库/数据安全/加密/设置透明数据加密TDE.md)

## 相关API

|API|描述|
|---|--|
|[开启TDE](/cn.zh-CN/API 参考/安全加密/开启TDE.md)|开启RDS实例透明数据加密。|

