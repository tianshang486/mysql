# ST\_DeletePyramid

删除矢量金字塔。

## 语法

```
boolean ST_DeletePyramid(cstring  name)
```

## 参数

|参数名称|描述|
|:---|:-|
|name|金字塔的名称。|

## 示例

```
--删除矢量数据的金字塔。
select ST_DeletePyramid('roads');
st_deletepyramid
----------
t
```

