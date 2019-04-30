# RDS for MySQL备份文件下载工具 {#concept_183280 .concept}

## 功能说明 {#section_1eq_eis_zc7 .section}

自动下载RDS for MySQL的备份文件到本地，默认下载前一天的备份文件（时间范围可以自定义修改）。

## 使用系统 {#section_ytl_i44_jni .section}

Linux、Windows等支持Python 2.7运行环境的系统。

## 前提条件 {#section_0nz_5rd_9tm .section}

-   需要Python2.7环境，已安装RDS SDK。
-   工具要足够的执行权限。
-   工具所在的客户端要能访问RDS的公网地址。

## 工具下载 {#section_lsd_jqt_z6n .section}

[点击下载](http://aliyun_portal_storage.oss-cn-hangzhou.aliyuncs.com/help/rds/get_rds_backup.tar?spm=a2c4g.11186623.2.10.16ce2022wZZjJU&file=get_rds_backup.tar)

## 使用方法 {#section_k68_qmn_6tw .section}

运行get\_rds\_backup.py脚本，后边加上参数**RDS实例ID**、**key**、**key\_secret**、备份保存位置，参数之间用空格隔开。

**格式**

``` {#codeblock_xwr_xvx_5m9}
python get_rds_backup.py <RDS实例ID> <key> <key_secret> /mnt/
```

**示例**

``` {#codeblock_g2d_b6s_dhf}
python get_rds_backup.py rm-m5exxx LTAIPxxxxxxx Cd0xxxxxxx /mnt/
```

