# Access control

ApsaraDB for RDS implements multi-dimensional access control to ensure data security.

You can use one of the following methods to create an account on your RDS instance:

-   Create a standard account by using the ApsaraDB RDS console or API. Then, grant the read-only, read/write, DDL-only, or DML-only permissions on specific databases to the account. For more information, see [Create an account on an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Account/Create an account on an ApsaraDB RDS for MySQL instance.md).
-   If you require access control at fine-grained levels, such as the table, view, and field levels, you can create a privileged account by using the ApsaraDB RDS console or API. Then, you can use the privileged account to log on to your RDS instance and create standard accounts that are authorized to manage specific databases. The privileged account can grant permissions at fine-grained levels to standard accounts. For more information, see [Authorize accounts to manage tables, views, and fields](/intl.en-US/RDS MySQL Database/Account/Authorize accounts to manage tables, views, and fields.md).

## Whitelist-based access control

ApsaraDB RDS allows you to configure whitelists that are used to control access to your RDS instance. For more information, see [Configure a whitelist for an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Data security/Configure a whitelist for an ApsaraDB RDS for MySQL instance.md).

The default IP address whitelist contains only the 127.0.0.1 IP address. This indicates that your RDS instance denies access from all IP addresses over the Internet or an internal network. You can configure a whitelist on the **Data Security** page of the ApsaraDB RDS console. You can also configure a whitelist by using the ApsaraDB RDS API. After you update a whitelist, you do not need to restart your RDS instance. This avoids interruptions to your workloads.

