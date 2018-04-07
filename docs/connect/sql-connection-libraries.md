---
title: 用于 Microsoft SQL 数据库的连接库 |Microsoft 文档
description: 提供用于启用与 Microsoft SQL Server 和 Azure SQL 数据库，从多种编程语言的客户端的连接的模块下载链接。
author: MightyPen
ms.service: ''
ms.component: connect
ms.suite: sql
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.technology: dbe-data-tier-apps
ms.custom: ''
ms.workload: data-management
ms.topic: article
ms.date: 03/29/2018
ms.author: genemi
ms.openlocfilehash: c6c459949c63dc11308ac5bf042149775950882d
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
# <a name="connection-modules-for-microsoft-sql-databases"></a>Microsoft SQL 数据库的连接模块

这篇文章提供连接模块的下载链接或*驱动程序*，客户端程序可以使用与交互[Microsoft SQL Server](../index.md)，并使用其在云中的双向[AzureSQL 数据库](http://docs.microsoft.com/azure/sql-database/)。 驱动程序是可用于各种编程语言，在以下操作系统上运行：

- Linux (Ubuntu)
- MacOS
- Windows

#### <a name="oop-to-relational-mismatch"></a>OOP-到-关系不匹配

*关系*： 通常用一种面向对象编程 (OOP) 语言编写的客户端程序使用 SQL 驱动程序是多个关系比面向对象的格式返回查询的数据。 C# 使用 ADO.NET 是一个示例。 OOP 关系格式不匹配有时有 OOP 代码更难地编写和理解。

*ORM*： 其他驱动程序或框架中避免这种不匹配的 OOP 格式返回查询的数据。 这些驱动程序工作应为类具有已定义以匹配特定的 SQL 表的数据列。 然后，该驱动程序执行*对象关系映射*(ORM) 类的实例形式返回查询的数据。 Microsoft 的 Entity Framework (EF)，对于 C# 中，和 for Java 的休眠是两个示例。

本文用于单独的章节形成这些两种类型的连接驱动程序。

<a name="anchor-20-drivers-relational-access" />

## <a name="drivers-for-relational-access"></a>关系访问的驱动程序


<!--
Each given Microsoft Download Center page should be enhanced
with a link to the next NEWER version page, on the day that the
original page is no longer the latest because the newer page is being added.
But this policy is not agreed on or observed,
putting the links in the following table at risk for being outdated.

PHP driver in Github.com also uses this FWLink:  http://go.microsoft.com/fwlink/?LinkID=518036 ,
although the FWLink is less precise than is http://github.com/Microsoft/msphpsql/tree/dev#install-unix .
-->

| 语言 | 下载 SQL 驱动程序 |
| :------- | :---------------------- |
| C# | [ADO.NET](http://www.microsoft.com/net/download/)<br /><br />[.NET 核心，适用于 Linux Ubuntu](https://www.microsoft.com/net/core#Ubuntu)<br />[.NET Core, for MacOS](https://www.microsoft.com/net/core#macos)<br />[.NET 核心，适用于 Windows](https://www.microsoft.com/net/core) |
| C++ | [ODBC](./odbc/download-odbc-driver-for-sql-server.md)<br /><br />[OLE DB](./oledb/oledb-driver-for-sql-server-programming.md) |
| Java | [JDBC](./jdbc/download-microsoft-jdbc-driver-for-sql-server.md) |
| Node.js | [Node.js 驱动程序，安装说明](./node-js/step-1-configure-development-environment-for-node-js-development.md) |
| PHP | *操作系统：*<br /><br />[Windows PHP driver](https://www.microsoft.com/download/details.aspx?id=55642)<br />[从 Github 的 Linux 或 macOS PHP 驱动程序](http://github.com/Microsoft/msphpsql/) |
| Python | [pyodbc，安装说明](./python/pyodbc/step-1-configure-development-environment-for-pyodbc-python-development.md)<br />[下载 ODBC](./odbc/download-odbc-driver-for-sql-server.md) |
| Ruby | [Ruby 驱动程序，安装说明](./ruby/step-1-configure-development-environment-for-ruby-development.md)<br />[Ruby 下载页](https://rubyinstaller.org/downloads/) |
| &nbsp; | <br /> |

<a name="anchor-40-drivers-orm-access" />

## <a name="drivers-for-orm-access"></a>ORM 访问的驱动程序


下表列出客户端应用程序用于连接到 Microsoft SQL 数据库的对象关系映射 (ORM) 框架的例子。


| 语言 | ORM 驱动程序下载 |
| :------- | :------------------ |
| C# | [实体框架核心](http://docs.microsoft.com/ef/core/)<br />[实体框架 (6.x 或更高版本)](http://docs.microsoft.com/ef/) |
| Java | [休眠 ORM](http://hibernate.org/orm)|
| PHP | [最强大的 ORM，包含在 Laravel 安装](http://laravel.com/docs/) |
| Node.js | [Sequelize ORM](http://docs.sequelizejs.com) |
| Python | [Django](http://www.djangoproject.com/) |
| Ruby | [Ruby on Rails](http://rubyonrails.org/) |


<a name="anchor-60-build-an-app-webpages" />

## <a name="build-an-app-webpages"></a>生成的应用的网页
[http://aka.ms/sqldev](http://aka.ms/sqldev) 将你带到一组*生成的应用*网页。 网页提供大量组合的编程语言、 操作系统和 SQL 连接驱动程序有关的信息。 生成的应用网页提供的信息包括以下各项：

- 有关如何开始从一开始，对于每个语言 + 操作系统 + 驱动程序组合的详细信息。
    - 安装最新的 SQL 连接驱动程序说明。
- 为每个以下项的代码示例：
    - 对象关系的代码示例。
    - ORM 代码示例。
    - 更快的性能的列存储索引演示。

#### <a name="first-page-of-build-an-app-webpages"></a>第一页，生成的应用的网页
![生成的应用网页，第一页的屏幕截图][image-ref-163-buildanapp-webpages-first-page]

#### <a name="menu-for-java---ubuntu-of-build-an-app-webpages"></a>Java-Ubuntu，生成的应用的网页的菜单
![生成的应用网页，菜单 Java Ubuntu][image-ref-167-buildanapp-webpages-menu-java-ubuntu]

&nbsp;

## <a name="related-links"></a>相关链接
- [代码示例用于连接到 Azure SQL 数据库在云中，使用 Java 和其他语言](http://docs.microsoft.com/azure/sql-database/sql-database-connect-query-java)。

<!-- Image references -->

[image-ref-163-buildanapp-webpages-first-page]: ./media/homepage-sql-connection-drivers/gm-aka-ms-sqldev-choose-language-g21.png
[image-ref-167-buildanapp-webpages-menu-java-ubuntu]: ./media/homepage-sql-connection-drivers/gm-aka-ms-sqldev-java-ubuntu-c31.png
