# 数组相似度计算（smlar）

smlar插件可以用来计算两个相同类型数组的相似度。

实例版本如下：

-   PostgreSQL 12（内核小版本20200421及以上）
-   PostgreSQL 11（内核小版本20200402及以上）

**说明：** 您可以在**基本信息**页面的**配置信息**区域查看是否有**升级内核小版本**按钮。如果有按钮，您可以单击按钮查看当前版本；如果没有按钮，表示已经是最新版。详情请参见[升级内核小版本](/cn.zh-CN/RDS PostgreSQL 数据库/实例/升级内核小版本.md)。

![pgsql升级内核](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/4919259951/p101917.png)

smlar插件提供多种函数计算两个相同类型数组的相似度，同时提供参数来控制相似度计算方法，目前支持所有内置的数据类型。

## 基本函数介绍

-   float4 smlar\(anyarray, anyarray\)

    计算两个相同数据类型数组的相似度。

-   float4 smlar\(anyarray, anyarray, bool useIntersect\)

    计算两个自定义复合类型（元素，权重）数组的相似度，复合类型如下：

    ```
    CREATE TYPE type_name AS (element_name anytype, weight_name FLOAT4);
    ```

    useIntersect为true时，计算过程只包含重叠元素的部分；为false时计算过程包含所有元素。

-   float4 smlar\( anyarray a, anyarray b, text formula \)

    计算两个相同数据类型数组的相似度，数组通过formula指定。

    formula的预定义变量说明如下：

    -   N.i：两个数组的共有元素的个数。
    -   N.a：数组a中不重复元素的个数。
    -   N.b：数组b中不重复元素的个数。
-   float4 set\_smlar\_limit\(float4\)

    设置参数smlar.threshold的值。

-   float4 show\_smlar\_limit\(\)

    查看参数smlar.threshold的值。

-   anyarray % anyarray

    如果两个数组的相似度大于参数smlar.threshold的值，返回true，否则返回false。

-   text\[\] tsvector2textarray\(tsvector\)

    转化tsvector类型为text。

-   anyarray array\_unique\(anyarray\)

    对数组中的元素排序，排序结果不包含重复元素。

-   float4 inarray\(anyarray, anyelement\)

    如果anyelement存在于anyarray中，返回1，否则返回0。

-   float4 inarray\(anyarray, anyelement, float4, float4\)

    如果anyelement存在于anyarray中，返回第3个参数，否则返回第4个参数。


相关参数说明和支持的数据类型请参见[smlar](https://github.com/jirutka/smlar)。

## 使用插件

-   连接实例后创建smlar插件，命令如下：

    ```
    testdb=> create extension smlar;
    ```

-   验证插件基本功能，示例如下：

    ```
    testdb=> SELECT smlar('{1,4,6}'::int[], '{5,4,6}' );
      smlar   
    ----------
     0.666667
    (1 row)
    testdb=> SELECT smlar('{1,4,6}'::int[], '{5,4,6}', 'N.i / sqrt(N.a * N.b)' );
      smlar   
    ----------
     0.666667
    (1 row)
    ```

-   卸载插件，命令如下：

    ```
    testdb=> drop extension smlar;
    ```


