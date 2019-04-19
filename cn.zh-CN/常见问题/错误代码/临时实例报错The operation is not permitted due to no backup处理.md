# 临时实例报错The operation is not permitted due to no backup处理 {#concept_186381 .concept}

## 错误信息 {#section_qom_tnp_cey .section}

在控制台创建临时实例报错如下：

``` {#codeblock_ggk_8sx_7x2}
The operation is not permitted due to no backup
```

## 错误原因 {#section_39z_52u_kha .section}

实例进行过覆盖性恢复后，RDS API会禁止在覆盖性恢复的时间到上一个备份时间之间的时间段内创建临时实例，即用户的覆盖性恢复的时间点到上一个备份集之间是做了限制的，不能再进行还原（即不能再创建临时实例）。

## 详细说明 {#section_b3o_dee_zp5 .section}

-   **场景一** 

    当前时间a，最近的一个备份集时间点b，b的上一个备份集时间点为c。

    用户在当前时间a，回滚数据到了时间点b；回滚后，在c到b时间点内是不能创建临时实例的；c时间点之前的创建是不受影响的。

-   **场景二** 

    当前时间a，最近的一个备份集时间点b，b的上一个备份集时间点为c。

    用户在b-a之间的某个时间点a1创建临时实例，并进行回滚到a1，b--a1之间是不能创建临时实例的，b时间点之前的创建是不受影响的。

-   **场景三** 

    当前时间a，最近的一个备份集时间点b，b的上一个备份集时间点为c。

    用户在c--b之间的某个时间点b1创建临时实例，并进行回滚到b1，c--b1之间是不能创建临时实例的，c时间点之前的创建是不受影响的。


