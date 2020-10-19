# Configure data encryption for an RDS PostgreSQL instance

This topic describes how to configure SSL encryption and disk encryption for an RDS PostgreSQL instance to ensure data security.

-   If you require SSL encryption, your RDS instance is equipped with standard SSDs or enhanced SSDs \(ESSDs\).
-   If you require disk encryption, your RDS instance is equipped with standard SSDs or enhanced SSDs \(ESSDs\).
-   If you require disk encryption, disk encryption is configured. For more information, see [Configure disk encryption](#section_ffo_jzy_q7z). You can only enable disk encryption when you create an RDS instance.
-   If you require disk encryption, your RDS instance resides in one of the following regions:
    -   China \(Hangzhou\)
    -   China \(Shanghai\)
    -   China \(Qingdao\)
    -   China \(Beijing\)
    -   China \(Shenzhen\)
    -   China \(Hong Kong\)
    -   Singapore
    -   Malaysia \(Kuala Lumpur\)
    -   Indonesia \(Jakarta\)
    -   Germany \(Frankfurt\)

## Precautions

-   After you enable SSL encryption, data transmitted over an internal network or the Internet is encrypted by using SSL. SSL encryption protects data from theft.
-   After you enable SSL encryption, you must disconnect the existing connection and establish a new one so that SSL encryption takes effect.

## Configure SSL encryption

1.  Log on to the [ApsaraDB for RDS console](https://rds.console.aliyun.com/).

2.  In the top navigation bar, select the region where the target RDS instance resides.

    ![Select a region](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Find the target RDS instance and click its ID.

4.  In the left-side navigation pane, click **Parameters**.

5.  Click the edit button corresponding to the **ssl** parameter. In the dialog box that appears, change the value to **on** and click **Confirm**.

    ![Change the value of the ssl parameter](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/6450359951/p67643.png)

    **Note:**

    -   After you enable SSL encryption, you must set the SSL mode to **Prefer** when you log on from your client.

        ![SSLMODE](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/6450359951/p74979.png)

    -   If you want to disable SSL encryption, you must change the value of the **ssl** parameter to **off**.

## Configure disk encryption

Disk encryption provides maximum protection for your data with minimal impact on your businesses or applications. In addition, both the snapshots generated from encrypted disks and the disks created from those snapshots are automatically encrypted.

Disk encryption is free of charge. You do not need to pay additional fees for the read and write operations you perform on encrypted disks.

1.  Log on to the [KMS console](https://kms.console.aliyun.com/cn-hongkong/key/list).

2.  In the top navigation bar, select the region where you want to create an RDS instance.

    ![Select a region](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/8651559951/p36543.png)

3.  Click **Create Key**.

4.  Configure the following parameters.

    |Parameter|Description|
    |---------|-----------|
    |**Key Spec**|Valid values:    -   Symmetric keys:
        -   Aliyun\_AES\_256
        -   Aliyun\_SM4
    -   Asymmetric keys:
        -   RSA\_2048
        -   EC\_P256
        -   EC\_P256K
        -   EC\_SM2
**Note:** Aliyun\_SM4 and EC\_SM2 types are used only in mainland China regions where Managed HSM is available. |
    |**Purpose**|    -   Encrypt/Decrypt: The purpose of the CMK is to encrypt or decrypt data.
    -   Sign/Verify: The purpose of the CMK is to generate or verify a digital signature. |
    |**Alias Name**|The optional identifier of the CMK. For more information, see [Use aliases](/intl.en-US/User Guide/Use aliases.md).|
    |**Protection Level**|    -   Software: Use a software module to protect the CMK.
    -   Hsm: Host the CMK in a hardware security module \(HSM\). Managed HSM uses the HSM as dedicated hardware to safeguard the CMK. |
    |**Description**|The description of the CMK.|
    |**Rotation Period**|The automatic rotation period. Valid values:    -   30 Days
    -   90 Days
    -   180 Days
    -   365 Days
    -   Disable: Rotation is disabled.
    -   Customize: Customize a period that ranges from 7 days to 730 days.
**Note:** You can specify this parameter only if Key Spec is set to Aliyun\_AES\_256 or Aliyun\_SM4. |

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/4651703061/p55744.png)

5.  Click **OK**.

6.  On the [Cloud Resource Access Authorization](https://ram.console.aliyun.com/#/role/authorize?request=%7B%22Requests%22%3A%20%7B%22request1%22%3A%20%7B%22RoleName%22%3A%20%22AliyunPostgreSQLInstanceEncryptionRole%22%2C%20%22TemplateId%22%3A%20%22PostgreSQLInstanceEncryptionRole%22%7D%7D%2C%20%22ReturnUrl%22%3A%20%22https%3A//postgresql.console.aliyun.com%22%2C%20%22Service%22%3A%20%22PostgreSQL%22%7D) page, click **Confirm Authorization Policy**.

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/6450359951/p55746.png)

    **Note:** This step is only required when you are creating an RDS instance for the first time with disk encryption enabled in the selected region. You can go to the [RAM console](https://ram.console.aliyun.com/roles) and navigate to the RAM Roles page to check whether you have the **AliyunPostgreSQLInstanceEncryptionRole** permission.

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/6450359951/p55749.png)

7.  Create an RDS instance with disk encryption enabled. For more information, see [Create an ApsaraDB RDS for PostgreSQL instance](/intl.en-US/RDS PostgreSQL Database/Quick start/Create an ApsaraDB RDS for PostgreSQL instance.md).

    **Note:** After the RDS instance is created, you can view its key for disk encryption on the Basic Information page.

    ![](https://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/en-US/7450359951/p72793.png)


