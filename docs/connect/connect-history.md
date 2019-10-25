---
title: Microsoft SQL Server 的驱动程序历史记录 |Microsoft Docs
ms.custom: ''
ms.date: 05/04/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a0eb869cf19f128515951421efddc229aa785cdd
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/16/2019
ms.locfileid: "72451830"
---
# <a name="driver-history-for-microsoft-sql-server"></a>Microsoft SQL Server 的驱动程序历史记录

本页介绍了 Microsoft 用于连接到 SQL Server 的历史数据连接技术。

## <a name="odbc"></a>ODBC

有三代不同的 Microsoft ODBC Driver for SQL Server。 第一个 "SQL Server" ODBC 驱动程序仍作为[Windows 数据访问组件](#microsoft-or-windows-data-access-components)的一部分提供。 不建议使用此驱动程序进行新的开发。 从 SQL Server 2005 开始， [SQL Server Native Client](#sql-server-native-client)包含一个 odbc 接口，它是随 SQL Server 2005 到 SQL Server 2012 一起提供的 odbc 驱动程序。 不建议使用此驱动程序进行新的开发。 SQL Server 2012 后， [Microsoft ODBC Driver for SQL Server](#microsoft-odbc-driver-for-sql-server)是使用后续服务器功能更新的驱动程序。

### <a name="sql-server-native-client"></a>SQL Server Native Client

SQL Server Native Client 是一种独立的库，用于 OLE DB 和 ODBC。 SQL Server 2005 到2012中包含 SQL Server Native Client （通常为缩写的 SNAC）。 SQL Server Native Client 可用于需要利用 SQL Server 2005 到 SQL Server 2012 中引入的新功能的应用程序。 （对于 SQL Server 中的这些新功能，Microsoft/Windows 数据访问组件不会更新。）对于超出 SQL Server 2012 的新功能，SQL Server Native Client 将不会更新。 如果你想要充分利用新的 SQL Server 功能，请切换到 SQL Server 的 Microsoft ODBC Driver for SQL Server 或 Microsoft OLE DB 驱动程序。

有关 SQL Server Native Client 的完整文档，请参阅[SQL Server Native Client 文档](../relational-databases/native-client/sql-server-native-client-programming.md)。

### <a name="microsoft-odbc-driver-for-sql-server"></a>Microsoft ODBC Driver for SQL Server

SQL Server 2012 后，SQL Server 的主 ODBC 驱动程序已开发并作为 Microsoft ODBC Driver for SQL Server 发布。 有关详细信息，请参阅[Microsoft ODBC Driver for SQL Server 文档](./odbc/microsoft-odbc-driver-for-sql-server.md)。

## <a name="ole-db"></a>OLE DB

有三个不同代的 Microsoft OLE DB Provider for SQL Server。 第一代“Microsoft OLE DB Provider for SQL Server”(SQLOLEDB) 仍作为 [Windows 数据访问组件](#microsoft-or-windows-data-access-components)的一部分提供。 此提供程序将不会使用新功能进行更新，因此不建议使用此驱动程序进行新的开发。 从 SQL Server 2005 开始， [SQL Server Native Client](#sql-server-native-client)包括 OLE DB 提供程序接口（sqlncli.msi），并且是2005通过 SQL Server 2017 提供的 OLE DB 提供程序。 它[于 2011 年宣布弃用](https://blogs.msdn.microsoft.com/sqlnativeclient/2011/08/29/microsoft-is-aligning-with-odbc-for-native-relational-data-access/)，且不建议在新开发中使用此驱动程序。 在2017中，OLE DB 的数据访问技术随后[取消弃用，并宣布为2018发布新的计划版本](https://blogs.msdn.microsoft.com/sqlnativeclient/2017/10/06/announcing-the-new-release-of-ole-db-driver-for-sql-server/)。 新的 OLE DB 提供程序称为 "适用于 SQL Server 的 Microsoft OLE DB 驱动程序" （MSOLEDBSQL），目前已维护并受支持。

## <a name="adonet"></a>ADO.NET

ADO.NET 是随 Microsoft .NET 框架引入的，可继续进行改进和维护。 它是 Microsoft .NET 框架的核心组件。 有关详细信息，请参阅[Microsoft ADO.NET for SQL Server](ado-net/microsoft-ado-net-sql-server.md)。

## <a name="jdbc"></a>JDBC

### <a name="microsoft-jdbc-driver-for-sql-server"></a>Microsoft JDBC Driver for SQL Server

2000中引入了 Microsoft JDBC Driver for SQL Server 继续改进和维护。 它在2016中是开源的。 有关最新信息（包括如何下载驱动程序），请参阅[JDBC 驱动程序概述](./jdbc/overview-of-the-jdbc-driver.md)。

## <a name="php"></a>PHP

### <a name="microsoft-drivers-for-php-for-sql-server"></a>Microsoft Drivers for PHP for SQL Server

在2009中引入为开源项目，适用于 PHP for SQL Server 的 Microsoft 驱动程序将继续改进和维护。 有关最新信息（包括如何下载 PHP 驱动程序），请参阅[Microsoft 用于 php 的驱动程序 SQL Server](./php/microsoft-php-driver-for-sql-server.md)。

## <a name="nodejs"></a>Node.js

### <a name="microsoft-driver-for-nodejs-for-sql-server"></a>适用于 SQL Server 的 Microsoft Node.JS 驱动程序

Microsoft 的 node.js for SQL Server 驱动程序允许在 Microsoft Windows 上使用 node.js 应用程序，Microsoft Azure 访问 Microsoft SQL Server 和 Microsoft Azure SQL 数据库。 开发工作不再专注于此驱动程序。 建议不要使用适用于 node.js 的 Microsoft Driver for SQL Server 来创建新应用程序。

有关适用于 node.js 的 Microsoft Driver for SQL Server 的详细信息，请参阅[windowsazure.storage/node-sqlserver](https://github.com/Azure/node-sqlserver)。

### <a name="tedious"></a>Tedious

Microsoft 当前在 node.js 中参与和支持开源单调的模块，以便使用 JavaScript 连接到 SQL Server。 有关详细信息，请参阅[Node.js Driver for SQL Server](./node-js/node-js-driver-for-sql-server.md)。

## <a name="microsoft-or-windows-data-access-components"></a>Microsoft 或 Windows 数据访问组件

Microsoft/Windows 数据访问组件（MDAC/WDAC）随附于 Windows，并受其支持，以实现应用程序向后兼容性，并且不是当前 SQL Server 技术堆栈的一部分。 不会向 MDAC/WDAC 中的组件添加任何新功能，也不建议使用它们来进行新的应用程序开发。

出于本文档的目的，可以根据技术和产品将 MDAC/WDAC 堆栈划分为以下组件：

* **ADO** （包括 ADOMD 和 ADOX）
* **OLE DB** （包括 OLE DB 核心服务、SQL Server OLE DB 提供程序、Oracle OLE DB 提供程序、用于 ODBC 驱动程序的 OLE DB 提供程序、数据形状提供程序以及远程数据提供程序）
* **Odbc** （包括 odbc 驱动程序管理器、SQL Odbc 驱动程序和 Oracle Odbc 驱动程序）

### <a name="mdacwdac-components"></a>MDAC/WDAC 组件

MDAC/WDAC 包含以下组件：

* **ODBC：** Microsoft 开放式数据库连接（ODBC）接口是一种 C 编程语言接口，它允许应用程序访问各种数据库管理系统（DBMS）的数据。 使用此 API 的应用程序仅限访问关系数据源。
* **OLE DB：** OLE DB 是一组 COM 接口，用于访问各种数据存储中的数据。 OLE DB 提供程序用于访问数据库、文件系统、消息存储、目录服务、工作流和文档存储区中的数据。
* **ADO：** ActiveX 数据对象（ADO）提供了一个高级编程模型。 尽管比直接对 OLE DB 或 ODBC 编码更小，但 ADO 非常简单，只是了解和使用。 它可用于脚本语言，如 Microsoft Visual Basic Scripting Edition （VBScript）或 Microsoft JScript。
* **ADOMD:**.ADO 多维 (ADOMD) 是与多维数据提供程序，如 Microsoft OLAP 访问接口，也称为 Microsoft Analysis Services 提供程序一起使用。 自 MDAC 2.0 开始，未对其进行重大功能增强。
* **ADOX：** 使用适用于 DDL 和安全性（ADOX）的 ADO 扩展，可以创建和修改数据库、表、索引或存储过程的定义。 可以将 ADOX 用于任何提供程序。 Microsoft Jet OLE DB 提供程序完全支持 ADOX，而 Microsoft SQL Server OLE DB 提供程序提供有限的支持。
* **Microsoft SQL Server 网络库：** SQL Server 的网络库允许 SQLOLEDB 和 SQLODBC 与 SQL Server 数据库通信。 以下 SQL Server 网络库在 MDAC/WDAC 版本中已弃用： Banyan Vines、AppleTalk、ServerNet、IPX/SPX、Giganet 和 RPC。 TCP/IP 和命名管道将继续受支持，并且在64位 Windows 操作系统上可用。
* **MSDASQL:** Microsoft OLE DB Provider for ODBC (MSDASQL) 允许应用程序访问数据源的 ODBC 驱动程序通过 OLE DB 和 ADO （它在内部使用 OLEDB） 上构建的。 MSDASQL 是连接到 ODBC 而不是数据库的 OLEDB 访问接口。 当数据源没有直接 OLE DB 提供程序时，它将作为 OLE DB 到 ODBC 驱动程序的桥。 MSDASQL 随 Windows 操作系统一起提供，Windows Server 2008 和 Vista SP1 是第一个 Windows 版本，其中包含64位版本的技术。

### <a name="deprecated-mdacwdac-components"></a>弃用的 MDAC/WDAC 组件

MDAC/WDAC 的当前版本仍支持这些组件，但在将来的版本中可能会将其删除。 开发新应用程序时，Microsoft 建议避免使用这些组件。 此外，在升级或修改现有应用程序时，请删除对这些组件的任何依赖项。

* **SQLOLEDB:** Microsoft OLE DB Provider for SQL Server (SQLOLEDB)，它支持对 Microsoft SQL Server 的访问，已被弃用。 可能不支持与将来版本的 SQL Server 建立连接。 Windows 7 之后，将从操作系统中删除连接到 SQL Server 7 之前的版本的功能。 新应用程序应使用适用于 SQL Server （MSOLEDBSQL）的 Microsoft OLE DB 驱动程序，该驱动程序支持新的 SQL Server 功能。 现有的应用程序还应迁移到用于 SQL Server 的 Microsoft OLE DB 驱动程序，以获得更好的性能、可靠性和可支持性。 有关详细信息，请参阅[将应用程序更新为从 MDAC SQL Server OLE DB 驱动程序](oledb/applications/updating-an-application-to-oledb-driver-for-sql-server-from-mdac.md)。
* **SQLODBC：** 支持访问 Microsoft SQL Server Microsoft SQL Server ODBC 驱动程序（SQLODBC）已弃用。 可能不支持与将来版本的 SQL Server 建立连接。 Windows 7 之后，将从操作系统中删除连接到 SQL Server 7 之前的版本的功能。 新应用程序应使用支持新 SQL Server 功能的 Windows Microsoft ODBC Driver for SQL Server。 现有的应用程序还应迁移到 Microsoft ODBC Driver for SQL Server，以获得更好的性能、可靠性和可支持性。 有关相关信息，请参阅[将应用程序更新为从 MDAC SQL Server Native Client](../relational-databases/native-client/applications/updating-an-application-to-sql-server-native-client-from-mdac.md)。
* **Microsoft Jet 数据库引擎4.0：** 从版本2.6 开始，MDAC 不再包含 Jet 组件。 换句话说，MDAC 2.6、2.7 和2.8 不包含 Microsoft Jet、Microsoft Jet OLE DB 提供程序、ODBC 桌面数据库驱动程序或 Jet 数据访问对象（DAO）。 

  没有64位版本的 Jet 数据库引擎、Jet OLEDB 驱动程序、Jet ODBC 驱动程序或 Jet DAO 可用。 有关详细信息，请参阅[知识库文章 957570](https://support.microsoft.com/kb/957570)。 在64位版本的 Windows 上，32位 Jet 在 Windows WOW64 子系统下运行。 有关 WOW64 的详细信息，请参阅[MSDN WOW64 文档](/windows/desktop/WinProg64/wow64-implementation-details)。 本机64位应用程序不能与在 WOW64 中运行的32位 Jet 驱动程序通信。

  Microsoft 建议在开发需要关系数据存储的新的非 Microsoft Access 应用程序时，使用[Microsoft SQL Server Express 版](https://www.microsoft.com/sql-server/sql-server-editions-express)，而不是 microsoft Jet。 这些新的或转换后的 Jet 应用程序可以继续使用 Jet，目的是将 Microsoft Office 2003 及更低版本的文件（.mdb 和 .xls）用于非主数据存储。 但是，对于这些应用程序，你应该计划从 Jet 迁移到 Microsoft Access 数据库引擎。 可以[下载 Microsoft Access 数据库引擎](https://www.microsoft.com/download/details.aspx?id=54920)，它可便于对已有 Office 2003（.mdb 和.xls）或 Office 2007（*.accdb、*.xlsm、*.xlsx 和 *.xlsb）文件执行读取和写入操作。

  > [!IMPORTANT]
  > 请阅读 2007 Office 系统最终用户许可协议，了解具体的使用限制。

  > [!NOTE]
  > SQL Server 应用程序还可以通过 2007 Office 系统驱动程序访问 2007 Office 系统，以及更早版本的文件，来自 SQL Server 异构数据连接和集成服务功能。 另外，64位 SQL Server 应用程序可以通过在64位 Windows 上使用32位 SQL Server Integration Services （SSIS）访问32位 Jet 和 2007 Office 系统文件。

* **MSDADS：** 使用用于数据定形的 Microsoft OLE DB 提供程序（MSDADS），可以在应用程序中的键、字段或行集之间创建层次结构关系。 自 MDAC 2.1 以来，未进行重大功能增强。 此提供程序已被弃用。 Microsoft 建议使用 XML，而不是 MSDADS。
* **ORACLE ODBC 和 oracle OLE DB：** Microsoft Oracle ODBC 驱动程序（Oracle ODBC）和 Oracle 的 Microsoft OLE DB 提供程序（Oracle OLE DB）提供对 Oracle 数据库服务器的访问权限。 它们是使用 Oracle 调用接口（OCI）版本7构建的，并为 Oracle 7 提供完全支持。 此外，它还使用 Oracle 7 仿真为 Oracle 8 数据库提供有限的支持。 Oracle 不再支持使用 OCI 版本7调用的应用程序。 这些技术已弃用。 如果你使用的是 Oracle 数据源，则应该迁移到 Oracle 提供的驱动程序和提供程序。
* **RDS:** 远程数据服务 (RDS) 是用于在 Internet 或 Intranet 访问远程 ADO 记录集对象的专有 Microsoft 机制。 RDS 已弃用;自 MDAC 2.1 开始，没有对 RDS 的重大功能增强。 Microsoft 发布了 .NET Framework，它具有广泛的 SOAP 功能并替换了 RDS 组件。 Windows 7 之后，将从操作系统中删除所有 RDS 服务器组件。
* **JRO：** Jet 复制对象（JRO）已弃用。 JRO 用于在 ADO 中使用 Jet （ *.mdb）数据库来创建和压缩 Jet 数据库（.mdb）并执行 Jet 复制管理。MDAC 2.7 将是其最后一个版本。JRO 在64位 Windows 操作系统上不可用。Microsoft Access 2007 文件格式（* .accdb）不支持 JRO。
* **16 位 ODBC 支持：** 如果你使用的是16位应用程序，则应迁移到32位应用程序。 16位功能已弃用，将从64位操作系统中删除。 有关详细信息，请参阅[知识库文章 896458](https://support.microsoft.com/kb/896458)。
* **OLEDB 简单提供程序（MSDAOSP）：** OLEDB 简单提供程序提供了一个框架，用于在简单数据上快速生成 OLE DB 提供程序。 MSDAOSP 已被弃用。
* **ODBC 游标库：** ODBC 游标库（ODBCCR32）提供受限制的客户端数据游标。 ODBC 游标库已弃用;应用程序可以使用服务器端游标实现作为替代。
* **OLE DB 进程外接口远程处理：** OLEDB 接口远程处理（msdaps）尝试允许 OLE DB 提供程序在进程外运行。 已弃用 OLEDB 进程外接口远程处理。
* **AppleTalk 和 Banyan VINES SQL 网络库：** 不推荐使用 Banyan Vines、AppleTalk、ServerNet、IPX/SPX、Giganet 和 RPC SQL 网络库。 如果正在使用其中的任何一项技术，则应修改应用程序以使用其他网络库，如 TCP/IP 和命名管道。

### <a name="mdacwdac-releases"></a>MDAC/WDAC 版本

下面是过去的 MDAC/WDAC 版本的可支持性方案列表，从最早开始。

* **Mdac 1.5、mdac 2.0 和 mdac 2.1：** 这些版本的 MDAC 是独立版本，通过 Microsoft Windows NT 选项包、Microsoft Windows 平台 SDK 或 MDAC 网站发布。 这些 MDAC 版本不再受支持。
* **MDAC 2.5:** 此版本的 MDAC 是随 Windows 2000 操作系统。 MDAC 2.5 的 service pack 随附在相应的 Windows 2000 service pack 中。
* **MDAC 2.6:** MDAC 2.6 RTM、 SP1 和 SP2 已包含 Microsoft SQL Server 2000 RTM、 SP1 和 SP2，分别。 此外，这些 MDAC service pack 按照 Microsoft SQL Server 2000 service pack 版本计划发布到 MDAC 网站。 可以在 Windows 2000、Windows Millennium Edition、Windows NT、Windows 95 和 Windows 98 平台上安装此版本的 MDAC 及其 service pack。 此版本的 MDAC 不再受支持。
* **MDAC 2.7:** 此版本的 MDAC 是随 Microsoft Windows XP RTM 和 SP1 的操作系统。 可以在 Windows 2000、Windows Millennium、Windows NT 和 Windows 98 平台上安装此版本的 MDAC 及其 service pack。 仅可通过操作系统或其服务包在 Windows XP 平台上安装此版本。 此版本的 MDAC 不再受支持。
* **MDAC 2.8:** 此版本的 MDAC 已包含在 Windows Server 2003 和 Windows XP SP2 及更高版本。 你还可以在 Windows 2000 上安装此版本的 MDAC 及其 service pack。

  * Windows Server 2003 发布给客户的同时，也会在 MDAC 网站上发布32位版本的 MDAC 2.8。
  * 64位版本的 MDAC 2.8 随64位版本的 Windows Server 2003 和 Windows XP 一起发布。

* **Windows 数据访问组件（WDAC）：** 从 Windows Vista 和 Windows Server 2008 开始，MDAC 将其名称更改为 "Windows 数据访问组件"。 WDAC 包含为操作系统的一部分，不能单独用于再分发。 适用于 WDAC 的可维护性取决于操作系统的生命周期。

  32位和64位版本的 WDAC 分别与32位和64位版本的 Windows 操作系统一起发布。

## <a name="obsolete-data-access-technologies"></a>过时的数据访问技术

过时的技术是在多个产品版本中尚未增强或更新的技术，这些技术将从未来的产品版本中排除。 编写新应用程序时，请勿使用这些技术。 修改使用这些技术编写的现有应用程序时，请考虑将这些应用程序迁移到 ADO.NET 或其他当前技术。

以下组件被视为已过时：

* **DB-Library:** DB 库是特定于 SQL Server 的编程模型，其中包含 C Api。 自 SQL Server 6.5 起，对 DB-LIBRARY 没有功能增强。 其最终版本是 SQL Server 2000，不会移植到64位 Windows 操作系统。
* **EMBEDDED SQL （E-sql）：** E-SQL 是一种特定于 SQL Server 的编程模型，它允许在 Visual C 代码中嵌入 Transact-sql 语句。 自 SQL Server 6.5 开始，对 E SQL 没有功能增强。 其最终版本是 SQL Server 2000，不会移植到64位 Windows 操作系统。
* **数据访问对象（DAO）：** DAO 提供对 JET （Access）数据库的访问。 此 API 可用于 Microsoft Visual Basic、Microsoft 视觉对象C++和脚本语言。 它包含在 Microsoft Office 2000 和 Office XP 中。 DAO 3.6 是此技术的最终版本。 它在64位 Windows 操作系统上不可用。
* **远程数据对象（RDO）：** RDO 专门用于访问远程 ODBC 关系数据源，并使无需复杂的应用程序代码即可更轻松地使用 ODBC。 它包含在 Microsoft Visual Basic 版本4、5和6中。 RDO 版本2.0 是此技术的最终版本。

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]
