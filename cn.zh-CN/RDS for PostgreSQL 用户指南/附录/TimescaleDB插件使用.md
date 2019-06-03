# TimescaleDB插件使用 {#concept_265491 .concept}

RDS for PostgreSQL基础版和高可用版实例新增TimescaleDB插件1.3.0版本，支持时序数据的自动分片、高效写入、检索、准实时聚合等。

目前RDS for PostgreSQL 10对外开放的是Open Source版本的TimescaleDB，由于License等问题，可能暂不支持一些高级特性，详情参见[TimescaleDB](https://www.timescale.com/products)。

## 前提条件 {#section_lcb_463_s1f .section}

2019年5月20日之后创建的实例可直接使用插件TimescaleDB插件1.3.0版本。2019年5月20日之前创建的实例可以重启实例后使用最新的TimescaleDB插件1.3.0版本。

**说明：** 如果重启后提示如下错误信息：

``` {#codeblock_sw9_nq2_omp}
ERROR:  could not access file "$libdir/timescaledb-0.8.0": No such file or directory
```

请在对应数据库执行如下SQL更新插件即可：

``` {#codeblock_eeh_lt3_vhw}
alter extension timescaledb update;
```

## 添加TimescaleDB插件 {#section_n3h_gqh_thb .section}

使用pgAdmin客户端[连接实例](../../../../cn.zh-CN/RDS for PostgreSQL 快速入门/连接实例.md#section_yfs_phg_wdb)，添加TimescaleDB，命令如下：

``` {#codeblock_hcx_rc9_3m9}
CREATE EXTENSION IF NOT EXISTS timescaledb CASCADE;
```

## 创建时序表 {#section_c42_fqh_thb .section}

1.  创建标准表conditions，示例如下：

    ``` {#codeblock_3x9_qrz_c06}
    CREATE TABLE conditions (
      time        TIMESTAMPTZ       NOT NULL,
      location    TEXT              NOT NULL,
      temperature DOUBLE PRECISION  NULL,
      humidity    DOUBLE PRECISION  NULL
    );
    ```

2.  创建时序表，示例如下：

    ``` {#codeblock_u7t_l3y_dja}
    SELECT create_hypertable('conditions', 'time');
    ```


**说明：** 详细命令说明请参见[Create a Hypertable](https://docs.timescale.com/v1.3/using-timescaledb/hypertables#create)。

## 高效写入 {#section_wmv_nrh_thb .section}

您可以使用标准SQL命令将数据插入超表（Hypertables），示例如下：

``` {#codeblock_iic_b3v_vpj}
INSERT INTO conditions(time, location, temperature, humidity)
  VALUES (NOW(), 'office', 70.0, 50.0);
```

您还可以一次将多行数据插入到超表中，示例如下：

``` {#codeblock_h9g_98x_xty}
INSERT INTO conditions
  VALUES
    (NOW(), 'office', 70.0, 50.0),
    (NOW(), 'basement', 66.5, 60.0),
    (NOW(), 'garage', 77.0, 65.2);
```

## 检索 {#section_npf_m5h_thb .section}

您可以使用高级SQL查询检索数据，示例如下：

``` {#codeblock_615_wlj_oel}
--过去3小时内，每15分钟采集一次数据，按时间和温度排序。
SELECT time_bucket('15 minutes', time) AS fifteen_min,
    location, COUNT(*),
    MAX(temperature) AS max_temp,
    MAX(humidity) AS max_hum
  FROM conditions
  WHERE time > NOW() - interval '3 hours'
  GROUP BY fifteen_min, location
  ORDER BY fifteen_min DESC, max_temp DESC;
```

![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/219313/155955557647336_zh-CN.png)

您可也使用固有的函数进行分析查询，示例如下：

``` {#codeblock_ugr_ing_843}
--均值查询（Median）
SELECT percentile_cont(0.5)
  WITHIN GROUP (ORDER BY temperature)
  FROM conditions;
```

![均值百分查询](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/219313/155955557647337_zh-CN.png)

``` {#codeblock_ez0_9vy_04m}
--移动平均数（Moving Average）
SELECT time, AVG(temperature) OVER(ORDER BY time
      ROWS BETWEEN 9 PRECEDING AND CURRENT ROW)
    AS smooth_temp
  FROM conditions
  WHERE location = 'garage' and time > NOW() - interval '1 day'
  ORDER BY time DESC;
```

![移动平均数](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/219313/155955557647338_zh-CN.png)

