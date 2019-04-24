# DMS导出数据到CSV文件 {#concept_188051 .concept}

## 检查源数据 {#section_och_3kx_uf2 .section}

在DMS中，查询中文显示正常，如下图。

![检查源数据](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8414/155608865545292_zh-CN.png)

## 查看表的字符集 {#section_efv_d5c_b7i .section}

显示表的创建语句命令如下：

``` {#codeblock_wll_kj5_vkj}
show create table <表名>;
```

![查看表的字符集](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8414/155608865545295_zh-CN.png)

## 创建导出任务 {#section_ac4_o3c_sg5 .section}

1.  在DMS中，选择**数据方案** \> **导出**。
2.  选择**新增导出任务** \> **导出数据库**。

    ![创建导出任务](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8414/155608865645296_zh-CN.png)

3.  勾选需要导出的表，设置好文件类型、字符集等，单击**确定**。

    ![设置导出任务](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8414/155608865845297_zh-CN.png)


