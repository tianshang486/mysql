# 金蝶K/3 WISE 接入阿里云RDS for SQL Server {#concept_995029 .concept}

本文介绍金蝶K/3 WISE 15.0/15.1如何接入阿里云RDS for SQL Server，实现在RDS实例和服务器之间执行分布式事务。

## 解决方案介绍 {#section_orq_a90_mhl .section}

解决方案主要分为如下三个步骤：

1.  [恢复账套数据到RDS](#)：将本地金蝶K/3 WISE的账套数据库全量数据备份上传到OSS，之后恢复到RDS。
2.  [设置允许执行分布式事务](#)：调整RDS、ECS、Windows系统的访问设置，确保端口畅通，可以执行分布式事务。
3.  [替换账套管理工具](#)：替换账套管理工具以便兼容RDS。

## 准备工作 {#section_dqu_ia9_hgl .section}

-   在Windows Server 2016系统的ECS实例上安装金蝶K/3 WISE。
-   [创建RDS for SQL Server实例](../../../../cn.zh-CN/RDS for SQL Server 快速入门/创建RDS for SQL Server实例.md#)。
-   本地金蝶K/3 WISE的账套数据库文件已经做好全量数据备份。

**说明：** 

-   安装金蝶的ECS实例需要和RDS实例在同一个地域，且[VPC](https://help.aliyun.com/document_detail/100380.html)相同。
-   RDS for SQL Server实例需要为如下版本：
    -   SQL Server 2012/2016企业版高可用版
    -   SQL Server 2012/2016标准版

## 恢复账套数据到RDS {#section_jk1_kdq_mdl .section}

**上传账套数据备份文件**

1.  登录[OSS控制台](https://oss.console.aliyun.com/overview)。
2.  在左侧单击![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/803375/156516311450835_zh-CN.png)创建存储空间。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/803375/156516311450836_zh-CN.png)

3.  设置如下参数。

    |参数|说明|
    |--|--|
    |**Bucket名称**|存储空间名称。|
    |**区域**|存储空间所在地域。请确保存储空间和ECS、RDS实例在同一地域。|
    |**存储类型**|选择**低频访问**。|
    |**读写权限**|选择**私有**。|
    |**服务端加密**|选择**无**。|
    |**同城冗余存储**|选择**关闭**。|
    |**实时日志查询**|选择**不开通**。|

    **说明：** 详细的参数介绍请参见[创建存储空间](https://help.aliyun.com/document_detail/31885.html)。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/803375/156516311450846_zh-CN.png)

4.  单击**确定**。
5.  在左侧选择刚创建的存储空间。
6.  选择**文件管理** \> **上传文件**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/803375/156516311550848_zh-CN.png)

7.  将要上传的数据库备份文件拖拽到**上传文件**区域；或者单击**直接上传**，选择备份文件。

    **说明：** 详细的参数介绍请参见[上传文件](https://help.aliyun.com/document_detail/31886.html)。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/803375/156516311550849_zh-CN.png)


**创建高权限账号**

1.  登录[RDS管理控制台](https://rdsnext.console.aliyun.com/)。
2.  在页面左上角，选择实例所在地域。
3.  找到目标实例，单击实例ID。
4.  在左侧导航栏选择**账号管理**。
5.  在右侧单击**创建账号**。
6.  设置如下参数。

    |参数|说明|
    |--|--|
    |**数据库账号**|长度为2~16个字符，由小写字母、数字或下划线组成。由小写字母开头，结尾必须是字母或数字。|
    |**账号类型**|选择**高权限账号**。|
    |**密码**|设置账号密码。要求如下：     -   长度为8~32个字符。
    -   由大写字母、小写字母、数字、特殊字符中的任意三种组成。
    -   特殊字符为!@\#$%^&\*\(\)\_+-=
 |
    |**确认密码**|再次输入密码。|
    |**备注说明**|输入备注说明便于区分业务。|

7.  单击**确定**。

**OSS备份数据恢复上云**

1.  登录[RDS管理控制台](https://rdsnext.console.aliyun.com/)。
2.  在页面左上角，选择实例所在地域。
3.  找到目标实例，单击实例ID。
4.  在左侧导航栏选择**备份恢复**。
5.  在右上角单击**OSS备份数据恢复上云**。

    **说明：** 如果没有此按钮，请确认您的[实例版本](#section_dqu_ia9_hgl)。

6.  两次单击**下一步**进入**数据导入**页签。
7.  设置如下参数。

    |参数|说明|
    |--|--|
    |**数据库名**|目标实例上的目标数据库名称。|
    |**OSS Bucket**|选择备份文件所在的OSS存储空间。|
    |**OSS 子文件夹名**|备份文件所在的子文件夹名称。|
    |**OSS 文件列表**|单击右侧放大镜按钮，可以按照备份文件名前缀模糊查找，会展示文件名、文件大小和更新时间。请选择需要上云的备份文件。|
    |**上云方案**|选择**打开数据库**。|
    |**一致性检查方式**|选择**同步执行 DBCC**。|

    **说明：** 如果您是第一次使用OSS备份数据恢复上云功能，该页面会提示您给RDS官方服务账号授予访问OSS的权限，单击**授权地址**并**授权地址**即可。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/803375/156516311550875_zh-CN.png)

8.  单击**确定**。

    **说明：** 请您耐心等待数据导入完成，可以在数据库管理页面查看数据库状态。


## 设置允许执行分布式事务 {#section_jqg_mfn_abz .section}

**RDS设置**

1.  登录[RDS管理控制台](https://rdsnext.console.aliyun.com/)。
2.  在页面左上角，选择实例所在地域。
3.  找到目标实例，单击实例ID。
4.  在左侧导航栏单击**数据安全性**。
5.  在右侧单击**修改**，填写ECS实例的IP地址。

    **说明：** 

    -   如果ECS与RDS在相同VPC内，请填写ECS的私有IP。私有IP可以在ECS实例的实例详情页面查看。
    -   如果ECS与RDS在不同VPC内，请填写ECS的公网IP，且需要为RDS实例[申请外网地址](../../../../cn.zh-CN/RDS for SQL Server 快速入门/初始化配置/申请外网地址.md#)。
    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/803375/156516311550870_zh-CN.png)

6.  单击**确定**。
7.  选择分布式事务白名单页签。
8.  单击**添加白名单分组**。
9.  设置如下参数。

    |参数|说明|
    |--|--|
    |**分组名称**|长度为2~32个字符。由数字、小写字母以及下划线（\_）组成。由小写字母开头，结尾必须是字母或数字。|
    |**组内白名单**|填写ECS实例的IP地址和Windows系统的计算机名，以英文逗号（,）分隔。示例：192.168.1.100,k3ecstest。 如果需要填写多组，请分行填写。

 **说明：** 计算机名在服务器的**控制面板** \> **系统和安全** \> **系统**页面查看。

 |

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/803375/156516311650885_zh-CN.png)

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/803375/156516311650883_zh-CN.png)

10. 单击**确定**。

**ECS设置**

1.  登录[ECS管理控制台](https://ecs.console.aliyun.com/)
2.  在页面左上角，选择实例所在地域。
3.  找到目标实例，单击实例ID。
4.  在左侧导航栏单击**本实例安全组**。
5.  在右侧单击**配置规则**。
6.  在右上方单击**添加安全组规则**。
7.  设置如下参数。

    |参数|说明|
    |--|--|
    |**规则方向**|选择**入方向**。|
    |**授权策略**|选择**允许**。|
    |**协议类型**|选择**自定义 TCP**。|
    |**端口范围**|填写**135**。 **说明：** 135是RPC服务的固定端口。

 |
    |**优先级**|填写**1**。|
    |**授权类型**|选择**IPv4地址段访问**。|
    |**授权对象**|查看RDS实例的**数据安全性** \> **分布式事务白名单**页面，将RDS实例信息的2个IP地址填写到**授权对象**框。![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/803375/156516311650892_zh-CN.png)

|
    |**描述**|长度为2~256个字符，不能以http://或https://开头。|

8.  单击**确定**。
9.  再次添加安全组规则，**端口范围**填写**1024/65535**，其他参数和上一条规则相同。

**Windows系统设置**

1.  登录Windows Server 2016系统。
2.  打开hosts文件，路径为C:\\Windows\\System32\\drivers\\etc\\hosts。
3.  查看RDS实例的**数据安全性** \> **分布式事务白名单**页面，将RDS实例信息的2条信息填写到hosts文件的结尾处。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/803375/156516311650896_zh-CN.png)

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/803375/156516311650898_zh-CN.png)

4.  保存hosts文件。
5.  在**控制面板** \> **系统和安全** \> **管理工具**页面打开**组件服务**。
6.  选择**组件服务** \> **计算机** \> **我的电脑** \> **Distributed Transaction Coordinator**。
7.  在右侧**本地DTC**上单击鼠标右键，选择**属性**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/803375/156516311750901_zh-CN.png)

8.  选择安全页签，参照下图进行设置。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/803375/156516311750903_zh-CN.png)

9.  单击**确定**，在弹出的MSDTC服务对话框中单击**是**，等待MSDTC服务重新启动完成。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/803375/156516311850906_zh-CN.png)


## 账套管理初始化 {#section_qnz_69u_5xl .section}

1.  下载对应的账套管理工具。

    -   [金蝶K/3 WISE 15.1](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/128809/cn_zh/1565162995121/K3WISE15.1%20ForRDS.rar)
    -   [金蝶K/3 WISE 15.0](http://docs-aliyun.cn-hangzhou.oss.aliyun-inc.com/assets/attach/128809/cn_zh/1565162975502/K3WISE15.0%20ForRDS.rar)
    **说明：** 不同金蝶K/3 WISE版本需要的账套管理工具不同，当前仅提供金蝶K/3 WISE 15.0/15.1的账套管理工具。

2.  解压替换到金蝶的安装目录：K3ERP\\KDSYSTEM\\KDCOM。
3.  打开金蝶K/3 WISE软件。
4.  在弹出的账套管理数据库设置页面设置相关身份验证信息和**数据服务器**。

    **说明：** **数据服务器**填写RDS实例的内网地址。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/803375/156516311851668_zh-CN.png)

5.  在系统的下拉菜单里单击**预设连接**，设置预设连接，方便使用。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/803375/156516311851669_zh-CN.png)

6.  在数据库的下拉菜单里单击**注册账套**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/803375/156516311851676_zh-CN.png)

7.  选择对应的数据库，并单击**所有**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/803375/156516311951670_zh-CN.png)


## 登录使用金蝶K/3 WISE {#section_7wl_ome_4lj .section}

全部设置完成后，ECS实例和RDS实例之间就能够支持分布式事务，您也可以正常登录并使用金蝶K/3 WISE。

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/803375/156516311951672_zh-CN.png)

