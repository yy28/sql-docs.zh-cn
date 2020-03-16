---
title: 用于 Microsoft SQL 数据库的连接库 | Microsoft Docs
description: 提供模块的下载链接，这些模块支持使用各种客户端编程语言连接到 Microsoft SQL Server 和 Azure SQL 数据库。
author: RothJa
ms.prod: sql
ms.technology: ''
ms.custom: ''
ms.topic: article
ms.date: 03/05/2020
ms.author: JRoth
ms.openlocfilehash: eb842769490b521b248ed4114953b8d828fa80d3
ms.sourcegitcommit: 4baa8d3c13dd290068885aea914845ede58aa840
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "79286401"
---
# <a name="connection-modules-for-microsoft-sql-databases"></a>Microsoft SQL 数据库的连接模块

本文提供了连接模块或驱动程序  的下载链接，客户端程序可以使用这些链接与 [Microsoft SQL Server](../relational-databases/database-features.md) 及其在云中的孪生平台 [Azure SQL 数据库](https://docs.microsoft.com/azure/sql-database/)进行交互。 驱动程序适用于多种编程语言，在以下操作系统上运行：

- Linux
- MacOS
- Windows

**OOP 与关系不匹配：**

*关系*：使用面向对象的编程 (OOP) 语言编写的客户端程序通常使用 SQL 驱动程序，这些驱动程序返回的查询数据的格式更倾向于关系，而不是面向对象。 使用 ADO.NET 的 C# 就是一个示例。 OOP 关系格式不匹配有时会使 OOP 代码更难以编写和理解。

*ORM*：其他驱动程序或框架以 OOP 格式返回查询的数据，避免了不匹配。 这些驱动程序的工作原理是：使定义的类与特定 SQL 表的数据列相匹配。 然后，该驱动程序将执行对象关系映射  (ORM)，以将查询的数据作为类的实例返回。 如以下两个示例：适用于 C# 的 Microsoft 实体框架 (EF) 和适用于 Java 的 Hibernate。

本文将分别讨论这两种连接驱动程序。

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

| 语言 | 下载 SQL 驱动程序 |
| :------- | :---------------------- |
| C# | [ADO.NET](https://www.microsoft.com/net/download/)<br />[Microsoft.Data.SqlClient](https://www.nuget.org/packages/Microsoft.Data.SqlClient/)<br /><br />[适用于以下系统的 .NET Core：Linux-Ubuntu、macOS、Windows](https://dotnet.microsoft.com/download) |
| C++ | [ODBC](./odbc/download-odbc-driver-for-sql-server.md)<br /><br />[OLE DB](./oledb/download-oledb-driver-for-sql-server.md) |
| Java | [JDBC](./jdbc/download-microsoft-jdbc-driver-for-sql-server.md) |
| Node.js | [Node.js 驱动程序，安装说明](./node-js/step-1-configure-development-environment-for-node-js-development.md) |
| PHP | [PHP](./php/download-drivers-php-sql-server.md) |
| Python | [pyodbc 安装说明](./python/pyodbc/step-1-configure-development-environment-for-pyodbc-python-development.md)<br />[下载 ODBC](./odbc/download-odbc-driver-for-sql-server.md) |
| Ruby | [Ruby 驱动程序，安装说明](./ruby/step-1-configure-development-environment-for-ruby-development.md)<br />[Ruby 下载页](https://rubyinstaller.org/downloads/) |
| &nbsp; | <br/> |

<a name="anchor-40-drivers-orm-access" />

## <a name="drivers-for-orm-access"></a>用于 ORM 访问的驱动程序

下表列出了客户端应用程序用于连接到 Microsoft SQL 数据库的对象关系映射 (ORM) 框架的示例。

| 语言 | ORM 驱动程序下载 |
| :------- | :------------------ |
| C# | [Entity Framework Core](https://docs.microsoft.com/ef/core/)<br />[实体框架（6.x 或更高版本）](https://docs.microsoft.com/ef/) |
| Java | [Hibernate ORM](https://hibernate.org/orm)|
| PHP | [Eloquent ORM，包含在 Laravel 安装中](https://laravel.com/docs/) |
| Node.js | [Sequelize ORM](https://docs.sequelizejs.com) |
| Python | [Django](https://www.djangoproject.com/) |
| Ruby | [Ruby on Rails](https://rubyonrails.org/) |
| &nbsp; | <br/> |

<a name="anchor-60-build-an-app-webpages" />

## <a name="build-an-app-webpages"></a>“生成应用程序”网页
可以通过 [https://aka.ms/sqldev](https://aka.ms/sqldev)  转到一组“生成应用程序”  网页。 网页提供有关编程语言、操作系统和 SQL 连接驱动程序的多种组合的信息。 “生成应用程序”网页提供的信息包括以下各项：

- 有关语言 + 操作系统 + 驱动程序的各组合的入门方式的详细信息。
    - 安装最新 SQL 连接驱动程序的说明。
- 以下各项的代码示例：
    - 对象关系代码示例。
    - ORM 代码示例。
    - 列存储索引演示如何实现更快的性能。

**“生成应用程序”网页的第一页：**  
![“生成应用程序”网页的第一页屏幕截图](media/homepage-sql-connection-drivers/gm-aka-ms-sqldev-choose-language-g21.png)

**“生成应用程序”网页的“Java - Ubuntu”菜单**  
![“生成应用程序”网页的 Java Ubuntu 菜单](media/homepage-sql-connection-drivers/gm-aka-ms-sqldev-java-ubuntu-c31.png)

&nbsp;

## <a name="related-links"></a>相关链接
- [使用 Java 和其他语言连接到云中的 Azure SQL 数据库的代码示例](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-java)。

<!--
Image references, **obsolete** markdown syntax alternative:

![Build-an-app webpages, first page screenshot][image-ref-163-buildanapp-webpages-first-page]
![Build-an-app webpages, menu Java Ubuntu][image-ref-167-buildanapp-webpages-menu-java-ubuntu]

[image-ref-163-buildanapp-webpages-first-page]: ./media/homepage-sql-connection-drivers/gm-aka-ms-sqldev-choose-language-g21.png
[image-ref-167-buildanapp-webpages-menu-java-ubuntu]: ./media/homepage-sql-connection-drivers/gm-aka-ms-sqldev-java-ubuntu-c31.png
-->
