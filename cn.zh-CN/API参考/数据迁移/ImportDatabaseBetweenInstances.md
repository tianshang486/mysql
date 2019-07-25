# ImportDatabaseBetweenInstances {#doc_api_Rds_ImportDatabaseBetweenInstances .reference}

调用ImportDatabaseBetweenInstances接口从其它RDS实例迁入数据。

迁移过程中，源实例的状态处于**迁移中**，目标实例的状态处于**数据导入中**。

调用该接口时，实例必须满足以下条件，否则将操作失败：

-   仅支持MySQL和SQL Server的独享和独占规格的实例，关于实例规格详情，请参见[实例规格表](~~26312~~)；
-   仅适用于不同实例间（实例都属于同一个用户）的数据库迁移；
-   实例状态为运行中；
-   数据库状态为运行中；
-   确保目标实例的剩余存储空间\>源实例数据库的存储空间；
-   对于MySQL实例，待迁移数据库在源实例和目标实例都必须存在，而且状态为运行中。

**说明：** 

-   暂不支持SQL Server 2017集群版实例。
-   支持批量数据库迁入。

## 调试 {#api_explorer .section}

[您可以在OpenAPI Explorer中直接运行该接口，免去您计算签名的困扰。运行成功后，OpenAPI Explorer可以自动生成SDK代码示例。](https://api.aliyun.com/#product=Rds&api=ImportDatabaseBetweenInstances&type=RPC&version=2014-08-15)

## 请求参数 {#parameters .section}

|名称|类型|是否必选|示例值|描述|
|--|--|----|---|--|
|Action|String|是|ImportDatabaseBetweenInstances|系统规定参数，取值：**ImportDatabaseBetweenInstances**。

 |
|DBInstanceId|String|是|rm-uf6wjk5xxxxxxx|目标实例ID。

 |
|SourceDBInstanceId|String|是|rm-g4a1jk8xxxxxxx|源实例ID，不能与目标实例相同。

 |
|DBInfo|String|是|\{“DBNames”:\[“mydb”,”mydb2”\]\}|待迁移实例的数据库信息，格式为JSON串：

 -   对于MySQL实例，值为数组，MySQL类型要求源数据库和目的数据库名称必须一致。例如：

```
{“DBNames”:[“mydb”,”mydb2”]}
```

表示将两个数据库mydb和mydb2进行数据迁入，源实例和目的实例都要有这两个数据库。

-   对于SQL Server实例，值为key-value对，key为原数据库，目标为迁移目标数据库，SQL Server允许源数据库和目标数据库名称可以不一致。例如：

    ```
{“DBNames”:{“srcdb”:”destdb”,”srcdb2”:”destmydb2”}}
    ```

表示将srcdb迁入至destdb，将srcdb2迁入至destmydb2，但是多个源数据库名称不允许一样，多个目标数据库名称也不允许一样。


 |
|AccessKeyId|String|否|LTAIfCxxxxxxx|阿里云颁发给用户的访问服务所用的密钥ID。

 |

## 返回数据 {#resultMapping .section}

|名称|类型|示例值|描述|
|--|--|---|--|
|ImportId|String|85265475235|导入任务的ID。

 |
|RequestId|String|5A77D650-27A1-4E08-AD9E-59008EDB6927|请求ID。

 |

## 示例 {#demo .section}

请求示例

``` {#request_demo}

http(s)://rds.aliyuncs.com/?Action=ImportDatabaseBetweenInstances
&DBInstanceId=rm-uf6wjk5xxxxxxx
&SourceDBInstanceId=rm-g4a1jk8xxxxxxx
&DBInfo={“DBNames”:[“mydb”,”mydb2”]}
&<公共请求参数>

```

正常返回示例

`XML` 格式

``` {#xml_return_success_demo}
<ImportDatabaseBetweenInstancesResponse>
           <ImportId>2122321</ImportId>
         <RequestId>5A77D650-27A1-4E08-AD9E-59008EDB6927</RequestId>
</ImportDatabaseBetweenInstancesResponse>
```

`JSON` 格式

``` {#json_return_success_demo}
{
	"ImportId":2122321,
	"RequestId":"5A77D650-27A1-4E08-AD9E-59008EDB6927"
}
```

## 错误码 { .section}

访问[错误中心](https://error-center.aliyun.com/status/product/Rds)查看更多错误码。

