# DTS预检查时出现schema存在性检查错误处理 {#concept_187533 .concept}

## 错误信息 {#section_lgd_gfh_hax .section}

使用DTS进行RDS的数据迁移时，在预检查时出现schema 存在性检查错误，如下图。

![schema存在性检查](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8426/155600498545179_zh-CN.jpg)

![schema存在性检查具体报错](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8426/155600498545181_zh-CN.png)

## 解决方案 {#section_7b4_y97_17u .section}

如错误提示所述，该错误是由于目标库不存在或不匹配导致的。您需要在目标RDS实例下先创建与源库同名（注意大小写）的目标库。注意事项如下：

-   库名由小写字母、数字、下划线、中划线组成，字母开头，字母或者数字结尾。
-   如果源库与目标库名称不一致，在DTS迁移过程中可以修改迁移的库名。
-   由于目标库还未创建或创建异常，该错误通常还会伴随出现目标库权限检查的错误提示，目标库配置完成后，该错误也会解决。错误信息如下。

    ![目标库权限检查](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8426/155600498545182_zh-CN.png)


