# 设置透明数据加密TDE {#task_jrp_dw4_ydb .task}

透明数据加密TDE（Transparent Data Encryption）可对数据文件执行实时I/O加密和解密，数据在写入磁盘之前进行加密，从磁盘读入内存时进行解密。TDE不会增加数据文件的大小，开发人员无需更改任何应用程序，即可使用TDE功能。

-   实例类型为RDS for MySQL 5.6。
-   已开通KMS。如果您未开通KMS，可在开通TDE过程中根据引导开通KMS。

加密使用的密钥由密钥管理服务（KMS）产生和管理，RDS不提供加密所需的密钥和证书。部分可用区不仅可以使用阿里云自动生成的密钥，也可以使用自带的密钥材料生成数据密钥，然后授权RDS使用。

## 注意事项 {#section_49k_lh9_w3n .section}

-   TDE开通后无法关闭。
-   TDE开通后无法修改密钥。
-   开通TDE后，用户如果要恢复数据到本地，需要先通过RDS[解密数据](#section_0nx_bpi_ef8)。
-   开通TDE后，会显著增加CPU使用率。
-   使用已有自定义密钥时，需要注意：

    -   禁用密钥、设置密钥删除计划或者删除密钥材料都会造成密钥不可用。
    -   撤销授权关系后，重启RDS实例会导致RDS实例不可用。
    -   需要使用主账号或者具有AliyunSTSAssumeRoleAccess权限的账号。
    **说明：** 关于密钥的相关操作请参见[密钥管理服务](https://help.aliyun.com/document_detail/28935.html)。


## 使用由阿里云自动生成的密钥 {#section_08i_f90_kp4 .section}

1.  登录 [RDS 管理控制台](https://rds.console.aliyun.com/)。
2.  在页面左上角，选择实例所在地域。 

    ![选择地域](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7814/156695551236543_zh-CN.png)

3.  找到目标实例，单击实例ID。
4.  在左侧菜单栏中单击 **数据安全性**。
5.  在TDE页签单击**未开通**左边的滑块。 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7950/15669555124151_zh-CN.png)

6.  选择**使用由阿里云自动生成的密钥**，单击 **确定**，开通TDE。 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41827/156695551257154_zh-CN.png)


## 使用已有自定义密钥 {#section_879_j8c_txp .section}

1.  登录 [RDS 管理控制台](https://rds.console.aliyun.com/)。
2.  在页面左上角，选择实例所在地域。 

    ![选择地域](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7814/156695551236543_zh-CN.png)

3.  找到目标实例，单击实例ID。
4.  在左侧菜单栏中单击 **数据安全性**。
5.  在TDE页签单击**未开通**左边的滑块。 

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7950/15669555124151_zh-CN.png)

6.  选择**使用已有自定义密钥**，选择密钥，单击 **确定**，开通TDE。 

    **说明：** 如果没有自定义密钥，需要单击**前往创建**，在密钥管理服务控制台创建密钥并导入自带的密钥材料。详情请参见[管理密钥](https://help.aliyun.com/document_detail/108805.html)。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/41827/156695551257190_zh-CN.png)


## 加密操作 {#section_i5t_kod_4x2 .section}

登录数据库，执行如下命令，对要加密的表进行加密。

``` {#codeblock_x7t_d9q_yc4}
alter table <tablename> engine＝innodb,block_format=encrypted;
```

## 解密操作 {#section_0nx_bpi_ef8 .section}

如果您要对TDE加密的表解密，请执行如下命令。

``` {#codeblock_ync_c3v_ggv}
alter table <tablename> engine＝innodb,block_format=default;
```

## 相关API {#section_p0h_o8e_zs9 .section}

|API|描述|
|---|--|
|[ModifyDBInstanceTDE](../cn.zh-CN/API参考/安全管理/ModifyDBInstanceTDE.md#)|开启RDS实例透明数据加密。|

