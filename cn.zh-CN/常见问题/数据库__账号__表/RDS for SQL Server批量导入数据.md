# RDS for SQL Server批量导入数据 {#concept_266103 .concept}

RDS for SQL Server支持通过Bulk Insert批量导入数据，但存在一定限制。

**说明：** Bulk Insert会触发RDS for SQL Server 2008R2版本实例的一个Bug，因此需要在使用时将[开启CheckConstraints选项](https://docs.microsoft.com/en-us/previous-versions/sql/sql-server-2008-r2/ms186247(v=sql.105))。

## 通过BCP命令方式 {#section_6tq_euu_xq5 .section}

1.  生成XML格式文件，示例如下：

    ``` {#codeblock_di4_ea8_ut0}
    bcp jacky.dbo.my_bcp_test format nul /c /t"," /x /f "d:\tmp\my_bcp_test.xml"  /U jacky /P xxxx /S "xxx.sqlserver
    .rds.aliyuncs.com,3333"
    ```

2.  导入数据，示例如下：

    ``` {#codeblock_xj8_5zw_360}
    bcp jacky.dbo.my_bcp_test in "d:\tmp\my_test_data_file.txt" /f "d:\tmp\my_bcp_test.xml"  /q /k /h "CHECK_CONSTRAINTS"  /U jacky /P xxx /S "xxx.sqlserver.rds.aliyuncs.com,3333"
    ```


## 通过JDBC SQLBulkCopy方式 {#section_m2o_z5p_tb3 .section}

示例如下：

``` {#codeblock_esc_y4i_gz8}
SQLServerBulkCopyOptions copyOptions = new SQLServerBulkCopyOptions();
                        copyOptions.setCheckConstraints(true);
```

**说明：** 详情请参见[通过JDBC驱动程序使用大容量复制](https://msdn.microsoft.com/zh-cn/library/mt221490(v=sql.110).aspx?spm=a2c4g.11186623.2.14.4b887039rL38Y9)。

## 通过ADO.NET SQLBulkCopy方式 {#section_vio_4sj_hns .section}

将SqlBulkCopy指定为SqlBulkCopyOptions.CheckConstraints即可，示例如下：

``` {#codeblock_4o5_nmm_cks}
static void Main()
        {

            string srcConnString = "Data Source=(local);Integrated Security=true;Initial Catalog=testdb";
            string desConnString = "Data Source=****.sqlserver.rds.aliyuncs.com,3433;User ID=**;Password=**;Initial Catalog=testdb";

            SqlConnection srcConnection = new SqlConnection();
            SqlConnection desConnection = new SqlConnection();

            SqlCommand sqlcmd = new SqlCommand();
            SqlDataAdapter da = new SqlDataAdapter();
            DataTable dt = new DataTable();

            srcConnection.ConnectionString = srcConnString;
            desConnection.ConnectionString = desConnString;
            sqlcmd.Connection = srcConnection;

            sqlcmd.CommandText = @"SELECT top 1000000 [PersonType],[NameStyle],[Title],[FirstName],[MiddleName],[LastName],[Suffix],[EmailPromotion]
                             ,[AdditionalContactInfo],[Demographics],NULL as rowguid,[ModifiedDate] FROM [testdb].[dbo].[Person]";
            sqlcmd.CommandType = CommandType.Text;
            sqlcmd.Connection.Open();
            da.SelectCommand = sqlcmd;
            da.Fill(dt);


            using (SqlBulkCopy blkcpy = new SqlBulkCopy(desConnString, SqlBulkCopyOptions.CheckConstraints))
            //using (SqlBulkCopy blkcpy = new SqlBulkCopy(desConnString, SqlBulkCopyOptions.Default))
            {
                blkcpy.BatchSize = 2000;
                blkcpy.BulkCopyTimeout = 5000;
                blkcpy.SqlRowsCopied += new SqlRowsCopiedEventHandler(OnSqlRowsCopied);
                blkcpy.NotifyAfter = 2000;

                foreach (DataColumn dc in dt.Columns)
                {
                    blkcpy.ColumnMappings.Add(dc.ColumnName, dc.ColumnName);
                }

                try
                {
                    blkcpy.DestinationTableName = "Person";
                    blkcpy.WriteToServer(dt);
                }
                catch (Exception ex)
                {
                    Console.WriteLine(ex.Message);
                }
                finally
                {
                    sqlcmd.Clone();
                    srcConnection.Close();
                    desConnection.Close();

                }
            }

        }

        private static void OnSqlRowsCopied(
            object sender, SqlRowsCopiedEventArgs e)
        {
            Console.WriteLine("Copied {0} so far...", e.RowsCopied);
        }
```

