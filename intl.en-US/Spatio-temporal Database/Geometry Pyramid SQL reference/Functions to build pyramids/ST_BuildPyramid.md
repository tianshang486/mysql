# ST\_BuildPyramid

This topic describes the ST\_BuildPyramid function, which builds a vector pyramid for a spatial geometry data table to expedite data display.

## Syntax

```
boolean ST_BuildPyramid(cstring table, cstring geom, cstring fid, cstring config)
```

## Parameters

|Parameter|Description|
|:--------|:----------|
|table|The name of the spatial geometry table for which you want to build a pyramid.|
|geom|The name of the geometry field.|
|fid|The name of the element ID field.|
|config|The fields that are used to build a pyramid. These fields are specified in a JSON-formatted string.|

The following table describes the fields in the config parameter.

|Field|Data type|Default value|Description|
|-----|---------|-------------|-----------|
|name|string|Same as the table name|The name of the pyramid.|
|parallel|int|0|The maximum number of tasks that can run in parallel to build the pyramid. The value 0 indicates that the maximum number is not limited.|
|tileSize|int|1024|The tile size of the pyramid. Valid values must be greater than 0 but less than 4096.|
|tileExtend|int|8|The tile extension size of the pyramid. Valid values must be greater than 0.|
|maxLevel|int|16|The maximum number of layers in the pyramid. Valid values: 0 to 20.|
|buildRules|array\[object\]|null|The rule based on which you want to build the pyramid. Each rule consists of two parts: level and value.|
|└level|array\[int\]|None|The pyramid layers to which the rule applies.|
|└value|object|None|The value of the rule.|
|└filter|string|None|The expression that is used to filter data in PostgreSQL.|
|└attrFields|array\[string\]|None|The name of the attribute field when the MVT format is used.|
|└merge|array\[string\]|None|The filter conditions that are used to add data records to a group.|
|└cull|array\[string\]|None|The filter conditions that are used to remove data records from a group.|

The following example shows how to configure the config parameter:

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
         "filter": "code! =0",               
         "attrFields": ["name","color"],    
         "merge":["code=1","code! =1"],      
         "cull" :["code=1","code! =1"]       
       }
     }
   ]
}
```

## Examples

```
--Create a pyramid for the spatial geometric data table named roads.
select ST_BuildPyramid('roads', 'geom', 'id', '');
st_buildpyramid
----------
t
```

