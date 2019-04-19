# Unknown MySQL server host错误处理 {#concept_186360 .concept}

## 错误信息 {#section_wxt_zs3_o3p .section}

ECS实例使用Linux系统连接RDS for MySQL实例时报错如下：

``` {#codeblock_u4v_260_93s}
Unknown MySQL server host
```

## 错误原因 {#section_92n_rfb_i3v .section}

查看ECS系统日志，发现是由于iptables开启导致域名解析的数据包被丢弃。查看系统日志有如下报错。

![ECS连接报错](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8383/155565520444918_zh-CN.jpg)

## 解决方案 {#section_cdg_lyt_0i4 .section}

根据内存实际情况来调整sysctl.conf文件内的参数**net.nf\_conntrack\_max**。示例如下：

``` {#codeblock_p4a_8iy_vls}
vim /etc/sysctl.conf    --编辑文件
net.nf_conntrack_max = 6550400    --调整参数值
sysctl -p    --更新配置
```

![net.nf_conntrack_max](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8383/155565520444921_zh-CN.jpg)

**说明：** 更新内核参数如果报错`error: "nf_conntrack_max" is an unknown key`，需加载ip\_conntrack模块，建议加入到/etc/rc.local启动项中。以上操作基于CentOS 6.5版本，其他低版本的参数是**net.ipv4.ip\_conntrack\_max**。

