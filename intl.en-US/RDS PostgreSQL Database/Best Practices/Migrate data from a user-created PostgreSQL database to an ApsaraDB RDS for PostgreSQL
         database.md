# Migrate data from a user-created PostgreSQL database to an ApsaraDB RDS for PostgreSQL database

This topic describes two methods that are used to migrate data from a user-created PostgreSQL database to an ApsaraDB RDS for PostgreSQL database.

## Use Alibaba Cloud Data Transmission Service \(DTS\)

-   Benefits
    -   DTS provides a graphical user interface \(GUI\) that simplifies operations. This GUI can also direct you to technical support in the event of errors.
    -   DTS supports the migration of incremental data at the minimal downtime.
    -   DTS supports the migration of full data free of charge. However, you must pay for the migration of incremental data.
-   Drawbacks

    You cannot specify tables by uploading files.


For more information, see [Overview of data migration scenarios]().

## Use native PostgreSQL

If DTS cannot meet your business requirements, you can use native PostgreSQL to migrate data.

-   Benefits
    -   Native PostgreSQL ensures compatibility with the user-created PostgreSQL database and the ApsaraDB RDS for PostgreSQL database.
    -   Native PostgreSQL migrates data at high speeds.
    -   Native PostgreSQL allows you to specify schemas and databases. This way, you can migrate only the tables that you want to migrate.
-   Drawbacks
    -   Native PostgreSQL does not support the migration of incremental data. It only supports the migration of full data.
    -   Native PostgreSQL requires you to understand the technical basics of PostgreSQL and Linux.

For more information, see [Migrate an on-premises PostgreSQL database to ApsaraDB RDS PostgreSQL by using the psql command tool](/intl.en-US/RDS PostgreSQL Database/Data Migration/Migrate an on-premises PostgreSQL database to ApsaraDB RDS PostgreSQL by using the psql command tool.md).

