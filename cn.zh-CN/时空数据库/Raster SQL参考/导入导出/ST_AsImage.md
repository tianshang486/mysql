# ST\_AsImage

将栅格对象转化为影像格式二进制流。

## 语法

```
bytea ST_AsImage(raster raster_obj,
        box extent,
        integer pyramidLevel default 0,
        cstring bands default '',
        cstring format default 'PNG',
        cstring option default '');
```

## 参数

|参数名称|描述|
|:---|:-|
|raster\_obj|需要计算的raster对象。|
|extent|影像的范围，默认使用地理坐标系统。|
|pyramidLevel|影像金字塔层级，从0开始，默认值为0。|
|bands|需要获取的波段列表，从0开始，用`'0-2'`或者`‘1,2,3’`这种形式表示。默认为空。JPEG为1或3，PNG为1、2、3或4。默认使用前三个波段。|
|format|输出影像格式，取值如下：-   PNG
-   JPEG |
|option|JSON字符串类型的转换选项。|

option参数说明如下。

|参数名称|描述|类型|默认值|说明|
|----|--|--|---|--|
|nodata|是否使用nodata值。|bool|false|-   true：需要处理nodata值。
-   false：nodata值作为普通值处理。 |
|nodataValue|nodata值。|integer|0|当nodata=true时，需为nodata设置参数值。|
|rast\_coord|传入的box是否为像元坐标。|bool|false|如果是像元坐标，横坐标x表示像元的列号（起始为0），纵坐标y表示像元的行号（起始为0）。|
|strength|是否进行增强。|string|none|显示增强的方式，取值：-   none：不进行增强。
-   stats：使用统计值进行拉伸。 |
|quality|压缩质量。|integer|75|压缩质量，取值为1~100。|

## 描述

-   函数将返回一个bytea表示的影像格式。
-   默认的裁剪缓存为100 MB，代表最多只能裁剪出100 MB大小的结果数据，如果需要调整返回结果大小，可使用参数**ganos.raster.clip\_max\_buffer\_size**设置缓存的大小。
-   波段数量说明如下：
    -   1：表示灰度影像。
    -   2：表示灰度和Alpha波段。
    -   3：表示R波段、G波段和B波段。
    -   4：表示R波段、G波段、B波段和Alpha波段。

## 示例

```
--使用裁剪范围。
SELECT ST_AsImage(raster_obj, 
                  '(-180,-90), (0,0)'::Box) 
FROM raster_table    
WHERE id=1;

--指定金字塔层级。
SELECT ST_AsImage(raster_obj, 
                  '(-180,-90), (0,0)'::Box,
                 1) 
FROM raster_table    
WHERE id=1;

--指定波段使用裁剪范围。
SELECT ST_AsImage(raster_obj, 
                  '(-180,-90), (0,0)'::Box,
                 1,
                 '0-2') 
FROM raster_table    
WHERE id=1;

--指定压缩格式。
SELECT ST_AsImage(raster_obj, 
                  '(-180,-90), (0,0)'::Box,
                 1,
                 '0-2',
                 'PNG') 
FROM raster_table    
WHERE id=1;

--使用统计值拉伸。
SELECT ST_AsImage(rast, 
                  '(-180,-90), (0,0)'::Box, 
                  0, 
                  '',
                  'PNG', 
                  '{"nodata":"false", "nodatavalue":"0","rast_coord":"false", "strength":"stats", "quality":"75"}')
FROM raster_table    
WHERE id=1;

--指定象元坐标裁剪并使用统计值拉伸。
SELECT ST_AsImage(rast, 
                  '(0,0), (200,100)'::Box, 
                  0, 
                  '',
                  'PNG', 
                  '{"nodata":"false", "nodatavalue":"0","rast_coord":"true", "strength":"stats", "quality":"75"}')
FROM raster_table    
WHERE id=1;
```

