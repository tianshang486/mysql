# 阿里云在RDS遭受攻击时提供什么安全服务 {#concept_265539 .concept}

当您的数据库的公网访问遇到以下情况时，阿里云的安全体系认为数据库受到攻击，会自动启动流量清洗或黑洞处理。

## 流量清洗 {#section_8ys_l6k_ope .section}

以下任一条件将会触发流量清洗（针对公网入流量）。

-   PPS（Package Per Second ）达到3万；
-   BPS（Bits per Second）达到180Mb；
-   每秒新建并发连接达到1万；
-   激活连接数达到1万；
-   非激活链接数达到10万。

**说明：** 此时RDS仍然可以被正常访问。

## 黑洞处理 {#section_xvi_ewo_y2r .section}

以下任一条件将会触发黑洞（针对公网入流量）。

-   BPS（Bits per Second）达到2Gb；
-   流量清洗无效。

**说明：** 触发黑洞后RDS在4小时内无法访问。

