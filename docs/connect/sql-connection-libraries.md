---
title: Microsoft SQL 数据库的连接库 |Microsoft Docs
description: 提供了可从各种客户端编程语言连接到 Microsoft SQL Server 和 Azure SQL 数据库的模块的下载链接。
author: MightyPen
ms.prod: sql
ms.technology: ''
ms.custom: ''
ms.topic: article
ms.date: 06/18/2018
ms.author: genemi
ms.openlocfilehash: 71254b937c4c0173af9e1549efb98a0b42f65e02
ms.sourcegitcommit: 66dbc3b740f4174f3364ba6b68bc8df1e941050f
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 11/05/2019
ms.locfileid: "73632819"
---
# <a name="connection-modules-for-microsoft-sql-databases"></a>Microsoft SQL 数据库的连接模块

本文提供了一些链接，这些链接指向客户端程序可以用来与[Microsoft SQL Server](../relational-databases/database-features.md)进行交互的连接模块或*驱动程序*，并将其克隆到云[Azure SQL 数据库](https://docs.microsoft.com/azure/sql-database/)中。 驱动程序适用于多种编程语言，在以下操作系统上运行：

- Linux
- MacOS
- Windows

#### <a name="oop-to-relational-mismatch"></a>OOP 到关系不匹配

*关系*：以面向对象编程（OOP）语言编写的客户端程序通常使用 SQL 驱动程序，该驱动程序以比面向对象更高的格式返回查询的数据。 C#使用 ADO.NET 是一个示例。 OOP 关系格式不匹配有时会使 OOP 代码更难以编写和理解。

*ORM*：其他驱动程序或框架以 OOP 格式返回查询的数据，避免不匹配。 这些驱动程序的工作原理是：定义了类，使其与特定 SQL 表的数据列相匹配。 然后，驱动程序执行*对象关系映射*（ORM），以将查询的数据作为类的实例返回。 适用于的C#Microsoft 实体框架（EF）和 Java 休眠，是两个示例。

本文介绍这两种连接驱动程序的各个部分都用于。

<a name="anchor-20-drivers-relational-access" />

## <a name="drivers-for-relational-access"></a>用于关系访问的驱动程序


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
| C# | [ADO.NET](https://www.microsoft.com/net/download/)<br />[Microsoft.Data.SqlClient](https://www.nuget.org/packages/Microsoft.Data.SqlClient/)<br /><br />[.NET Core，适用于 Linux-Ubuntu](https://www.microsoft.com/net/core#Ubuntu)<br />[.NET Core，适用于 MacOS](https://www.microsoft.com/net/core#macos)<br />[.NET Core，适用于 Windows](https://www.microsoft.com/net/core) |
| C++ | [ODBC](./odbc/download-odbc-driver-for-sql-server.md)<br /><br />[OLE DB](./oledb/download-oledb-driver-for-sql-server.md) |
| Java | [JDBC](./jdbc/download-microsoft-jdbc-driver-for-sql-server.md) |
| Node.js | [Node.js 驱动程序，安装说明](./node-js/step-1-configure-development-environment-for-node-js-development.md) |
| PHP | [PHP](./php/download-drivers-php-sql-server.md) |
| Python | [pyodbc 安装说明](./python/pyodbc/step-1-configure-development-environment-for-pyodbc-python-development.md)<br />[下载 ODBC](./odbc/download-odbc-driver-for-sql-server.md) |
| Ruby | [Ruby 驱动程序，安装说明](./ruby/step-1-configure-development-environment-for-ruby-development.md)<br />[Ruby 下载页面](https://rubyinstaller.org/downloads/) |
| &nbsp; | <br /> |

<a name="anchor-40-drivers-orm-access" />

## <a name="drivers-for-orm-access"></a>用于 ORM 访问的驱动程序


下表列出了客户端应用程序用来连接到 Microsoft SQL 数据库的对象关系映射（ORM）框架的示例。


| “报表” | ORM 驱动程序下载 |
| :------- | :------------------ |
| C# | [Entity Framework Core](https://docs.microsoft.com/ef/core/)<br />[实体框架（1.x 或更高版本）](https://docs.microsoft.com/ef/) |
| Java | [Hibernate ORM](https://hibernate.org/orm)|
| PHP | [Eloquent 包含在 Laravel 安装中的 ORM](https://laravel.com/docs/) |
| Node.js | [Sequelize ORM](https://docs.sequelizejs.com) |
| Python | [Django](https://www.djangoproject.com/) |
| Ruby | [Ruby on Rails](https://rubyonrails.org/) |


<a name="anchor-60-build-an-app-webpages" />

## <a name="build-an-app-webpages"></a>生成-应用网页
[https://aka.ms/sqldev](https://aka.ms/sqldev)转到一组生成-*应用*网页。 网页提供有关编程语言、操作系统和 SQL 连接驱动程序的多种组合的信息。 "生成-应用" 网页提供的信息包括以下各项：

- 有关如何开始从语言 + 操作系统 + 驱动程序的每个组合开始的详细信息。
    - 安装最新 SQL 连接驱动程序的说明。
- 以下每个项的代码示例：
    - 对象关系代码示例。
    - ORM 代码示例。
    - 列存储索引演示，以实现更快的性能。

#### <a name="first-page-of-build-an-app-webpages"></a>"生成-应用" 网页的第一页
![生成-应用网页，第一页屏幕截图][image-ref-163-buildanapp-webpages-first-page]

#### <a name="menu-for-java---ubuntu-of-build-an-app-webpages"></a>用于 "生成-应用" 网页的 Java-Ubuntu 菜单
![生成-应用网页，菜单 Java Ubuntu][image-ref-167-buildanapp-webpages-menu-java-ubuntu]

&nbsp;

## <a name="related-links"></a>相关链接
- [用于利用 Java 和其他语言连接到云中的 AZURE SQL 数据库的代码示例](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-java)。

<!-- Image references -->

[image-ref-163-buildanapp-webpages-first-page]: ./media/homepage-sql-connection-drivers/gm-aka-ms-sqldev-choose-language-g21.png
[image-ref-167-buildanapp-webpages-menu-java-ubuntu]: ./media/homepage-sql-connection-drivers/gm-aka-ms-sqldev-java-ubuntu-c31.png
