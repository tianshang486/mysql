# Connect to an ApsaraDB RDS instance by using an application

This topic describes how to connect to an ApsaraDB RDS instance by using a Java, Python, or C application.

After you obtain the connection information about an RDS instance, you can use code to connect to the RDS instance. For more information ,see [View and change the internal and public endpoints and port numbers of an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Database connection/View and change the internal and public endpoints and port numbers of an ApsaraDB
         RDS for MySQL instance.md).

## Sample code

The following table describes the parameters in the sample code.

|Parameter|Description|
|---------|-----------|
|Host|The internal or public endpoint of the RDS instance.-   If the client runs on an Elastic Compute Service \(ECS\) instance that resides in the same region and has the same network type as the RDS instance, use the internal endpoint. For example, if the ECS and RDS instances reside in virtual private clouds \(VPCs\) in the China \(Hangzhou\) region, you can use the internal endpoint to establish a secure connection.
-   In other scenarios, use the public endpoint.

For more information about how to view the internal and public endpoints and port numbers of the RDS instance, see [View and change the internal and public endpoints and port numbers of an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Database connection/View and change the internal and public endpoints and port numbers of an ApsaraDB
         RDS for MySQL instance.md). |
|Port|The port number of the RDS instance. If you want to connect to the RDS instance over an internal network, enter the internal port number of the RDS instance. If you want to connect to the RDS instance over the Internet, enter the public port number of the RDS instance.|
|myDatabase|The name of the RDS instance.|
|myUsername|The username of the account that you use to connect to the RDS instance.|
|myPassword|The password of the account that you use to connect to the RDS instance.|

-   Java sample code

    ```
    import java.sql.Connection;
    import java.sql.DriverManager;
    import java.sql.ResultSet;
    import java.sql.Statement;
    
    public class DatabaseConnection
    {
        public static void main(String args[]) {
            String connectionUrl= "jdbc:mysql://<Host>:<Port>/<myDatabase>";    
    
            ResultSet resultSet;
    
            try (Connection connection=DriverManager.getConnection(connectionUrl,"<myUsername>","<myPassword>");  
                 Statement statement = connection.createStatement()) {
    
                String selectSql = "SELECT * FROM `courses`";            //Enter the SQL statement that you want to execute.
                resultSet = statement.executeQuery(selectSql);
    
                while (resultSet.next()) {
                    System.out.println(resultSet.getString("name"));
                }
            }
            catch (SQLException e) {
                e.printStackTrace();
            }
        }
    }
    ```

-   Python sample code

    ```
    import pymysql
    
    connection = pymysql.connect(host='<Host>',     
                           port=<Port>,
                           user='<myUsername>',
                           passwd='<myPassword>',
                           db='<myDatabase>')
    
    try:
        with connection.cursor() as cursor:
            sql = "SELECT * FROM `courses`"        //Enter the SQL statement that you want to execute.
            cursor.execute(sql)
            for result in cursor:
                 print(result)
    finally:
        connection.close()
    ```

-   C sample code:

    ```
    #include <stdio.h>
    #include <mysql.h>
    #include <string.h>
    
    void main(void)
    {
        MYSQL *t_mysql;
    
        MYSQL_RES       *res = NULL;
        MYSQL_ROW       row;
        char            *query_str = NULL;
        int             rc, i, fields;
        int             rows;
    
        char select[] = "select * from courses";    //Enter the SQL statement that you want to execute.
        t_mysql = mysql_init(NULL);
    
        if(NULL == t_mysql){
            printf("init failed\n");
        }
    
        if(NULL == mysql_real_connect(t_mysql, <Host>, <myUsername>, <myPassword>, <myDatabase>,
                <Port>, NULL, 0)){
            printf("connect failed\n");
        }
    
        if(mysql_real_query(t_mysql, select, strlen(select)) ! = 0){
            printf("select failed\n");
        }
    
        res = mysql_store_result(t_mysql);
        if (NULL == res) {
             printf("mysql_restore_result(): %s\n", mysql_error(t_mysql));
             return -1;
        }
    
        fields = mysql_num_fields(res);
        while ((row = mysql_fetch_row(res))) {
            for (i = 0; i < fields; i++) {
                printf("%s\t", row[i]);
            }
            printf("\n");
        }
        mysql_close(t_mysql);
    
    }
                        
    ```


