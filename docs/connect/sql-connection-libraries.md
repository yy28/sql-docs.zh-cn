---
title: Microsoft SQL 数据库的连接库 |Microsoft Docs
description: 提供用于支持连接到 Microsoft SQL Server 和 Azure SQL 数据库，从各种客户端编程语言的模块下载链接。
author: MightyPen
ms.prod: sql
ms.technology: ''
ms.custom: ''
ms.topic: article
ms.date: 06/18/2018
ms.author: genemi
ms.openlocfilehash: 4286a9a1fcc2eff3becd483d658b371bb6452032
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 11/13/2018
ms.locfileid: "51600367"
---
# <a name="connection-modules-for-microsoft-sql-databases"></a>Microsoft SQL 数据库的连接模块

本文提供了连接模块的下载链接或*驱动程序*的客户端程序可以使用用来与交互[Microsoft SQL Server](../relational-databases/database-features.md)，并使用在云中孪生[AzureSQL 数据库](https://docs.microsoft.com/azure/sql-database/)。 驱动程序是可用于多种编程语言，在以下操作系统上运行：

- Linux (Ubuntu)
- MacOS
- Windows

#### <a name="oop-to-relational-mismatch"></a>OOP 到关系不匹配

*关系*： 通常以面向对象编程 (OOP) 语言编写的客户端程序使用 SQL 驱动程序，它是比面向对象的多个关系的格式返回查询的数据。 C# 使用 ADO.NET 是一个示例。 OOP 关系格式不匹配有时也 OOP 代码编写和理解更加困难。

*ORM*： 其他驱动程序或框架中避免不匹配的 OOP 格式返回查询的数据。 这些驱动程序处理应为类，已定义以匹配特定的 SQL 表的数据列。 然后，该驱动程序执行*对象关系映射*(ORM) 作为类的实例返回查询的数据。 Microsoft 的 Entity Framework (EF)，适用于 C# 和 java，休眠是两个示例。

本文重点关注到这两种连接驱动程序的各单独章节。

<a name="anchor-20-drivers-relational-access" />

## <a name="drivers-for-relational-access"></a>驱动程序的关系访问


<!--
Each given Microsoft Download Center page should be enhanced
with a link to the next NEWER version page, on the day that the
original page is no longer the latest because the newer page is being added.
But this policy is not agreed on or observed,
putting the links in the following table at risk for being outdated.

PHP driver in Github.com also uses this FWLink:  https://go.microsoft.com/fwlink/?LinkID=518036 ,
although the FWLink is less precise than is https://github.com/Microsoft/msphpsql/tree/dev#install-unix .
-->

| “报表” | 下载 SQL 驱动程序 |
| :------- | :---------------------- |
| C# | [ADO.NET](https://www.microsoft.com/net/download/)<br /><br />[.NET core，适用于 Linux Ubuntu](https://www.microsoft.com/net/core#Ubuntu)<br />[用于 MacOS 的.NET core](https://www.microsoft.com/net/core#macos)<br />[用于 Windows 的.NET core](https://www.microsoft.com/net/core) |
| C++ | [ODBC](./odbc/download-odbc-driver-for-sql-server.md)<br /><br />[OLE DB](./oledb/download-oledb-driver-for-sql-server.md) |
| Java | [JDBC](./jdbc/download-microsoft-jdbc-driver-for-sql-server.md) |
| Node.js | [安装说明的 Node.js 驱动程序](./node-js/step-1-configure-development-environment-for-node-js-development.md) |
| PHP | [PHP](./php/download-drivers-php-sql-server.md) |
| Python | [pyodbc 安装说明](./python/pyodbc/step-1-configure-development-environment-for-pyodbc-python-development.md)<br />[下载 ODBC](./odbc/download-odbc-driver-for-sql-server.md) |
| Ruby | [Ruby 驱动程序，安装说明](./ruby/step-1-configure-development-environment-for-ruby-development.md)<br />[Ruby 下载页](https://rubyinstaller.org/downloads/) |
| &nbsp; | <br /> |

<a name="anchor-40-drivers-orm-access" />

## <a name="drivers-for-orm-access"></a>ORM 访问驱动程序


下表列出了客户端应用程序使用连接到 Microsoft SQL 数据库的对象关系映射 (ORM) 框架的示例。


| “报表” | ORM 驱动程序下载 |
| :------- | :------------------ |
| C# | [Entity Framework Core](https://docs.microsoft.com/ef/core/)<br />[实体框架 (6.x 或更高版本)](https://docs.microsoft.com/ef/) |
| Java | [Hibernate ORM](https://hibernate.org/orm)|
| PHP | [最强大的 ORM，Laravel 安装中包括](https://laravel.com/docs/) |
| Node.js | [Sequelize ORM](https://docs.sequelizejs.com) |
| Python | [Django](https://www.djangoproject.com/) |
| Ruby | [Ruby on Rails](https://rubyonrails.org/) |


<a name="anchor-60-build-an-app-webpages" />

## <a name="build-an-app-webpages"></a>生成一个应用网页
[https://aka.ms/sqldev](https://aka.ms/sqldev) 将您带到一系列*生成的应用*网页。 网页提供有关大量组合的编程语言、 操作系统和 SQL 连接驱动程序的信息。 生成一个应用网页提供的信息包括以下各项：

- 有关如何开始从一开始，为每个语言、 操作系统和驱动程序组合的详细信息。
    - 有关安装最新的 SQL 连接驱动程序的说明。
- 以下各项的每个代码示例：
    - 对象关系的代码示例。
    - ORM 代码示例。
    - 列存储索引的更快的性能的演示。

#### <a name="first-page-of-build-an-app-webpages"></a>第一页，生成的应用网页
![生成的应用的网页，第一页屏幕截图][image-ref-163-buildanapp-webpages-first-page]

#### <a name="menu-for-java---ubuntu-of-build-an-app-webpages"></a>用于 Java 的 Ubuntu，生成的应用的网页的菜单
![生成的应用的网页，菜单 Java Ubuntu][image-ref-167-buildanapp-webpages-menu-java-ubuntu]

&nbsp;

## <a name="related-links"></a>相关链接
- [代码示例用于连接到 Azure SQL 数据库中使用 Java 和其他语言在云中](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-java)。

<!-- Image references -->

[image-ref-163-buildanapp-webpages-first-page]: ./media/homepage-sql-connection-drivers/gm-aka-ms-sqldev-choose-language-g21.png
[image-ref-167-buildanapp-webpages-menu-java-ubuntu]: ./media/homepage-sql-connection-drivers/gm-aka-ms-sqldev-java-ubuntu-c31.png
