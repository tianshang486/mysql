# Change the time zone of an ApsaraDB RDS for PostgreSQL instance

This topic describes how to change the time zone of an ApsaraDB RDS for PostgreSQL instance.

The RDS instance uses standard or enhanced SSDs.

## Change the time zone

You can change the time zone only of an RDS instance that uses standard or enhanced SSDs. To change the time zone, log on to the ApsaraDB for RDS console and modify the **timezone** parameter on the **Parameters** page. For more information, see [Reconfigure parameters for an RDS PostgreSQL instance](/intl.en-US/RDS PostgreSQL Database/Instance/Reconfigure parameters for an RDS PostgreSQL instance.md).

![timezone](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/2722582061/p169398.png)

**Note:** If an RDS instance uses local SSDs, the **timezone** parameter is not supported.

## Query supported time zones

You can run the following command to query supported time zones:

```
select name,utc_offset from pg_timezone_names;
```

**Note:** For more information about the pg\_timezone\_names table, see [pg\_timezone\_names](https://www.postgresql.org/docs/12/view-pg-timezone-names.html).

![Query supported time zones](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/9676252061/p163755.png)

