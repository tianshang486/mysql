# 授权RDS访问KMS

需要给RDS授予访问密钥管理服务KMS（Key Management Service）的权限，才能正常使用云盘加密功能，您可以在访问控制RAM控制台上进行授权。

需要使用阿里云主账号。

## 创建权限策略AliyunRDSInstanceEncryptionRolePolicy

1.  登录访问控制的[权限策略管理](https://ram.console.aliyun.com/policies)页面。

2.  单击**创建权限策略**。

    **说明：** [权限策略](https://www.alibabacloud.com/help/zh/doc-detail/28628.htm)是用语法结构描述的一组权限的集合，可以精确地描述被授权的资源、操作以及授权条件。

3.  设置如下参数。

    |参数|说明|
    |--|--|
    |**策略名称**|填写策略名称。请填写**AliyunRDSInstanceEncryptionRolePolicy**。|
    |**备注**|填写备注。例如：用于RDS访问KMS。|
    |**配置模式**|策略配置模式。请选择**脚本配置**，复制下方脚本内容并粘贴。|

    脚本配置如下：

    ```
    {
        "Version": "1",
        "Statement": [
            {
                "Action": [
                    "kms:List*",
                    "kms:DescribeKey",
                    "kms:TagResource",
                    "kms:UntagResource"
                ],
                "Resource": [
                    "acs:kms:*:*:*"
                ],
                "Effect": "Allow"
            },
            {
                "Action": [
                    "kms:Encrypt",
                    "kms:Decrypt",
                    "kms:GenerateDataKey"
                ],
                "Resource": [
                    "acs:kms:*:*:*"
                ],
                "Effect": "Allow",
                "Condition": {
                    "StringEqualsIgnoreCase": {
                        "kms:tag/acs:rds:instance-encryption": "true"
                    }
                }
            }
        ]
    }
    ```

4.  单击**确定**。


## 创建RAM角色AliyunRDSInstanceEncryptionDefaultRole并授权

创建完策略之后，需要将策略授权给RAM角色，RDS就可以访问KMS资源。

1.  登录访问控制的[RAM角色管理](https://ram.console.aliyun.com/roles)页面。

2.  单击**创建RAM角色**。

3.  选择**阿里云账号**，单击**下一步**。

4.  设置如下参数。**角色名称**。

    |参数|说明|
    |--|--|
    |**角色名称**|填写**AliyunRDSInstanceEncryptionDefaultRole**。|
    |**备注**|添加备注信息。|
    |**选择云账号**|选择**当前云账号**。|

5.  在**角色创建成功**的提示下单击**为角色授权**。

    ![角色创建成功](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/0851507061/p187971.png)

    **说明：** 如果关闭了**角色创建成功**页面，也可以在[RAM角色管理](https://ram.console.aliyun.com/roles)页面搜索**AliyunRDSInstanceEncryptionRolePolicy**，然后单击**添加权限**。

6.  在**添加权限**页面搜索之前创建的权限**AliyunRDSInstanceEncryptionRolePolicy**并单击该名称，使之移动到右侧**已选择**框内。

    ![授权](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3967796061/p187389.png)

7.  单击**确定**。


## 查看角色ARN（可选）

ARN（Alibaba Cloud Resource Name）是RAM角色的全局资源描述符，即描述该RAM角色具有哪些资源的访问权限。调用API进行云盘加密时需要传入ARN，用于指定一个具有KMS访问权限的RAM角色，具体操作，请参见[CreateDBInstance](/intl.zh-CN/API 参考/实例/创建RDS实例.md)。

1.  登录访问控制的[RAM角色管理](https://ram.console.aliyun.com/roles)页面。

2.  找到目标角色，单击角色名称。

3.  在右上角查看ARN。

    ![](https://static-aliyun-doc.oss-accelerate.aliyuncs.com/assets/img/zh-CN/3967796061/p66346.png)


