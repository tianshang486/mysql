# Out of resources when opening file './xxx.MYD' \(Errcode: 24\)错误处理 {#concept_185685 .concept}

## 错误信息 {#section_2m3_qqd_yi1 .section}

在使用RDS for MySQL时遇到如下错误：

``` {#codeblock_w0v_xz5_tjc}
Out of resources when opening file './xxx.MYD' (Errcode: 24)
```

## 错误原因 {#section_0vh_sem_lgr .section}

出现这个错误是因为RDS中打开的文件数超过了open\_files\_limit限制。

## 解决方案 {#section_gzb_ni0_jhs .section}

在RDS管理控制台的参数设置中修改参数**open\_files\_limit**，修改后需要重启实例才生效。

![open_files_limit](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8290/155548911144708_zh-CN.png)

**说明：** 参数**open\_files\_limit**默认值是65535，在RDS中取值范围是4000~65535。

