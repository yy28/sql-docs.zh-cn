---
title: Microsoft SQL server 驱动程序历史记录 |Microsoft Docs
ms.custom: ''
ms.date: 5/4/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
author: David-Engel
ms.author: v-daveng
manager: kenvh
ms.openlocfilehash: 98f49213afaaac17ea41a366bf4888043cc61045
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52529436"
---
# <a name="driver-history-for-microsoft-sql-server"></a>Microsoft SQL server 驱动程序历史记录

本页介绍 Microsoft 的历史数据连接技术连接到 SQL Server。

## <a name="odbc"></a>ODBC

有三个不同 SQL Server 的 Microsoft ODBC 驱动程序代。 第一个"SQL Server"ODBC 驱动程序的一部分仍附带[Windows 数据访问组件](#microsoft-or-windows-data-access-components)。 建议不要用于新的开发使用此驱动程序。 从 SQL Server 2005 开始[SQL Server Native Client](#sql-server-native-client)包含 ODBC 接口，并且与通过 SQL Server 2012 的 SQL Server 2005 一起提供的 ODBC 驱动程序。 建议不要用于新的开发使用此驱动程序。 SQL Server 2012 后[Microsoft ODBC Driver for SQL Server](#microsoft-odbc-driver-for-sql-server)是最新的服务器功能，今后使用更新的驱动程序。

### <a name="sql-server-native-client"></a>SQL Server Native Client

SQL Server Native Client 是一个用于 OLE DB 和 ODBC 的独立库。 SQL Server Native Client (常缩写 SNAC) 中 SQL Server 2005 包含到 2012 年。 SQL Server Native Client 可用于需要利用通过 SQL Server 2012 的 SQL Server 2005 中引入的新功能的应用程序。 （Microsoft/Windows 数据访问组件不会更新为 SQL Server 中的新功能。）有关超出 SQL Server 2012 的新功能，将不会更新 SQL Server Native Client。 切换到 Microsoft ODBC 驱动程序为 SQL Server 或 Microsoft OLE DB 驱动程序的 SQL Server 如果你想要充分利用新今后的 SQL Server 功能。

SQL Server Native Client 的完整文档，请参阅[SQL Server Native Client 文档](../relational-databases/native-client/sql-server-native-client-programming.md)。

### <a name="microsoft-odbc-driver-for-sql-server"></a>Microsoft ODBC Driver for SQL Server

SQL Server 2012 起的主要的 ODBC driver for SQL Server 已通过开发并发布作为 Microsoft ODBC 驱动程序适用于 SQL Server。 有关详细信息，请参阅[Microsoft ODBC Driver for SQL Server 文档](./odbc/microsoft-odbc-driver-for-sql-server.md)。

## <a name="ole-db"></a>OLE DB

有三个不同代的 SQL Server 的 Microsoft OLE DB 提供程序。 第一个"Microsoft OLE DB Provider for SQL Server"(SQLOLEDB) 仍附带作为的一部分[Windows 数据访问组件](#microsoft-or-windows-data-access-components)。 此提供程序将不会更新新功能并不建议新的开发使用此驱动程序。 从 SQL Server 2005 开始[SQL Server Native Client](#sql-server-native-client)包含一个 OLE DB 提供程序接口 (SQLNCLI)，并且随 SQL Server 2005 到 SQL Server 2017 的 OLE DB 访问接口。 它是[宣布弃用在 2011 年](https://blogs.msdn.microsoft.com/sqlnativeclient/2011/08/29/microsoft-is-aligning-with-odbc-for-native-relational-data-access/)，不建议新的开发使用此驱动程序。 在 2017 中，OLE DB 数据访问技术已随后[取消弃用和新计划的发布已宣布](https://blogs.msdn.microsoft.com/sqlnativeclient/2017/10/06/announcing-the-new-release-of-ole-db-driver-for-sql-server/)2018 年。 新的 OLE DB 访问接口称为"Microsoft OLE DB Driver for SQL Server"(MSOLEDBSQL) 和当前维护和支持。

## <a name="adonet"></a>ADO.NET

ADO.NET 中引入了 Microsoft.NET Framework，并持续改进和维护。 它是 Microsoft.NET Framework 的核心组件。 有关详细信息，请参阅[用于 SQL Server 的 Microsoft ADO.NET](ado-net/microsoft-ado-net-for-sql-server.md)。

## <a name="jdbc"></a>JDBC

### <a name="microsoft-jdbc-driver-for-sql-server"></a>Microsoft JDBC Driver for SQL Server

在 2000 年引进继续进行改进和维护 Microsoft JDBC Driver for SQL Server。 它是开源 2016年中。 有关最新信息，包括如何下载该驱动程序，请参阅[JDBC 驱动程序概述](./jdbc/overview-of-the-jdbc-driver.md)。

## <a name="php"></a>PHP

### <a name="microsoft-drivers-for-php-for-sql-server"></a>Microsoft Drivers for PHP for SQL Server

在 2009 年引入作为开放源代码项目，继续进行改进和维护 Microsoft Drivers for PHP for SQL Server。 有关最新信息，包括如何下载 PHP 驱动程序，请参阅[Microsoft Drivers for PHP for SQL Server](./php/microsoft-php-driver-for-sql-server.md)。

## <a name="nodejs"></a>Node.js

### <a name="microsoft-driver-for-nodejs-for-sql-server"></a>Microsoft 的 Node.js for SQL Server 驱动程序

Microsoft Driver for Node.js for SQL Server 允许 Node.js 应用程序在 Microsoft Windows 和 Microsoft Windows Azure 上的，若要访问 Microsoft SQL Server 和 Microsoft Windows Azure SQL 数据库。 开发工作不再正在关注此驱动程序。 建议不要创建新的应用程序使用 Microsoft Driver for Node.js for SQL Server。

有关详细信息，Microsoft 驱动程序适用于 Node.js 的 SQL Server，请参阅[WindowsAzure / 节点 sqlserver](https://github.com/Azure/node-sqlserver)。

### <a name="tedious"></a>单调乏味

当前，Microsoft 可能会导致，并在 Node.js 中支持的开源单调乏味模块，与使用 JavaScript 的 SQL Server 的连接。 有关详细信息，请参阅[Node.js Driver for SQL Server](./node-js/node-js-driver-for-sql-server.md)。

## <a name="microsoft-or-windows-data-access-components"></a>Microsoft 或 Windows 数据访问组件

Microsoft/Windows 数据访问组件 (MDAC/WDAC) 都附带有和支持的 Windows 应用程序向后兼容性并不是当前的 SQL Server 技术堆栈的一部分。 没有新的功能将添加到 MDAC/WDAC 中的组件和不建议将其用于开发新应用程序。

有关此文档的目的，你可以将 MDAC/WDAC 堆栈划分为根据技术和产品的以下组件：

* **ADO** （包括 ADOMD 和 ADOX）
* **OLE DB** （请包括 OLE DB 核心服务、 SQL Server OLE DB 访问接口、 Oracle OLE DB 访问接口、 OLE DB Provider for ODBC 驱动程序、 数据形状提供程序和远程数据访问接口）
* **ODBC** （包括 ODBC 驱动程序管理器、 SQL ODBC 驱动程序和 Oracle ODBC 驱动程序）

### <a name="mdacwdac-components"></a>MDAC/WDAC 组件

MDAC/WDAC 包含以下组件：

* **ODBC:** Microsoft 开放式数据库连接 (ODBC) 接口是一个 C 编程语言界面，使应用程序从各种数据库管理系统 (DBMS) 访问数据。 使用此 API 的应用程序被限制为访问仅关系数据源。
* **OLE DB:** OLE DB 是一组用于访问各种数据存储中的数据的 COM 接口。 OLE DB 访问接口存在访问数据库、 文件系统、 消息存储中，目录服务、 工作流和文档存储中的数据。
* **ADO:** ActiveX 数据对象 (ADO) 提供高级的编程模型。 虽然有点不太高性能比直接编码到 OLE DB 或 ODBC ADO 非常简单易用。 可以从 Microsoft Visual Basic Scripting Edition (VBScript) 或 Microsoft JScript 等脚本语言，使用它。
* **ADOMD:** ADO 多维 (ADOMD) 是与多维数据提供程序，如 Microsoft OLAP 访问接口，也称为 Microsoft Analysis Services 提供程序一起使用。 自 MDAC 2.0 以来，没有主要的增强功能，具有对它进行。
* **ADOX:** DDL 和安全 (ADOX) 的 ADO 扩展来创建和修改数据库、 表、 索引或存储的过程的定义。 ADOX 可使用任何提供程序。 Microsoft Jet OLE DB 访问接口提供对 ADOX，完全支持，而 Microsoft SQL Server OLE DB 访问接口提供有限的支持。
* **Microsoft SQL Server 网络库：** SQL 服务器的网络库允许 SQLOLEDB 和 SQLODBC 与 SQL Server 数据库进行通信。 已弃用以下 SQL Server 网络库在 MDAC/WDAC 版本： Banyan Vines、 AppleTalk、 ServerNet、 IPX/SPX、 Giganet 和 RPC。 TCP/IP 和 Named Pipes 将继续支持和 64 位 Windows 操作系统上可用。
* **MSDASQL:** Microsoft OLE DB Provider for ODBC (MSDASQL) 允许在 OLE DB 和 ADO （它在内部使用 OLEDB） 通过 ODBC 驱动程序访问数据源生成的应用程序。 MSDASQL 是 OLEDB 访问接口连接到 ODBC，而不是数据库。 它旨在好似一架桥从 OLE DB 的 ODBC 驱动程序时没有直接的 OLE DB 提供程序存在的数据源。 MSDASQL 附带 Windows 操作系统和 Windows Server 2008 和 Vista SP1 是第一个 Windows 版本包括 64 位版本的技术。

### <a name="deprecated-mdacwdac-components"></a>不推荐使用的 MDAC/WDAC 组件

这些组件在当前版本的 MDAC/WDAC 中仍受支持，但它们可能在将来的版本中删除。 当开发新应用程序，Microsoft 建议您不要使用这些组件。 此外，在升级或修改现有应用程序，则删除这些组件的任何依赖。

* **SQLOLEDB:** Microsoft OLE DB Provider for SQL Server (SQLOLEDB)，它支持对 Microsoft SQL Server 的访问，已弃用。 其连接到 SQL Server 的未来版本可能不支持。 在 Windows 7 后，将从操作系统删除连接到版本早于 SQL Server 7 的功能。 新的应用程序应使用 Microsoft OLE DB 驱动程序的 SQL Server (MSOLEDBSQL)，它支持新的 SQL Server 功能。 现有的应用程序应该迁移到 Microsoft OLE DB 驱动程序适用于 SQL Server 也以提高性能、 可靠性和可支持性。 有关详细信息，请参阅[更新到 OLE DB 驱动程序的应用程序适用于 SQL Server 从 MDAC](oledb/applications/updating-an-application-to-oledb-driver-for-sql-server-from-mdac.md)。
* **SQLODBC:** Microsoft SQL Server ODBC 驱动程序 (SQLODBC)，它支持对 Microsoft SQL Server 的访问，已被弃用。 其连接到 SQL Server 的未来版本可能不支持。 在 Windows 7 后，将从操作系统删除连接到版本早于 SQL Server 7 的功能。 新的应用程序应使用 Windows，支持新的 SQL Server 功能上的 SQL Server 的 Microsoft ODBC 驱动程序。 现有的应用程序应该迁移到 Microsoft ODBC Driver for SQL Server 也以提高性能、 可靠性和可支持性。 有关相关信息，请参阅[更新到 SQL Server Native Client 应用程序从 MDAC](../relational-databases/native-client/applications/updating-an-application-to-sql-server-native-client-from-mdac.md)。
* **Microsoft Jet 数据库引擎 4.0:** 从 2.6 版开始，MDAC 不再包含 Jet 组件。 换而言之，MDAC 2.6，2.7、 2.8 不包含 Microsoft Jet、 Microsoft Jet OLE DB 访问接口或 ODBC 桌面数据库驱动程序，Jet 数据访问对象 (DAO)。 Microsoft Jet 数据库引擎 4.0 组件输入功能不推荐使用的状态和持续的工程设计，并成为 Windows 2000 中的 Microsoft Windows 的一部分以来未收到的增强功能级别。

  没有可用的 64 位版本的 Jet 数据库引擎、 Jet OLEDB 驱动程序、 Jet ODBC 驱动程序或 Jet DAO。 有关详细信息，请参阅[知识库文章 957570](https://support.microsoft.com/kb/957570)。 在 64 位版本的 Windows，32 位 Jet Windows WOW64 子系统下运行。 WOW64 的详细信息，请参阅[MSDN WOW64 文档](/windows/desktop/WinProg64/wow64-implementation-details)。 本机 64 位应用程序无法在 WOW64 中运行的 32 位 Jet 驱动程序与通信。

  Microsoft 建议使用而不是 Microsoft Jet [Microsoft SQL Server Express Edition](https://www.microsoft.com/sql-server/sql-server-editions-express)开发新的、 需要关系数据存储区的 Microsoft Access 应用程序时。 这些新的或转换后的 Jet 应用程序可以继续使用 Jet 使用 Microsoft Office 2003 和更早的文件 （.mdb 和.xls） 的目的进行非主数据存储。 但是，对于这些应用程序，你应计划将 Jet 迁移到 2007 Office 系统驱动程序。 你可以[下载 2007 Office System Driver](https://www.microsoft.com/downloads/details.aspx?displaylang=en&FamilyID=7554f536-8c28-4598-9b72-ef94e038c891)，可用于读取和写入到预先存在的文件 （.mdb 和.xls） 的 Office 2003 或 Office 2007 （*.accdb，*.xlsm、 *.xlsx 和 *.xlsb） 文件格式中。

  > [!IMPORTANT]
  > 请阅读有关特定的用量限制 2007 Office 系统最终用户许可协议。

  > [!NOTE]
  > SQL Server 应用程序还可以访问 2007 Office System 和更早版本，文件从 SQL Server 异类数据连接和集成服务功能，通过 2007 Office 系统驱动程序。 此外，64 位 SQL Server 应用程序可以访问 32 位 Jet 和 2007 Office System 文件在 64 位 Windows 上使用 32 位 SQL Server Integration Services (SSIS)。

* **MSDADS:** 使用 Microsoft OLE DB 访问接口的数据整理 (MSDADS)，可以创建密钥、 字段或行集之间的层次结构关系应用程序中。 自 MDAC 2.1 不进行了任何主要功能的增强功能。 已弃用此提供程序。 Microsoft 建议你使用 XML，而不是 MSDADS。
* **Oracle ODBC 和 Oracle OLE DB:** Microsoft Oracle ODBC 驱动程序 (Oracle ODBC) 和 Microsoft OLE DB Provider for Oracle (Oracle OLE DB) 提供对 Oracle 数据库服务器的访问。 它们使用 Oracle 调用接口 (OCI) 版本 7 生成的并提供对 Oracle 7 的完全支持。 此外，它使用 Oracle 7 仿真对于 Oracle 8 数据库提供有限的支持。 Oracle 不再支持使用 OCI 版本 7 调用的应用程序。 不推荐使用这些技术。 如果使用 Oracle 数据源，则应迁移到 Oracle 提供的驱动程序和提供程序。
* **RDS:** 远程数据服务 (RDS) 是用于在 Internet 或 Intranet 访问远程 ADO 记录集对象的专有 Microsoft 机制。 RDS 是不推荐使用;已自 MDAC 2.1 到 RDS 没有主要功能的增强功能。 Microsoft 发布了.NET Framework 中，具有广泛的 SOAP 功能并将 RDS 组件。 在 Windows 7 后，将从操作系统删除所有 RDS 服务器组件。
* **JRO:** Jet 复制对象 (JRO) 已弃用。 中与 Jet 的 ADO 使用 JRO (*.mdb) 数据库来创建和压缩 Jet 数据库 (.mdb) 以及执行 Jet 复制管理。MDAC 2.7 将其上一版本。JRO 不能在 64 位 Windows 操作系统上。Microsoft Access 2007 文件格式中不支持 JRO (*.accdb)。
* **16 位 ODBC 支持：** 如果使用的 16 位应用程序，则应迁移到 32 位应用程序。 16 位功能已弃用，并且正在从 64 位操作系统中删除。 有关详细信息，请参阅[知识库文章 896458](https://support.microsoft.com/kb/896458)。
* **OLEDB 简单的提供程序 (MSDAOSP):** OLEDB 简单的提供程序提供了一个框架，用于快速构建简单的数据通过 OLE DB 访问接口。 MSDAOSP 已弃用。
* **ODBC 游标库：** ODBC 游标库 (ODBCCR32.dll) 提供了有限的客户端的数据游标。 已不推荐使用 ODBC 游标库;你的应用程序可以使用服务器端游标实现来替换。
* **OLE DB 进程外接口远程处理：** OLEDB 接口远程处理 (msdaps.dll) 已尝试允许 OLE DB 提供程序以进程外运行。 OLEDB 进程外接口远程处理不推荐使用。
* **AppleTalk 和 Banyan Vines SQL 网络库：** Banyan Vines、 AppleTalk、 ServerNet、 IPX/SPX、 Giganet 和 RPC SQL 网络库不推荐使用。 如果使用任何一种技术，则应修改应用程序以使用其中一个其他网络库，如 TCP/IP 和命名管道。

### <a name="mdacwdac-releases"></a>MDAC/WDAC 版本

下面是开始使用的最早的过去 MDAC/WDAC 版本可支持性方案的列表。

* **MDAC 1.5、 MDAC 2.0 和 MDAC 2.1:** 这些版本的 MDAC 已通过 Microsoft Windows NT Option Pack、 Microsoft Windows Platform SDK 或 MDAC 网站上发布的独立版本。 不再支持这些版本的 MDAC。
* **MDAC 2.5:** 此版本的 MDAC 是随 Windows 2000 操作系统。 Service pack 的 MDAC 2.5 已随附相应的 Windows 2000 service pack。
* **MDAC 2.6:** MDAC 2.6 RTM、 SP1 和 SP2 已包含 Microsoft SQL Server 2000 RTM、 SP1 和 SP2，分别。 此外，这些 MDAC service pack 发布到 Microsoft SQL Server 2000 service pack 发布计划根据 MDAC Web 站点。 您可以在 Windows 2000、 Windows Millennium Edition、 Windows NT、 Windows 95 和 Windows 98 平台上安装此版本的 MDAC 和其服务包。 此版本的 MDAC 不再是受支持。
* **MDAC 2.7:** 此版本的 MDAC 是随 Microsoft Windows XP RTM 和 SP1 的操作系统。 您可以在 Windows 2000、 Windows Millennium、 Windows NT 和 Windows 98 平台上安装此版本的 MDAC 和其服务包。 你可以仅通过操作系统或其服务包在 Windows XP 平台上安装此版本。 此版本的 MDAC 不再是受支持。
* **MDAC 2.8:** 此版本的 MDAC 已包含在 Windows Server 2003 和 Windows XP SP2 及更高版本。 您也可以安装此版本的 MDAC 和其服务包在 Windows 2000 上。

  * MDAC 2.8 的 32 位版本也已发布到 MDAC Web 站点已发布给客户的 Windows Server 2003 时。
  * MDAC 2.8 的 64 位版本使用 64 位版本的 Windows Server 2003 和 Windows XP 发布。

* **Windows 数据访问组件 (WDAC):** MDAC 已更名为 WDAC-"Windows 数据访问组件"从 Windows Vista 和 Windows Server 2008 开始。 WDAC 是作为操作系统的一部分，并不是可单独用于再分发。 WDAC 的可维护性均受操作系统的生命周期。

  分别使用 32 位和 64 位版本的 Windows 操作系统，发布的 WDAC 的 32 位和 64 位版本。

## <a name="obsolete-data-access-technologies"></a>过时的数据访问技术

已过时的技术是的技术和的尚未被增强或多个产品版本中更新，将从将来产品发布中排除。 在编写新的应用程序时，不要使用这些技术。 在修改现有应用程序使用这些技术编写的请考虑这些应用程序迁移到 ADO.NET 或另一种当前技术。

以下组件被视为已过时：

* **Db-library:** DB 库是一个特定于 SQL Server 的编程模型，其中包含 C Api。 SQL Server 6.5 以来已有的 Db-library 没有功能的增强功能。 它的最终版本与 SQL Server 2000，将不能移植到 64 位 Windows 操作系统。
* **(E SQL) 的嵌入式 SQL:** E SQL 是特定于 SQL Server 的编程模型，在 Visual C 代码中嵌入的 TRANSACT-SQL 语句。 无需增强功能具有已对 SQL Server 6.5 E SQL。 它的最终版本与 SQL Server 2000，将不能移植到 64 位 Windows 操作系统。
* **数据访问对象 (DAO):** DAO 提供对 JET （访问） 数据库的访问。 此 API 可用于从 Microsoft Visual Basic、 Microsoft Visual c + + 和脚本语言。 它已包含在 Microsoft Office 2000 和 Office XP。 DAO 3.6 是这项技术的最终版本。 它不会在 64 位 Windows 操作系统上可用。
* **远程数据对象 (RDO):** RDO 设计为专门用于访问远程 ODBC 关系数据源，并更轻松地使用 ODBC，而无需复杂的应用程序代码。 它是随 Microsoft Visual Basic 版本 4、 5 和 6。 RDO 2.0 版是这项技术的最终版本。
