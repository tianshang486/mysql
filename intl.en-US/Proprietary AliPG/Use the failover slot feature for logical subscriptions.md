# Use the failover slot feature for logical subscriptions

This topic describes the failover slot feature. This feature synchronizes all of the logical replication slots in your ApsaraDB RDS database system from the primary RDS instance to the secondary RDS instance.

The primary RDS instance runs PostgreSQL 11.

If you do not enable the failover slot feature, the logical replication slots in your database system cannot be automatically switched over to the new primary RDS instance in the event of a primary/secondary switchover. In this case, the logical subscriptions are disconnected. You must manually re-create the logical replication slots. The failover slot feature can synchronize the logical replication slots from the primary RDS instance to the secondary RDS instance. This ensures that the logical subscriptions remain connected.

**Note:** The failover slot feature supports only logical subscriptions. It does not support physical subscriptions.

You can enable the failover slot feature by setting the **rds\_failover\_slot\_mode** parameter. After the setting is complete, the value of this parameter immediately takes effect and you do not need to restart the primary RDS instance. Valid values:

-   sync: enables the failover slot feature in synchronous mode.
-   async: enables the failover slot feature in asynchronous mode.
-   off: disables the failover slot feature.

For more information about how to set this parameter, see [Reconfigure parameters for an RDS PostgreSQL instance](/intl.en-US/RDS PostgreSQL Database/Instance/Reconfigure parameters for an RDS PostgreSQL instance.md).

The following sections provide more information about the two modes.

## Synchronous mode

In most cases, the synchronous mode ensures that no data from logical subscriptions is lost after a primary/secondary switchover. However, data may still be lost in some unexpected cases.

For example, if the secondary RDS instance remains disconnected for a long period of time or is being re-created, the latency between the primary and secondary RDS instances is high. If you perform a primary/secondary switchover at this time, data from the logical subscriptions may be lost. The lost data includes the data that is lost during the primary/secondary switchover. The lost data also includes the data that is generated on the new primary RDS instance.

To avoid data losses, you can set the **rds\_priority\_replication\_force\_wait** parameter to **on**. The default value of this parameter is **off**. After the setting is complete, the new value of this parameter immediately takes effect and you do not need to restart the primary RDS instance. After you set this parameter to on, the primary RDS instance does not send data to the subscriber until the secondary RDS instance is reconnected or re-created. However, this reduces the availability of logical subscriptions. Therefore, we recommend that you do not set this parameter to on.

## Asynchronous mode

The asynchronous mode ensures that no data from logical subscriptions is lost after a primary/secondary switchover. However, duplicate data may be sent to the subscriber. This may cause inconsistent data.

If the inconsistent data affects your business, we recommend that you use the synchronous mode.

