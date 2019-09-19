# Delete tags {#concept_ohx_xx4_ydb .concept}

This topic describes how to delete tags from an RDS instance when you no longer need the tags or due to adjustments to the instance.

## Limits {#section_lhh_cy4_ydb .section}

-   You can bind or unbind up to five tags at a time.
-   After you unbind a tag from an RDS instance, the tag is deleted if it is not bound to any other instance.

## Procedure {#section_dz4_dy4_ydb .section}

1.  Log on to the [RDS console](https://rdsnew.console.aliyun.com/) and in the left-side navigation pane, click **Instances**.
2.  In tne upper-left corner, select the region where the target RDS instance is located.

    ![选择地域](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7814/156888631536543_en-US.png)

3.  Find the target RDS instance and in the **Actions** column, choose **More** \> **Edit Tag**.
4.  Find the tag you want to delete, and click the **X** button following the tag.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/7972/15688863154154_en-US.png)

5.  Click **Confirm**.

## APIs {#section_hcn_555_jgb .section}

|API|Description|
|---|-----------|
|[RemoveTagsFromResource](../intl.en-US/API Reference/Tag management/RemoveTagsFromResource.md#)|Used to unbind a tag from an RDS instance.|

