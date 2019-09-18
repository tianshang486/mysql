# 十分钟了解云数据库RDS {#concept_c2t_fvy_p2b .concept}

阿里云数据库RDS版包含有MySQL、SQL Server、PostgreSQL、PPAS和MariaDB TX，用户可以在几分钟内创建出适合自己应用场景的数据库实例，迅速投产，按需付费。本文我们将以MySQL为例，向大家展示如何点几下鼠标就生成业务所需的数据库。

开始动手实践之前我们先介绍一下阿里云数据库RDS for MySQL版的几个基本知识，便于您准确选择适用于您业务场景的MySQL配置。

## 基本概念 {#section_v87_dj4_5bh .section}

-   地域和可用区

    阿里云在国内外多个地域部署了数据中心，并提供多线BGP骨干网线路接入。请根据您以及目标用户所在的地理位置选择地域，从而提升用户访问速度。一般情况下RDS应该和ECS服务器选择在同一地域，这样您部署于ECS服务器中的应用和数据库之间的网络连接效率是最高的。

    可用区是指在同一地域内，拥有独立电力和网络的物理区域，实现故障隔离。在同一地域内多个可用区采用高速链路互通，您可以选择将RDS与应用软件的ECS创建在同一可用区或不同的可用区，因为同一地域的不同可用区之间没有实质性区别。同时，MySQL在特定地域提供了多可用区部署的选择，也就是说，高可用版的主节点和备节点分别位于不同的可用区，从而提供跨可用区的容灾高可用能力。

    ![选择可用区](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7771/156877174039535_zh-CN.png)

-   版本

    阿里云上的MySQL提供三种版本的实例：基础版、高可用版和三节点企业版（原金融版）。

    -   基础版：一般用于个人学习或开发测试。目前基础版只提供MySQL 5.7版本，采用单节点部署，性价比非常高。基础版采用计算节点与存储分离的实现方式，当计算节点宕机时MySQL服务不可用，但存储在云盘里的数据不会丢失。基础版的缺陷是可用性不高，适用于相对不重要的场景，所以不建议您在生产环境中使用基础版。
    -   高可用版：RDS MySQL高可用版采用一主一备的经典高可用架构，采用基于binlog的数据复制技术维护数据库的可用性和数据一致性。同时，高可用版在配置上采用物理服务器和本地SSD硬盘，提供最佳性能，满足业务生产环境的需求。
    -   三节点企业版（原金融版）：三节点企业版主要应用于金融、证券、保险等行业的核心数据库，这些行业对数据安全性、可用性要求非常高。三节点企业版采用一主两备架构，通过binlog日志多副本多级别复制，确保数据的强一致性，可提供金融级的数据可靠性和跨机房容灾能力。
    ![选择版本](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7771/156877174039536_zh-CN.png)

-   规格

    阿里云上MySQL实例有三种规格类型：通用型、独享型和独占型。

    通用型和独享型都是在一台物理服务器上划分多个资源隔离的区域，为不同用户提供MySQL数据库实例。他们的不同点在于：

    -   通用型对于CPU和存储空间采用了复用的技术。部署在同一台服务器上的所有MySQL实例会共享CPU和存储；
    -   独享型是多个数据库实例共享一台物理服务器，但资源隔离策略确保每个实例都可以独享所分配到的CPU、内存、I/O、存储。
    最高级别的是独占型，是指一个MySQL实例独占一台服务器，会获得最好的性能，当然价格也最贵。追求极致性能但对价格不敏感的客户一般会在重要业务系统采用独占型实例。

    ![选择规格](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7771/156877174039538_zh-CN.png)

    关于通用型和独享型实例的性能，我们以MySQL 5.6实例做了基准实测，可参见如下结果。

    ![通用型基准测试](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7771/156877174139539_zh-CN.png)

    ![独享型基准测试](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7771/156877174139541_zh-CN.png)

-   应用上云

    现有业务系统的数据库有可能运行在自己的机房、托管的IDC、VMware虚拟机、OpenStack私有云或在阿里云ECS云服务器上。阿里云数据传输服务DTS（Data Transmission Service）提供了多种数据迁移方案，可满足不同上云或迁云的业务需求，使您在不影响业务的情况下将数据库平滑迁移至云数据库RDS上。

    您可以实现MySQL数据库的结构迁移、全量迁移和增量迁移。另外，您也不用担心被云锁定，无法从阿里云迁回本地。RDS支持通过物理备份或逻辑备份的方式，将云上数据迁移到本地数据库。

    ![应用上云](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7771/156877174139542_zh-CN.png)


## 创建实例 {#section_7r2_2y7_06t .section}

通过上面的学习，相信您已经对阿里云上的MySQL具有了初步的认识，现在一定正跃跃欲试地想要实践体验吧？RDS具有非常简单易用的用户界面，下面，我们一起“鼠标点点，即刻开通”。

1.  进入[RDS购买页](https://rds-buy.aliyun.com/#/create/rds)。
2.  选择所希望的地域，建议RDS实例和ECS实例在同一地域。

    ![选择地域](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7771/156877174139545_zh-CN.png)

3.  选择数据库版本、系列，以及对应的存储类型和可用区。

    目前MySQL 5.7支持基础版、高可用版和三节点企业版。MySQL 5.6支持高可用版和三节点企业版。MySQL 5.5支持高可用版。

    ![选择系列版本](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7771/156877174139546_zh-CN.png)

4.  选择网络类型、实例规格、存储空间以及购买时长。

    网络类型默认是VPC，即专有网络。除非您是老客户已经在用经典网络，否则推荐使用VPC专有网络，组网比较灵活也更加安全。关于购买时长，我们推荐包年包月，毕竟数据库支撑业务系统不会经常释放资源，而且包年包月订购的时间越长折扣越好，可以帮助您的业务应用省好多钱。但如果您只是用于测试或学习，可以创建实例时在左上角切换到按量付费。

    ![选择网络类型时长](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7771/156877174139548_zh-CN.png)

5.  提交订单和付款。

    ![付款](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7771/156877174139549_zh-CN.png)


几分钟后，当您收到短信和邮件的通知时，RDS实例就创建成功了，可以在管理控制台上查看和使用。

![实例列表](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7771/156877174139551_zh-CN.png)

## 连接实例 {#section_ugq_qri_424 .section}

最后，您打算如何连接访问MySQL？如何管理云上的MySQL？当然相信您也是高手一定知道SQLyog、phpMyAdmin等独立管理工具。这些都没有问题，但更专业的用法，还是使用阿里云为数万研发人员量身打造的数据管理软件DMS。

DMS是一款用于访问云数据库的Web服务，支持MySQL、SQL Server、PostgreSQL、Redis和MongoDB等数据源。DMS提供了数据管理、对象管理、数据流转和实例管理等功能，使用方式也非常简单，让我们来看一看吧。

1.  登录云数据库RDS的[管理控制台](https://rds.console.aliyun.com/)。
2.  在页面左上角，选择实例所在的地域。
3.  找到目标实例，单击实例ID，进入基本信息页面。
4.  在右上角单击**登录数据库**跳转到DMS登录页面，具体功能请参见[DMS功能总览](https://help.aliyun.com/document_detail/47593.html)。

    ![DMS](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7771/156877174139558_zh-CN.png)


