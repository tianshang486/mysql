# JAVA连接RDS for SQL Server {#concept_266014 .concept}

## 前提条件 {#section_dne_mg1_bwl .section}

需要jdk1.7及以上版本，参考微软官方要求并[下载jar包](https://www.microsoft.com/zh-CN/download/details.aspx?spm=a2c4g.11186623.2.10.1d523515wbuV67&id=11774)。

## 工程代码 {#section_3gy_r1f_0kd .section}

使用sqljdbc42.jar导入到项目工程代码片段：

``` {#codeblock_vbt_41e_6tu}
 String userName = "user";  //默认用户名
 String userPwd = "pass321";   //密码
 String url="jdbc:sqlserver://rds.sqlserver.rds.aliyuncs.com:3433;DatabaseName=dbtest";
 java.sql.Connection  dbConn = DriverManager.getConnection(url, userName, userPwd);
 Object sta = dbConn.createStatement();
 String sql = "create table student"+ "     (id int , name varchar(10))";
 int row = ((Statement) sta).executeUpdate(sql);
 System.out.println("successfully");
```

