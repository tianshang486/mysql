# SQL Server接入自建域

本文介绍如何配置ECS实例的域控服务器，以及如何将RDS SQL Server实例接入域。

-   实例版本如下：
    -   2019标准版（非共享型规格）
    -   2017标准版和企业集群版（非共享型规格）
    -   2016标准版和企业版（非共享型规格）
    -   2012标准版和企业版（非共享型规格）
-   RDS和域控服务器所在ECS在相同VPC。
-   ECS安全组放通RDS的内网IP。详情请参见[添加安全组规则](/intl.zh-CN/安全/安全组/添加安全组规则.md)。
-   ECS实例系统防火墙放通RDS的内网IP。ECS实例系统防火墙默认关闭，如果您开启过，需要放通RDS的内网IP。
-   域账号属于Domain Admins组（由于客户端主动加域需要高权限）。
-   域控服务器与DNS是相同IP。
-   登录的阿里云账号为主账号。

**说明：** 当前仅面向特定客户开放该功能，若有需求，请通过[工单](https://workorder-intl.console.aliyun.com/#/ticket/createIndex)或客户经理申请。

Microsoft AD即Active Directory（活动目录），是微软提供的面向Windows Standard Server、Windows Enterprise Server以及Microsoft SQL Server等产品的目录服务。目录是一种分层结构，用于存储同一局域网络上对象的信息。例如，AD存储有关用户账号的信息，例如名称、密码、电话号码等，并允许同一局域网络上的其他授权用户访问此信息。

AD是Windows生态体系下的重要组成单元。诸多大型企业，会通过域控来实现统筹的集中式访问管理，是企业内部长期依赖的原生管理方式。在上述背景下，当您从自建环境迁移整体服务至云上或使用混合云架构时，往往也需要在云上体系中支持AD服务，以便于全局管理。具体至SQL Server数据库，作为微软生态体系下的重要一环，大型企业在搬迁上云时AD的支持成为最基础的要素。

基于上述情况，RDS SQL Server提供实例接入自建域功能，帮助您完善业务生态体系。

## 注意事项

开通该功能后，不再提供[SLA](http://terms.aliyun.com/legal-agreement/terms/suit_bu1_ali_cloud/suit_bu1_ali_cloud201910310944_35008.html)保障。

## Windows版本选择

域控服务器需要建立在Windows Server操作系统之上，ECS创建实例时，系统最低版本为Windows Server 2012R2，建议使用Windows Server 2016及以上版本，语言选择英文，下文我们将以Windows Server 2016为例指导您建立可供RDS使用的域控服务器。

## 流程说明

1.  [ECS实例系统配置域控服务器](#section_v9u_b9r_sri)
2.  [配置ECS实例安全组](#section_w3w_z00_bg4)
3.  [配置RDS实例](#section_ds5_cby_zmo)

## ECS实例系统配置域控服务器

1.  登录[ECS管理控制台](https://ecs.console.aliyun.com)。

2.  在左侧导航栏，单击**实例与镜像** \> **实例**。

3.  在顶部菜单栏左上角处，选择地域。

4.  在**实例列表**页面中，单击目标实例ID。

5.  远程登录ECS的Windows Server 2016系统。

6.  搜索**Server Manager**并打开。

7.  单击**Add roles and features**，进行如下设置。

    |页面名称|设置说明|
    |----|----|
    |**Installation Type**|保持默认设置。|
    |**Server Selection**|保持默认设置。|
    |**Server Roles**|    -   选中**Active Directory Domain Services**，并在弹出的对话框中单击**Add Features**。
    -   选中**DNS Server**，并在弹出的对话框中单击**Add Features**。如果提示您电脑不是固定IP，建议您修改电脑为固定IP，防止IP自动变更导致DNS服务器无法使用。
![Server Roles](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/4213729951/p113917.png) |
    |**Features**|保持默认设置。|
    |**AD DS**|保持默认设置。|
    |**DNS Server**|保持默认设置。|
    |**Confirmation**|单击**Install**进行安装。|

8.  等待安装完成后，单击**Close**关闭页面。

9.  在左侧导航栏单击**AD DS**，然后在右上方单击**More**。

    ![More](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/5213729951/p113918.png)

10. 单击**Promote this server to a domain...**，进行如下设置。

    ![Promote](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/5213729951/p113919.png)

    |页面名称|设置说明|
    |----|----|
    |**Deployment Configuration**|选择**Add a new forest**，设置域名。![new forest](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/5213729951/p113920.png) |
    |**Domain Controller Options**|设置恢复模式密码。![恢复模式密码](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/5213729951/p113921.png) |
    |**DNS Options**|取消**Create DNS delegation**选项的**√**。![取消选项](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/5213729951/p113922.png) |
    |**Additional Options**|保持默认设置。|
    |**Paths**|保持默认设置。|
    |**Review Options**|保持默认设置。|
    |**Prerequisites Check**|单击**Install**进行安装。 **说明：** 安装完成后系统会重启。 |

11. 等待系统重启，再次搜索**Server Manager**并打开。

12. 在左侧导航栏单击**AD DS**，然后在右侧目标域控服务器上单击鼠标右键，选择**Active Directory Users and Computers**，进入AD用户管理模块。

    ![ad用户管理](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/5213729951/p113923.png)

13. 在**testdomain.net** \> **Users**上单击鼠标右键，选择**New** \> **User**。

    ![创建新用户](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/5213729951/p113924.png)

14. 设置登录的用户名称，然后单击**Next**。

    ![用户名](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/5213729951/p113925.png)

15. 设置登录密码，并设置密码永不过期，然后单击**Next**及**Finish**完成创建。

    ![设置密码](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/5213729951/p113926.png)

16. 双击新创建的用户，将该用户加入Domain Admins管理员组。

    ![加入管理员组](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/5213729951/p113927.png)

    ![添加成功](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/5213729951/p113928.png)


## 配置ECS实例安全组

1.  登录[ECS管理控制台](https://ecs.console.aliyun.com)。

2.  在左侧导航栏，单击**实例与镜像** \> **实例**。

3.  在顶部菜单栏左上角处，选择地域。

4.  在**实例列表**页面中，单击目标实例ID。

5.  在左侧导航栏单击**本实例安全组**，然后在右侧单击**配置规则**。

    **说明：** 域控服务器需要开放较多端口，因此不建议和其他ECS实例共享安全组，建议创建单独的安全组使用。

6.  在**入方向**页签内单击**手动添加**，允许如下端口访问ECS实例。

    ![放通RDS访问ECS](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/5213729951/p116505.png)

    |协议类型|端口范围|说明|
    |----|----|--|
    |TCP|88|Kerberos认证协议端口。|
    |TCP|135|远程过程调用协议（RPC）端口。|
    |TCP/UDP|389|轻型目录访问协议（LDAP）端口。|
    |TCP|445|通用互联网文档系统协议（CIFS）端口。|
    |TCP|3268|Global Catalog端口。|
    |TCP/UDP|53|DNS端口。|
    |TCP|49152~65535|连接的默认动态端口范围。输入格式为：49152/65535。|


## 配置RDS实例

1.  登录[RDS管理控制台](https://rds.console.aliyun.com/)。

2.  在左侧单击**实例列表**，然后在上方选择实例所在地域。

    ![选择地域](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/3074469951/p36543.png)

3.  找到目标实例，单击实例ID。

4.  在左侧导航栏单击**账号管理**。

5.  单击**AD域服务信息**页签，然后单击**配置AD域服务**。

    ![配置AD域服务](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/5213729951/p120531.png)

6.  设置如下参数，并选中**我已阅读并知晓配置AD域服务对《RDS 服务等级协议》的影响。**。

    **警告：** 开通AD域功能后，不再提供[SLA](http://terms.aliyun.com/legal-agreement/terms/suit_bu1_ali_cloud/suit_bu1_ali_cloud201910310944_35008.html)保障。

    ![加域](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/6213729951/p120541.png)

    |参数|说明|
    |--|--|
    |**域名**|创建活动目录时（**Deployment Configuration**页面）指定的域名，例如本文设置的是testdomian.net。|
    |**目录IP地址**|域控服务器所在ECS的IP，可以在ECS中使用ipconfig获取，也可以在阿里云ECS控制台中查看。![查看私网IP](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/6213729951/p120538.png) |
    |**域账号**|之前创建的用户名。|
    |**域密码**|用户名对应的密码。|

7.  单击**确定**，等待域操作完成。

    ![添加完成](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/6213729951/p120680.png)


## 常见问题

RDS使用什么权限用户加入域？如何控制其权限？

建议您使用域管理员权限的账号让RDS加入域，如果不希望使用域管理员权限，可以按照下面方法使用最小权限，但是使用最小权限账号退出域时，需要在域控服务器中手动删除对应的计算机对象，否则将同一RDS再次加入本域时会报错。

1.  创建新用户并确认用户属于Domain Users组后，在**Computers** \> **Delegate Control...**页面添加刚才创建的新用户。

    ![控制权限1](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/6213729951/p114804.png)

    ![控制权限2](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/6213729951/p114805.png)

2.  在创建的用户上单击右键，选择**Create a custom task to delegate**，然后单击**Next**。
3.  选择**Only the following objects in the folder**，按下图所示进行选中，然后单击**Next**。

    ![控制权限3](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/6213729951/p114823.png)

4.  按下图所示进行选中，然后单击**Next**直至完成。

    ![控制权限4](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/6213729951/p114824.png)


