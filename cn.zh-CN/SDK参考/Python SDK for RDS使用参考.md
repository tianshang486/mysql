# Python SDK for RDS使用参考 {#concept_xnm_kyn_fgb .concept}

## 前提条件 {#section_aqd_rjt_2gb .section}

**已下载Python SDK版本安装包**

若未下载安装包，请参考如下步骤：

1.  进入[阿里云开发工具包](https://develop.aliyun.com/tools/sdk#/python)的Python SDK页面。
2.  单击**从PyPI上获取安装包**。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/82215/155288653835006_zh-CN.png)

3.  单击**Download files**，在右侧下载压缩文件。

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/82215/155288653835007_zh-CN.png)


## 请求步骤 {#section_ur2_pqn_fgb .section}

1.  发起调用，导入相关产品的SDK。

    ```
    from aliyunsdkcore.client import AcsClient
    from aliyunsdkcore.acs_exception.exceptions import ClientException
    from aliyunsdkcore.acs_exception.exceptions import ServerException
    from aliyunsdkrds.request.v20140815.DescribeSQLLogRecordsRequest import DescribeSQLLogRecordsRequest
    ```

2.  新建AcsClient。

    ```
    client = AcsClient(
    "<access-key-id>", 
    "<access-key-secret>",
    "<region-id>")
    ```

3.  设置域名。

    ```
    client.addEndpoint("<region-id>", "<region-id>", "< product>", "<endpoint>");
    ```

    **说明：** 域名请参见[表 1](#table_rjg_k5n_fgb)。

    |域名|支持的区域|公网IP|控制台链接|
    |--|-----|----|-----|
    |rds.aliyuncs.com| 青岛：cn-qingdao；

 北京：cn-beijing；

 杭州：cn-hangzhou；

 上海：cn-shanghai；

 深圳：cn-shenzhen；

 香港：cn-hongkong；

 亚太东南 1 \(新加坡\)：ap-southeast-1；

 美国东部 1 \(弗吉尼亚\)：us-east-1；

 美国西部 1 \(硅谷\)：us-west-1。

 |106.11.55.113| [cn-qingdao](https://rdsnew.console.aliyun.com/?accounttraceid=76c21e52-d07e-4cf4-9356-a3b8f9e86a6c#/rdsList/cn-qingdao/basic/) ；

 [cn-beijing](https://rdsnew.console.aliyun.com/?accounttraceid=76c21e52-d07e-4cf4-9356-a3b8f9e86a6c#/rdsList/cn-beijing/basic/) ；

 [cn-hangzhou](https://rdsnew.console.aliyun.com/?accounttraceid=76c21e52-d07e-4cf4-9356-a3b8f9e86a6c#/rdsList/cn-hangzhou/basic/)；

 [cn-shanghai](https://rdsnew.console.aliyun.com/?accounttraceid=76c21e52-d07e-4cf4-9356-a3b8f9e86a6c#/rdsList/cn-shanghai/basic/)；

 [cn-shenzhen](https://rdsnew.console.aliyun.com/?accounttraceid=76c21e52-d07e-4cf4-9356-a3b8f9e86a6c#/rdsList/cn-shenzhen/basic/)；

 [cn-hongkong](https://rdsnew.console.aliyun.com/?accounttraceid=76c21e52-d07e-4cf4-9356-a3b8f9e86a6c#/rdsList/cn-hongkong/basic/)；

 [ap-southeast-1](https://rdsnew.console.aliyun.com/?accounttraceid=76c21e52-d07e-4cf4-9356-a3b8f9e86a6c#/rdsList/ap-southeast-1/basic/)；

 [us-east-1](https://rdsnew.console.aliyun.com/?accounttraceid=76c21e52-d07e-4cf4-9356-a3b8f9e86a6c#/rdsList/us-east-1/basic/)；

 [us-west-1](https://rdsnew.console.aliyun.com/?accounttraceid=76c21e52-d07e-4cf4-9356-a3b8f9e86a6c#/rdsList/us-west-1/basic/)。

 |
    |rds.cn-zhangjiakou.aliyuncs.com|华北3（张家口）：cn-zhangjiakou|47.92.21.4|[cn-zhangjiakou](https://rdsnew.console.aliyun.com/?accounttraceid=76c21e52-d07e-4cf4-9356-a3b8f9e86a6c#/rdsList/cn-zhangjiakou/basic/)|
    |rds.ap-northeast-1.aliyuncs.com|亚太东北 1 \(东京\)：ap-northeast-1|47.91.8.8|[ap-northeast-1](https://rdsnew.console.aliyun.com/?accounttraceid=76c21e52-d07e-4cf4-9356-a3b8f9e86a6c#/rdsList/ap-northeast-1/basic/)|
    |rds.ap-southeast-3.aliyuncs.com|亚太东南3 \(吉隆坡\)：ap-southeast-3|47.254.226.21|[ap-southeast-3](https://rdsnew.console.aliyun.com/?accounttraceid=76c21e52-d07e-4cf4-9356-a3b8f9e86a6c#/rdsList/ap-southeast-3/basic/)|
    |rds.ap-southeast-2.aliyuncs.com|亚太东南 2 \(悉尼\)：ap-southeast-2|47.254.226.21|[ap-southeast-3](https://rdsnew.console.aliyun.com/?accounttraceid=76c21e52-d07e-4cf4-9356-a3b8f9e86a6c#/rdsList/ap-southeast-3/basic/)|
    |rds.me-east-1.aliyuncs.comm|中东东部 1 \(迪拜\)：me-east-1|47.91.39.7|[me-east-1](https://rdsnew.console.aliyun.com/?accounttraceid=76c21e52-d07e-4cf4-9356-a3b8f9e86a6c#/rdsList/me-east-1/basic/)|
    |rds.cn-huhehaote.aliyuncs.com|华北 5：cn-huhehaote|39.104.36.3|[cn-huhehaote](https://rdsnew.console.aliyun.com/?accounttraceid=76c21e52-d07e-4cf4-9356-a3b8f9e86a6c#/rdsList/cn-huhehaote/basic/)|
    |rds.ap-south-1.aliyuncs.com|亚太南部 1 \(孟买\)：ap-south-1|149.129.159.7|[ap-south-1-1](https://rdsnew.console.aliyun.com/#/rdsList/ap-south-1/basic/)|
    |rds.ap-southeast-5.aliyuncs.com|亚太东南 5 \(雅加达\)：ap-southeast-5|149.129.204.7|[ap-southeast-5](https://rdsnew.console.aliyun.com/#/rdsList/ap-southeast-5/basic/)|

4.  创建Request对象（查询实例详情），并设置请求参数。

    ```
    request =DescribeDBInstanceAttributeRequest();
    request.set_DBInstanceId("实例名称");
    ```

5.  初始化客户端。

    ```
    response = client.do_action_with_exception(request)
    ```

6.  调用返回结果。

    ```
    print response
    ```


## 实例生命周期参考实例 {#section_sws_3xn_fgb .section}

1.  **创建实例。**

    **调用示例**

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

    **返回结果**

    ```
    {
      "OrderId":"202796346400941",
      "DBInstanceId":"pgm-1111111111",
      "RequestId":"BAF2A62B-804B-4C6C-BEE4-BAD2CA4C79E1"
    }
    ```

2.  **实例变配。**

    **调用示例**

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
    request.set_DBInstanceId("pgm-1111111111");
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

    **返回结果**

    ```
    {"RequestId":"B77F7694-B632-4C2A-BEA5-F8E44AD3A97E"}
    ```

3.  **创建只读实例。**

    **调用示例**

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
    request.set_DBInstanceId("rm-11111111111111");
    request.set_EngineVersion("5.6");
    request.set_DBInstanceClass("rds.mysql.s1.small");
    request.set_DBInstanceStorage("20");
    request.set_DBInstanceDescription("aaa");
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

    **返回结果**

    ```
    {
            "OrderId": "1214369754489523", 
            "ConnectionString": "rr-bp1111111111.mysql.rds.aliyuncs.com", 
            "DBInstanceId": "rr-bp1111111111", 
            "Port": "3306", 
            "RequestId": "1E43AAE0-BEE8-43DA-860D-EAF2AA0724DC"
           
    }
    ```

4.  **重启实例。**

    **调用示例**

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
    request.set_DBInstanceId("rm-bp1111111111");
    try:
            response = client.do_action_with_exception(request)
            print response
    except ServerException as e:
            print e
    except ClientException as e:
            print e
    ```

    **返回结果**

    ```
    {"RequestId":"EED6E546-099A-4434-AB09-C85DD396E17B"}
    ```

5.  **实例列表。**

    **调用示例**

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

    **返回结果**

    ```
    {
        "Items": {
            "DBInstance": [
                {
                    "LockMode": "Unlock",
                    "DBInstanceNetType": "Intranet",
                    "DBInstanceClass": "rds.mysql.s2.large",
                    "ResourceGroupId": "rg-acf1111111111",
                    "DBInstanceId": "rm-bp1111111111111",
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
                    "ResourceGroupId": "rg-acf1111111111",
                    "DBInstanceId": "rm-bp1111111111111",
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


