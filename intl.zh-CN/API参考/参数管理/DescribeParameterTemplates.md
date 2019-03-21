# DescribeParameterTemplates {#doc_api_1104912 .reference}

调用DescribeParameterTemplates接口查看数据库参数模板。

该接口适用的实例版本如下：

-   MySQL 5.5/5.6/5.7
-   SQL Server 2008 R2
-   PostgreSQL 9.4/10.0
-   PPAS 9.3/10.0
-   MariaDB 10.3

## 调试 {#apiExplorer .section}

前往【[API Explorer](https://api.aliyun.com/#product=Rds&api=DescribeParameterTemplates)】在线调试，API Explorer 提供在线调用 API、动态生成 SDK Example 代码和快速检索接口等能力，能显著降低使用云 API 的难度，强烈推荐使用。

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|DescribeParameterTemplates|系统规定参数，取值：**DescribeParameterTemplates**。

 |
|Engine|String|是|MySQL|数据库类型，取值：

 -   **mysql**：MySQL数据库；
-   **mssql**：SQL Server数据库；
-   **PostgreSQL**：PostgreSQL数据库；
-   **PPAS**：PPAS数据库；
-   **MariaDB**：MariaDB数据库。

 |
|EngineVersion|String|是|5.6|数据库版本号，取值：

 -   MySQL数据库：**5.5/5.6/5.7**；
-   SQL Server数据库：**2008r2**；
-   PostgreSQL数据库：**9.4/10.0**；
-   PPAS数据库：**9.3/10.0**；
-   MariaDB数据库：**10.3**。

 |
|ClientToken|String|否|ETnLKlblzczshOTUbOCzxxxxxxx|用于保证请求的幂等性，防止重复提交请求。由客户端生成该参数值，要保证在不同请求间唯一，最大值不超过64个ASCII字符，且该参数值中不能包含非ASCII字符。

 |
|AccessKeyId|String|否|LTAIfCxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |
|Category|String|否|basic|实例类别，取值：

 -   **basic**：基础版；
-   **standard**：标准版；
-   **enterprise**：金融版（仅支持中国站）。

 |

## 返回参数 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|Engine|String|MySQL|数据库类型。

 |
|EngineVersion|String|5.5|数据库版本号。

 |
|ParameterCount|String|56|参数个数。

 |
|Parameters| | |参数列表。

 |
|└ParameterName|String|auto\_increment\_increment|参数名。

 |
|└ParameterValue|String|1|参数默认值。

 |
|└ForceModify|String|true|参数是否可修改，取值：**true | false**

 |
|└ForceRestart|String|false|是否重启才生效，取值：**true | false**

 |
|└CheckingCode|String|\[10-3000\]|参数取值范围。

 |
|└ParameterDescription|String|determines the starting point for the AUTO\_INCREMENT column value.|参数描述。

 |
|RequestId|String|1AD222E9-E606-4A42-BF6D-8A4442913CEF|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=DescribeParameterTemplates
&Engine=MySQL
&EngineVersion=5.6
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<DescribeParameterTemplatesResponse>
  <Engine>mssql</Engine>
  <EngineVersion>2008r2</EngineVersion>
  <ParameterCount>1</ParameterCount>
  <Parameters>
    <TemplateRecord>
      <CheckingCode>[0-100]</CheckingCode>
      <ForceRestart>True</ForceRestart>
      <Factor>1</Factor>
      <ParameterDescription>此选项设置服务器范围内的默认填充因子值。提供填充因子是为了优化索引数据存储和性能。</ParameterDescription>
      <ParameterName>fill factor</ParameterName>
      <ParameterValue>0</ParameterValue>
      <ForceModify>True</ForceModify>
      <Unit>INT</Unit>
    </TemplateRecord>
  </Parameters>
  <RequestId>7B96585A-0FF2-4979-8FE5-7D147A29FDC0</RequestId>
</DescribeParameterTemplatesResponse>

```

`JSON` 格式

``` {#json_return_success_demo}
{
	"requestId":"9202A4F7-A7AE-44B8-B852-8C1824C19D52",
	"engine":"mysql",
	"parameterCount":"56",
	"parameters":[
		{
			"parameterValue":"1",
			"parameterDescription":"auto_increment_increment and auto_increment_offset are intended for use with master-to-master replication, and can be used to control the operation of AUTO_INCREMENT columns. Both variables have global and session values, and each can assume an integer value between 1 and 65,535 inclusive. Setting the value of either of these two variables to 0 causes its value to be set to 1 instead. Attempting to set the value of either of these two variables to an integer greater than 65,535 or less than 0 causes its value to be set to 65,535 instead. Attempting to set the value of auto_increment_increment or auto_increment_offset to a noninteger value gives rise to an error, and the actual value of the variable remains unchanged.",
			"forceRestart":"false",
			"checkingCode":"[1-65535]",
			"parameterName":"auto_increment_increment",
			"forceModify":"true"
		},
		{
			"parameterValue":"1",
			"parameterDescription":"determines the starting point for the AUTO_INCREMENT column value.",
			"forceRestart":"false",
			"checkingCode":"[1-65535]",
			"parameterName":"auto_increment_offset",
			"forceModify":"true"
		},
		{
			"parameterValue":"3000",
			"parameterDescription":"The number of outstanding connection requests MySQL can have.",
			"forceRestart":"true",
			"checkingCode":"[10-3000]",
			"parameterName":"back_log",
			"forceModify":"true"
		},
		{
			"parameterValue":"utf8",
			"parameterDescription":"The server's default character set. ",
			"forceRestart":"true",
			"checkingCode":"[utf8|latin1|gbk]",
			"parameterName":"character_set_server",
			"forceModify":"true"
		},
		{
			"parameterValue":"1",
			"parameterDescription":"0-Disables concurrent inserts;1-(Default) Enables concurrent insert for MyISAM tables that do not have holes;2-Enables concurrent inserts for all MyISAM tables, even those that have holes. For a table with a hole, new rows are inserted at the end of the table if it is in use by another thread. Otherwise, MySQL acquires a normal write lock and inserts the row into the hole.",
			"forceRestart":"false",
			"checkingCode":"[0|1|2]",
			"parameterName":"concurrent_insert",
			"forceModify":"true"
		},
		{
			"parameterValue":"10",
			"parameterDescription":"The number of seconds that the mysqld server waits for a connect packet before responding with Bad handshake. The default value is 10 seconds as of MySQL 5.1.23 and 5 seconds before that.Increasing the connect_timeout value might help if clients frequently encounter errors of the form Lost connection to MySQL server at 'XXX', system error: errno.",
			"forceRestart":"false",
			"checkingCode":"[1-3600]",
			"parameterName":"connect_timeout",
			"forceModify":"true"
		},
		{
			"parameterValue":"0",
			"parameterDescription":"The default mode value to use for the WEEK() function",
			"forceRestart":"false",
			"checkingCode":"[0-7]",
			"parameterName":"default_week_format",
			"forceModify":"true"
		},
		{
			"parameterValue":"100",
			"parameterDescription":"After inserting delayed_insert_limit delayed rows, the INSERT DELAYED handler thread checks whether there are any SELECT statements pending. If so, it permits them to execute before continuing to insert delayed rows",
			"forceRestart":"false",
			"checkingCode":"[1-4294967295]",
			"parameterName":"delayed_insert_limit",
			"forceModify":"true"
		},
		{
			"parameterValue":"300",
			"parameterDescription":"How many seconds an INSERT DELAYED handler thread should wait for INSERT statements before terminating.",
			"forceRestart":"false",
			"checkingCode":"[1-3600]",
			"parameterName":"delayed_insert_timeout",
			"forceModify":"true"
		},
		{
			"parameterValue":"1000",
			"parameterDescription":"This is a per-table limit on the number of rows to queue when handling INSERT DELAYED statements. If the queue becomes full, any client that issues an INSERT DELAYED statement waits until there is room in the queue again",
			"forceRestart":"false",
			"checkingCode":"[1-4294967295]",
			"parameterName":"delayed_queue_size",
			"forceModify":"true"
		},
		{
			"parameterValue":"ON",
			"parameterDescription":"This option applies only to MyISAM tables. It can have one of the following values to affect handling of the DELAY_KEY_WRITE table option that can be used in CREATE TABLE statements",
			"forceRestart":"false",
			"checkingCode":"[ON|OFF|ALL]",
			"parameterName":"delay_key_write",
			"forceModify":"true"
		},
		{
			"parameterValue":"4",
			"parameterDescription":"This variable indicates the number of digits by which to increase the scale of the result of division operations performed with the / operator. The default value is 4. The minimum and maximum values are 0 and 30, respectively. The following example illustrates the effect of increasing the default value.",
			"forceRestart":"false",
			"checkingCode":"[0-30]",
			"parameterName":"div_precision_increment",
			"forceModify":"true"
		},
		{
			"parameterValue":"4",
			"parameterDescription":"The minimum length of the word to be included in a FULLTEXT index.",
			"forceRestart":"true",
			"checkingCode":"[1-3600]",
			"parameterName":"ft_min_word_len",
			"forceModify":"true"
		},
		{
			"parameterValue":"20",
			"parameterDescription":"The number of top matches to use for full-text searches performed using WITH QUERY EXPANSION.",
			"forceRestart":"true",
			"checkingCode":"[0-1000]",
			"parameterName":"ft_query_expansion_limit",
			"forceModify":"true"
		},
		{
			"parameterValue":"1024",
			"parameterDescription":"The maximum permitted result length in bytes for the GROUP_CONCAT() function. The default is 1024,Unit:Byte",
			"forceRestart":"false",
			"checkingCode":"[4-1844674407370954752]",
			"parameterName":"group_concat_max_len",
			"forceModify":"true"
		},
		{
			"parameterValue":"1",
			"parameterDescription":"The locking mode to use for generating auto-increment values. The permissible values are 0, 1, or 2, for ",
			"forceRestart":"true",
			"checkingCode":"[0|1|2]",
			"parameterName":"innodb_autoinc_lock_mode",
			"forceModify":"true"
		},
		{
			"parameterValue":"500",
			"parameterDescription":"The number of threads that can enter InnoDB concurrently is determined by the innodb_thread_concurrency variable.",
			"forceRestart":"false",
			"checkingCode":"[100-1000]",
			"parameterName":"innodb_concurrency_tickets",
			"forceModify":"true"
		},
		{
			"parameterValue":"50",
			"parameterDescription":"The timeout in seconds an InnoDB transaction may wait for a row lock before giving up. The default value is 50 seconds. Unit:Second",
			"forceRestart":"false",
			"checkingCode":"[1-1073741824]",
			"parameterName":"innodb_lock_wait_timeout",
			"forceModify":"true"
		},
		{
			"parameterValue":"75",
			"parameterDescription":"This is an integer in the range from 0 to 100. The default value is 90 for the built-in InnoDB, 75 for InnoDB Plugin. The main thread in InnoDB tries to write pages from the buffer pool so that the percentage of dirty (not yet written) pages will not exceed this value.",
			"forceRestart":"false",
			"checkingCode":"[50-90]",
			"parameterName":"innodb_max_dirty_pages_pct",
			"forceModify":"true"
		},
		{
			"parameterValue":"37",
			"parameterDescription":"(InnoDB Plugin only) Specifies the approximate percentage of the InnoDB buffer pool used for the old block sublist. The range of values is 5 to 95. The default value is 37 (that is, 3/8 of the pool).",
			"forceRestart":"false",
			"checkingCode":"[5-95]",
			"parameterName":"innodb_old_blocks_pct",
			"forceModify":"true"
		},
		{
			"parameterValue":"0",
			"parameterDescription":"(InnoDB Plugin only) Specifies how long in milliseconds (ms) a block inserted into the old sublist must stay there after its first access before it can be moved to the new sublist. The default value is 0: A block inserted into the old sublist moves immediately to the new sublist the first time it is accessed, no matter how soon after insertion the access occurs. If the value is greater than 0, blocks remain in the old sublist until an access occurs at least that many ms after the first access.Unit:ms",
			"forceRestart":"false",
			"checkingCode":"[0-1000]",
			"parameterName":"innodb_old_blocks_time",
			"forceModify":"true"
		},
		{
			"parameterValue":"300",
			"parameterDescription":"This variable is relevant only if you use multiple InnoDB tablespaces. It specifies the maximum number of .ibd files that MySQL can keep open at one time. The minimum value is 10. The default value is 300.",
			"forceRestart":"true",
			"checkingCode":"[1-8192]",
			"parameterName":"innodb_open_files",
			"forceModify":"true"
		},
		{
			"parameterValue":"56",
			"parameterDescription":"(InnoDB Plugin only) Controls the sensitivity of linear read-ahead that InnoDB uses to prefetch pages into the buffer pool. If InnoDB reads at least innodb_read_ahead_threshold pages sequentially from an extent (64 pages), it initiates an asynchronous read for the entire following extent.",
			"forceRestart":"false",
			"checkingCode":"[0-64]",
			"parameterName":"innodb_read_ahead_threshold",
			"forceModify":"true"
		},
		{
			"parameterValue":"4",
			"parameterDescription":"(InnoDB Plugin only) The number of I/O threads for read operations in InnoDB. The default value is 4.",
			"forceRestart":"true",
			"checkingCode":"[1-64]",
			"parameterName":"innodb_read_io_threads",
			"forceModify":"true"
		},
		{
			"parameterValue":"OFF",
			"parameterDescription":"InnoDB rolls back only the last statement on a transaction timeout by default. If --innodb_rollback_on_timeout is specified, a transaction timeout causes InnoDB to abort and roll back the entire transaction (the same behavior as in MySQL 4.1). This variable was added in MySQL 5.1.15",
			"forceRestart":"true",
			"checkingCode":"[OFF|ON]",
			"parameterName":"innodb_rollback_on_timeout",
			"forceModify":"true"
		},
		{
			"parameterValue":"nulls_equal",
			"parameterDescription":"How the server treats NULL values when collecting statistics about the distribution of index values for InnoDB tables. This variable has three possible values, nulls_equal, nulls_unequal, and nulls_ignored. For nulls_equal, all NULL index values are considered equal and form a single value group that has a size equal to the number of NULL values. For nulls_unequal, NULL values are considered unequal, and each NULL forms a distinct value group of size 1. For nulls_ignored, NULL values are ignored.",
			"forceRestart":"false",
			"checkingCode":"[nulls_equal|nulls_unequal|nulls_ignored]",
			"parameterName":"innodb_stats_method",
			"forceModify":"true"
		},
		{
			"parameterValue":"OFF",
			"parameterDescription":"When this variable is enabled (which is the default, as before the variable was created), InnoDB updates statistics during metadata statements such as SHOW TABLE STATUS or SHOW INDEX, or when accessing the INFORMATION_SCHEMA tables TABLES or STATISTICS. (These updates are similar to what happens for ANALYZE TABLE.) When disabled, InnoDB does not update statistics during these operations. Disabling this variable can improve access speed for schemas that have a large number of tables or indexes. It can also improve the stability of execution plans for queries that involve InnoDB tables.",
			"forceRestart":"false",
			"checkingCode":"[ON|OFF]",
			"parameterName":"innodb_stats_on_metadata",
			"forceModify":"true"
		},
		{
			"parameterValue":"8",
			"parameterDescription":"(InnoDB Plugin only) The number of index pages to sample for index distribution statistics such as are calculated by ANALYZE TABLE. The default value is 8.",
			"forceRestart":"false",
			"checkingCode":"[1-4294967296]",
			"parameterName":"innodb_stats_sample_pages",
			"forceModify":"true"
		},
		{
			"parameterValue":"OFF",
			"parameterDescription":"(InnoDB Plugin only) Whether InnoDB returns errors rather than warnings for certain conditions. This is analogous to strict SQL mode. The default value is OFF. See InnoDB Strict Mode for a list of the conditions that are affected.",
			"forceRestart":"false",
			"checkingCode":"[ON|OFF]",
			"parameterName":"innodb_strict_mode",
			"forceModify":"true"
		},
		{
			"parameterValue":"0",
			"parameterDescription":"InnoDB tries to keep the number of operating system threads concurrently inside InnoDB less than or equal to the limit given by this variable. Once the number of threads reaches this limit, additional threads are placed into a wait state within a FIFO queue for execution.",
			"forceRestart":"false",
			"checkingCode":"[0-128]",
			"parameterName":"innodb_thread_concurrency",
			"forceModify":"true"
		},
		{
			"parameterValue":"10000",
			"parameterDescription":"How long InnoDB threads sleep before joining the InnoDB queue, in microseconds. The default value is 10,000. A value of 0 disables sleep.Unit:ms",
			"forceRestart":"false",
			"checkingCode":"[1-3600000]",
			"parameterName":"innodb_thread_sleep_delay",
			"forceModify":"true"
		},
		{
			"parameterValue":"4",
			"parameterDescription":"(InnoDB Plugin only) The number of I/O threads for write operations in InnoDB. The default value is 4.",
			"forceRestart":"true",
			"checkingCode":"[1-64]",
			"parameterName":"innodb_write_io_threads",
			"forceModify":"true"
		},
		{
			"parameterValue":"7200",
			"parameterDescription":"The number of seconds the server waits for activity on an interactive connection before closing it. An interactive client is defined as a client that uses the CLIENT_INTERACTIVE option to mysql_real_connect(). Unit:second.",
			"forceRestart":"false",
			"checkingCode":"[10-86400]",
			"parameterName":"interactive_timeout",
			"forceModify":"true"
		},
		{
			"parameterValue":"300",
			"parameterDescription":"This value controls the demotion of buffers from the hot sublist of a key cache to the warm sublist. Lower values cause demotion to happen more quickly. The minimum value is 100. The default value is 300.Unit:Second.",
			"forceRestart":"false",
			"checkingCode":"[100-4294967295]",
			"parameterName":"key_cache_age_threshold",
			"forceModify":"true"
		},
		{
			"parameterValue":"1024",
			"parameterDescription":"The size in bytes of blocks in the key cache. The default value is 1024.Unit:Byte.",
			"forceRestart":"false",
			"checkingCode":"[512-16384]",
			"parameterName":"key_cache_block_size",
			"forceModify":"true"
		},
		{
			"parameterValue":"100",
			"parameterDescription":"The division point between the hot and warm sublists of the key cache buffer list. The value is the percentage of the buffer list to use for the warm sublist. Permissible values range from 1 to 100. The default value is 100.",
			"forceRestart":"false",
			"checkingCode":"[1-100]",
			"parameterName":"key_cache_division_limit",
			"forceModify":"true"
		},
		{
			"parameterValue":"OFF",
			"parameterDescription":"Whether queries that do not use indexes are logged to the slow query log.",
			"forceRestart":"false",
			"checkingCode":"[ON|OFF]",
			"parameterName":"log_queries_not_using_indexes",
			"forceModify":"true"
		},
		{
			"parameterValue":"1",
			"parameterDescription":"If a query takes longer than this many seconds, the server increments the Slow_queries status variable. If the slow query log is enabled, the query is logged to the slow query log file;Unit:Second.",
			"forceRestart":"false",
			"checkingCode":"[0.5-10]",
			"parameterName":"long_query_time",
			"forceModify":"true"
		},
		{
			"parameterValue":"0",
			"parameterDescription":"If set to 1, all INSERT, UPDATE, DELETE, and LOCK TABLE WRITE statements wait until there is no pending SELECT or LOCK TABLE READ on the affected table. This affects only storage engines that use only table-level locking (such as MyISAM, MEMORY, and MERGE). This variable previously was named sql_low_priority_updates.",
			"forceRestart":"false",
			"checkingCode":"[0|1]",
			"parameterName":"low_priority_updates",
			"forceModify":"true"
		},
		{
			"parameterValue":"1073741824",
			"parameterDescription":"The maximum size of one packet or any generated/intermediate string,Unit:Byte",
			"forceRestart":"false",
			"checkingCode":"[16384-1073741824]",
			"parameterName":"max_allowed_packet",
			"forceModify":"true"
		},
		{
			"parameterValue":"20",
			"parameterDescription":"If more than this many successive connection requests from a host are interrupted without a successful connection, the server blocks that host from further connections. You can unblock blocked hosts by flushing the host cache.",
			"forceRestart":"false",
			"checkingCode":"[1-4096]",
			"parameterName":"max_connect_errors",
			"forceModify":"true"
		},
		{
			"parameterValue":"262144",
			"parameterDescription":"The size of the buffer that is allocated when sorting MyISAM indexes during a REPAIR TABLE or when creating indexes with CREATE INDEX or ALTER TABLE. ",
			"forceRestart":"false",
			"checkingCode":"[262144-16777216]",
			"parameterName":"myisam_sort_buffer_size",
			"forceModify":"true"
		},
		{
			"parameterValue":"30",
			"parameterDescription":"The number of seconds to wait for more data from a connection before aborting the read.",
			"forceRestart":"false",
			"checkingCode":"[1-31536000]",
			"parameterName":"net_read_timeout",
			"forceModify":"true"
		},
		{
			"parameterValue":"10",
			"parameterDescription":"If a read or write on a communication port is interrupted, retry this many times before giving up.",
			"forceRestart":"false",
			"checkingCode":"[1-4294967295]",
			"parameterName":"net_retry_count",
			"forceModify":"true"
		},
		{
			"parameterValue":"60",
			"parameterDescription":"The number of seconds to wait for a block to be written to a connection before aborting the write.",
			"forceRestart":"false",
			"checkingCode":"[1-31536000]",
			"parameterName":"net_write_timeout",
			"forceModify":"true"
		},
		{
			"parameterValue":"8192",
			"parameterDescription":"The allocation size of memory blocks that are allocated for objects created during statement parsing and execution. Unit:Byte",
			"forceRestart":"false",
			"checkingCode":"[1024-16384]",
			"parameterName":"query_alloc_block_size",
			"forceModify":"true"
		},
		{
			"parameterValue":"1048576",
			"parameterDescription":"Don't cache results that are larger than this number of bytes. The default value is 1MB. ",
			"forceRestart":"false",
			"checkingCode":"[1-1048576]",
			"parameterName":"query_cache_limit",
			"forceModify":"true"
		},
		{
			"parameterValue":"0",
			"parameterDescription":"The amount of memory allocated for caching query results. The default value is 0, which disables the query cache. The permissible values are multiples of 1024; other values are rounded down to the nearest multiple. Unit:Byte",
			"forceRestart":"false",
			"checkingCode":"[0-104857600]",
			"parameterName":"query_cache_size",
			"forceModify":"true"
		},
		{
			"parameterValue":"1",
			"parameterDescription":"",
			"forceRestart":"true",
			"checkingCode":"[0|1|2]",
			"parameterName":"query_cache_type",
			"forceModify":"true"
		},
		{
			"parameterValue":"8192",
			"parameterDescription":"The size of the persistent buffer used for statement parsing and execution. This buffer is not freed between statements. If you are running complex queries, a larger query_prealloc_size value might be helpful in improving performance, because it can reduce the need for the server to perform memory allocation during query execution operations.Unit:Byte",
			"forceRestart":"false",
			"checkingCode":"[8192-1048576]",
			"parameterName":"query_prealloc_size",
			"forceModify":"true"
		},
		{
			"parameterValue":"2",
			"parameterDescription":"If creating a thread takes longer than this many seconds, the server increments the Slow_launch_threads status variable.",
			"forceRestart":"false",
			"checkingCode":"[1-1024]",
			"parameterName":"slow_launch_time",
			"forceModify":"true"
		},
		{
			"parameterValue":"",
			"parameterDescription":"Modes define what SQL syntax MySQL should support and what kind of data validation checks it should perform.",
			"forceRestart":"false",
			"checkingCode":"(\\s*|REAL_AS_FLOAT|PIPES_AS_CONCAT|ANSI_QUOTES|IGNORE_SPACE|ONLY_FULL_GROUP_BY|NO_UNSIGNED_SUBTRACTION|NO_DIR_IN_CREATE|POSTGRESQL|ORACLE|MSSQL|DB2|MAXDB|NO_KEY_OPTIONS|NO_TABLE_OPTIONS|NO_FIELD_OPTIONS|MYSQL323|MYSQL40|ANSI|NO_AUTO_VALUE_ON_ZERO|NO_BACKSLASH_ESCAPES|STRICT_TRANS_TABLES|STRICT_ALL_TABLES|NO_ZERO_IN_DATE|NO_ZERO_DATE|ALLOW_INVALID_DATES|ERROR_FOR_DIVISION_BY_ZERO|TRADITIONAL|HIGH_NOT_PRECEDENCE|NO_ENGINE_SUBSTITUTION|PAD_CHAR_TO_FULL_LENGTH)(,REAL_AS_FLOAT|,PIPES_AS_CONCAT|,ANSI_QUOTES|,IGNORE_SPACE|,ONLY_FULL_GROUP_BY|,NO_UNSIGNED_SUBTRACTION|,NO_DIR_IN_CREATE|,POSTGRESQL|,ORACLE|,MSSQL|,DB2|,MAXDB|,NO_KEY_OPTIONS|,NO_TABLE_OPTIONS|,NO_FIELD_OPTIONS|,MYSQL323|,MYSQL40|,ANSI|,NO_AUTO_VALUE_ON_ZERO|,NO_BACKSLASH_ESCAPES|,STRICT_TRANS_TABLES|,STRICT_ALL_TABLES|,NO_ZERO_IN_DATE|,NO_ZERO_DATE|,ALLOW_INVALID_DATES|,ERROR_FOR_DIVISION_BY_ZERO|,TRADITIONAL|,HIGH_NOT_PRECEDENCE|,NO_ENGINE_SUBSTITUTION|,PAD_CHAR_TO_FULL_LENGTH)*",
			"parameterName":"sql_mode",
			"forceModify":"true"
		},
		{
			"parameterValue":"512",
			"parameterDescription":"The number of table definitions (from .frm files) that can be stored in the definition cache. If you use a large number of tables, you can create a large table definition cache to speed up opening of tables. The table definition cache takes less space and does not use file descriptors, unlike the normal table cache. The minimum and default values are both 400.",
			"forceRestart":"false",
			"checkingCode":"[400-80480]",
			"parameterName":"table_definition_cache",
			"forceModify":"true"
		},
		{
			"parameterValue":"2000",
			"parameterDescription":"The number of open tables for all threads. Increasing this value increases the number of file descriptors that mysqld requires. You can check whether you need to increase the table cache by checking the Opened_tables status variable. See  “Server Status Variables”. If the value of Opened_tables is large and you do not use FLUSH TABLES often (which just forces all tables to be closed and reopened), then you should increase the value of the table_open_cache variable",
			"forceRestart":"false",
			"checkingCode":"[400-524288]",
			"parameterName":"table_open_cache",
			"forceModify":"true"
		},
		{
			"parameterValue":"2097152",
			"parameterDescription":"The maximum size of internal in-memory temporary tables",
			"forceRestart":"false",
			"checkingCode":"[262144-16777216]",
			"parameterName":"tmp_table_size",
			"forceModify":"true"
		},
		{
			"parameterValue":"86400",
			"parameterDescription":"The number of seconds the server waits for activity on a noninteractive connection before closing it.",
			"forceRestart":"false",
			"checkingCode":"[10-259200]",
			"parameterName":"wait_timeout",
			"forceModify":"true"
		}
	],
	"engineVersion":"5.1"
}
```

## 错误码 { .section}

[查看本产品错误码](https://error-center.aliyun.com/status/product/Rds)

