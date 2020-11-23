# Use the PL/Proxy plug-in for horizontal sharding

The PL/Proxy plug-in allows you to access your ApsaraDB RDS instance in CLUSTER or CONNECT mode.

Your RDS instance runs one of the following PostgreSQL versions:

-   PostgreSQL 12 \(with a minor engine version of 20200421 or later\)
-   PostgreSQL 11 \(with a minor engine version of 20200402 or later\)

**Note:** If you want to view the minor engine version, perform the following steps: Log on to the ApsaraDB RDS console, find your RDS instance and navigate to the **Basic Information** page. In the **Configuration Information** section of the page, check whether the **Upgrade Minor Version** button exists. If the button exists, you can click it to view and update the minor engine version. If the button does not exist, you are using the latest minor engine version. For more information, see [Upgrade the kernel version of an ApsaraDB RDS for PostgreSQL instance](/intl.en-US/RDS PostgreSQL Database/Instance/Upgrade the kernel version of an ApsaraDB RDS for PostgreSQL instance.md).

![Upgrade the minor PostgreSQL version](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/en-US/8618549951/p101917.png)

The PL/Proxy plug-in supports the following modes:

-   CLUSTER

    This mode supports horizontal sharding and SQL replication.

-   CONNECT

    This mode allows ApsaraDB RDS to route SQL requests to specified databases.


For more information about how to use the PL/Proxy plug-in, visit [PL/Proxy](https://plproxy.github.io/tutorial.html).

## Precautions

-   You can directly manage tables across RDS instances that reside in the same virtual private cloud \(VPC\).
-   An Elastic Compute Service \(ECS\) instance that resides in the same VPC as your RDS instance can serve as a proxy to redirect access requests for your RDS instance. This allows you to manage tables across RDS instances that reside in different VPCs.
-   The number of data nodes that are served by the proxy node must be 2 to the power of n.

## Test environment

Select an RDS instance as the proxy node and another two RDS instances as the data nodes. The following table provides details about the three RDS instances.

|IP address|Node type|Instance name|Username|
|----------|---------|-------------|--------|
|100.xx.xx.136|Proxy node|postgres|postgres|
|100.xx.xx.72|Data node|pl\_db0|postgres|
|11.xx.xx.9|Data node|pl\_db1|postgres|

## Create a PL/Proxy plug-in

Execute the following statement to create a PL/Proxy plug-in:

```
create extension plproxy
```

## Create a PL/Proxy cluster

**Note:** If you use the CONNECT mode, you can skip the operations that are described in this section.

1.  Create a PL/Proxy cluster and specify the names, IP addresses, and ports of the RDS instances that you want to connect as data nodes in the cluster. Example:

    ```
    postgres=# CREATE SERVER cluster_srv1 FOREIGN DATA WRAPPER plproxy
    postgres-# OPTIONS (
    postgres(#         connection_lifetime '1800',
    postgres(#         disable_binary '1',
    postgres(#         p0 'dbname=pl_db0 host=100.xxx.xxx.72 port=5678',
    postgres(#         p1 'dbname=pl_db1 host=11.xxx.xxx.9 port=5678'
    postgres(#         );
    CREATE SERVER
    ```

2.  Grant the permissions on the created PL/Proxy cluster to the postgres user. Example:

    ```
    postgres=# grant usage on FOREIGN server cluster_srv1 to postgres;
    GRANT 
    ```

3.  Create a user mapping. Example:

    ```
    postgres=> create user mapping for postgres server cluster_srv1 options (user 'postgres');
    CREATE USER MAPPING
    ```


## Create a test table

Create a test table named users on each data node. Example:

```
create table users(userid int, name text);
```

## Test the CLUSTER mode

To test horizontal sharding, perform the following steps:

1.  Create a function that is used to insert data on each data node. Example:

    ```
    pl_db0=> CREATE OR REPLACE FUNCTION insert_user(i_id int, i_name text)
    pl_db0-> RETURNS integer AS $$
    pl_db0$>        INSERT INTO users (userid, name) VALUES ($1,$2);
    pl_db0$>        SELECT 1;
    pl_db0$> $$ LANGUAGE SQL;
    CREATE FUNCTION
    
    pl_db1=> CREATE OR REPLACE FUNCTION insert_user(i_id int, i_name text)
    pl_db1-> RETURNS integer AS $$
    pl_db1$>        INSERT INTO users (userid, name) VALUES ($1,$2);
    pl_db1$>        SELECT 1;
    pl_db1$> $$ LANGUAGE SQL;
    CREATE FUNCTION
    ```

2.  Create a function that is used to insert data on the proxy node. This function has the same name as the function that is used to insert data on each data node. Example:

    ```
    postgres=> CREATE OR REPLACE FUNCTION insert_user(i_id int, i_name text)
    postgres-> RETURNS integer AS $$
    postgres$>     CLUSTER 'cluster_srv1';
    postgres$>     RUN ON ANY;
    postgres$> $$ LANGUAGE plproxy;
    CREATE FUNCTION
    ```

3.  Create a function that is used to read data on the proxy node. Example:

    ```
    postgres=> CREATE OR REPLACE FUNCTION get_user_name()
    postgres-> RETURNS TABLE(userid int, name text) AS $$
    postgres$>     CLUSTER 'cluster_srv1';
    postgres$>     RUN ON ALL ;
    postgres$> SELECT userid,name FROM users;
    postgres$> $$ LANGUAGE plproxy;
    CREATE FUNCTION
    ```

4.  Insert 10 test records on the proxy node. Example:

    ```
    SELECT insert_user(1001, 'Sven');
    SELECT insert_user(1002, 'Marko');
    SELECT insert_user(1003, 'Steve');
    SELECT insert_user(1004, 'lottu');
    SELECT insert_user(1005, 'rax');
    SELECT insert_user(1006, 'ak');
    SELECT insert_user(1007, 'jack');
    SELECT insert_user(1008, 'molica');
    SELECT insert_user(1009, 'pg');
    SELECT insert_user(1010, 'oracle');
    ```

5.  View the data on each data node. The function that is used to insert data contains the RUN ON ANY statement. This statement randomly inserts data into either data node. Therefore, you may find the following data on the two data nodes:

    ```
    pl_db0=> select * from users;
     userid |  name
    --------+--------
       1001 | Sven
       1003 | Steve
       1004 | lottu
       1005 | rax
       1006 | ak
       1007 | jack
       1008 | molica
       1009 | pg
    (8 rows)
    
    pl_db1=> select * from users;
     userid |  name
    --------+--------
       1002 | Marko
       1010 | oracle
    (2 rows)
    ```

    **Note:** The query results indicate that the 10 data records are unevenly distributed between the two data nodes.

6.  Invoke the function that is used to read data on the proxy node. This function contains the RUN ON ALL statement that reads data from both data nodes. Example:

    ```
    postgres=> SELECT USERID,NAME FROM GET_USER_NAME();
     userid |  name
    --------+--------
       1001 | Sven
       1003 | Steve
       1004 | lottu
       1005 | rax
       1006 | ak
       1007 | jack
       1008 | molica
       1009 | pg
       1002 | Marko
       1010 | oracle
    (10 rows)
    ```


To test SQL replication, perform the following steps:

1.  Create a function that is used to truncate the users table on each node. Example:

    ```
    pl_db0=> CREATE OR REPLACE FUNCTION trunc_user()
    pl_db0-> RETURNS integer AS $$
    pl_db0$>        truncate table users;
    pl_db0$>        SELECT 1;
    pl_db0$> $$ LANGUAGE SQL;
    CREATE FUNCTION
    
    pl_db1=> CREATE OR REPLACE FUNCTION trunc_user()
    pl_db1-> RETURNS integer AS $$
    pl_db1$>        truncate table users;
    pl_db1$>        SELECT 1;
    pl_db1$> $$ LANGUAGE SQL;
    CREATE FUNCTION
    
    postgres=> CREATE OR REPLACE FUNCTION trunc_user()
    postgres-> RETURNS SETOF integer AS $$
    postgres$>     CLUSTER 'cluster_srv1';
    postgres$>     RUN ON ALL;
    postgres$> $$ LANGUAGE plproxy;
    CREATE FUNCTION
    ```

2.  Invoke the function that is used to truncate data on the proxy node. Example:

    ```
    postgres=> SELECT TRUNC_USER();
     trunc_user
    ------------
              1
              1
    (2 rows)
    ```

3.  Create a function that is used to insert data on the proxy node. Example:

    ```
    postgres=> CREATE OR REPLACE FUNCTION insert_user_2(i_id int, i_name text)
    postgres-> RETURNS SETOF integer AS $$
    postgres$>     CLUSTER 'cluster_srv1';
    postgres$>     RUN ON ALL;
    postgres$> TARGET insert_user;
    postgres$> $$ LANGUAGE plproxy;
    CREATE FUNCTION
    ```

4.  Insert four test records into the proxy node. Example:

    ```
    SELECT insert_user_2(1004, 'lottu');
    SELECT insert_user_2(1005, 'rax');
    SELECT insert_user_2(1006, 'ak');
    SELECT insert_user_2(1007, 'jack');
    ```

5.  View the data on each data node. Example:

    ```
    pl_db0=> select * from users;
     userid | name
    --------+-------
       1004 | lottu
       1005 | rax
       1006 | ak
       1007 | jack
    (4 rows)
    
    pl_db1=> select * from users;
     userid | name
    --------+-------
       1004 | lottu
       1005 | rax
       1006 | ak
       1007 | jack
    (4 rows)
    ```

    **Note:** The data is the same on each data node. This indicates that SQL replication is successful.

6.  Query data on the proxy node. You need only to execute the RUN ON ANY statement that randomly reads data from either data node. Example:

    ```
    postgres=> CREATE OR REPLACE FUNCTION get_user_name_2()
    postgres-> RETURNS TABLE(userid int, name text) AS $$
    postgres$>     CLUSTER 'cluster_srv1';
    postgres$>     RUN ON ANY ;
    postgres$> SELECT userid,name FROM users;
    postgres$> $$ LANGUAGE plproxy;
    CREATE FUNCTION
    
    postgres=> SELECT USERID,NAME FROM GET_USER_NAME_2();
     userid | name
    --------+-------
       1004 | lottu
       1005 | rax
       1006 | ak
       1007 | jack
    (4 rows)
    ```


## Test the CONNECT mode

When you use the CONNECT mode, you can access other RDS instances from the proxy node. Examples:

```
postgres=> CREATE OR REPLACE FUNCTION get_user_name_3()
postgres-> RETURNS TABLE(userid int, name text) AS $$
postgres$>     CONNECT 'dbname=pl_db0 host=100.81.137.72 port=56789';
postgres$> SELECT userid,name FROM users;
postgres$> $$ LANGUAGE plproxy;
CREATE FUNCTION

postgres=> SELECT USERID,NAME FROM GET_USER_NAME_3();
 userid | name
--------+-------
   1004 | lottu
   1005 | rax
   1006 | ak
   1007 | jack
(4 rows)
```

