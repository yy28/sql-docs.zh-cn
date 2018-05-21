---
title: Microsoft SQL Server 的驱动程序历史记录 |Microsoft 文档
ms.custom: ''
ms.date: 5/4/2018
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
author: David-Engel
ms.author: v-daveng
manager: kenvh
ms.openlocfilehash: 2f2f4bafe48018da5c6f634b272a540021fd4ca2
ms.sourcegitcommit: 6fd8a193728abc0a00075f3e4766a7e2e2859139
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/17/2018
---
# <a name="driver-history-for-microsoft-sql-server"></a>Microsoft SQL Server 的驱动程序历史记录

本页介绍用于连接到 SQL Server 的 Microsoft 的历史数据连接技术。

## <a name="odbc"></a>ODBC

有三个不同 SQL Server 的 Microsoft ODBC 驱动程序代。 第一个"SQL Server"ODBC 驱动程序仍作为的一部分附带[Windows 数据访问组件](#microsoft-or-windows-data-access-components)。 不建议新的开发使用该驱动程序。 从 SQL Server 2005 开始[SQL Server Native Client](#sql-server-native-client)包含 ODBC 接口，并且随通过 SQL Server 2012 的 SQL Server 2005 的 ODBC 驱动程序。 不建议新的开发使用该驱动程序。 SQL Server 2012 之后, [Microsoft ODBC Driver for SQL Server](#microsoft-odbc-driver-for-sql-server)是最新的服务器功能，今后使用更新的驱动程序。

### <a name="sql-server-native-client"></a>SQL Server Native Client

SQL Server Native Client 是一个独立的库，用于 OLE DB 和 ODBC。 SQL Server Native Client (通常缩写 SNAC) 通过 2012年已包含在 SQL Server 2005 中。 SQL Server Native Client 可以用于应用程序需要利用通过 SQL Server 2012 的 SQL Server 2005 中引入的新功能。 （Microsoft/Windows 数据访问组件不会更新为 SQL Server 中的这些新功能。）有关超出 SQL Server 2012 的新功能，将不会更新 SQL Server Native Client。 如果，切换到 Microsoft ODBC 驱动程序为 SQL Server 或 Microsoft OLE DB 驱动程序的 SQL Server 你想要利用新今后的 SQL Server 功能。

SQL Server Native Client 的完整文档，请参阅[SQL Server Native Client 文档](../relational-databases/native-client/sql-server-native-client-programming.md)。

### <a name="microsoft-odbc-driver-for-sql-server"></a>Microsoft ODBC Driver for SQL Server

SQL Server 2012 起主 ODBC driver for SQL Server 已开发和发布为 Microsoft ODBC Driver for SQL Server。 有关详细信息，请参阅[Microsoft ODBC Driver for SQL Server 文档](./odbc/microsoft-odbc-driver-for-sql-server.md)。

## <a name="ole-db"></a>OLE DB

有三个不同级别的 SQL server 的 Microsoft OLE DB 提供程序。 第一个"Microsoft OLE DB Provider for SQL Server"(SQLOLEDB) 仍作为的一部分附带[Windows 数据访问组件](#microsoft-or-windows-data-access-components)。 此提供程序将不会更新与新的功能并不建议新的开发使用该驱动程序。 从 SQL Server 2005 开始[SQL Server Native Client](#sql-server-native-client)包含 OLE DB 提供程序接口 (SQLNCLI)，并且随 SQL Server 2017 通过 SQL Server 2005 的 OLE DB 访问接口。 它是[宣布弃用在 2011 年](https://blogs.msdn.microsoft.com/sqlnativeclient/2011/08/29/microsoft-is-aligning-with-odbc-for-native-relational-data-access/)，不建议新的开发使用该驱动程序。 自 2017 年，OLE DB 数据访问技术是在随后[undeprecated 和新计划的发布已宣布](https://blogs.msdn.microsoft.com/sqlnativeclient/2017/10/06/announcing-the-new-release-of-ole-db-driver-for-sql-server/)为 2018年。 新的 OLE DB 访问接口称为"Microsoft OLE DB 驱动程序的 SQL Server"(MSOLEDBSQL) 是当前维护和支持。

## <a name="adonet"></a>ADO.NET

ADO.NET 中引入了 Microsoft.NET Framework，并持续改进和维护。 它是 Microsoft.NET Framework 的核心组件。 有关详细信息，请参阅[的 SQL Server 的 Microsoft ADO.NET](ado-net/microsoft-ado-net-for-sql-server.md)。

## <a name="jdbc"></a>JDBC

### <a name="microsoft-jdbc-driver-for-sql-server"></a>Microsoft JDBC Driver for SQL Server

在 2000年中引入，继续改进和维护 Microsoft JDBC Driver for SQL Server。 它是开源 2016年中。 有关最新信息，包括如何下载驱动程序，请参阅[JDBC 驱动程序概述](./jdbc/overview-of-the-jdbc-driver.md)。

## <a name="php"></a>PHP

### <a name="microsoft-drivers-for-php-for-sql-server"></a>Microsoft Drivers for PHP for SQL Server

作为开放源代码项目引入在 2009 年，继续改进和维护 Microsoft Drivers for PHP for SQL Server。 有关最新信息，包括如何下载 PHP 驱动程序，请参阅[Microsoft Drivers for PHP for SQL Server](./php/microsoft-php-driver-for-sql-server.md)。

## <a name="nodejs"></a>Node.js

### <a name="microsoft-driver-for-nodejs-for-sql-server"></a>Microsoft 的 Node.js for SQL Server 驱动程序

Microsoft Driver for Node.js for SQL Server 允许 Node.js 应用程序在 Microsoft Windows 和 Microsoft Windows Azure 上的，若要访问 Microsoft SQL Server 和 Microsoft Windows Azure SQL 数据库。 开发工作不再正在关注此驱动程序。 建议不要创建新应用程序使用的 Node.js for SQL Server 的 Microsoft 驱动程序。

有关详细信息 Microsoft Driver for Node.js for SQL Server，请参阅[WindowsAzure / 节点 sqlserver](https://github.com/Azure/node-sqlserver)。

### <a name="tedious"></a>需要很长时间

当前，Microsoft 可能会导致，并用于连接到 SQL Server 使用 JavaScript 在 Node.js 中支持的开源乏味模块。 有关详细信息，请参阅[Node.js Driver for SQL Server](./node-js/node-js-driver-for-sql-server.md)。

## <a name="microsoft-or-windows-data-access-components"></a>Microsoft 或 Windows 数据访问组件

Microsoft/Windows 数据访问组件 (MDAC/WDAC) 都附带有和支持的 Windows 应用程序向后兼容性不是当前的 SQL Server 技术堆栈的一部分。 没有新功能将添加到中 MDAC/WDAC 的组件，并且不建议以将其用于开发新应用程序。

出于本文档的目的，你可以将 MDAC/WDAC 堆栈划分为以下组件，根据技术和产品：

* **ADO** （包括 ADOMD 和 ADOX）
* **OLE DB** （对于 ODBC 驱动程序、 数据 Shape 提供程序和远程数据提供程序，包括 OLE DB 核心服务、 SQL Server OLE DB 提供程序、 Oracle OLE DB 访问接口、 OLE DB 访问接口）
* **ODBC** （包括 ODBC 驱动程序管理器、 SQL ODBC 驱动程序和 Oracle ODBC 驱动程序）

### <a name="mdacwdac-components"></a>MDAC/WDAC 组件

MDAC/WDAC 包括这些组件：

* **ODBC:** Microsoft 开放式数据库连接 (ODBC) 接口是一个 C 编程语言接口，允许应用程序使用不同的数据库管理系统 (DBMS) 访问数据。 使用此 API 的应用程序仅限于访问仅关系数据源。
* **OLE DB:** OLE DB 是一套用于访问各种数据存储中的数据的 COM 接口。 OLE DB 提供程序存在访问数据库、 文件系统、 消息存储、 目录服务、 流和文档存储中的数据。
* **ADO:** ActiveX 数据对象 (ADO) 提供了高级的编程模型。 尽管少见性能高于直接编码到 OLE DB 或 ODBC，ADO 是简单地了解和使用。 它可以从脚本语言，如 Microsoft Visual Basic Scripting Edition (VBScript) 或 Microsoft JScript 中使用。
* **ADOMD:** ADO 多维 (ADOMD) 是与多维数据提供程序，如 Microsoft OLAP 提供，也称为 Microsoft Analysis Services 提供程序一起使用。 自 MDAC 2.0 以来，没有主要增强功能，具有对它进行。
* **ADOX:** DDL 和安全 (ADOX) 的 ADO 扩展启用的创建和修改数据库、 表、 索引或存储的过程的定义。 ADOX 可以使用任何提供程序。 Microsoft Jet OLE DB 提供程序提供对 ADOX，完全支持，而 Microsoft SQL Server OLE DB 提供程序提供有限的支持。
* **Microsoft SQL Server 网络库：** SQL Server 网络库允许 SQLOLEDB 和 SQLODBC 与 SQL Server 数据库进行通信。 已弃用以下 SQL Server 网络库在 MDAC/WDAC 版本： Banyan Vines、 AppleTalk、 ServerNet、 IPX/SPX、 Giganet 和 RPC。 TCP/IP 和命名管道将继续提供支持，并在 64 位 Windows 操作系统上可用。
* **MSDASQL:** Microsoft OLE DB 提供程序的 ODBC (MSDASQL) 允许访问数据源的 ODBC 驱动程序通过 OLE DB 和 ADO （它在内部使用 OLEDB） 构建的应用程序。 MSDASQL 是 OLEDB 访问接口连接到 ODBC，而不是数据库。 它旨在作为桥从 OLE DB 的 ODBC 驱动程序时没有直接的 OLE DB 提供程序的某个数据源。 MSDASQL 附带了 Windows 操作系统和 Windows Server 2008 和 Vista SP1 中的第一个 Windows 释放以包括该技术的 64 位版本。

### <a name="deprecated-mdacwdac-components"></a>不推荐使用的 MDAC/WDAC 组件

MDAC/WDAC，当前版本中仍支持这些组件，但它们可能在将来的版本中删除。 当开发新应用程序，Microsoft 建议你避免使用这些组件。 此外，当你升级或修改现有应用程序时，删除任何依赖于这些组件。

* **SQLOLEDB:** Microsoft OLE DB 提供程序的 SQL Server (SQLOLEDB)，它支持对 Microsoft SQL Server 的访问，已弃用。 其连接到 SQL Server 的未来版本可能不支持。 在 Windows 7 之后，将从操作系统删除早于 SQL Server 7 连接到版本的功能。 新的应用程序应使用 Microsoft OLE DB 驱动程序的 SQL Server (MSOLEDBSQL)，它支持新的 SQL Server 功能。 现有应用程序应该迁移到 Microsoft OLE DB 驱动程序适用于 SQL Server 以及更好的性能、 可靠性和可支持性的。 有关详细信息，请参阅[更新为 OLE DB 驱动程序的应用程序适用于 SQL Server 从 MDAC](oledb/applications/updating-an-application-to-oledb-driver-for-sql-server-from-mdac.md)。
* **SQLODBC:** Microsoft SQL Server ODBC 驱动程序 (SQLODBC)，它支持对 Microsoft SQL Server 的访问，已弃用。 其连接到 SQL Server 的未来版本可能不支持。 在 Windows 7 之后，将从操作系统删除早于 SQL Server 7 连接到版本的功能。 新的应用程序应使用用于在 Windows 上，支持新的 SQL Server 功能的 SQL Server 的 Microsoft ODBC 驱动程序。 现有应用程序应该迁移到 Microsoft ODBC Driver for SQL Server 以及更好的性能、 可靠性和可支持性的。 有关相关信息，请参阅[更新到 SQL Server Native Client 应用程序从 MDAC](../relational-databases/native-client/applications/updating-an-application-to-sql-server-native-client-from-mdac.md)。
* **Microsoft Jet 数据库引擎 4.0:** 从版本 2.6 开始，MDAC 不再包含 Jet 组件。 换而言之，MDAC 2.6、 2.7 和 2.8 不包含 Microsoft Jet、 Microsoft Jet OLE DB 提供程序、 ODBC 桌面数据库驱动程序或 Jet 数据访问对象 (DAO)。 Microsoft Jet 数据库引擎 4.0 组件输入函数的弃用的状态和持续保持工程和加入在 Windows 2000 中的 Microsoft Windows 以来未收到的增强功能级别。

  没有可用的 64 位版本的 Jet 数据库引擎、 Jet ole DB 驱动程序、 Jet ODBC 驱动程序或 Jet DAO。 有关详细信息，请参阅[知识库文章 957570](http://support.microsoft.com/kb/957570)。 在 64 位版本的 Windows，32 位 Jet Windows WOW64 子系统下运行。 在 WOW64 上的详细信息，请参阅[MSDN WOW64 文档](https://msdn.microsoft.com/library/windows/desktop/aa384274(v=vs.85).aspx)。 本机 64 位应用程序无法与在 WOW64 中运行的 32 位 Jet 驱动程序通信。

  Microsoft 建议使用而不是 Microsoft Jet [Microsoft SQL Server Express Edition](https://www.microsoft.com/sql-server/sql-server-editions-express)开发新的、 非 Microsoft Access 应用程序需要关系数据存储时。 这些新的或转换后的 Jet 应用程序可以继续使用 Jet 目的是要使用 Microsoft Office 2003 和更早版本的文件 （.mdb 和.xls） 进行非主数据存储。 但是，对于这些应用程序，你应计划将 Jet 迁移到 2007 Office System 驱动程序。 你可以[下载 2007 Office System 驱动程序](https://www.microsoft.com/downloads/details.aspx?displaylang=en&FamilyID=7554f536-8c28-4598-9b72-ef94e038c891)，可用于读取和写入到预先存在的文件，在 Office 2003 （.mdb 和.xls） 或 Office 2007 （您可能正在、 *.xlsm、 *.xlsx 和 *.xlsb） 文件格式。

  > [!IMPORTANT]
  > 请阅读有关特定的用量限制 2007 Office 系统最终用户许可协议。

  > [!NOTE]
  > SQL Server 应用程序还可以访问 2007 Office System，和更早版本，文件从 SQL Server 异类数据连接和 Integrations Services 功能，通过 2007 Office System 驱动程序。 此外，64 位 SQL Server 应用程序可以通过访问的 32 位 Jet 和 2007 Office System 文件在 64 位 Windows 上使用 32 位 SQL Server Integration Services (SSIS)。

* **MSDADS:** Microsoft OLE DB 提供程序的数据调整 (MSDADS)，你可以创建应用程序密钥、 字段或行集之间的层次结构关系。 以来 MDAC 2.1 不进行了任何主要功能增强功能。 已弃用此提供程序。 Microsoft 建议你使用的 XML，而不是 MSDADS。
* **Oracle ODBC 和 Oracle OLE DB:** Microsoft Oracle ODBC 驱动程序 (Oracle ODBC) 和 Microsoft OLE DB Provider for Oracle (Oracle OLE DB) 提供对 Oracle 数据库服务器的访问。 它们使用 Oracle 调用接口 (OCI) 版本 7 生成的并对 Oracle 7 提供完全支持。 此外，它使用 Oracle 7 仿真为 Oracle 8 数据库提供有限的支持。 Oracle 不再支持使用 OCI 版本 7 调用应用程序。 这些技术，已弃用。 如果你使用的 Oracle 数据源，则应迁移到 Oracle 提供的驱动程序和提供程序。
* **RDS:** 远程数据服务 (RDS) 是用于通过 Internet 或 Intranet 访问远程 ADO 记录集对象的专有 Microsoft 机制。 RDS 已弃用;任何主要增强功能，以来不进行了到 RDS MDAC 2.1。 Microsoft 已发布.NET Framework 中，具有大量 SOAP 功能并将 RDS 组件。 在 Windows 7 后，将从操作系统删除所有的 RDS 服务器组件。
* **JRO:** Jet 复制对象 (JRO) 已弃用。 在与 Jet 的 ADO 内使用 JRO (*.mdb) 数据库来创建和压缩 Jet 数据库 (.mdb) 以及执行 Jet 复制管理。MDAC 2.7 将其最后一个版本。JRO 不能在 64 位 Windows 操作系统上。JRO 不支持在 Microsoft Access 2007 文件格式 (*.accdb)。
* **16 位 ODBC 支持：** 如果使用的 16 位应用程序，则应迁移到 32 位应用程序。 16 位功能已弃用，并正在从 64 位操作系统中删除。 有关详细信息，请参阅[知识库文章 896458](http://support.microsoft.com/kb/896458)。
* **OLEDB 简单的提供程序 (MSDAOSP):** OLEDB 简单提供商提供一个框架，用于快速创建通过简单的数据的 OLE DB 提供程序。 MSDAOSP 已弃用。
* **ODBC 游标库：** ODBC 游标库 (ODBCCR32.dll) 提供有限的客户端数据游标。 ODBC 游标库已弃用;作为替代，你的应用程序可以使用服务器端游标实现。
* **OLE DB 进程外接口远程处理：** OLEDB 接口远程处理 (msdaps.dll) 试图允许 OLE DB 提供程序在进程外运行。 OLEDB 进程外接口远程处理已弃用。
* **AppleTalk 和 Banyan Vines SQL 网络库：** Banyan Vines、 AppleTalk、 ServerNet、 IPX/SPX、 Giganet 和 RPC SQL 网络库已弃用。 如果你使用任何一种技术，则应修改你的应用程序使用的其他网络库，如 TCP/IP 和命名管道之一。

### <a name="mdacwdac-releases"></a>MDAC/WDAC 版本

下面是过去 MDAC/WDAC 版本中，从开始的最早的可支持性方案的列表。

* **MDAC 1.5、 MDAC 2.0 和 MDAC 2.1:** MDAC 这些版本已通过 Microsoft Windows NT 选项包、 Microsoft Windows 平台 SDK 或 MDAC Web 站点已发布的独立版本。 不再支持这些版本的 MDAC。
* **MDAC 2.5:** MDAC 此版本不包括 Windows 2000 操作系统。 Service pack 的 MDAC 2.5 中已包含相应的 Windows 2000 service pack。
* **MDAC 2.6:** MDAC 2.6 RTM、 SP1 和 SP2 已包含 Microsoft SQL Server 2000 RTM、 SP1 和 SP2，分别。 此外，这些 MDAC service pack 发布到 Microsoft SQL Server 2000 服务包版本计划根据 MDAC Web 站点。 你可以在 Windows 2000、 Windows Millennium Edition、 Windows NT、 Windows 95 和 Windows 98 平台上安装此版本的 MDAC 和其 service pack。 此版本的 MDAC 不再被支持。
* **MDAC 2.7:** MDAC 此版本不包括在 Microsoft Windows XP RTM 和 SP1 操作系统。 你可以在 Windows 2000、 Windows Millennium、 Windows NT 和 Windows 98 平台上安装此版本的 MDAC 和其 service pack。 您可以仅通过操作系统或其服务包在 Windows XP 平台上安装此版本。 此版本的 MDAC 不再被支持。
* **MDAC 2.8:** MDAC 此版本已包含在 Windows Server 2003 和 Windows XP SP2 和更高版本。 你还可以安装此版本的 MDAC 和其 service pack 在 Windows 2000 上。

  * MDAC 2.8 的 32 位版本也已发布到 MDAC Web 站点在同一时间 Windows Server 2003 发布给客户。
  * MDAC 2.8 的 64 位版本的 Windows Server 2003 和 Windows XP 64 位版本发布。

* **Windows 数据访问组件 (WDAC):** MDAC 更改其名称为 WDAC 的"Windows 数据访问组件"启动 Windows Vista 和 Windows Server 2008。 WDAC 是操作系统的一部分包括，并且不可单独于重新分发。 有关 WDAC 的可维护性受到操作系统的生命周期。

  分别带有 32 位和 64 位版本的 Windows 操作系统，发布的 WDAC 的 32 位和 64 位版本。

## <a name="obsolete-data-access-technologies"></a>过时的数据访问技术

已过时的技术，它们是的技术和，尚未增强或在多个产品版本中更新，将从未来的产品版本中排除。 当你编写新的应用程序，则不使用这些技术。 当修改现有应用程序使用这些技术编写的时，请考虑迁移到 ADO.NET 或另一种当前技术这些应用程序。

以下组件将被视为已过时：

* **Db-library:** DB 库是一个 SQL Server 特定编程模型，包括 C Api。 自 SQL Server 6.5 以来已被 Db-library 没有功能增强功能。 最终发布与 SQL Server 2000 中，但它不移植到 64 位 Windows 操作系统。
* **(E SQL) 的嵌入式 SQL:** E SQL 是使 Transact SQL 语句能够嵌入到 Visual C 代码中的 SQL Server 特定编程模型。 没有功能增强功能进行了 E SQL 到 SQL Server 6.5。 最终发布与 SQL Server 2000 中，但它不移植到 64 位 Windows 操作系统。
* **数据访问对象 (DAO):** DAO 提供对 JET （访问） 数据库的访问权限。 此 API 可以用于从 Microsoft Visual Basic、 Microsoft Visual c + + 和脚本语言。 它已包含在 Microsoft Office 2000 和 Office XP。 DAO 3.6 是这种技术的最终版本。 它将不能在 64 位 Windows 操作系统上。
* **远程数据对象 (RDO):** RDO 设计为专门用于访问远程 ODBC 关系数据源，并使其更易于而无需复杂的应用程序代码中使用 ODBC。 它不包括 Microsoft Visual Basic 版本 4、 5 和 6。 RDO 2.0 版时此技术的最终版本。