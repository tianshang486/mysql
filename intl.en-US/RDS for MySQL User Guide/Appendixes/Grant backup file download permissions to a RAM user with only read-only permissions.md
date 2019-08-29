# Grant backup file download permissions to a RAM user with only read-only permissions {#concept_qmt_zxm_cgb .concept}

This topic describes how to grant backup file download permissions to a RAM user who only has read-only permissions. For security purposes, a typical RAM user cannot download backup files.

## Procedure {#section_ik1_gym_cgb .section}

1.  Log on to the [RAM console](https://ram.console.aliyun.com/overview).
2.  In the left-side navigation pane, choose **Permissions** \> **Policies**.
3.  Click **Create Policy** and set the parameters.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/79847/156704660234182_en-US.png)

    The policy content is as follows:

    ``` {#codeblock_c21_klt_yu7}
    {
        "Statement": [
            {
                "Effect": "Allow",
                "Action": [
                    "rds:Describe*",
                    "rds:ModifyBackupPolicy"
                ],
                "Resource": "*"
            }
        ],
        "Version": "1"
    }
    ```

4.  Click **OK**.
5.  In the left-side navigation pane, choose **Permissions** \> **Grants**.
6.  Click **Grant Permission** and add the new permission policy to the target RAM user.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/79847/156704660234183_en-US.png)

7.  Click **OK**.

