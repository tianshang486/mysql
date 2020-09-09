# ST\_BuildPyramid

为一个空间几何数据表创建矢量金字塔，加速数据显示。

## 语法

```
boolean ST_BuildPyramid(cstring table, cstring geom, cstring fid, cstring config)
```

## 参数

|参数名称|描述|
|:---|:-|
|table|空间几何表名。|
|geom|几何字段名。|
|fid|要素标识字段名。|
|config|创建金字塔的参数，JSON格式的字符串。|

config参数说明如下。

|参数名称|类型|默认值|说明|
|----|--|---|--|
|name|string|与table名称相同|金字塔的名称。|
|parallel|int|0|并行构建任务数，0表示并行最大化。|
|tileSize|int|1024|瓦片大小，取值需大于0且小于4096。|
|tileExtend|int|8|瓦片的外扩大小，取值需大于0。|
|maxLevel|int|16|金字塔的最大层级，取值为0~20。|
|buildRules|array\[object\]|null|构建规则，每个object中包含level和value两个值。|
|└level|array\[int\]|无|规则适用的层级数组。|
|└value|object|无|构建规则值。|
|└filter|string|无|过滤表达式，PostgreSQL的查询语法。|
|└attrFields|array\[string\]|无|mvt中的属性字段名称。|
|└merge|array\[string\]|无|对数据进行分组合并的过滤条件。|
|└cull|array\[string\]|无|对数据进行分组剔除的过滤条件。|

config示例：

```
{
   "name" : "hello",      
   "parallel": 0,         
   "tileSize": 1024,      
   "tileExtend": 8,       
   "maxLevel": 16,        
   "buildRules": [        
     {
       "level": [0,1,2],  
       "value": {
         "filter": "code!=0",               
         "attrFields": ["name","color"],    
         "merge":["code=1","code!=1"],      
         "cull" :["code=1","code!=1"]       
       }
     }
   ]
}
```

## 示例

```
--为空间几何表roads创建矢量金字塔。
select ST_BuildPyramid('roads', 'geom', 'id', '');
st_buildpyramid
----------
t
```

