---
title: SQL 客户端编程主页 |Microsoft Docs
description: 包含带批注链接的中心页面，这些链接指向用于连接到 SQL Server 或 Azure SQL 数据库的多种语言和操作系统组合的下载和文档。
author: MightyPen
ms.date: 11/07/2018
ms.prod: sql
ms.prod_service: connectivity
ms.custom: ''
ms.technology: connectivity
ms.topic: conceptual
ms.reviewer: v-daveng
ms.author: genemi
ms.openlocfilehash: 6961f8c23b4acfd787958cc9a160faf88362b54c
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/16/2019
ms.locfileid: "72451850"
---
# <a name="homepage-for-client-programming-to-microsoft-sql-server"></a>Microsoft SQL Server 客户端编程的主页


欢迎在我们的主页上了解有关客户端编程的信息，以便与 Microsoft SQL Server 和云中的 Azure SQL 数据库交互。 本文提供了以下信息：

- 列出并描述可用的语言和驱动程序组合。
    - 提供适用于 Linux （Ubuntu 和其他）、MacOS 和 Windows 的操作系统的信息。
- 提供每个组合的详细文档的链接。
- 显示某些语言的分层文档的区域和子区域（如果适用）。


#### <a name="azure-sql-database"></a>Azure SQL Database

在任何给定的语言中，连接到 SQL Server 的代码与用于连接到 Azure SQL 数据库的代码几乎完全相同。

有关连接到 Azure SQL 数据库的连接字符串的详细信息，请参阅：

- [使用 .Net Core （C#）查询 Azure SQL 数据库](/azure/sql-database/sql-database-connect-query-dotnet-core)。
- 目录中上一篇附近的其他 Azure SQL 数据库，关于其他语言。 例如，请参阅[使用 PHP 查询 AZURE SQL 数据库](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-php)。


#### <a name="build-an-app-webpages"></a>生成-应用网页

我们的*生成-应用*网页以替代格式显示代码示例以及配置信息。 有关详细信息，请参阅本文后面的[标记为 "*生成-应用" 网站*的部分](#an-204-aka-ms-sqldev)。



<a name="an-050-languages-clients" />

## <a name="languages-and-drivers-for-client-programs"></a>客户端程序的语言和驱动程序


在下表中，每个语言图像都是一个链接，指向有关将语言与 SQL Server 结合使用的详细信息。 每个链接可跳转到本文的后面部分。

| &nbsp; | &nbsp; | &nbsp; |
| :-- | :-- | :-- |
| &nbsp; [![C#徽标][image-ref-320-csharp]](#an-110-ado-net-docu) | &nbsp; [![ORM 实体框架，.NET Framework][image-ref-333-ef]](#an-116-csharp-ef-orm) | &nbsp; [![Java 徽标][image-ref-330-java]](#an-130-jdbc-docu) |
| &nbsp; [![Node .js 徽标][image-ref-340-node]](#an-140-node-js-docu) | &nbsp; [`ODBC for C++`  ](#an-160-odbc-cpp-docu)<br/>[![cpp-big-plus][image-ref-322-cpp]](#an-160-odbc-cpp-docu) | &nbsp; [![PHP 徽标][image-ref-360-php]](#an-170-php-docu) |
| &nbsp; [![Python 徽标][image-ref-370-python]](#an-180-python-docu) | &nbsp; [![Ruby 徽标][image-ref-380-ruby]](#an-190-ruby-docu) | &nbsp; ... |
| &nbsp; | &nbsp; | <br />|


#### <a name="downloads-and-installs"></a>下载和安装

以下文章专门介绍如何下载和安装各种 SQL 连接驱动程序，以供编程语言使用：

- [SQL Server 驱动程序](sql-server-drivers.md)



<a name="an-110-ado-net-docu" />

## <a name="c-logoimage-ref-320-csharp-c-using-adonet"></a>![C#徽标键][image-ref-320-csharp] C#使用 ADO.NET

.NET 托管语言（例如C#和 Visual Basic）是最常见的 ADO.NET 用户。 *ADO.NET*是 .NET Framework 类的子集的随意名称。

#### <a name="code-examples"></a>代码示例

|||
| :-- | :-- |
| [使用 ADO.NET 连接到 SQL 的概念证明](./ado-net/step-3-connect-sql-ado-net.md) | 一个小代码示例，重点介绍如何连接和查询 SQL Server。 |
| [使用 ADO.NET 实现对 SQL 的弹性连接](./ado-net/step-4-connect-resiliently-sql-ado-net.md) | 在代码示例中重试逻辑，因为连接有时会在连接丢失时出现。<br /><br />重试逻辑适用于通过 internet 维护的连接到任何云数据库（例如 Azure SQL 数据库）。 |
| [Azure SQL 数据库：演示如何在 Windows/Linux/macOS 上使用 .NET Core 来创建C#程序、进行连接和查询](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-dotnet-core) | Azure SQL 数据库示例。 |
| [生成-应用： C#、ADO.NET、Windows](https://www.microsoft.com/sql-server/developer-get-started/csharp/win/) | 配置信息和代码示例。 |
| &nbsp; | <br /> |

#### <a name="documentation"></a>文档

|||
| :-- | :-- |
| [C#使用 ADO.NET](./ado-net/index.md)| 文档的根。 |
| [命名空间： System.web](https://docs.microsoft.com/dotnet/api/system.data) | 用于 ADO.NET 的一组类。 |
| [命名空间：System.Data.SqlClient](https://docs.microsoft.com/dotnet/api/system.data.SqlClient) | 最直接位于 ADO.NET 中心的类集。 |
| &nbsp; | <br /> |



<a name="an-116-csharp-ef-orm" />

## <a name="entity-framework-logoimage-ref-333-ef-entity-framework-ef-with-cx23"></a>![实体框架徽标][image-ref-333-ef] 实体框架（EF）与 C&#x23;

实体框架（EF）提供对象关系映射（ORM）。 通过 ORM，你可以更轻松地使用面向对象的编程（OOP）源代码来操作从关系 SQL 数据库中检索的数据。

EF 具有与以下技术的直接或间接关系：

- .NET Framework
- [LINQ to SQL](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/linq/)或[LINQ to Entities](https://docs.microsoft.com/dotnet/framework/data/adonet/ef/language-reference/linq-to-entities)
- 语言语法增强功能，例如中  C#的 => 运算符。
- 为映射到 SQL 数据库中的表的类生成源代码的便利程序。 例如， [edmgen.exe](https://docs.microsoft.com/dotnet/framework/data/adonet/ef/edm-generator-edmgen-exe)。


#### <a name="original-ef-and-new-ef"></a>原始 EF 和新 EF

[实体框架的起始页](https://docs.microsoft.com/ef/)介绍了 EF，其中包含类似于以下内容的说明：

- 实体框架是一种对象关系映射程序（O/RM），它使 .NET 开发人员能够使用 .NET 对象处理数据库。 开发人员无需再像往常一样编写大部分数据访问源代码。

*实体框架*是由两个单独的源代码分支共享的名称。 一个 EF 分支更旧，其源代码现在可以由公共维护。 另一个 EF 是新的。 下面介绍了这两个 EFs：

|     |     |
| :-- | :-- |
| [EF 6.x](https://docs.microsoft.com/ef/ef6/) | Microsoft 首次发布 EF 于2008年8月。 2015年3月，Microsoft 宣布 EF 1.x 是 Microsoft 要开发的最终版本。 Microsoft 已将源代码发布到公共域。<br /><br />最初 EF 是 .NET Framework 的一部分。 但已从 .NET Framework 中删除 EF 1.x。<br /><br />[Github 上的 EF 1.x 源代码（存储库中的*aspnet/EntityFramework6* ）](https://github.com/aspnet/EntityFramework6) |
| [EF Core](https://docs.microsoft.com/ef/core/) | Microsoft 在2016年6月发布了新开发的 EF Core。 EF Core 旨在提供更好的灵活性和可移植性。 EF Core 可以在仅 Microsoft Windows 以外的操作系统上运行。 除 Microsoft SQL Server 和其他关系数据库外，EF Core 可以与数据库进行交互。<br /><br />**C&#x23;代码示例：**<br />[Entity Framework Core 入门](https://docs.microsoft.com/ef/core/get-started/index)<br />[使用现有数据库的 .NET Framework 上的 EF Core 入门](https://docs.microsoft.com/ef/core/get-started/full-dotnet/existing-db) |
| &nbsp; | <br /> |

EF 和相关技术非常强大，为想要掌握整个领域的开发人员了解这一点非常重要。

&nbsp;



<a name="an-130-jdbc-docu" />

## <a name="java-logoimage-ref-330-java-java-and-jdbc"></a>![Java 徽标][image-ref-330-java] Java 和 JDBC

Microsoft 提供了一个 Java Database Connectivity （JDBC）驱动程序用于 SQL Server （当然，也可以与 Azure SQL 数据库配合使用）。 它是 Type 4 JDBC 驱动程序，通过标准 JDBC 应用程序编程接口 (API) 提供数据库连接。

#### <a name="code-examples"></a>代码示例

|||
| :-- | :-- |
| [代码示例](./jdbc/code-samples/index.md) | 介绍数据类型、结果集和大型数据的代码示例。 |
| [连接 URL 示例](./jdbc/connection-url-sample.md) | 描述如何使用连接 URL 连接到 SQL Server。 然后使用它来使用 SQL 语句检索数据。 |
| [数据源示例](./jdbc/data-source-sample.md) | 描述如何使用数据源连接到 SQL Server。 然后，使用存储过程检索数据。 |
| [使用 Java 查询 Azure SQL 数据库](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-java) | Azure SQL 数据库示例。 |
| [使用 Ubuntu 上的 SQL Server 创建 Java 应用](https://www.microsoft.com/sql-server/developer-get-started/java/ubuntu/) | 配置信息和代码示例。 |
| &nbsp; | <br /> |

#### <a name="documentation"></a>文档

JDBC 文档包含以下主要方面：

|||
| :-- | :-- |
| [Java Database Connectivity （JDBC）](./jdbc/index.md) | JDBC 文档的根。 |
| [参考](./jdbc/reference/index.md) | 接口、类和成员。 |
| [JDBC SQL 驱动程序编程指南](./jdbc/programming-guide-for-jdbc-sql-driver.md) | 配置信息和代码示例。 |
| &nbsp; | <br /> |



<a name="an-140-node-js-docu" />

## <a name="nodejs-logoimage-ref-340-node-nodejs"></a>![Node.js 徽标][image-ref-340-node] Node.js

利用 Node.js，你可以从 Windows、Linux 或 Mac 连接到 SQL Server。 [此处](./node-js/index.md)是 node.js 文档的根目录。

用于 SQL Server 的 node.js 连接驱动程序在 JavaScript 中实现。 驱动程序使用 TDS 协议，SQL Server 的所有新式版本都支持该协议。 该驱动程序是一个开源项目，[在 Github 上提供](https://tediousjs.github.io/tedious/)。

#### <a name="code-examples"></a>代码示例

|||
| :-- | :-- |
| [使用 Node.js 连接到 SQL 的概念证明](./node-js/step-3-proof-of-concept-connecting-to-sql-using-node-js.md) | 用于连接到 SQL Server 和执行查询的 Bare 源代码。 |
| [Azure SQL 数据库：使用 node.js 进行查询](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-nodejs) | 云中的 Azure SQL 数据库的示例。 |
| [创建要在 macOS 上使用 SQL Server 的 node.js 应用](https://www.microsoft.com/sql-server/developer-get-started/node/mac/) | 配置信息和代码示例。 |
| &nbsp; | <br /> |



<a name="an-160-odbc-cpp-docu" />

## <a name="odbc-for-c"></a>ODBC forC++ 

![ODBC 徽标][image-ref-350-odbc] ![cpp-big-plus][image-ref-322-cpp]

开放式数据库连接（ODBC）是在二十世纪九十年代开发的，它早于 .NET Framework。 ODBC 旨在独立于任何特定的数据库系统，并且独立于操作系统。

多年来，许多 ODBC 驱动程序已由 Microsoft 内部和外部的组创建和发布。 驱动程序的范围涉及多个客户端编程语言。 数据目标的列表在 SQL Server 的范围之外。

其他一些连接驱动程序在内部使用 ODBC。

#### <a name="code-example"></a>代码示例

- [使用 ODBC 的 C++ 代码示例](../odbc/reference/sample-odbc-program.md)

#### <a name="documentation-outline"></a>文档大纲

本部分中的 ODBC 内容重点介绍如何从C++访问 SQL Server 或 Azure SQL 数据库。 下表列出了 ODBC 的主要文档的大致概述。


| 区域 | 区域 | 描述 |
| :--- | :------ | :---------- |
| [ODBC forC++](./odbc/index.md) | 文档的根。 |
| [Linux-Mac](./odbc/linux-mac/index.md) | &nbsp; | 有关在 Linux 或 MacOS 操作系统上使用 ODBC 的信息。 |
| [Windows](./odbc/windows/index.md)     | &nbsp; | 有关在 Windows 操作系统上使用 ODBC 的信息。 |
| [管理](../odbc/admin/index.md) | &nbsp; | 用于管理 ODBC 数据源的管理工具。 |
| [Microsoft](../odbc/microsoft/index.md)  | &nbsp; | Microsoft 创建和提供的各种 ODBC 驱动程序。 |
| [概念和参考](../odbc/reference/index.md) | &nbsp; | 除传统引用外，有关 ODBC 接口的概念信息。 |
| &nbsp; " | [附录](../odbc/reference/appendixes/index.md)    | 状态转换表、ODBC 游标库等。 |
| &nbsp; " | [开发应用](../odbc/reference/develop-app/index.md)  | 函数、句柄和更多内容。 |
| &nbsp; " | [开发驱动程序](../odbc/reference/develop-driver/index.md) | 如果有专用数据源，如何开发自己的 ODBC 驱动程序。 |
| &nbsp; " | [安装](../odbc/reference/install/index.md) | ODBC 安装、子项等。 |
| &nbsp; " | [语法](../odbc/reference/syntax/index.md)   | 用于安装、安装程序、转换和数据访问的 Api。 |
| &nbsp; | &nbsp; | <br /> |



<a name="an-170-php-docu" />

## <a name="php-logoimage-ref-360-php-php"></a>![PHP 徽标][image-ref-360-php] PHP

您可以使用 PHP 与 SQL Server 进行交互。 [本文介绍](./php/index.md)了 PHP 文档的根目录。

#### <a name="code-examples"></a>代码示例

|||
| :-- | :-- |
| [使用 PHP 连接到 SQL 的概念验证](./php/step-3-proof-of-concept-connecting-to-sql-using-php.md) | 一个小代码示例，重点介绍如何连接和查询 SQL Server。 |
| [使用 PHP 实现对 SQL 的弹性连接](./php/step-4-connect-resiliently-to-sql-with-php.md) | 在代码示例中重试逻辑，因为通过 Internet 和云进行的连接有时会出现连接丢失的时间。 |
| [Azure SQL 数据库：使用 PHP 进行查询](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-php) | Azure SQL 数据库示例。 |
| [创建 PHP 应用以在 RHEL 上使用 SQL Server](https://www.microsoft.com/sql-server/developer-get-started/php/rhel/) | 配置信息和代码示例。 |
| &nbsp; | <br /> |



<a name="an-180-python-docu" />

## <a name="python-logoimage-ref-370-python-python"></a>![Python 徽标][image-ref-370-python] Python


可以使用 Python 与 SQL Server 进行交互。

#### <a name="code-examples"></a>代码示例

|||
| :-- | :-- |
| [使用 pyodbc 通过 Python 连接到 SQL 的概念证明](./python/pyodbc/step-3-proof-of-concept-connecting-to-sql-using-pyodbc.md) | 一个小代码示例，重点介绍如何连接和查询 SQL Server。 |
| [Azure SQL 数据库：使用 Python 进行查询](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-python) | Azure SQL 数据库示例。 |
| [创建要在 SLES 上使用 SQL Server 的 PHP 应用](https://www.microsoft.com/sql-server/developer-get-started/python/sles/) | 配置信息和代码示例。 |
| &nbsp; | <br /> |

#### <a name="documentation"></a>文档

| 区域 | 描述 |
| :--- | :---------- |
| [Python 到 SQL Server](./python/index.md) | 文档的根。 |
| [pymssql 驱动程序](./python/pymssql/index.md) | Microsoft 不维护或测试 pymssql 驱动程序。<br /><br />Pymssql 连接驱动程序是一个简单的 SQL 数据库界面，可在 Python 程序中使用。 Pymssql 在 FreeTDS 的基础上构建，以提供用于 Microsoft SQL Server 的 Python DB API （PEP-249）接口。 |
| [pyodbc 驱动程序](./python/pyodbc/index.md)   | Pyodbc 连接驱动程序是一种开放源代码 Python 模块，可简化对 ODBC 数据库的访问。 它实现 DB API 2.0 规范，但打包后更易于 Pythonic。 |
| &nbsp; | <br /> |


<a name="an-190-ruby-docu" />

## <a name="ruby-logoimage-ref-380-ruby-ruby"></a>![Ruby 徽标][image-ref-380-ruby] Ruby

您可以使用 Ruby 与 SQL Server 进行交互。 [这里](./ruby/index.md)是 Ruby 文档的根目录。

#### <a name="code-examples"></a>代码示例

|||
| :-- | :-- |
| [使用 Ruby 连接到 SQL 的概念证明](./ruby/step-3-proof-of-concept-connecting-to-sql-using-ruby.md) | 一个小代码示例，重点介绍如何连接和查询 SQL Server。 |
| [Azure SQL 数据库：使用 Ruby 进行查询](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-ruby) | Azure SQL 数据库示例。 |
| [创建要在 MacOS 上使用 SQL Server 的 Ruby 应用](https://www.microsoft.com/sql-server/developer-get-started/ruby/mac/) | 配置信息和代码示例。 |
| &nbsp; | <br /> |



<a name="an-204-aka-ms-sqldev" />

## <a name="build-an-app-website-for-sql-client-developmenthttpswwwmicrosoftcomsql-serverdeveloper-get-started"></a>[用于 SQL 客户端开发的生成-应用网站](https://www.microsoft.com/sql-server/developer-get-started/)


在我们的[*生成-应用*](https://www.microsoft.com/sql-server/developer-get-started/)网页上，你可以从用于连接到 SQL Server 的一系列编程语言中进行选择。 你的客户端程序可以运行各种操作系统。

对于刚开始使用的开发人员而言，*生成-应用*强调简单和完整性。 这些步骤说明了以下任务：

1. 如何安装 Microsoft SQL Server
2. 如何下载和安装工具和驱动程序。
3. 如何根据所选操作系统做出必要的配置。
4. 如何编译提供的源代码。
5. 如何运行该程序。

下面是网站上提供的详细信息的一些大致概述：

#### <a name="java-on-ubuntu"></a>Ubuntu 上的 Java：

1. 设置你的环境
    - 步骤 1.1：安装 SQL Server
    - 步骤1.2 安装 Java
    - 步骤1.3 安装 Java 开发工具包（JDK）
    - 步骤1.4 安装 Maven
2. 创建具有 SQL Server 的 Java 应用程序
    - 步骤2.1 创建连接到 SQL Server 并执行查询的 Java 应用
    - 步骤2.2 创建一个 Java 应用程序，该应用程序使用常用框架休眠连接到 SQL Server
3. 使 Java 应用程序更快100倍
    - 步骤3.1 创建用于演示列存储索引的 Java 应用

#### <a name="python-on-windows"></a>Windows 上的 Python：

1. 设置你的环境
    - 步骤 1.1：安装 SQL Server
    - 步骤1.2 安装 Python
    - 步骤1.3 为 SQL Server 安装 ODBC 驱动程序和 SQL 命令行实用工具
2. 创建具有 SQL Server 的 Python 应用程序
    - 步骤2.1 安装适用于 SQL Server 的 Python 驱动程序
    - 步骤2.2 为应用程序创建数据库
    - 步骤2.3 创建连接到 SQL Server 并执行查询的 Python 应用
3. 使你的 Python 应用程序更快100倍
    - 步骤3.1 使用 sqlcmd 创建新表5000000
    - 步骤3.2 创建查询此表并度量所用时间的 Python 应用
    - 步骤3.3 度量运行查询所用的时间
    - 步骤3.4 向表中添加列存储索引
    - 步骤3.5 度量使用列存储索引运行查询所用的时间

以下屏幕截图提供了 SQL 开发文档网站的外观。

#### <a name="choose-a-language"></a>选择语言：

![SQL 开发网站，入门][image-ref-390-aka-ms-sqldev-choose-language]

&nbsp;

#### <a name="choose-an-operating-system"></a>选择操作系统：

![SQL 开发网站，Java Ubuntu][image-ref-400-aka-ms-sqldev-java-ubuntu]

&nbsp;



## <a name="other-development"></a>其他开发


本部分提供有关其他开发选项的链接。 这包括通常使用相同的 Azure 开发语言。 该信息不仅面向 Azure SQL 数据库和 Microsoft SQL Server。

#### <a name="developer-hub-for-azure"></a>适用于 Azure 的开发人员中心

- [适用于 Azure 的开发人员中心](https://docs.microsoft.com/azure/)
- [面向 .NET 开发人员的 Azure](https://docs.microsoft.com/dotnet/azure/)
- [面向 Java 开发人员的 Azure](https://docs.microsoft.com/java/azure/)
- [面向 Node.js 开发人员的 Azure](https://docs.microsoft.com/nodejs/azure/)
- [面向 Python 开发人员的 Azure](https://docs.microsoft.com/python/azure/)
- [在 Azure 中创建 PHP web 应用](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-php)

#### <a name="other-languages"></a>其他语言

- [使用 Windows 上的 SQL Server 创建开始应用](https://www.microsoft.com/sql-server/developer-get-started/go/windows/)



<!-- Image references. -->

[image-ref-322-cpp]: ./media/homepage-sql-connection-drivers/gm-cpp-4point-p61f.png
[image-ref-320-csharp]: ./media/homepage-sql-connection-drivers/gm-csharp-c10c.png
[image-ref-333-ef]: ./media/homepage-sql-connection-drivers/gm-entity-framework-ef20d.png
[image-ref-330-java]: ./media/homepage-sql-connection-drivers/gm-java-j18c.png
[image-ref-340-node]: ./media/homepage-sql-connection-drivers/gm-node-n30.png
[image-ref-350-odbc]: ./media/homepage-sql-connection-drivers/gm-odbc-ic55826-o35.png
[image-ref-360-php]: ./media/homepage-sql-connection-drivers/gm-php-php60.png
[image-ref-370-python]: ./media/homepage-sql-connection-drivers/gm-python-py72.png
[image-ref-380-ruby]: ./media/homepage-sql-connection-drivers/gm-ruby-un-r82.png
[image-ref-390-aka-ms-sqldev-choose-language]: ./media/homepage-sql-connection-drivers/gm-aka-ms-sqldev-choose-language-g21.png
[image-ref-400-aka-ms-sqldev-java-ubuntu]: ./media/homepage-sql-connection-drivers/gm-aka-ms-sqldev-java-ubuntu-c31.png

