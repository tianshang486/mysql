# Quick Start

If you are new to ApsaraDB for RDS, see the following topics to know about ApsaraDB for RDS:

-   [Create an ApsaraDB RDS for MySQL instance](/intl.en-US/RDS MySQL Database/Quick start/Create an ApsaraDB RDS for MySQL instance.md)
-   [Create an ApsaraDB RDS for SQL Server instance](/intl.en-US/RDS SQL Server Database/Quick start/Create an ApsaraDB RDS for SQL Server instance.md)
-   [Create an ApsaraDB RDS for PostgreSQL instance](/intl.en-US/RDS PostgreSQL Database/Quick start/Create an ApsaraDB RDS for PostgreSQL instance.md)
-   [Create an ApsaraDB RDS for PPAS instance](/intl.en-US/RDS PPAS Database/Quick start/Create an ApsaraDB RDS for PPAS instance.md)
-   [Create an ApsaraDB RDS for MariaDB instance](/intl.en-US/RDS MariaDB TX Database/Quick start/Creates an ApsaraDB RDS for MariaDB instance.md)

## Database engines

ApsaraDB for RDS supports the following five database engines:

-   MySQL

    MySQL is the world's most popular open-source database management system. As an important part of the open-source software bundle LAMP \(Linux, Apache, MySQL, and Perl/PHP/Python\), MySQL is widely used for various applications.

    Since the Web 2.0 era, MySQL has been serving as a basis for the underlying infrastructure of Discuz!, a popular BBS software system, and WordPress, a blogging platform. In the Web 3.0 era, leading Internet companies, such as Alibaba Group, Facebook, and Google, have built large-sized, mature database clusters by taking advantage of the advanced flexibility of MySQL.

    ApsaraDB RDS for MySQL is developed based on the MySQL source code branch of Alibaba Cloud. It has withstood traffic bursts from highly concurrent requests and proven its excellent performance and high throughput over years of Double 11, a shopping festival in China. In addition, ApsaraDB RDS for MySQL provides enhanced advanced features, such as read/write splitting, dedicated proxy, and intelligent optimization. For more information, see [Read/write splitting](/intl.en-US/RDS MySQL Database/Database proxy(read/write splitting)/Read/write splitting.md), [Dedicated proxy](/intl.en-US/RDS MySQL Database/Database proxy(read/write splitting)/Dedicated proxy.md), and [DAS overview](/intl.en-US/RDS MySQL Database/Performance optimization and diagnosis (autonomy service)/DAS overview.md).

    Supported MySQL versions are 5.5, 5.6, 5.7, and 8.0.

-   SQL Server

    SQL Server is one of the first commercial database management systems. As an important part of the Windows platform \(IIS + .NET + SQL Server\), SQL Server provides support for a wide range of enterprise applications. SQL Server Management Studio provided with SQL Server offers a complete suite of built-in graphical tools and script editors. You can quickly get started with a variety of database operations by using visual user interfaces \(UIs\).

    ApsaraDB RDS for SQL Server provides the high availability architecture and the capability to [restore data](/intl.en-US/RDS SQL Server Database/Restoration/Restore the data of an ApsaraDB RDS for SQL Server instance.md) to a point in time. This allows ApsaraDB RDS for SQL Server to support various enterprise applications. In addition, ApsaraDB RDS for SQL Server is offered with a valid license. You do not need to pay Microsoft licensing fees.

    Supported SQL Server versions are as follows:

    -   SQL Server 2008 R2
    -   SQL Server 2012 Web, 2012 SE, and 2012 EE
    -   SQL Server 2016 Web, 2016 SE, and 2016 EE
    -   SQL Server 2017 SE and 2017 EE
    -   SQL Server 2019 SE
-   PostgreSQL

    PostgreSQL is the world's most advanced open-source database management system. As the ancestor of academic relational database management systems, PostgreSQL provides full compliance with SQL specifications and robust support for diverse data formats, such as JSON, IP, and geometric data. These data formats are not supported in most of the commercial database management systems that are available on the market today.

    ApsaraDB RDS for PostgreSQL supports basic features such as transactions, subqueries, Multi-Version Concurrency Control \(MVCC\), and data integrity check. It also supports advanced features such as high availability, backup, and restoration. These features make database O&M easier.

    Supported PostgreSQL versions are 9.4, 10, 11, and 12.

-   PPAS

    Postgres Plus Advanced Server \(PPAS\) is a stable, secure, and scalable enterprise-class relational database management system that is designed based on PostgreSQL. It provides enhanced performance, application solutions, and compatibility. You can run various enterprise applications, including Oracle applications, on PPAS stably at low costs.

    ApsaraDB RDS for PPAS provides features such as account management, resource monitoring, backup and restoration, and security control. These features are under continuous improvement, and more features are under development to adapt to ApsaraDB RDS for PPAS.

    Supported PPAS versions are 9.3 and 10.

-   MariaDB TX

    MariaDB is a branch of MySQL. It is maintained mainly by the open source community and follows GNU General Public License \(GPL\) specifications. MariaDB is designed to be fully compatible with MySQL, including the API and command line interface \(CLI\), with an intention to substitute MySQL. MariaDB 10.0.9 and later use the XtraDB storage engine \(code-named Aria\) to replace the InnoDB storage engine that is used with MySQL.

    MariaDB TX is compatible with the Procedural Language/SQL \(PL/SQL\) language offered by Oracle Corporation. It is a transactional database platform based on MariaDB Server, MariaDB MaxScale, and MariaDB Cluster. This enterprise-oriented platform integrates database connectors and management tools and provides technical support and expert services.

    Only MariaDB TX 10.3 is supported.


