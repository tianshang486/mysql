# How do I find the public IP address of my computer that needs to connect to RDS for MySQL or MariaDB TX? {#concept_qfv_2g5_42b .concept}

## Problem {#section_f4x_fg5_42b .section}

-   You have added the public IP address of your computer to the IP address whitelist of the RDS instance. However, your computer cannot access the instance while other devices can.
-   You have added the public IP address of your computer to the IP address whitelist of the RDS instance, but your computer cannot access the instance unless you set the IP address whitelist to 0.0.0.0/0 or your company's address range.

If either of the preceding problems occurs, the public IP address you add to the whitelist of the RDS instance may be incorrect. You need to find the real public IP address of your computer.

**Note:** This topic applies only when you access the RDS instance from a device other than an ECS instance. If you access the RDS instance from an ECS instance, you can find the public and private IP addresses of the ECS instance on the ECS console.

## Precautions {#section_nby_fjp_yfb .section}

If the public IP address of your computer is not fixed and your RDS instance is used in a production environment, we recommend that you use a private connection instead or configure an appropriate IP address range in the whitelist. This is to ensure that the connection remains available even if the public IP address of your computer changes.

## Procedure {#section_ffh_njp_yfb .section}

1.  Add your company's public IP address range or 0.0.0.0/0 to the IP address whitelist of the RDS instance. For more information, see [Configure a whitelist](../../../../intl.en-US/Quick Start for MySQL/Initial configuration/Configure a whitelist.md#).

    **Note:** 0.0.0.0/0 indicates that all devices are allowed to access the RDS instance. Use the address with caution. If you add 0.0.0.0/0 to the whitelist, we recommend that you remote it from the whitelist immediately once you no longer need it.

2.  Connect your computer to the RDS instance by using a client or the command line interface \(CLI\).

    ``` {#codeblock_vka_9wd_rdj}
    mysql -h*<RDS Connection address\>* -u*<Username\>* -p*<Password\>* -P3306
    ```

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8224/156402041433319_en-US.jpg)

3.  Check the process information.

    ``` {#codeblock_aoz_0qq_po2}
    show processlist
    ```

    As shown in the following figure, the value of **Host** for the **show processlist** record is the real public IP address of your computer.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/8224/156402041533320_en-US.jpg)

4.  Remove 0.0.0.0/0 from the whitelist and add the real public IP address of your computer to the whitelist.

