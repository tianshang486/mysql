# 授权RDS访问KMS

开通云盘加密前，需要给RDS授予访问密钥管理服务KMS（Key Management Service）的权限，您可以在访问控制RAM控制台上进行授权。

云盘加密能够最大限度保护您的数据安全，您的业务和应用程序无需做额外的改动。关于云盘加密的更多详情请参见[云盘加密](/cn.zh-CN/RDS MySQL 数据库/数据安全/加密/云盘加密.md)。

## 授权操作

1.  登录访问控制的[权限策略管理](https://ram.console.aliyun.com/policies)页面。

2.  单击**新建权限策略**并创建新权限策略。

    **说明：** [权限策略](https://help.aliyun.com/document_detail/28628.html)是用语法结构描述的一组权限的集合，可以精确地描述被授权的资源集、操作集以及授权条件。

    1.  设置如下参数。

        |参数|说明|
        |--|--|
        |**策略名称**|填写策略名称。策略名称必须唯一。|
        |**备注**|填写备注。|
        |**配置模式**|策略配置模式。         -   可视化配置：通过**添加授权语句**按钮设置权限效力、产品/服务、操作名称等。
        -   脚本配置：通过指定格式的文本快速设置策略。您可以直接复制下方说明内的脚本内容。 |

        **说明：** 脚本配置如下：

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

        ![新建策略](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/6323729951/p66333.png)

    2.  单击**确定**。

3.  在左侧导航栏选择**RAM角色管理**。

4.  搜索**AliyunRDSInstanceEncryptionDefaultRole**并在右侧单击**添加权限**。

5.  在**自定义权限策略**中搜索之前创建的策略，然后单击策略移动到右侧**已选择**框中。

    ![授权策略](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/6510443061/p66341.png)

6.  单击**确定**。


## 查看ARN

ARN是角色的全局资源描述符，用来指定具体角色。ARN遵循阿里云ARN的命名规范。例如，某个云账号下的devops角色的ARN为：`acs:ram::123456789012****:role/samplerole`。

1.  登录访问控制的[RAM角色管理](https://ram.console.aliyun.com/roles)页面。

2.  找到目标角色，单击角色名称。

    ![查找角色](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/6323729951/p66344.png)

3.  在右上角查看ARN。

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/zh-CN/6323729951/p66346.png)


