# Create a database on an ApsaraDB RDS for PostgreSQL instance

Before you start to use your ApsaraDB RDS for PostgreSQL instance, you must create databases on the RDS instance. This topic describes how to create a database on an ApsaraDB RDS for PostgreSQL instance.

## Terms

-   Instance: a virtualized database server, on which you can create and manage a number of databases.
-   Database: a set of data that is stored in an organized manner and can be shared by a number of users. A database provides the minimal redundancy and is independent of applications. In simple words, a database is a data warehouse that is used to store data.
-   Character set: a collection of letters, special characters, and encoding rules that are used in a database.

## Precautions

-   If the RDS instance uses standard or enhanced SSDs, you can create and manage databases in the ApsaraDB RDS console.
-   If the RDS instance uses local SSDs, you can create and manage databases by using SQL statements.
-   If you want to migrate data from an on-premises database to the RDS instance, you must create a database and an account on the RDS instance. The created database must have the same name as the on-premises database. The created account must have the same name as the account that is authorized to manage the on-premises database.

## Create a database for an RDS instance with standard or enhanced SSDs

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).

2.  In the left-side navigation pane, click **Instances**. In the top navigation bar, select the region where your RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find your RDS instance and click its ID.

4.  In the left-side navigation pane, click **Databases**.

5.  Click **Create Database**.

6.  Configure the following parameters.

    ![Create a database for an RDS instance with standard or enhanced SSDs](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/9250359951/p99288.png)

    |Parameter|Description|
    |---------|-----------|
    |**Database Name:**|    -   The name of the database can contain up to 64 characters.
    -   The name of the database can contain lowercase letters, digits, hyphens \(-\), and underscores \(\_\).
    -   The name of the database must start with a lowercase letter and end with a lowercase letter or digit. |
    |**Supported Character Sets:**|The character set that is supported by the database.|
    |**Collate**|The rule that is used to sort strings.|
    |**Ctype**|The type of character that is supported by the database.|
    |**Authorized Account:**|The owner of the database. The owner has all permissions on the database.|
    |**Description:**|The description of the database.|

7.  Click **Create**.


## Create a database for an RDS instance with local SSDs

1.  Log on to the [ApsaraDB RDS console](/intl.en-US/RDS PostgreSQL Database/Quick start/Connect to an ApsaraDB RDS for PostgreSQL instance.md).

2.  In the SQL window, execute the following statement to create a database:

    ```
    CREATE DATABASE name
     [ [ WITH ] [ OWNER [=] user_name ]
            [ TEMPLATE [=] template ]
            [ ENCODING [=] encoding ]
            [ LC_COLLATE [=] lc_collate ]
            [ LC_CTYPE [=] lc_ctype ]
            [ TABLESPACE [=] tablespace_name ]
            [ CONNECTION LIMIT [=] connlimit ] ]
    ```

    For example, if you want to create a database named test, execute the following statement:

    ```
    create database test;
    ```


## What to do next

Connect to the RDS instance. For more information, see [Connect to an ApsaraDB RDS for PostgreSQL instance](/intl.en-US/RDS PostgreSQL Database/Quick start/Connect to an ApsaraDB RDS for PostgreSQL instance.md).

