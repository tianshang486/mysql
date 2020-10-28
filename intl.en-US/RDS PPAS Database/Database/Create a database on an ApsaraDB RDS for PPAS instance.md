# Create a database on an ApsaraDB RDS for PPAS instance

Before you start to use ApsaraDB RDS, you must create databases and accounts on your RDS instance. This topic describes how to create a database on an ApsaraDB RDS for PPAS instance.

[Create an ApsaraDB RDS for PPAS instance](/intl.en-US/RDS PPAS Database/Quick start/Create an ApsaraDB RDS for PPAS instance.md)

## Terms

-   Instance: a virtualized database server, on which you can create and manage a number of databases.
-   Database: a set of data that is stored in an organized manner and can be shared by a number of users. A database provides the minimal redundancy and is independent of applications. In simple words, a database is a data warehouse that is used to store data.
-   Character set: a collection of letters, special characters, and encoding rules that are used in a database.

## Precautions

-   Databases on the same RDS instance share all of the resources that belong to the instance. You can create and manage a number of databases on your RDS instance by using SQL statements.
-   If you want to migrate data from an on-premises database to your RDS instance, you must create a database and an account on your RDS instance. The database and the account must have the same names as the on-premises database and its authorized account.

## Procedure

1.  Connect to your RDS instance. For more information, see [Connect to an ApsaraDB RDS for PPAS instance](/intl.en-US/RDS PPAS Database/Quick start/Connect to an ApsaraDB RDS for PPAS instance.md).

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


