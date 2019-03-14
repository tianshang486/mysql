# ModifyCollationTimeZone {#concept_uff_hks_cfb .concept}

对于RDS for SQL Server 2012或以上版本的实例，您可以修改系统库的字符集排序规则和时区。系统库包括master、msdb、tempdb和model。

-   默认的字符集排序规则：Chinese\_PRC\_CI\_AS
-   默认的时区：China Standard Time

## 前提条件 {#section_uxp_lwp_cfb .section}

-   实例类型为RDS for SQL Server 2012或以上版本。
-   实例中没有任何用户数据库（即您创建的数据库，非系统数据库）。

## 注意事项 {#section_mdb_fdj_dfb .section}

修改期间，实例将处于不可用状态。修改时区需要大约1分钟，修改字符集排序规则需要2到10分钟。

## 请求参数 {#section_qzx_w32_12b .section}

|名称|类型|是否必须|描述|
|--|--|----|--|
|Action|String|是| 要执行的操作，取值：ModifyCollationTimeZone

 |
|DBInstanceId|String|是|实例ID。|
|Collation|String|否|要修改成的系统字符集排序规则，为空表示不修改。系统字符集排序规则与时区必须修改其中至少一个。

可选的系统字符集排序规则如下：

-   Latin1\_General\_CI\_AS
-   Latin1\_General\_CS\_AS
-   SQL\_Latin1\_General\_CP1\_CI\_AS
-   SQL\_Latin1\_General\_CP1\_CS\_AS
-   Chinese\_PRC\_CS\_AS
-   Chinese\_PRC\_BIN
-   Chinese\_PRC\_CI\_AS
-   Japanese\_CI\_AS
-   Japanese\_CS\_AS
-   Chinese\_Taiwan\_Stroke\_CI\_AS
-   Chinese\_Taiwan\_Stroke\_CS\_AS

|
|Timezone|String|否|要修改成的系统时区，为空表示不修改。系统字符集排序规则与时区必须修改其中至少一个。

可选的时区见下表。

|

|时区|与标准时间的偏移量|说明|
|--|---------|--|
|Afghanistan Standard Time|\(UTC+04:30\)|Kabul|
|Alaskan Standard Time|\(UTC–09:00\)|Alaska|
|Arabian Standard Time|\(UTC+04:00\)|Abu Dhabi, Muscat|
|Atlantic Standard Time|\(UTC–04:00\)|Atlantic Time \(Canada\)|
|AUS Central Standard Time|\(UTC+09:30\)|Darwin|
|AUS Eastern Standard Time|\(UTC+10:00\)|Canberra, Melbourne, Sydney|
|Belarus Standard Time|\(UTC+03:00\)|Minsk|
|Canada Central Standard Time|\(UTC–06:00\)|Saskatchewan|
|Cape Verde Standard Time|\(UTC–01:00\)|Cabo Verde Is.|
|Cen. Australia Standard Time|\(UTC+09:30\)|Adelaide|
|Central America Standard Time|\(UTC–06:00\)|Central America|
|Central Asia Standard Time|\(UTC+06:00\)|Astana|
|Central Brazilian Standard Time|\(UTC–04:00\)|Cuiaba|
|Central Europe Standard Time|\(UTC+01:00\)|Belgrade, Bratislava, Budapest, Ljubljana, Prague|
|Central European Standard Time|\(UTC+01:00\)|Sarajevo, Skopje, Warsaw, Zagreb|
|Central Pacific Standard Time|\(UTC+11:00\)|Solomon Islands, New Caledonia|
|Central Standard Time|\(UTC–06:00\)|Central Time \(US and Canada\)|
|Central Standard Time \(Mexico\)|\(UTC–06:00\)|Guadalajara, Mexico City, Monterrey|
|China Standard Time|\(UTC+08:00\)|Beijing, Chongqing, Hong Kong, Urumqi|
|E. Africa Standard Time|\(UTC+03:00\)|Nairobi|
|E. Australia Standard Time|\(UTC+10:00\)|Brisbane|
|E. Europe Standard Time|\(UTC+02:00\)|Chisinau|
|E. South America Standard Time|\(UTC–03:00\)|Brasilia|
|Eastern Standard Time|\(UTC–05:00\)|Eastern Time \(US and Canada\)|
|Georgian Standard Time|\(UTC+04:00\)|Tbilisi|
|GMT Standard Time|\(UTC\)|Dublin, Edinburgh, Lisbon, London|
|Greenland Standard Time|\(UTC–03:00\)|Greenland|
|Greenwich Standard Time|\(UTC\)|Monrovia, Reykjavik|
|GTB Standard Time|\(UTC+02:00\)|Athens, Bucharest|
|Hawaiian Standard Time|\(UTC–10:00\)|Hawaii|
|India Standard Time|\(UTC+05:30\)|Chennai, Kolkata, Mumbai, New Delhi|
|Jordan Standard Time|\(UTC+02:00\)|Amman|
|Korea Standard Time|\(UTC+09:00\)|Seoul|
|Middle East Standard Time|\(UTC+02:00\)|Beirut|
|Mountain Standard Time|\(UTC–07:00\)|Mountain Time \(US and Canada\)|
|Mountain Standard Time \(Mexico\)|\(UTC–07:00\)|Chihuahua, La Paz, Mazatlan|
|US Mountain Standard Time|\(UTC–07:00\)|Arizona|
|New Zealand Standard Time|\(UTC+12:00\)|Auckland, Wellington|
|Newfoundland Standard Time|\(UTC–03:30\)|Newfoundland|
|Pacific SA Standard Time|\(UTC–03:00\)|Santiago|
|Pacific Standard Time|\(UTC–08:00\)|Pacific Time \(US and Canada\)|
|Pacific Standard Time \(Mexico\)|\(UTC–08:00\)|Baja California|
|Russian Standard Time|\(UTC+03:00\)|Moscow, St. Petersburg, Volgograd|
|SA Pacific Standard Time|\(UTC–05:00\)|Bogota, Lima, Quito, Rio Branco|
|SE Asia Standard Time|\(UTC+07:00\)|Bangkok, Hanoi, Jakarta|
|China Standard Time|\(UTC+08:00\)|Kuala Lumpur, Singapore|
|Tokyo Standard Time|\(UTC+09:00\)|Osaka, Sapporo, Tokyo|
|US Eastern Standard Time|\(UTC–05:00\)|Indiana \(East\)|
|UTC|UTC|Coordinated Universal Time|
|UTC–02|\(UTC–02:00\)|Coordinated Universal Time–02|
|UTC–08|\(UTC–08:00\)|Coordinated Universal Time–08|
|UTC–09|\(UTC–09:00\)|Coordinated Universal Time–09|
|UTC–11|\(UTC–11:00\)|Coordinated Universal Time–11|
|UTC+12|\(UTC+12:00\)|Coordinated Universal Time+12|
|W. Australia Standard Time|\(UTC+08:00\)|Perth|
|W. Central Africa Standard Time|\(UTC+01:00\)|West Central Africa|
|W. Europe Standard Time|\(UTC+01:00\)|Amsterdam, Berlin, Bern, Rome, Stockholm, Vienna|

## 返回参数 {#section_a5x_zlh_12b .section}

|名称|类型|描述|
|--|--|--|
|<公共返回参数\>| |详见[公共参数](cn.zh-CN/API参考/使用API/公共参数.md#)。|
|DBInstanceId|String|实例ID。|
|TaskId|String|任务ID。|
|Timezone|String|时区。|
|Collation|String|系统字符集排序规则。|

