# 位图功能扩展（varbitx）

社区版PostgreSQL内置的varbit插件仅支持的比较简单的BIT类型操作函数，阿里云RDS PostgreSQL对varbit插件进行了扩展，支持更多的BIT操作，可以覆盖更多应用场景，例如实时用户画像推荐系统、门禁广告系统、购票系统等。

RDS PostgreSQL版本如下：

-   PostgreSQL 11
-   PostgreSQL 10

## 函数说明

|函数|说明|
|--|--|
|`get_bit (varbit a, int b, int c) returns varbit`|从指定位置b开始获取c个BIT位，返回varbit。例如： get\_bit\('111110000011', 3, 5\) 返回11000。 |
|`set_bit_array (varbit a, int b, int c, int[] d) returns varbit`|将下标位置数组d对应的BIT位设置为b（0或1），超出原始长度的部分填充c（0或1）。例如： set\_bit\_array\('111100001111', 0, 1, array\[1,15\]\)返回 1011000011111110。 |
|`bit_count (varbit a, int b, int c, int d) returns int`|从第c位开始，统计d个BIT位中有多少个b（0或1），如果超出长度，则只计算已经存在的。 例如：bit\_count\('1111000011110000', 1, 5, 4\)返回1（0001）。 |
|`bit_count (varbit a, int b) returns int`|统计b（1或0）的个数。 例如：bit\_count\('1111000011110000', 1\)返回8。 |
|`bit_fill (int a, int b) returns varbit`|填充b长度的a（0或1）。例如：bit\_fill\(0,10\)返回 0000000000。 |
|`bit_rand (int a, int b, float c) returns varbit`|填充a长度的随机BIT，并指定b（0或1）的随机比例c。例如：bit\_rand\(10, 1, 0.3\)可能返回0101000001。 |
|`bit_posite (varbit a, int b, boolean c) returns int[]`|返回b（0或1）的下标位置数组，下标从0开始计数，c为true时正向返回，c为false时反向返回。例如：bit\_posite \('11110010011', 1, true\)返回 \[0,1,2,3,6,9,10\]，bit\_posite \('11110010011', 1, false\)返回 \[10,9,6,3,2,1,0\]。 |
|`bit_posite (varbit a, int b, int c, boolean d) returns int[]`|返回b（0或1）的下标位置数组，返回c个为止，下标从0开始计数，d为true时正向返回，d为false时反向返回。例如：bit\_posite \('11110010011', 1, 3, true\)返回 \[0,1,2\]，bit\_posite \('11110010011', 1, 3, false\)返回 \[10,9,6\]。 |
|`get_bit_array (varbit a, int b, int c, int d) returns int[]`|从b位置开始获取c个BIT位，返回d（0或1）的下标位置数组。例如： get\_bit\_array\('111110000011', 3, 5, 1\)返回11000的下标array\[3,4\]。 |
|`get_bit_array (varbit a, int b, int[] c) returns int[]`|查询指定下标位置数组c对应的BIT位为b（0或1）的，返回下标位置数组，超出部分的下标不统计。例如： get\_bit\_array\('111110000011', 1, array\[1,5,6,7,10,11\]\)返回array\[1,10,11\]。 |
|`set_bit_array (varbit a, int b, int c, int[] d, int e) returns varbit`|将指定下标位置数组d对应的BIT位设置为b（0或1），设置e位即返回，超出原始长度的部分填充c（0或1）。例如：set\_bit\_array\('111100001111', 1, 0, array\[4,5,6,7\], 2\)返回111111001111（设置为1，超出补0，设置满2位即返回）。 |
|`set_bit_array_record (varbit a, int b, int c, int[] d) returns (varbit,int[])`|将指定下标位置数组d对应的BIT位设置为b（0或1），超出原始长度的部分填充c（0或1），返回设置后的varbit，同时返回此次操作中被设置为b的下标位置数组。例如： set\_bit\_array\_record\('111100001111', 0, 1, array\[1,15\]\)返回1011000011111110（设置为0，超出补1）同时返回array\[1,15\]。 |
|`set_bit_array_record (varbit a, int b, int c, int[] d, int e) returns (varbit,int[])`|将指定下标位置数组d对应的BIT位设置为b（0或1），超出原始长度的部分填充c（0或1），设置成功e位即返回，返回设置后的varbit，同时返回此次操作被设置为b的下标位置数组。例如：set\_bit\_array\_record\('111100001111', 1, 0, array\[1,4,5,6,7\], 2\)返回111111001111（设置为1，超出补0，设置成功2位即返回）同时返回array\[4,5\]（array\[1\]本身为1，未设置成功）。 |
|`bit_count_array (varbit a, int b, int[] c) returns int`|统计指定下标位置数组中0或1的个数。例如： bit\_count\_array\('1111000011110000', 1, array\[1,2,7,8\]\)返回3。 |

## 使用方法

-   创建插件

    ```
    CREATE EXTENSION varbitx;
    ```

-   删除插件

    ```
    DROP EXTENSION varbitx;
    ```

-   函数使用命令

    使用`select <函数>`即可，例如：

    -   bit\_count函数

        ```
        select bit_count('1111000011110000', 1, 5, 4);
        ```

        返回结果为：

        ```
         bit_count   
        -----------  
                 1  
        (1 row)  
        ```

    -   set\_bit\_array\_record函数

        ```
        select set_bit_array_record('111100001111', 1, 0, array[1,4,5,6,7], 2);
        ```

        返回结果为：

        ```
          set_bit_array_record    
        ------------------------  
         (111111001111,"{4,5}")  
        (1 row)
        ```

    具体函数及说明请参见[函数说明](#section_awr_lo4_nyj)。


