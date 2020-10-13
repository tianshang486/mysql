# View the supported time zones of an ApsaraDB RDS for PostgreSQL instance

This topic describes how to view the time zones that are supported by an ApsaraDB RDS for PostgreSQL instance.

You can log on to the ApsaraDB for RDS console and reconfigure the **timezone** parameter of your RDS instance on the **Parameters** page. For more information, see [Reconfigure parameters for an RDS PostgreSQL instance](/intl.en-US/RDS PostgreSQL Database/Instance/Reconfigure parameters for an RDS PostgreSQL instance.md).

## Procedure

Run the following command to view the supported time zones of your RDS instance:

```
select name,utc_offset from pg_timezone_names ;
```

**Note:** For more information about the pg\_timezone\_names table, see [pg\_timezone\_names](https://www.postgresql.org/docs/12/view-pg-timezone-names.html).

![View supported time zones](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/9676252061/p163755.png)

