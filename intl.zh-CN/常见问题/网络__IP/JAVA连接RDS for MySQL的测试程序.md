# JAVA连接RDS for MySQL的测试程序 {#concept_41741_zh .concept}

若您要连接云数据库MySQL版的测试程序，您可以选择以下任意一种方法：

-   通过阿里云SDK

    在使用Java开发RDS管理和连接时，您可以通过阿里云的SDK连接云数据库MySQL版的测试程序。您需要先安装JDK1.7及以上版本，然后通过maven安装阿里云的Java SDK。单击[这里](https://develop.aliyun.com/sdk/java?spm=5176.1980653.0.0.0lGtNy)，然后下载阿里云关系型数据库所对应的SDK。

-   通过MySQL客户端

    您可以使用MySQL Connector连接云数据库MySQL版的测试程序。单击[这里](http://dev.mysql.com/downloads/connector/j/)下载，将对应的Jar包引入到build path。

-   通过代码

    您可以通过代码连接云数据库MySQL版的测试程序，示例代码如下：

    ``` {#codeblock_5b2_1kn_twt .language-java}
        import java.sql.Connection;
        import java.sql.DriverManager;
        import java.sql.ResultSet;
        import java.sql.SQLException;
        import java.sql.Statement;
    
        public class mysqlconnection {
    
        public static void main(String[] args) {
    
        Connection conn = null;
               String sql;      
               String url = "jdbc:mysql://rdssoxxxxxxxxx.mysql.rds.aliyuncs.com:3306?zeroDateTimeBehavior=convertToNull&amp;"
                       + "user=michael&amp;password=password&amp;useUnicode=true&amp;characterEncoding=UTF8";
               try {
    
                   Class.forName("com.mysql.jdbc.Driver");            
                   conn = DriverManager.getConnection(url);
                   Statement stmt = conn.createStatement();
                  String  sqlusedb="use test_5";
    
                  int result1 = stmt.executeUpdate(sqlusedb);
    
                   sql = "create table teacher(NO char(20),name varchar(20),primary key(NO))";
                   int result = stmt.executeUpdate(sql);
                   if (result != -1) {
    
                       sql = "insert into teacher(NO,name) values('2016001','wangsan')";
                       result = stmt.executeUpdate(sql);
                       sql = "insert into teacher(NO,name) values('2016002','zhaosi')";
                       result = stmt.executeUpdate(sql);
                       sql = "select * from teacher";
                       ResultSet rs = stmt.executeQuery(sql);
                       System.out.println("学号\t姓名");
                       while (rs.next()) {
                           System.out
                                   .println(rs.getString(1) + "\t" + rs.getString(2));
                       }
                   }
               } catch (SQLException e) {
                   System.out.println("MySQL操作错误");
                   e.printStackTrace();
               } catch (Exception e) {
                   e.printStackTrace();
               } finally {
                   try {
        conn.close();
        } catch (SQLException e) {
        // TODO Auto-generated catch block
        e.printStackTrace();
        }
               }
    
        }
    
        }
    				
    ```


