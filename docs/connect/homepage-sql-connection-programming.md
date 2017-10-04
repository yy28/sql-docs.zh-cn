---
title: "SQL 客户端编程的主页 |Microsoft 文档"
description: "使用带批注的链接下载和文档的语言和操作系统，用于连接到 SQL Server 或 Azure SQL 数据库的多个组合的中心页面。"
author: MightyPen
ms.date: 09/13/2017
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.topic: article
ms.reviewer: meetb
ms.author: genemi
ms.translationtype: MT
ms.sourcegitcommit: 71ca2fac0a6b9f087f9d434c5a701f5656889b9e
ms.openlocfilehash: 000325a2e2c53e36f7a74a725962b8dd3be98988
ms.contentlocale: zh-cn
ms.lasthandoff: 09/13/2017

---
# <a name="homepage-for-client-programming-to-microsoft-sql-server"></a>客户端编程到 Microsoft SQL Server 主页


欢迎使用客户端编程以与 Microsoft SQL Server，和在云中的 Azure SQL 数据库交互有关我们的主页。 本文提供以下信息：

- 列出并描述了可用的语言和驱动程序组合。
    - 对于 Linux （Ubuntu 及其他）、 MacOS，和 Windows 操作系统提供信息。
- 提供指向每个组合的详细文档。
- 在适当的显示区域和的某些语言的分层文档的子区域。


#### <a name="azure-sql-database"></a>Azure SQL Database

在任何给定的语言中，连接到 SQL Server 的代码是几乎与连接到 Azure SQL 数据库的代码。

有关连接到 Azure SQL 数据库的连接字符串的详细信息，请参阅：

- [使用.NET Core (C#) 来查询 Azure SQL 数据库](http://docs.microsoft.com/azure/sql-database/sql-database-connect-query-dotnet-core)。
- 邻近的表中的内容，其他语言有关前面的文章将其他 Azure SQL 数据库。 例如，请参阅[使用 PHP，Azure SQL 数据库中查询](http://docs.microsoft.com/azure/sql-database/sql-database-connect-query-php)。


#### <a name="build-an-app-webpages"></a>生成的应用的网页

我们*生成的应用*网页备用格式中存在代码示例，以及配置信息。 有关详细信息，请参阅本文后面[部分标记为*生成的应用网站*](#an-204-aka-ms-sqldev)。



<a name="an-050-languages-clients" />

## <a name="languages-and-drivers-for-client-programs"></a>语言和客户端程序的驱动程序


在以下表中，每个语言映像是到有关使用 SQL Server 的语言的详细信息的链接。 每个链接跳转到本文后面的部分。

| &nbsp; | &nbsp; | &nbsp; |
| :-- | :-- | :-- |
| &nbsp;[![C# 徽标][映像-ref-320-csharp]](#an-110-ado-net-docu) | &nbsp;[![ORM 实体框架中，.NET framework][映像-ref-333 的 ef]](#an-116-csharp-ef-orm) | &nbsp;[![Java 徽标][映像-ref-330-java]](#an-130-jdbc-docu) |
| &nbsp;[![Node.js 徽标][映像-ref-340-node]](#an-140-node-js-docu) | &nbsp; [**`ODBC for C++`**](#an-160-odbc-cpp-docu) | &nbsp;[![PHP 徽标][映像-ref-360-php]](#an-170-php-docu) |
| &nbsp;[![Python 徽标][映像-ref-370-python]](#an-180-python-docu) | &nbsp;[![Ruby 徽标][映像-ref-380-ruby]](#an-190-ruby-docu) | &nbsp; ... |
| &nbsp; | &nbsp; | <br />|


#### <a name="downloads-and-installs"></a>下载和安装

以下文章专用于下载和安装各种 SQL 连接驱动程序，以供编程语言：

- [SQL Server 驱动程序](sql-server-drivers.md)



<a name="an-110-ado-net-docu" />

## <a name="c-logoimage-ref-320-csharp-c-using-adonet"></a>![C# 徽标][image-ref-320-csharp] C# 使用 ADO.NET

托管的.NET 语言中，如 C# 和 Visual Basic 中，是的 ADO.NET 最常见的用户。 *ADO.NET*是.NET Framework 类的子集的非正式名称。

#### <a name="code-examples"></a>代码示例

|||
| :-- | :-- |
| [连接到使用 ADO.NET 的 SQL 的概念证明](./ado-net/step-3-proof-of-concept-connecting-to-sql-using-ado-net.md) | 小的代码示例侧重于连接和查询 SQL Server。 |
| [与使用 ADO.NET 的 SQL 的弹性连接](./ado-net/step-4-connect-resiliently-to-sql-with-ado-net.md) | 重试逻辑代码示例，因为连接可能偶尔会遇到的连接丢失的时间。<br /><br />重试逻辑会应用很好地维护连接通过 internet 到任何云数据库，如到 Azure SQL 数据库。 |
| [如何在 Windows/Linux/macOS 上使用.NET Core 创建一个 C# 程序的 azure SQL 数据库： 演示来连接和查询](http://docs.microsoft.com/azure/sql-database/sql-database-connect-query-dotnet-core) | Azure SQL 数据库示例。 |
| [生成的应用： C#，ADO.NET 中，Windows](http://www.microsoft.com/sql-server/developer-get-started/csharp/win/) | 配置信息，以及代码示例。 |
| &nbsp; | <br /> |

#### <a name="documentation"></a>文档

|||
| :-- | :-- |
| [C# 使用 ADO.NET](./ado-net/index.md)| 我们的文档的根。 |
| [Namespace: System.Data](http://docs.microsoft.com/dotnet/api/system.data) | 一组用于 ADO.NET 的类。 |
| [Namespace: System.Data.SqlClient](http://docs.microsoft.com/dotnet/api/system.data.SqlClient) | 最直接 ADO.NET center 类集。 |
| &nbsp; | <br /> |



<a name="an-116-csharp-ef-orm" />

## <a name="entity-framework-logoimage-ref-333-ef-entity-framework-ef-with-cx23"></a>![实体框架徽标][image-ref-333-ef] 使用 C&#x23; 实体框架 (EF)

Entity Framework (EF) 提供对象关系映射 (ORM)。 ORM 便于你面向编程 (OOP) 的源代码来处理关系的 SQL 数据库中检索到的数据。

EF 有直接或间接关系具有以下技术：

- .NET Framework
- [LINQ to SQL](http://docs.microsoft.com/dotnet/framework/data/adonet/sql/linq/)，或[LINQ to Entities](http://docs.microsoft.com/dotnet/framework/data/adonet/ef/language-reference/linq-to-entities)
- 语言语法增强功能，如 **=>**  C# 中的运算符。
- 便捷的程序，以便将映射到 SQL 数据库中的表的类生成源代码。 例如， [EdmGen.exe](http://docs.microsoft.com/dotnet/framework/data/adonet/ef/edm-generator-edmgen-exe)。


#### <a name="original-ef-and-new-ef"></a>原始 EF 和新 EF

[实体框架的起始页](http://docs.microsoft.com/ef/)引入 EF 了类似于以下的说明：

- 实体框架是对象关系映射器 (O/RM)，使.NET 开发人员可以使用.NET 对象的数据库使用。 它消除了对大多数开发人员通常需要编写数据访问源代码的需求。

*实体框架*是共享由两个单独的源代码分支的名称。 一个 EF 分支都是较旧，并且现在可以通过公共维护其源代码。 其他 EF 是新增功能。 接下来将介绍两个 EFs:

|     |     |
| :-- | :-- |
| [EF 6.x](http://docs.microsoft.com/ef/ef6/) | Microsoft 在 2008 年 8 月首次发布 EF。 在 2015 年 3 月 Microsoft 宣布，EF 6.x 是开发将 Microsoft 的最终版本。 Microsoft 发布到的公共域的源代码。<br /><br />最初 EF 是.NET Framework 的一部分。 但 EF 6.x 已从.NET Framework 中删除。<br /><br />[在 Github 上，在存储库中的 EF 6.x 源代码*aspnet/EntityFramework6*](http://github.com/aspnet/EntityFramework6) |
| [EF 核心](http://docs.microsoft.com/ef/core/) | Microsoft 于 2016 年 6 月发布新开发的 EF 核心。 EF 核心旨在更好的灵活性和可移植性。 EF 核心可以在 Microsoft Windows 之外的操作系统上运行。 和 EF 核心可以与超出只是 Microsoft SQL Server 数据库和其他关系数据库进行交互。<br /><br />**C&#x23;代码示例：**<br />[开始使用实体框架核心](https://docs.microsoft.com/ef/core/get-started/index)<br />[EF 核心上使用现有的数据库的.NET Framework 入门](https://docs.microsoft.com/ef/core/get-started/full-dotnet/existing-db) |
| &nbsp; | <br /> |

EF 和相关的技术是功能强大，并且有许多值得了解的开发人员想要掌握整个区域。

&nbsp;



<a name="an-130-jdbc-docu" />

## <a name="java-logoimage-ref-330-java-java-and-jdbc"></a>![Java 徽标][image-ref-330-java] Java 和 JDBC

Microsoft 提供的 Java 数据库连接 (JDBC) 驱动程序以供与 SQL Server （或与 Azure SQL 数据库的过程）。 它是一个 Type 4 JDBC 驱动程序，并且它提供通过标准 JDBC 应用程序编程接口 (Api) 的数据库连接。

#### <a name="code-examples"></a>代码示例

|||
| :-- | :-- |
| [代码示例](./jdbc/code-samples/index.md) | 介绍有关数据类型、 结果集和大型数据的代码示例。 |
| [连接 URL 示例](./jdbc/connection-url-sample.md) | 介绍如何使用连接 URL 以连接到 SQL Server。 然后使用它以使用 SQL 语句来检索数据。 |
| [数据源示例](./jdbc/data-source-sample.md) | 描述如何使用数据源连接到 SQL Server。 然后使用存储的过程以检索数据。 |
| [使用 Java 来查询 Azure SQL 数据库](http://docs.microsoft.com/azure/sql-database/sql-database-connect-query-java) | Azure SQL 数据库示例。 |
| [创建 Java 应用程序在 Ubuntu 上使用 SQL Server](http://www.microsoft.com/sql-server/developer-get-started/java/ubuntu/) | 配置信息，以及代码示例。 |
| &nbsp; | <br /> |

#### <a name="documentation"></a>文档

JDBC 文档包括以下几个主要方面：

|||
| :-- | :-- |
| [Java 数据库连接 (JDBC)](./jdbc/index.md) | 我们的 JDBC 文档的根。 |
| [参考](./jdbc/reference/index.md) | 接口、 类和成员。 |
| [编程 JDBC SQL 驱动程序的指南](./jdbc/programming-guide-for-jdbc-sql-driver.md) | 配置信息，以及代码示例。 |
| &nbsp; | <br /> |



<a name="an-140-node-js-docu" />

## <a name="nodejs-logoimage-ref-340-node-nodejs"></a>![Node.js 徽标][image-ref-340-node] Node.js

借助 Node.js 你可以连接到 SQL Server 从 Windows、 Linux 或 mac。 我们的 Node.js 文档的根是[此处](./node-js/index.md)。

在 JavaScript 中实现的 Node.js 连接 driver for SQL Server。 驱动程序使用受所有最新版本的 SQL Server 的 TDS 协议。 该驱动程序是一个开源项目， [Github 上提供](http://tediousjs.github.io/tedious/)。

#### <a name="code-examples"></a>代码示例

|||
| :-- | :-- |
| [连接到 SQL 使用 Node.js 的概念证明](./node-js/step-3-proof-of-concept-connecting-to-sql-using-node-js.md) | 基本源以及连接到 SQL Server 执行查询的代码。 |
| [Azure SQL 数据库： 使用 Node.js 查询](http://docs.microsoft.com/azure/sql-database/sql-database-connect-query-nodejs) | 在云中的 Azure SQL 数据库的示例。 |
| [创建 Node.js 应用程序以在 macOS 上使用 SQL Server](http://www.microsoft.com/sql-server/developer-get-started/node/mac/) | 配置信息，以及代码示例。 |
| &nbsp; | <br /> |



<a name="an-160-odbc-cpp-docu" />

## <a name="odbc-for-c"></a>C + + 的 ODBC 

![ODBC 徽标][image-ref-350-odbc]

开放式数据库连接 (ODBC) 年代开发的它早于.NET Framework。 ODBC 被旨在作为独立于任何特定的数据库系统，并独立于操作系统。

多年来多个 ODBC 驱动程序已创建并发布组之内或之外 Microsoft。 驱动程序的范围涉及多个客户端编程语言。 数据目标列表超出了 SQL Server。

某些其他连接驱动程序在内部使用 ODBC。

#### <a name="code-example"></a>代码示例

- [C + + 代码示例中，使用 ODBC](../odbc/reference/sample-odbc-program.md)

#### <a name="documentation-outline"></a>文档大纲

本部分中的 ODBC 内容侧重于从 c + + 访问 SQL Server 或 Azure SQL 数据库。 下表列出了适用于 ODBC 的主要文档的近似边框。


| 区域 | 子区域 | Description |
| :--- | :------ | :---------- |
| [C + + 的 ODBC](./odbc/index.md) | 我们的文档的根。 |
| [Linux Mac](./odbc/linux-mac/index.md) | &nbsp; | 有关在 Linux 或 MacOS 操作系统上使用 ODBC 的信息。 |
| [Windows](./odbc/windows/index.md)     | &nbsp; | 有关在 Windows 操作系统上使用 ODBC 的信息。 |
| [管理](../odbc/admin/index.md) | &nbsp; | 用于管理 ODBC 数据源的管理工具。 |
| [Microsoft](../odbc/microsoft/index.md)  | &nbsp; | 各种 ODBC 驱动程序创建并由 Microsoft 提供。 |
| [概念和参考](../odbc/reference/index.md) | &nbsp; | 有关 ODBC 接口，除了传统的引用的概念信息。 |
| &nbsp; " | [附录中](../odbc/reference/appendixes/index.md)    | 状态转换表、 ODBC 游标库和的详细信息。 |
| &nbsp; " | [开发应用程序](../odbc/reference/develop-app/index.md)  | 函数、 句柄和其他更多。 |
| &nbsp; " | [开发驱动程序](../odbc/reference/develop-driver/index.md) | 如何开发自己的 ODBC 驱动程序，如果你有一个专用的数据源。 |
| &nbsp; " | [安装](../odbc/reference/install/index.md) | ODBC 安装、 子项和的详细信息。 |
| &nbsp; " | [语法](../odbc/reference/syntax/index.md)   | 安装程序、 安装程序、 转换和数据访问的 Api。 |
| &nbsp; | &nbsp; | <br /> |



<a name="an-170-php-docu" />

## <a name="php-logoimage-ref-360-php-php"></a>![PHP 徽标][image-ref-360-php] PHP

可以使用 PHP 与 SQL Server 进行交互。 我们的 Node.js 文档的根是[此处](./php/index.md)。

#### <a name="code-examples"></a>代码示例

|||
| :-- | :-- |
| [连接到使用 PHP 的 SQL 的概念证明](./php/step-3-proof-of-concept-connecting-to-sql-using-php.md) | 小的代码示例侧重于连接和查询 SQL Server。 |
| [到使用 PHP 的 SQL 的弹性连接](./php/step-4-connect-resiliently-to-sql-with-php.md) | 重试逻辑代码示例，因为通过 Internet 和云的连接偶尔可能遇到的连接丢失的时间。 |
| [Azure SQL 数据库： 使用 PHP 查询](http://docs.microsoft.com/azure/sql-database/sql-database-connect-query-php) | Azure SQL 数据库示例。 |
| [创建 PHP 应用程序以在 RHEL 上使用 SQL Server](http://www.microsoft.com/sql-server/developer-get-started/php/rhel/) | 配置信息，以及代码示例。 |
| &nbsp; | <br /> |



<a name="an-180-python-docu" />

## <a name="python-logoimage-ref-370-python-python"></a>![Python 徽标][image-ref-370-python] Python


可以使用 Python 与 SQL Server 进行交互。

#### <a name="code-examples"></a>代码示例

|||
| :-- | :-- |
| [连接到通过 Python 使用 pyodbc SQL 的概念证明](./python/pyodbc/step-3-proof-of-concept-connecting-to-sql-using-pyodbc.md) | 小的代码示例侧重于连接和查询 SQL Server。 |
| [Azure SQL 数据库： 对查询使用 Python](http://docs.microsoft.com/azure/sql-database/sql-database-connect-query-python) | Azure SQL 数据库示例。 |
| [创建 PHP 应用程序以在 SLES 上使用 SQL Server](http://www.microsoft.com/sql-server/developer-get-started/python/sles/) | 配置信息，以及代码示例。 |
| &nbsp; | <br /> |

#### <a name="documentation"></a>文档

| 区域 | Description |
| :--- | :---------- |
| [到 SQL Server 的 Python](./python/index.md) | 我们的文档的根。 |
| [pymssql 驱动程序](./python/pymssql/index.md) | Microsoft 不维护或测试 pymssql 驱动程序。<br /><br />Pymssql 连接驱动程序是一个简单接口到 SQL 数据库，以供 Python 程序使用。 Pymssql 生成基于 FreeTDS 用于与 Microsoft SQL Server 提供的 Python DB API (PEP 249) 接口。 |
| [pyodbc 驱动程序](./python/pyodbc/index.md)   | Pyodbc 连接驱动程序是一个开放源代码 Python 模块，使访问 ODBC 数据库变得简单。 它实现 DB API 2.0 规范中，但具有更多的 Pythonic 便利性打包。 |
| &nbsp; | <br /> |


<a name="an-190-ruby-docu" />

## <a name="ruby-logoimage-ref-380-ruby-ruby"></a>![Ruby 徽标][image-ref-380-ruby] Ruby

可以使用 Ruby 与 SQL Server 进行交互。 我们 Ruby 的文档的根是[此处](./ruby/index.md)。

#### <a name="code-examples"></a>代码示例

|||
| :-- | :-- |
| [连接到与 Ruby SQL 的概念证明](./ruby/step-3-proof-of-concept-connecting-to-sql-using-ruby.md) | 小的代码示例侧重于连接和查询 SQL Server。 |
| [Azure SQL 数据库： 对查询使用 Ruby](http://docs.microsoft.com/azure/sql-database/sql-database-connect-query-ruby) | Azure SQL 数据库示例。 |
| [创建 Ruby 应用以在 MacOS 上使用 SQL Server](http://www.microsoft.com/sql-server/developer-get-started/ruby/mac/) | 配置信息，以及代码示例。 |
| &nbsp; | <br /> |



<a name="an-204-aka-ms-sqldev" />

## <a name="build-an-app-website-for-sql-client-developmenthttpwwwmicrosoftcomsql-serverdeveloper-get-started"></a>[生成的应用网站，SQL 客户端开发](http://www.microsoft.com/sql-server/developer-get-started/)


在我们[*生成的应用*](https://www.microsoft.com/sql-server/developer-get-started/)网页，你可以选择从较长的编程语言连接到 SQL Server 列表。 和客户端程序可以运行各种操作系统。

*生成的应用*强调的开发人员只需启动的简洁性和完整性。 步骤介绍了以下任务：

1. 如何安装 Microsoft SQL Server
2. 如何下载和安装工具和驱动程序。
3. 如何进行任何必要的配置，根据所选操作系统。
4. 如何将提供的源代码编译。
5. 如何运行程序。

再下面是几个近似轮廓的网站上提供的详细信息：

#### <a name="java-on-ubuntu"></a>在 Ubuntu 上的 Java:

1. 设置你的环境
    - 步骤 1.1 安装 SQL Server
    - 步骤 1.2 安装 Java
    - 步骤 1.3 安装 Java 开发工具包 (JDK)
    - 步骤 1.4 安装 Maven
2. 创建使用 SQL Server 的 Java 应用程序
    - 步骤 2.1 创建 Java 应用程序连接到 SQL Server 并执行查询
    - 步骤 2.2 创建的 Java 应用程序连接到使用常用框架休眠的 SQL Server
3. 使您最多 100 x 的 Java 应用程序更快
    - 步骤 3.1 创建 Java 应用程序来演示列存储索引

#### <a name="python-on-windows"></a>在 Windows 上的 Python:

1. 设置你的环境
    - 步骤 1.1 安装 SQL Server
    - 步骤 1.2 安装 Python
    - 步骤 1.3 适用于 SQL Server 安装的 ODBC 驱动程序和 SQL 命令行实用工具
2. 创建使用 SQL Server 的 Python 应用程序
    - 步骤 2.1 安装 Python 驱动程序适用于 SQL Server
    - 步骤 2.2 创建你的应用程序的数据库
    - 步骤 2.3 创建的 Python 应用程序连接到 SQL Server 并执行查询
3. 使您最多 100 x 的 Python 应用程序更快
    - 步骤 3.1 使用 5 万个使用 sqlcmd 创建一个新表
    - 步骤 3.2 创建 Python 应用程序用于查询此表并测量所花费的时间
    - 步骤 3.3 测量它所需的时间运行查询
    - 步骤 3.4 将添加到表的列存储索引
    - 步骤 3.5 度量值具有列存储索引运行查询所需的时间

以下屏幕截图让你了解我们 SQL 开发文档网站如下所示。

#### <a name="choose-a-language"></a>选择一种语言：

![SQL 开发人员网站开始][image-ref-390-aka-ms-sqldev-choose-language]

&nbsp;

#### <a name="choose-an-operating-system"></a>选择操作系统：

![SQL 开发人员网站，Java Ubuntu][image-ref-400-aka-ms-sqldev-java-ubuntu]

&nbsp;



## <a name="other-development"></a>其他开发


本部分提供有关其他开发选项的链接。 其中包括一般情况下进行 Azure 开发中使用这些相同的语言。 目标只是 Azure SQL 数据库和 Microsoft SQL Server 超出信息。

#### <a name="developer-hub-for-azure"></a>Azure 的开发人员中心

- [Azure 的开发人员中心](http://docs.microsoft.com/azure/)
- [.NET 开发人员的的 azure](http://docs.microsoft.com/dotnet/azure/)
- [Java 开发人员的 azure](http://docs.microsoft.com/java/azure/)
- [Node.js 开发人员的 azure](http://docs.microsoft.com/nodejs/azure/)
- [Python 开发人员的 azure](http://docs.microsoft.com/python/azure/)
- [在 Azure 中创建 PHP web 应用](http://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-php)

#### <a name="other-languages"></a>其他语言

- [创建在 Windows 上使用 SQL Server 的 Go 应用程序](http://www.microsoft.com/sql-server/developer-get-started/go/windows/)



<!-- Image references. -->

[image-ref-310-ado-net]: ./media/homepage-sql-connection-drivers/gm-ado-net-an51.png
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


