---
title: SQL 客户端编程的主页 |Microsoft Docs
description: 使用带批注的链接下载和文档的语言和操作系统，用于连接到 SQL Server 或 Azure SQL 数据库的许多组合的中心页。
author: MightyPen
ms.date: 11/07/2018
ms.prod: sql
ms.prod_service: connectivity
ms.custom: ''
ms.technology: connectivity
ms.topic: conceptual
ms.reviewer: v-daveng
ms.author: genemi
ms.openlocfilehash: d773e05a3ed953e5210c0ade3226b4a32e82aeab
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63182192"
---
# <a name="homepage-for-client-programming-to-microsoft-sql-server"></a>Microsoft SQL Server 客户端编程的主页


欢迎使用我们的主页有关客户端编程以使用 Microsoft SQL Server，以及与云中的 Azure SQL 数据库进行交互。 本文提供以下信息：

- 列出并描述了可用的语言和驱动程序组合。
    - 对于 Linux （Ubuntu 和其他人）、 MacOS 和 Windows 的操作系统提供信息。
- 提供指向每个组合的详细文档。
- 在适当的显示区域和某些语言的分层文档的子区域。


#### <a name="azure-sql-database"></a>Azure SQL Database

在任何给定语言中，连接到 SQL Server 的代码是与用于连接到 Azure SQL 数据库的代码几乎完全相同。

有关连接到 Azure SQL 数据库的连接字符串的详细信息，请参阅：

- [使用.NET Core (C#) 来查询 Azure SQL 数据库](/azure/sql-database/sql-database-connect-query-dotnet-core)。
- 附近的其他语言的内容，表中的上一篇文章是其他 Azure SQL 数据库。 例如，请参阅[使用 PHP 查询 Azure SQL 数据库](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-php)。


#### <a name="build-an-app-webpages"></a>生成一个应用网页

我们*生成的应用*网页备用格式中存在的代码示例，以及配置信息。 有关详细信息，请参阅本文后面[标记为部分*生成的应用网站*](#an-204-aka-ms-sqldev)。



<a name="an-050-languages-clients" />

## <a name="languages-and-drivers-for-client-programs"></a>语言和客户端程序的驱动程序


下表中每个语言映像是语言中使用的 SQL Server 的详细信息的链接。 每个链接跳转到本文中后面的部分。

| &nbsp; | &nbsp; | &nbsp; |
| :-- | :-- | :-- |
| &nbsp; [![C# 徽标][image-ref-320-csharp]](#an-110-ado-net-docu) | &nbsp; [![ORM 实体框架，.NET framework][image-ref-333-ef]](#an-116-csharp-ef-orm) | &nbsp; [![Java 徽标][image-ref-330-java]](#an-130-jdbc-docu) |
| &nbsp; [![Node.js 徽标][image-ref-340-node]](#an-140-node-js-docu) | &nbsp; [`ODBC for C++`  ](#an-160-odbc-cpp-docu)<br/>[![cpp-big-plus][image-ref-322-cpp]](#an-160-odbc-cpp-docu) | &nbsp; [![PHP 徽标][image-ref-360-php]](#an-170-php-docu) |
| &nbsp; [![Python 徽标][image-ref-370-python]](#an-180-python-docu) | &nbsp; [![Ruby 徽标][image-ref-380-ruby]](#an-190-ruby-docu) | &nbsp; ... |
| &nbsp; | &nbsp; | <br />|


#### <a name="downloads-and-installs"></a>下载并安装

以下文章专门介绍下载并安装各种 SQL 连接驱动程序，以供编程语言：

- [SQL Server 驱动程序](sql-server-drivers.md)



<a name="an-110-ado-net-docu" />

## <a name="c-logoimage-ref-320-csharp-c-using-adonet"></a>![C# 徽标][image-ref-320-csharp] 使用 ADO.NET 通过 C#

.NET 托管语言，如 C# 和 Visual Basic 中，是 ADO.NET 的最常见用户。 *ADO.NET*是.NET Framework 类的一个子集的临时名称。

#### <a name="code-examples"></a>代码示例

|||
| :-- | :-- |
| [使用 ADO.NET 连接到 SQL 的概念证明](./ado-net/step-3-proof-of-concept-connecting-to-sql-using-ado-net.md) | 小代码示例侧重于连接和查询 SQL Server。 |
| [使用 ADO.NET 实现对 SQL 的弹性连接](./ado-net/step-4-connect-resiliently-to-sql-with-ado-net.md) | 重试逻辑中的代码示例，因为连接可能偶尔会遇到的连接丢失。<br /><br />重试逻辑适用于通过维护，internet 到任何云数据库中，如 Azure SQL 数据库的连接良好。 |
| [Azure SQL 数据库： 演示如何在 Windows/Linux/macOS 上使用.NET Core 创建一个 C# 程序，来连接和查询](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-dotnet-core) | Azure SQL 数据库示例。 |
| [生成的应用： C#，ADO.NET 中，Windows](https://www.microsoft.com/sql-server/developer-get-started/csharp/win/) | 配置信息，以及代码示例。 |
| &nbsp; | <br /> |

#### <a name="documentation"></a>文档

|||
| :-- | :-- |
| [使用 ADO.NET 通过 C#](./ado-net/index.md)| 我们的文档的根。 |
| [Namespace: System.Data](https://docs.microsoft.com/dotnet/api/system.data) | 一组用于 ADO.NET 的类。 |
| [命名空间：System.Data.SqlClient](https://docs.microsoft.com/dotnet/api/system.data.SqlClient) | 最直接 ADO.NET center 的类的组。 |
| &nbsp; | <br /> |



<a name="an-116-csharp-ef-orm" />

## <a name="entity-framework-logoimage-ref-333-ef-entity-framework-ef-with-cx23"></a>![实体框架徽标][image-ref-333-ef] 实体框架 (EF) 和 C&#x23;

实体框架 (EF) 提供了对象关系映射 (ORM)。 ORM 轻松面向对象编程 (OOP) 源代码来操作关系 SQL 数据库中检索到的数据。

EF 有直接或间接关系具有以下技术：

- .NET Framework
- [LINQ to SQL](https://docs.microsoft.com/dotnet/framework/data/adonet/sql/linq/)，或[LINQ to Entities](https://docs.microsoft.com/dotnet/framework/data/adonet/ef/language-reference/linq-to-entities)
- 语言语法增强功能，如 **=>** C# 中的运算符。
- 便捷的程序，以便将映射到 SQL 数据库中表的类生成源代码。 例如， [EdmGen.exe](https://docs.microsoft.com/dotnet/framework/data/adonet/ef/edm-generator-edmgen-exe)。


#### <a name="original-ef-and-new-ef"></a>原始 EF 和新的 EF

[实体框架的起始页](https://docs.microsoft.com/ef/)引入 EF 了类似于以下的说明：

- 实体框架是对象关系映射器 (O/RM)，.NET 开发人员可使用使用.NET 对象的数据库。 它不需要的大部分开发人员通常需要编写数据访问源代码。

*实体框架*是由两个单独的源代码分支共享的名称。 更早版本，一个 EF 分支，现在可以通过公共维护其源代码。 其他 EF 是新增的。 接下来介绍了两个 EFs:

|     |     |
| :-- | :-- |
| [EF 6.x](https://docs.microsoft.com/ef/ef6/) | Microsoft 首次在 2008 年 8 月发布 EF。 在 2015 年 3 月 Microsoft 宣布推出的 EF 6.x 是 Microsoft 像开发的最终版本。 Microsoft 发布到公共域的源代码。<br /><br />最初 EF 是.NET Framework 的一部分。 但 EF 6.x 已从.NET Framework 中删除。<br /><br />[在 Github 存储库中的 EF 6.x 源代码*aspnet/EntityFramework6*](https://github.com/aspnet/EntityFramework6) |
| [EF Core](https://docs.microsoft.com/ef/core/) | 2016 年 6 月，Microsoft 发布了新开发的 EF Core。 EF Core 专为更好的灵活性和可移植性。 EF Core 可以只是 Microsoft Windows 以外的操作系统上运行。 和 EF Core 可以与超出不仅仅是 Microsoft SQL Server 数据库和其他关系数据库进行交互。<br /><br />**C&#x23;代码示例：**<br />[使用 Entity Framework Core 入门](https://docs.microsoft.com/ef/core/get-started/index)<br />[开始使用 EF Core 与现有数据库的.NET Framework 上](https://docs.microsoft.com/ef/core/get-started/full-dotnet/existing-db) |
| &nbsp; | <br /> |

EF 和相关的技术功能强大，并且是为开发人员想要掌握的整个区域学到很多。

&nbsp;



<a name="an-130-jdbc-docu" />

## <a name="java-logoimage-ref-330-java-java-and-jdbc"></a>![Java 徽标][image-ref-330-java] Java 和 JDBC

Microsoft 提供的 Java 数据库连接 (JDBC) 驱动程序使用与 SQL Server （或使用 Azure SQL 数据库，当然，）。 它是 Type 4 JDBC 驱动程序，通过标准 JDBC 应用程序编程接口 (API) 提供数据库连接。

#### <a name="code-examples"></a>代码示例

|||
| :-- | :-- |
| [代码示例](./jdbc/code-samples/index.md) | 介绍有关数据类型，结果集和大型数据的代码示例。 |
| [连接 URL 示例](./jdbc/connection-url-sample.md) | 介绍如何使用连接 URL 来连接到 SQL Server。 然后使用它来使用 SQL 语句来检索数据。 |
| [数据源示例](./jdbc/data-source-sample.md) | 介绍如何使用数据源连接到 SQL Server。 然后使用存储的过程来检索数据。 |
| [使用 Java 查询 Azure SQL 数据库](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-java) | Azure SQL 数据库示例。 |
| [创建在 Ubuntu 上使用 SQL Server 的 Java 应用](https://www.microsoft.com/sql-server/developer-get-started/java/ubuntu/) | 配置信息，以及代码示例。 |
| &nbsp; | <br /> |

#### <a name="documentation"></a>文档

JDBC 文档包括以下主要方面：

|||
| :-- | :-- |
| [Java 数据库连接 (JDBC)](./jdbc/index.md) | 我们的 JDBC 文档的根。 |
| [参考](./jdbc/reference/index.md) | 接口、 类和成员。 |
| [JDBC SQL 驱动程序编程指南](./jdbc/programming-guide-for-jdbc-sql-driver.md) | 配置信息，以及代码示例。 |
| &nbsp; | <br /> |



<a name="an-140-node-js-docu" />

## <a name="nodejs-logoimage-ref-340-node-nodejs"></a>![Node.js 徽标][image-ref-340-node] Node.js

与 Node.js 配合使用可以连接到 SQL Server 从 Windows、 Linux 或 mac。 我们的 Node.js 文档的根是[此处](./node-js/index.md)。

SQL Server 的 Node.js 连接驱动程序是在 JavaScript 中实现的。 驱动程序使用支持的所有最新版本的 SQL Server 的 TDS 协议。 该驱动程序是一个开放源代码项目，[可在 Github 上](https://tediousjs.github.io/tedious/)。

#### <a name="code-examples"></a>代码示例

|||
| :-- | :-- |
| [使用 Node.js 连接到 SQL 的概念证明](./node-js/step-3-proof-of-concept-connecting-to-sql-using-node-js.md) | 基本源连接到 SQL Server 和执行查询的代码。 |
| [Azure SQL 数据库： 使用 Node.js 查询](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-nodejs) | 在云中的 Azure SQL 数据库的示例。 |
| [创建 Node.js 应用程序以在 macOS 上使用 SQL Server](https://www.microsoft.com/sql-server/developer-get-started/node/mac/) | 配置信息，以及代码示例。 |
| &nbsp; | <br /> |



<a name="an-160-odbc-cpp-docu" />

## <a name="odbc-for-c"></a>有关 ODBCC++ 

![ODBC 徽标][image-ref-350-odbc] ![cpp-big-plus][image-ref-322-cpp]

开放式数据库连接 (ODBC) 在 20 世纪 90 年代中, 开发的它早于.NET Framework。 ODBC 被设计为独立于任何特定的数据库系统，并独立于操作系统。

多年来许多 ODBC 驱动程序已创建并发布的 Microsoft 内外的组。 驱动程序的范围涉及多个客户端编程语言。 数据目标的列表将远远超出了 SQL Server。

某些其他连接驱动程序在内部使用 ODBC。

#### <a name="code-example"></a>代码示例

- [使用 ODBC 的 C++ 代码示例](../odbc/reference/sample-odbc-program.md)

#### <a name="documentation-outline"></a>文档大纲

在本部分中的 ODBC 内容重点介绍从访问 SQL Server 或 Azure SQL 数据库C++。 下表列出了适用于 ODBC 的主要文档的近似概述。


| 区域 | 子区域 | 描述 |
| :--- | :------ | :---------- |
| [有关 ODBCC++](./odbc/index.md) | 我们的文档的根。 |
| [Linux-Mac](./odbc/linux-mac/index.md) | &nbsp; | 有关在 Linux 或 MacOS 操作系统上使用 ODBC 的信息。 |
| [Windows](./odbc/windows/index.md)     | &nbsp; | 有关 Windows 操作系统上使用 ODBC 的信息。 |
| [管理](../odbc/admin/index.md) | &nbsp; | 用于管理 ODBC 数据源的管理工具。 |
| [Microsoft](../odbc/microsoft/index.md)  | &nbsp; | 各种 ODBC 驱动程序创建并由 Microsoft 提供的。 |
| [概念和参考](../odbc/reference/index.md) | &nbsp; | 有关 ODBC 接口，除了传统的引用的概念信息。 |
| &nbsp; " | [附录](../odbc/reference/appendixes/index.md)    | 状态转换表、 ODBC 游标库和的详细信息。 |
| &nbsp; " | [开发应用程序](../odbc/reference/develop-app/index.md)  | 函数、 句柄，以及更多内容。 |
| &nbsp; " | [开发驱动程序](../odbc/reference/develop-driver/index.md) | 如何开发您自己的 ODBC 驱动程序，如果您拥有专用的数据源。 |
| &nbsp; " | [安装](../odbc/reference/install/index.md) | ODBC 安装、 子项和的详细信息。 |
| &nbsp; " | [语法](../odbc/reference/syntax/index.md)   | 安装程序，安装程序、 转换和数据访问 Api。 |
| &nbsp; | &nbsp; | <br /> |



<a name="an-170-php-docu" />

## <a name="php-logoimage-ref-360-php-php"></a>![PHP 徽标][image-ref-360-php] PHP

可以使用 PHP 来与 SQL Server 进行交互。 PHP 文档的根是[此处](./php/index.md)。

#### <a name="code-examples"></a>代码示例

|||
| :-- | :-- |
| [使用 PHP 连接到 SQL 的概念验证](./php/step-3-proof-of-concept-connecting-to-sql-using-php.md) | 小代码示例侧重于连接和查询 SQL Server。 |
| [使用 PHP 实现对 SQL 的弹性连接](./php/step-4-connect-resiliently-to-sql-with-php.md) | 重试逻辑中的代码示例，因为通过 Internet 和云的连接偶尔遇到的连接丢失。 |
| [Azure SQL 数据库： 使用 PHP 查询](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-php) | Azure SQL 数据库示例。 |
| [创建要在 RHEL 上使用 SQL Server 的 PHP 应用程序](https://www.microsoft.com/sql-server/developer-get-started/php/rhel/) | 配置信息，以及代码示例。 |
| &nbsp; | <br /> |



<a name="an-180-python-docu" />

## <a name="python-logoimage-ref-370-python-python"></a>![Python 徽标][image-ref-370-python] Python


可以使用 Python 与 SQL Server 进行交互。

#### <a name="code-examples"></a>代码示例

|||
| :-- | :-- |
| [连接到使用 pyodbc Python 与 SQL 的概念证明](./python/pyodbc/step-3-proof-of-concept-connecting-to-sql-using-pyodbc.md) | 小代码示例侧重于连接和查询 SQL Server。 |
| [Azure SQL 数据库： 使用 Python 查询](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-python) | Azure SQL 数据库示例。 |
| [创建 PHP 应用，在 SLES 上使用 SQL Server](https://www.microsoft.com/sql-server/developer-get-started/python/sles/) | 配置信息，以及代码示例。 |
| &nbsp; | <br /> |

#### <a name="documentation"></a>文档

| 区域 | 描述 |
| :--- | :---------- |
| [到 SQL Server 的 Python](./python/index.md) | 我们的文档的根。 |
| [pymssql 驱动程序](./python/pymssql/index.md) | Microsoft 不会维护或测试 pymssql 驱动程序。<br /><br />Pymssql 连接驱动程序是 SQL 数据库，以便在 Python 程序中使用的简单界面。 Pymssql FreeTDS Python DB API (PEP 249) 接口提供对 Microsoft SQL Server 的基础上构建。 |
| [pyodbc 驱动程序](./python/pyodbc/index.md)   | Pyodbc 连接驱动程序是一个开源 Python 模块，使访问 ODBC 数据库变得简单。 它实现 DB API 2.0 规范中，但提供了更多 Pythonic 方便起见。 |
| &nbsp; | <br /> |


<a name="an-190-ruby-docu" />

## <a name="ruby-logoimage-ref-380-ruby-ruby"></a>![Ruby 徽标][image-ref-380-ruby] Ruby

可以使用 Ruby 与 SQL Server 进行交互。 我们 Ruby 的文档的根是[此处](./ruby/index.md)。

#### <a name="code-examples"></a>代码示例

|||
| :-- | :-- |
| [使用 Ruby 连接到 SQL 的概念证明](./ruby/step-3-proof-of-concept-connecting-to-sql-using-ruby.md) | 小代码示例侧重于连接和查询 SQL Server。 |
| [Azure SQL 数据库： 使用 Ruby 查询](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-ruby) | Azure SQL 数据库示例。 |
| [创建 Ruby 应用程序以在 MacOS 上使用 SQL Server](https://www.microsoft.com/sql-server/developer-get-started/ruby/mac/) | 配置信息，以及代码示例。 |
| &nbsp; | <br /> |



<a name="an-204-aka-ms-sqldev" />

## <a name="build-an-app-website-for-sql-client-developmenthttpswwwmicrosoftcomsql-serverdeveloper-get-started"></a>[生成的应用网站，用于 SQL 客户端开发](https://www.microsoft.com/sql-server/developer-get-started/)


在我们[*生成的应用*](https://www.microsoft.com/sql-server/developer-get-started/)网页可以选择从一长串的编程语言连接到 SQL Server。 和客户端程序可以运行各种操作系统。

*生成一个应用*强调的开发人员刚开始的简单性和完整性。 步骤介绍了以下任务：

1. 如何安装 Microsoft SQL Server
2. 如何下载和安装工具和驱动程序。
3. 如何进行任何必要的配置，根据所选操作系统。
4. 如何编译提供的源代码。
5. 如何运行该程序。

接下来是几个近似轮廓的网站上提供的详细信息：

#### <a name="java-on-ubuntu"></a>在 Ubuntu 上的 Java:

1. 设置环境
    - 步骤 1.1：安装 SQL Server
    - 步骤 1.2 安装 Java
    - 步骤 1.3 安装 Java 开发工具包 (JDK)
    - 步骤 1.4 安装 Maven
2. 使用 SQL Server 中创建 Java 应用程序
    - 步骤 2.1 创建连接到 SQL Server 并执行查询的 Java 应用
    - 步骤 2.2 创建连接到使用常用的框架，休眠的 SQL Server 的 Java 应用程序
3. 更快地做出多达 100 倍的 Java 应用
    - 步骤 3.1 创建 Java 应用程序来演示列存储索引

#### <a name="python-on-windows"></a>在 Windows 上的 Python:

1. 设置环境
    - 步骤 1.1：安装 SQL Server
    - 步骤 1.2 安装 Python
    - 步骤 1.3 安装用于 SQL Server 的 ODBC 驱动程序和 SQL 命令行实用程序
2. 使用 SQL Server 创建 Python 应用程序
    - 步骤 2.1 安装 Python driver for SQL Server
    - 步骤 2.2 为创建的数据库应用程序
    - 步骤 2.3 创建一个 Python 应用，连接到 SQL Server 并执行查询
3. 更快地做出多达 100 倍将 Python 应用
    - 步骤 3.1 使用 5 百万个使用 sqlcmd 创建一个新表
    - 步骤 3.2 创建一个 Python 应用，将查询此表和度量值所用的时间
    - 步骤 3.3 测量运行查询所需的时间长度
    - 步骤 3.4 将添加到表的列存储索引
    - 步骤 3.5 度量值具有列存储索引运行查询所需的时间长度

下面的屏幕截图让了解我们的 SQL 开发文档网站如下所示。

#### <a name="choose-a-language"></a>选择语言：

![SQL 开发人员网站入门][image-ref-390-aka-ms-sqldev-choose-language]

&nbsp;

#### <a name="choose-an-operating-system"></a>选择操作系统：

![SQL 开发人员网站，Java Ubuntu][image-ref-400-aka-ms-sqldev-java-ubuntu]

&nbsp;



## <a name="other-development"></a>其他开发


本部分提供有关其他开发选项的链接。 其中包括在一般情况下使用这些相同的语言进行 Azure 开发。 信息超出了目标只是 Azure SQL 数据库和 Microsoft SQL Server。

#### <a name="developer-hub-for-azure"></a>适用于 Azure 的开发人员中心

- [适用于 Azure 的开发人员中心](https://docs.microsoft.com/azure/)
- [面向 .NET 开发人员的 Azure](https://docs.microsoft.com/dotnet/azure/)
- [面向 Java 开发人员的 azure](https://docs.microsoft.com/java/azure/)
- [面向 Node.js 开发人员的 azure](https://docs.microsoft.com/nodejs/azure/)
- [面向 Python 开发人员的 azure](https://docs.microsoft.com/python/azure/)
- [在 Azure 中创建 PHP web 应用](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-php)

#### <a name="other-languages"></a>其他语言

- [创建使用 Windows 上的 SQL Server 的 Go 应用](https://www.microsoft.com/sql-server/developer-get-started/go/windows/)



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

