# DTS迁移显示已完成的值超过总数的原因 {#concept_187515 .concept}

## 问题现象 {#section_me9_tif_7jb .section}

查看迁移详情，表的已完成行数超过总数。

![迁移详情](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8424/155600219745168_zh-CN.png)

## 原因 {#section_0d7_t6c_say .section}

这个总数是用MySQL预估的值，在迁移完成后会将总数调整为准确值。

