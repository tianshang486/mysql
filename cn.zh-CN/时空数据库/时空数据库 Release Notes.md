# 时空数据库 Release Notes

本文介绍时空数据库（Ganos）的版本更新说明。

|小版本|说明|
|---|--|
|3.2|-   新特性
    -   新增矢量金字塔返回图片格式（基于流形式）功能，用于矢量数据的快速图形化显示。
    -   新增栅格数据类型JPEG2000压缩算法，支持16bit栅格数据压缩存储。
    -   新增ganos\_update函数，用`select ganos_update() ;`命令可以升级所有的Ganos插件到最新版本。
    -   新增Trajectory数据类型：
        -   支持原生时空索引。
        -   新增Gist索引支持索引轨迹类型，并提供六种不同维度的算子族以支持不同维度的分析需求。
        -   新增时空外包框类型BoxND，可用于时空范围表示以及存储轨迹。
        -   新增对应不同维度的相交（&&）、包含（@\>）、被包含（<@）算子。
        -   新增[ST\_ndIntersects](/cn.zh-CN/时空数据库/Trajectory SQL参考/时空关系判断/ST_{Z|T|2D|2DT|3D|3DT}Intersects.md)、[ST\_ndDWithin](/cn.zh-CN/时空数据库/Trajectory SQL参考/时空关系判断/ST_{2D|2DT|3D|3DT}DWithin.md)、[ST\_ndContains](/cn.zh-CN/时空数据库/Trajectory SQL参考/时空关系判断/ST_{T|2D|2DT|3D|3DT}Contains.md)、[ST\_ndWithin](/cn.zh-CN/时空数据库/Trajectory SQL参考/时空关系判断/ST_{T|2D|2DT|3D|3DT}Within.md)四类轨迹处理函数。
        -   对轨迹类型提供统计信息收集功能，以及根据统计信息预估扫描代价功能。
        -   提供新的索引方式TrajGist，提供更好的索引选择。
-   性能优化
    -   优化st\_dwithin距离查询，提升查询性能。
    -   优化时空范围查询，GIST索引二阶段查询优化，提升查询性能。
    -   矢量金字塔功能改进：
        -   支持任意srid坐标的源数据，支持3857和4326两种瓦片输出。
        -   新增pixelSize参数设置，对点数据进行聚合，减少瓦片的数量。
-   Bug修复
    -   修复轨迹数据类型时间相交错误问题。
    -   修复某些情况下更新Ganos Raster失败问题。
    -   修复Ganos二进制文件更新到新版本后可能出现崩溃的问题。
    -   修复用默认参数构建矢量金字塔点数据后，顶级瓦片数据量过大的问题。 |
|3.0|-   新特性
    -   新增支持具有SubSet的NetCDF数据类型数据，可按照指定的图层名称导入。
    -   新增支持栅格数据自定义元数据以及时序信息：
        -   新增[ST\_MetaItems](/cn.zh-CN/时空数据库/Raster SQL参考/属性的查询与更新/ST_MetaItems.md)函数，用于获取所有的自定义元数据项目名称
        -   修改[ST\_MetaData](/cn.zh-CN/时空数据库/Raster SQL参考/属性的查询与更新/ST_MetaData.md)函数， 用于获取自定义元数据项以及返回以JSON方式表达的元数据项。
        -   新增[ST\_SetMetaData](/cn.zh-CN/时空数据库/Raster SQL参考/属性的查询与更新/ST_SetMetaData.md)函数，用于设置元数据项。
        -   新增[ST\_BeginDateTime](/cn.zh-CN/时空数据库/Raster SQL参考/属性的查询与更新/ST_BeginDateTime.md)函数，用于获取栅格数据的起始时间。
        -   新增[ST\_EndDateTime](/cn.zh-CN/时空数据库/Raster SQL参考/属性的查询与更新/ST_EndDateTime.md)函数, 用于获取栅格数据的终止时间。
        -   新增[ST\_SetBeginDateTime](/cn.zh-CN/时空数据库/Raster SQL参考/属性的查询与更新/ST_SetBeginDateTime.md)函数，用于设置栅格数据的开始时间。
        -   新增[ST\_SetEndDateTime](/cn.zh-CN/时空数据库/Raster SQL参考/属性的查询与更新/ST_SetEndDateTime.md)函数，用于设置栅格数据的结束时间。
        -   新增[ST\_SetDateTime](/cn.zh-CN/时空数据库/Raster SQL参考/属性的查询与更新/ST_SetDateTime.md)函数，用于设置栅格数据的开始、结束时间以及波段获取时间。
    -   新增支持栅格数据返回基于流形式的图片格式：
        -   新增[ST\_AsImage](/cn.zh-CN/时空数据库/Raster SQL参考/导入导出/ST_AsImage.md)函数，用于获取基于流形式的图片格式。
        -   新增[ST\_AsPNG](/cn.zh-CN/时空数据库/Raster SQL参考/导入导出/ST_AsPNG.md)函数，用于获取基于流形式的PNG图片格式。
        -   新增[ST\_AsJPEG](/cn.zh-CN/时空数据库/Raster SQL参考/导入导出/ST_AsJPEG.md)函数，用于获取基于流形式的JPEG图片格式。
    -   新增支持空间网格数据类型以及操作运算：
        -   新增geomgrid数据类型。
        -   新增[ST\_AsText](/cn.zh-CN/时空数据库/GeomGrid SQL参考/输出/ST_AsText.md)函数，用于将网格数据类型转换为文本表示方式。
        -   新增[ST\_AsGeometry](/cn.zh-CN/时空数据库/GeomGrid SQL参考/输出/ST_AsGeometry.md)函数，用于将网格数据类型转换为几何数据类型。
        -   新增[ST\_AsBinary](/cn.zh-CN/时空数据库/GeomGrid SQL参考/输出/ST_AsBinary.md)函数，用于将网格数据类型转换为二进制数据类型。
        -   新增[ST\_AsBox](/cn.zh-CN/时空数据库/GeomGrid SQL参考/输出/ST_AsBox.md)函数，用于将网格数据量类型转换为BOX数据类型。
        -   新增[ST\_AsGrid](/cn.zh-CN/时空数据库/GeomGrid SQL参考/网格对象计算/ST_AsGrid.md)函数，用于计算几何数据类型所对应的几何网格数据。
        -   新增[ST\_GridFromText](/cn.zh-CN/时空数据库/GeomGrid SQL参考/输入/ST_GridFromText.md)函数， 用于将基于文本表示网格转换为几何网格数据类型。
        -   新增[ST\_GridFromBinary](/cn.zh-CN/时空数据库/GeomGrid SQL参考/输入/ST_GridFromBinary.md)函数，用于将基于二进制的表示的网格转换为几何网格数据类型。
        -   新增[ST\_Intersects](/cn.zh-CN/时空数据库/GeomGrid SQL参考/空间关系判断/ST_Intersects.md)函数，用于判断网格数据类型与几何数据类型是否相交。
        -   新增[ST\_Contains](/cn.zh-CN/时空数据库/GeomGrid SQL参考/空间关系判断/ST_Contains.md)函数，用于判断网格数据与网格数据、网格数据与几何数据是否是包含关系。
        -   新增[ST\_Within](/cn.zh-CN/时空数据库/GeomGrid SQL参考/空间关系判断/ST_Within.md)函数，用于判断网格数据与网格数据、网格数据与几何数据是否是被包含关系。
    -   新增支持矢量金字塔及快速显示的功能：
        -   新增[ST\_BuildPyramid](/cn.zh-CN/时空数据库/Geometry Pyramid SQL参考/创建/ST_BuildPyramid.md)函数，用于创建矢量金字塔。
        -   新增[ST\_DeletePyramid](/cn.zh-CN/时空数据库/Geometry Pyramid SQL参考/删除/ST_DeletePyramid.md)函数，用于删除矢量金字塔。
        -   新增[ST\_Tile](/cn.zh-CN/时空数据库/Geometry Pyramid SQL参考/访问/ST_Tile.md)函数，用于获取MVT格式的矢量瓦片数据。
-   Bug修复
    -   修复在某些情况下创建金字塔会出现内存耗尽的问题。
    -   修复移动对象无法创建“2000-01-01”时间点的问题。
    -   修复某些场景下移动对象使用ST\_Intersection返回子轨迹错误的问题。 |
|2.9|-   新特性
    -   新增支持COG（Cloud Optimize Geotiff）文件格式，支持读取COG文件格式中存储的金字塔信息。
    -   新增[ST\_AddZ](/cn.zh-CN/时空数据库/Raster SQL参考/像素值操作/ST_AddZ.md)函数，支持通过栅格数据的像素值为几何对象添加Z值。
    -   栅格对象空间范围信息获取增强，支持基于金字塔层级查询：
        -   新增[ST\_Extent](/cn.zh-CN/时空数据库/Raster SQL参考/属性的查询与更新/ST_Extent.md)函数，用于获得栅格对象的空间范围，以BOX形式返回。
        -   新增[ST\_Envelope](/cn.zh-CN/时空数据库/Raster SQL参考/属性的查询与更新/ST_Envelope.md)函数，用于获得栅格对象的空间范围，以几何对象形式返回。
        -   新增[ST\_ConvexHull](/cn.zh-CN/时空数据库/Raster SQL参考/属性的查询与更新/ST_ConvexHull.md)函数，用于获得栅格对象的空间范围，以几何对象形式返回。
        -   新增[ST\_Height](/cn.zh-CN/时空数据库/Raster SQL参考/属性的查询与更新/ST_Height.md)函数，用于获得栅格对象的像素高度。
        -   新增[ST\_Width](/cn.zh-CN/时空数据库/Raster SQL参考/属性的查询与更新/ST_Width.md)函数，用于获得栅格对象的像素宽度。
        -   修改[ST\_XMin](/cn.zh-CN/时空数据库/Raster SQL参考/属性的查询与更新/ST_XMin.md)函数，用于获得栅格对象的X最小值。
        -   修改[ST\_YMin](/cn.zh-CN/时空数据库/Raster SQL参考/属性的查询与更新/ST_YMin.md)函数，用于获得栅格对象的Y最小值。
        -   修改[ST\_XMax](/cn.zh-CN/时空数据库/Raster SQL参考/属性的查询与更新/ST_XMax.md)函数，用于获得栅格对象的X最大值。
        -   修改[ST\_YMax](/cn.zh-CN/时空数据库/Raster SQL参考/属性的查询与更新/ST_YMax.md)函数，用于获得栅格对象的Y最大值。
-   Bug修复
    -   修复外部栅格数据会使用1 x n分块导致性能局限性的问题，允许用户通过存储选项自定义分块的大小。
    -   修复ST\_Values函数在查询某些方向的线对象时结果与坐标排序不一致的问题。
    -   修复ST\_BestPyramidLevel函数在某些情况下会返回负数的问题。
    -   修复ST\_BuildPyramid函数在某些情况下会重复创建金字塔的问题。
    -   修复Truncate栅格表时未能清理对应的块表的问题。
    -   修复ST\_ExportTo函数对于CreateOption在某些情况下无效的问题。
    -   修复ST\_ClearChunks函数对于表名存在大小写时会出现错误的问题。
    -   修复外部金字塔在某些情况下无法创建overview的问题。
    -   修复具有外部金字塔的栅格对象无法创建内部金字塔的问题。
    -   修复具有NaN数值的栅格数据在计算统计信息时会导致结果不正确的问题。 |
|2.8|-   新特性
    -   栅格数据元数据访问接口增强：
        -   新增[ST\_XMin](/cn.zh-CN/时空数据库/Raster SQL参考/属性的查询与更新/ST_XMin.md)函数，用于获取栅格数据X方向最小值。
        -   新增[ST\_YMin](/cn.zh-CN/时空数据库/Raster SQL参考/属性的查询与更新/ST_YMin.md)函数，用于获取栅格数据Y方向最小值。
        -   新增[ST\_XMax](/cn.zh-CN/时空数据库/Raster SQL参考/属性的查询与更新/ST_XMax.md)函数，用于获取栅格数据X方向最大值。
        -   新增[ST\_YMax](/cn.zh-CN/时空数据库/Raster SQL参考/属性的查询与更新/ST_YMax.md)函数，用于获取栅格数据Y方向最大值。
        -   新增[ST\_ChunkHeight](/cn.zh-CN/时空数据库/Raster SQL参考/属性的查询与更新/ST_ChunkHeight.md)函数，用于获取栅格数据分块高度。
        -   新增[ST\_ChunkWidth](/cn.zh-CN/时空数据库/Raster SQL参考/属性的查询与更新/ST_ChunkWidth.md)函数，用于获取栅格数据分块宽度。
        -   新增[ST\_ChunkBands](/cn.zh-CN/时空数据库/Raster SQL参考/属性的查询与更新/ST_ChunkBands.md)函数，用于获取栅格数据分块波段数量。
    -   新增[ST\_SrFromEsriWkt](/cn.zh-CN/时空数据库/SpatialRef SQL参考/ST_SrFromEsriWkt.md)函数，用于支持Esri格式空间参考字符串转换为OGC格式空间参考字符串。
    -   新增栅格数据类型支持Zstd和Snappy压缩方式。
    -   新增点云数据类型支持二进制拷贝功能。
    -   新增支持PROJ\_LIB和GDAL\_DATA环境变量设置，同时部署相关数据。
-   Bug修复
    -   修复OSS路径非法导致数据库崩溃问题。
    -   修复部分栅格数据导入SRID与定义不一致的问题。 |
|2.7|-   新特性
    -   新增空间栅格对象的MD5操作函数，可以用于数据的一致性检查和去重等操作：
        -   新增[ST\_MD5Sum](/cn.zh-CN/时空数据库/Raster SQL参考/属性的查询与更新/ST_MD5Sum.md)函数，用于获取栅格对象的MD5码值。
        -   新增[ST\_SetMD5Sum](/cn.zh-CN/时空数据库/Raster SQL参考/属性的查询与更新/ST_SetMD5Sum.md)函数，用于设置栅格对象的MD5码值。
    -   新增空间栅格对象OSS认证方式操作函数：
        -   新增[ST\_AKId](/cn.zh-CN/时空数据库/Raster SQL参考/辅助函数/ST_AKId.md)函数，用于获取以OSS方式存储的栅格对象的AcessKey ID。
        -   新增[ST\_SetAccessKey](/cn.zh-CN/时空数据库/Raster SQL参考/辅助函数/ST_SetAccessKey.md)函数，用于设置以OSS方式存储的栅格对象的AcessKey ID和AcessKey Secret。
        -   新增[ST\_SetAKId](/cn.zh-CN/时空数据库/Raster SQL参考/辅助函数/ST_SetAKId.md)函数，用于设置以OSS方式存储的栅格对象的AcessKey ID。
        -   新增[ST\_SetAKSecret](/cn.zh-CN/时空数据库/Raster SQL参考/辅助函数/ST_SetAKSecret.md)函数，用于设置以OSS方式存储的栅格对象的AcessKey Secret。
    -   新增空间栅格元数据操作函数：
        -   新增[ST\_ScaleX](/cn.zh-CN/时空数据库/Raster SQL参考/属性的查询与更新/ST_ScaleX.md)函数，用于获取栅格对象在空间参考系下X方向像素宽度。
        -   新增[ST\_ScaleY](/cn.zh-CN/时空数据库/Raster SQL参考/属性的查询与更新/ST_ScaleY.md)函数，用于获取栅格对象在空间参考系下Y方向像素宽度。
        -   新增[ST\_SetScale](/cn.zh-CN/时空数据库/Raster SQL参考/属性的查询与更新/ST_SetScale.md)函数，用于设置栅格对象在空间参考系下像素宽度。
        -   新增[ST\_SkewX](/cn.zh-CN/时空数据库/Raster SQL参考/属性的查询与更新/ST_SkewX.md)函数，用于获取栅格对象在空间参考系下X方向旋转。
        -   新增[ST\_SkewY](/cn.zh-CN/时空数据库/Raster SQL参考/属性的查询与更新/ST_SkewY.md)函数，用于获取栅格对象在空间参考系下Y方向旋转。
        -   新增[ST\_SetSkew](/cn.zh-CN/时空数据库/Raster SQL参考/属性的查询与更新/ST_SetSkew.md)函数，用于设置栅格对象在空间参考系下旋转。
        -   新增[ST\_UpperLeftX](/cn.zh-CN/时空数据库/Raster SQL参考/属性的查询与更新/ST_UpperLeftX.md)函数，用于获取栅格对象在空间参考系下左上角点的X坐标。
        -   新增[ST\_UpperLeftY](/cn.zh-CN/时空数据库/Raster SQL参考/属性的查询与更新/ST_UpperLeftY.md)函数，用于获取栅格对象在空间参考系下左上角点的Y坐标。
        -   新增[ST\_SetUpperLeft](/cn.zh-CN/时空数据库/Raster SQL参考/属性的查询与更新/ST_SetUpperLeft.md)函数，用于获取栅格对象在空间参考系下左上角点坐标。
        -   新增[ST\_PixelWidth](/cn.zh-CN/时空数据库/Raster SQL参考/属性的查询与更新/ST_PixelWidth.md)函数，用于获取栅格对象在空间参考系下像素宽度。
        -   新增[ST\_PixelHeight](/cn.zh-CN/时空数据库/Raster SQL参考/属性的查询与更新/ST_PixelHeight.md)函数，用于获取栅格对象在空间参考系下像素高度。
-   Bug修复

修复由于聚集函数会导致扩展升级失败的问题。 |
|2.6|-   新特性

新增[ST\_Clip](/cn.zh-CN/时空数据库/Raster SQL参考/像素值操作/ST_Clip.md)函数，支持基于象元坐标进行裁剪。

-   Bug修复
    -   修复ST\_NearestApproachDistance函数名称不正确的问题。
    -   修复ST\_MosaicFrom函数在某些情况下崩溃的问题。 |

