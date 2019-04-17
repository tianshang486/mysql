# 安装ThinkSNS网站调用RDS数据库提示OPERATION need to be executed set by ADMIN {#concept_185602 .concept}

## 错误信息 {#section_jv6_ndj_6gx .section}

在已经创建了数据库，以及授权操作账号的情况下，安装网站ThinkSNS调用阿里云RDS时，返回如下错误：

``` {#codeblock_hik_oft_xiy}
OPERATION need to be executed set by ADMIN
```

## 解决方案 {#section_di0_f0m_9ud .section}

找到安装包文件并进行备份，路径为ThinkSNS\_V4.1.170\_Beta\_Full\\ThinkSNS\_V4\_Beta\_Full\\install\\install.php，在542行左右，找到以下内容。

![install文件](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8277/155547884844659_zh-CN.jpg)

将上图中红框内的代码修改为：

``` {#codeblock_pr0_xuz_zaz}
mysql_select_db($db_config['db_name']);
```

