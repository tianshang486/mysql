# Install and use RDS SDK for Python

This topic describes how to install and use RDS SDK for Python.

## Debugging

Alibaba Cloud provides [OpenAPI Explorer](https://api.aliyun.com/) to simplify API usage. You can use OpenAPI Explorer to search for API operations, call API operations, and dynamically generate SDK sample code.

## Prerequisites

-   An AccessKey pair is created. For more information, see [Create an AccessKey](~~53045~~).

    **Note:** We recommend that you create a RAM user and grant the RAM user the permissions to access ApsaraDB for RDS instances. Then, you can use the AccessKey pair of the RAM user to call RDS SDK for Python. This allows you to protect the AccessKey pair of your Alibaba Cloud account. For more information, see [Implement access control by using RAM](https://www.alibabacloud.com/help/zh/doc-detail/25481.htm).

-   Python is installed.

## Precautions

Make sure that your account has the required permissions. For more information, see [RAM authorization](/intl.en-US/API Reference/RAM authorization.md).

## Install RDS SDK for Python

1.  Visit the [Python SDK](https://github.com/aliyun/aliyun-openapi-python-sdk/tree/master/aliyun-python-sdk-rds) page at GitHub.
2.  Download the RDS SDK for Python package and install the SDK by following the instructions provided in the README file.

## Procedure

1.  Import the RDS SDK for Python package.

    ```
    from aliyunsdkcore.client import AcsClient
    from aliyunsdkcore.acs_exception.exceptions import ClientException
    from aliyunsdkcore.acs_exception.exceptions import ServerException
    from aliyunsdkrds.request.v20140815.DescribeSQLLogRecordsRequest import DescribeSQLLogRecordsRequest
    ```

2.  Create an AcsClient.

    ```
    client = AcsClient(
    "<access-key-id>", 
    "<access-key-secret>",
    "<region-id>")
    ```

3.  Configure the endpoint that is used to connect to your RDS instance.

    ```
    client.addEndpoint(
    "<region-id>", 
    "<product>", 
    "<endpoint>");
    ```

    **Note:** For more information, see [Table 1](#table_rjg_k5n_fgb).

    |Endpoint|Region|Public IP address|ApsaraDB for RDS console|
    |--------|------|-----------------|------------------------|
    |rds.aliyuncs.com|China \(Qingdao\): cn-qingdao

China \(Beijing\): cn-beijing

China \(Hangzhou\): cn-hangzhou

China \(Shanghai\): cn-shanghai

China \(Shenzhen\): cn-shenzhen

China \(Hong Kong\): cn-hongkong

Singapore: ap-southeast-1

US \(Virginia\): us-east-1

US \(Silicon Valley\): us-west-1

|106.11.55.113|[cn-qingdao](https://rdsnew.console.aliyun.com/?accounttraceid=76c21e52-d07e-4cf4-9356-a3b8f9e86a6c#/rdsList/cn-qingdao/basic/)

[cn-beijing](https://rdsnew.console.aliyun.com/?accounttraceid=76c21e52-d07e-4cf4-9356-a3b8f9e86a6c#/rdsList/cn-beijing/basic/)

[cn-hangzhou](https://rdsnew.console.aliyun.com/?accounttraceid=76c21e52-d07e-4cf4-9356-a3b8f9e86a6c#/rdsList/cn-hangzhou/basic/)

[cn-shanghai](https://rdsnew.console.aliyun.com/?accounttraceid=76c21e52-d07e-4cf4-9356-a3b8f9e86a6c#/rdsList/cn-shanghai/basic/)

[cn-shenzhen](https://rdsnew.console.aliyun.com/?accounttraceid=76c21e52-d07e-4cf4-9356-a3b8f9e86a6c#/rdsList/cn-shenzhen/basic/)

[cn-hongkong](https://rdsnew.console.aliyun.com/?accounttraceid=76c21e52-d07e-4cf4-9356-a3b8f9e86a6c#/rdsList/cn-hongkong/basic/)

[ap-southeast-1](https://rdsnew.console.aliyun.com/?accounttraceid=76c21e52-d07e-4cf4-9356-a3b8f9e86a6c#/rdsList/ap-southeast-1/basic/)

[us-east-1](https://rdsnew.console.aliyun.com/?accounttraceid=76c21e52-d07e-4cf4-9356-a3b8f9e86a6c#/rdsList/us-east-1/basic/)

[us-west-1](https://rdsnew.console.aliyun.com/?accounttraceid=76c21e52-d07e-4cf4-9356-a3b8f9e86a6c#/rdsList/us-west-1/basic/) |
    |rds.cn-zhangjiakou.aliyuncs.com|China \(Zhangjiakou-Beijing Winter Olympics\): cn-zhangjiakou|47.92.21.4|[cn-zhangjiakou](https://rdsnew.console.aliyun.com/?accounttraceid=76c21e52-d07e-4cf4-9356-a3b8f9e86a6c#/rdsList/cn-zhangjiakou/basic/)|
    |rds.ap-northeast-1.aliyuncs.com|Japan \(Tokyo\): ap-northeast-1|47.91.8.8|[ap-northeast-1](https://rdsnew.console.aliyun.com/?accounttraceid=76c21e52-d07e-4cf4-9356-a3b8f9e86a6c#/rdsList/ap-northeast-1/basic/)|
    |rds.ap-southeast-3.aliyuncs.com|Malaysia \(Kuala Lumpur\): ap-southeast-3|47.254.226.21|[ap-southeast-3](https://rdsnew.console.aliyun.com/?accounttraceid=76c21e52-d07e-4cf4-9356-a3b8f9e86a6c#/rdsList/ap-southeast-3/basic/)|
    |rds.ap-southeast-2.aliyuncs.com|Australia \(Sydney\): ap-southeast-2|47.254.226.21|[ap-southeast-3](https://rdsnew.console.aliyun.com/?accounttraceid=76c21e52-d07e-4cf4-9356-a3b8f9e86a6c#/rdsList/ap-southeast-3/basic/)|
    |rds.me-east-1.aliyuncs.comm|UAE \(Dubai\): me-east-1|47.91.39.7|[me-east-1](https://rdsnew.console.aliyun.com/?accounttraceid=76c21e52-d07e-4cf4-9356-a3b8f9e86a6c#/rdsList/me-east-1/basic/)|
    |rds.cn-huhehaote.aliyuncs.com|China \(Hohhot\): cn-huhehaote|39.104.36.3|[cn-huhehaote](https://rdsnew.console.aliyun.com/?accounttraceid=76c21e52-d07e-4cf4-9356-a3b8f9e86a6c#/rdsList/cn-huhehaote/basic/)|
    |rds.ap-south-1.aliyuncs.com|India \(Mumbai\): ap-south-1|149.129.159.7|[ap-south-1-1](https://rdsnew.console.aliyun.com/#/rdsList/ap-south-1/basic/)|
    |rds.ap-southeast-5.aliyuncs.com|Indonesia \(Jakarta\): ap-southeast-5|149.129.204.7|[ap-southeast-5](https://rdsnew.console.aliyun.com/#/rdsList/ap-southeast-5/basic/)|

4.  Create a request to query details about your RDS instance, and configure the request parameters.

    ```
    request =DescribeDBInstanceAttributeRequest();
    request.set_DBInstanceId("Name of your RDS instance");
    ```

5.  Initialize the AcsClient.

    ```
    response = client.do_action_with_exception(request)
    ```

6.  View the response.

    ```
    print response
    ```


## Examples

1.  Create an RDS instance.

    Sample request:

    ```
    from aliyunsdkcore.client import AcsClient
    from aliyunsdkcore.acs_exception.exceptions import ClientException
    from aliyunsdkcore.acs_exception.exceptions import ServerException
    from aliyunsdkrds.request.v20140815.DescribeDBInstancePerformanceRequest import DescribeDBInstancePerformanceRequest
    from aliyunsdkrds.request.v20140815.CreateDBInstanceRequest import CreateDBInstanceRequest
    
    client = AcsClient(
            "<access-key-id>",
            "<access-key-secret>",
            "cn-hangzhou"
            );
    request =CreateDBInstanceRequest();
    request.set_Engine("PostgreSQL");
    request.set_EngineVersion("10.0");
    request.set_DBInstanceClass("pg.n1.micro.1");
    request.set_DBInstanceStorage("20");
    request.set_DBInstanceNetType("Intranet");
    request.set_DBInstanceDescription("aaa");
    request.set_SecurityIPList("127.0.0.1");
    request.set_PayType("Postpaid");
    request.set_ZoneId("cn-hangzhou-b");
    request.set_InstanceNetworkType("Classic");
    request.set_Period("Month");
    request.set_UsedTime("2");
    try:
            response = client.do_action_with_exception(request)
            print response
    except ServerException as e:
            print e
    except ClientException as e:
            print e
    ```

    Sample response:

    ```
    {
      "OrderId":"20279634xxxxxxx",
      "DBInstanceId":"pgm-xxxxxxx",
      "RequestId":"BAF2A62B-804B-4C6C-BEE4-BAD2CA4C79E1"
    }
    ```

2.  Change the specifications of an RDS instance.

    Sample request:

    ```
    from aliyunsdkcore.client import AcsClient
    from aliyunsdkcore.acs_exception.exceptions import ClientException
    from aliyunsdkcore.acs_exception.exceptions import ServerException
    from aliyunsdkrds.request.v20140815.DescribeDBInstancePerformanceRequest import DescribeDBInstancePerformanceRequest
    from aliyunsdkrds.request.v20140815.ModifyDBInstanceSpecRequest import ModifyDBInstanceSpecRequest
    
    client = AcsClient(
            "<access-key-id>",
            "<access-key-secret>",
            "cn-hangzhou"
            );
    request =ModifyDBInstanceSpecRequest();
    request.set_DBInstanceId("pgm-xxxxxxx");
    request.set_PayType("Postpaid");
    request.set_DBInstanceClass("pg.n2.small.1");
    try:
            response = client.do_action_with_exception(request)
            print response
    except ServerException as e:
            print e
    except ClientException as e:
            print e
                        
    ```

    Sample response:

    ```
    {"RequestId":"B77F7694-B632-4C2A-BEA5-F8E44AD3A97E"}
    ```

3.  Create a read-only RDS instance.

    Sample request:

    ```
    from aliyunsdkcore.client import AcsClient
    from aliyunsdkcore.acs_exception.exceptions import ClientException
    from aliyunsdkcore.acs_exception.exceptions import ServerException
    from aliyunsdkrds.request.v20140815.DescribeDBInstancePerformanceRequest import DescribeDBInstancePerformanceRequest
    from aliyunsdkrds.request.v20140815.CreateReadOnlyDBInstanceRequest import CreateReadOnlyDBInstanceRequest
    
    client = AcsClient(
            "<access-key-id>",
            "<access-key-secret>",
            "cn-hangzhou"
            );
    request =CreateReadOnlyDBInstanceRequest();
    request.set_DBInstanceId("rm-xxxxxxx");
    request.set_EngineVersion("5.6");
    request.set_DBInstanceClass("rds.mysql.s1.small");
    request.set_DBInstanceStorage("20");
    request.set_DBInstanceDescription("testDesc");
    request.set_PayType("Postpaid");
    request.set_ZoneId("cn-hangzhou-b");
    request.set_InstanceNetworkType("Classic");
    try:
            response = client.do_action_with_exception(request)
            print response
    except ServerException as e:
            print e
    except ClientException as e:
            print e
    ```

    Sample response:

    ```
    {
            "OrderId": "1214369xxxxxxx", 
            "ConnectionString": "rr-bpxxxxxxx.mysql.rds.aliyuncs.com", 
            "DBInstanceId": "rr-bpxxxxxxx", 
            "Port": "3306", 
            "RequestId": "1E43AAE0-BEE8-43DA-860D-EAF2AA0724DC"
    
    }
    ```

4.  Restart an RDS instance.

    Sample request:

    ```
    from aliyunsdkcore.client import AcsClient
    from aliyunsdkcore.acs_exception.exceptions import ClientException
    from aliyunsdkcore.acs_exception.exceptions import ServerException
    from aliyunsdkrds.request.v20140815.DescribeDBInstancePerformanceRequest import DescribeDBInstancePerformanceRequest
    from aliyunsdkrds.request.v20140815.RestartDBInstanceRequest import RestartDBInstanceRequest
    
    client = AcsClient(
            "<access-key-id>",
            "<access-key-secret>",
            "cn-hangzhou"
            );
    request =RestartDBInstanceRequest();
    request.set_DBInstanceId("rm-bpxxxxxxx");
    try:
            response = client.do_action_with_exception(request)
            print response
    except ServerException as e:
            print e
    except ClientException as e:
            print e
    ```

    Sample response:

    ```
    {"RequestId":"EED6E546-099A-4434-AB09-C85DD396E17B"}
    ```

5.  Query RDS instances.

    Sample request:

    ```
    from aliyunsdkcore.client import AcsClient
    from aliyunsdkcore.acs_exception.exceptions import ClientException
    from aliyunsdkcore.acs_exception.exceptions import ServerException
    from aliyunsdkrds.request.v20140815.DescribeDBInstancePerformanceRequest import DescribeDBInstancePerformanceRequest
    from aliyunsdkrds.request.v20140815.DescribeDBInstancesRequest import DescribeDBInstancesRequest
    
    client = AcsClient(
            "<access-key-id>",
            "<access-key-secret>",
            "cn-hangzhou"
            );
    request =DescribeDBInstancesRequest();
    print response
    try:
            response = client.do_action_with_exception(request)
            print response
    except ServerException as e:
            print e
    except ClientException as e:
            print e
    ```

    Sample response:

    ```
    {
        "Items": {
            "DBInstance": [
                {
                    "LockMode": "Unlock",
                    "DBInstanceNetType": "Intranet",
                    "DBInstanceClass": "rds.mysql.s2.large",
                    "ResourceGroupId": "rg-acfxxxxxxx",
                    "DBInstanceId": "rm-bpxxxxxxx",
                    "VpcCloudInstanceId": "",
                    "ZoneId": "cn-hangzhou-f",
                    "ReadOnlyDBInstanceIds": {
                        "ReadOnlyDBInstanceId": []
                    },
                    "InstanceNetworkType": "Classic",
                    "ConnectionMode": "Standard",
                    "Engine": "MySQL",
                    "MutriORsignle": false,
                    "InsId": 1,
                    "ExpireTime": "",
                    "CreateTime": "2018-11-07T15:52Z",
                    "DBInstanceType": "Primary",
                    "RegionId": "cn-hangzhou",
                    "EngineVersion": "5.7",
                    "LockReason": "",
                    "DBInstanceStatus": "Running",
                    "PayType": "Postpaid"
                },
                {
                    "LockMode": "Unlock",
                    "DBInstanceNetType": "Intranet",
                    "DBInstanceClass": "rds.mysql.s2.large",
                    "ResourceGroupId": "rg-acfxxxxxxx",
                    "DBInstanceId": "rm-bpxxxxxxx",
                    "VpcCloudInstanceId": "",
                    "ZoneId": "cn-hangzhou-g",
                    "ReadOnlyDBInstanceIds": {
                        "ReadOnlyDBInstanceId": []
                    },
                    "InstanceNetworkType": "Classic",
                    "ConnectionMode": "Standard",
                    "Engine": "MySQL",
                    "MutriORsignle": false,
                    "InsId": 1,
                    "ExpireTime": "2019-11-07T16:00:00Z",
                    "CreateTime": "2018-11-07T15:42Z",
                    "DBInstanceType": "Primary",
                    "RegionId": "cn-hangzhou",
                    "EngineVersion": "5.7",
                    "LockReason": "",
                    "DBInstanceStatus": "Running",
                    "PayType": "Prepaid"
                }
            ]
        },
        "TotalRecordCount": 209,
        "PageNumber": 1,
        "RequestId": "0C5793A6-80C3-4AC0-A5E1-CCA25F387AE6",
        "PageRecordCount": 30
    }
    ```


