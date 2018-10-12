---
title: 适用于 SQL Server 的 Microsoft OLE DB 驱动程序 | Microsoft Docs
description: 适用于 SQL Server 的 Microsoft OLE DB 驱动程序
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- MSOLEDBSQL, about OLE DB Driver for SQL Server
- OLE DB Driver for SQL Server, about OLE DB Driver for SQL Server
- data access [OLE DB Driver for SQL Server], about OLE DB Driver for SQL Server
- data access [OLE DB Driver for SQL Server]
- OLE DB Driver for SQL Server
- MSOLEDBSQL
- native data access [OLE DB Driver for SQL Server]
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: befcc84662b2273f81faaded76045d4d44b03e98
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47687861"
---
# <a name="microsoft-ole-db-driver-for-sql-server"></a>适用于 SQL Server 的 Microsoft OLE DB 驱动程序
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../includes/driver_oledb_download.md)]

  适用于 SQL Server 的 OLE DB 驱动程序是独立的数据访问应用程序编程接口 (API)，用于 OLE DB，是在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 中引入的。 适用于 SQL Server 的 OLE DB 驱动程序提供了一个动态链接库 (DLL) 中的 SQL OLE DB 驱动程序。 除 Windows 数据访问组件（Windows DAC，以前为 Microsoft 数据访问组件或 MDAC）提供的功能之外，它还提供新的功能。 适用于 SQL Server 的 OLE DB 驱动程序可用于创建新的应用程序或增强现有应用程序的性能，使其能够利用 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 中引入的功能，例如多个活动结果集 (MARS)、用户定义数据类型 (UDT)、查询通知、快照隔离和 XML 数据类型支持。  
  
> [!NOTE]  
>  有关适用于 SQL Server 的 OLE DB 驱动程序与 Windows DAC 之间差异的列表，以及将 Windows DAC 应用程序更新到适用于 SQL Server 的 OLE DB 驱动程序之前要考虑问题的信息，请参阅[从 MDAC 将应用程序更新到适用于 SQL Server 的 OLE DB 驱动程序](../oledb/applications/updating-an-application-to-oledb-driver-for-sql-server-from-mdac.md)。  
  
 适用于 SQL Server 的 OLE DB 驱动程序可与 Windows DAC 提供的 OLE DB 核心服务一起使用，但这不是必要条件；是否选择使用核心服务取决于单个应用程序的要求（例如是否必需连接池）。  
  
 ActiveX 数据对象 (ADO) 应用程序可能对于 SQL Server，使用 OLE DB 驱动程序，但建议使用 ADO 与结合**DataTypeCompatibility**连接字符串关键字 (或其对应**数据源**属性)。 ADO 应用程序时使用 SQL Server 的 OLE DB 驱动程序，可以利用这些新功能中引入[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]可通过 SQL Server 的 OLE DB 驱动程序通过连接字符串关键字或 OLE DB 属性或[!INCLUDE[tsql](../../includes/tsql-md.md)]。 有关这些功能与 ADO 一起使用的详细信息，请参阅[使用 ADO 与 OLE DB 驱动程序适用于 SQL Server](../oledb/applications/using-ado-with-oledb-driver-for-sql-server.md)。  
  
 适用于 SQL Server 的 OLE DB 驱动程序旨在让用户更简单地使用 OLE DB 获取对 SQL Server 的本机数据访问。 它提供了一种方法，以创新和开发新的数据访问功能而无需更改当前的 Windows DAC 组件现在是 Microsoft Windows 平台的一部分。  
  
 尽管 适用于 SQL Server 的 OLE DB 驱动程序使用 Windows DAC 中的组件，但它并不显式依赖特定版本的 Windows DAC。 可以使用随 SQL Server 的 OLE DB 驱动程序所支持任何操作系统一起安装的 Windows DAC 的版本适用于 SQL Server 中使用 OLE DB 驱动程序。  

 ## <a name="different-generations-of-ole-db-drivers"></a>不同代的 OLE DB 驱动程序

有三个不同代的 SQL Server 的 Microsoft OLE DB 提供程序。

### <a name="1-microsoft-ole-db-provider-for-sql-server-sqloledb"></a>1.Microsoft OLE DB Provider for SQL Server (SQLOLEDB)
[Microsoft OLE DB Provider for SQL Server](../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md) (SQLOLEDB) 仍附带作为的一部分[Windows 数据访问组件](https://msdn.microsoft.com/library/ms692897.aspx)。 不不再维护并不建议新的开发使用此驱动程序。

### <a name="2-sql-server-native-client-snac"></a>2.SQL Server Native Client (SNAC)
在中启动[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]，则[SQL Server Native Client (SNAC)](../../relational-databases/native-client/sql-server-native-client.md)包含一个 OLE DB 提供程序接口 (SQLNCLI)，并且附带的 OLE DB 访问接口[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]通过[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]。

它是[宣布弃用在 2011 年](https://blogs.msdn.microsoft.com/sqlnativeclient/2011/08/29/microsoft-is-aligning-with-odbc-for-native-relational-data-access/)，不建议新的开发使用此驱动程序。 有关 SNAC 生命周期和可下载的详细信息，请参阅[所述的 SNAC 生命周期](https://blogs.msdn.microsoft.com/sqlreleaseservices/snac-lifecycle-explained/)。

### <a name="3-microsoft-ole-db-driver-for-sql-server-msoledbsql"></a>3.适用于 SQL Server 的 Microsoft OLE DB 驱动程序 (MSOLEDBSQL)
OLE DB 已[取消弃用](https://blogs.msdn.microsoft.com/sqlnativeclient/2017/10/06/announcing-the-new-release-of-ole-db-driver-for-sql-server/)和 2018 年发布。

新的 OLE DB 访问接口称为 Microsoft OLE DB 驱动程序的 SQL Server (MSOLEDBSQL)。 新的提供程序将更新与今后的最新的服务器功能。

> [!NOTE]
> 若要在现有应用程序中使用 SQL Server，新 Microsoft OLE DB 驱动程序，您应计划将连接字符串从 SQLOLEDB 或 SQLNCLI，转换为 MSOLEDBSQL。
  
## <a name="in-this-section"></a>本节内容  
[何时使用适用于 SQL Server 的 OLE DB 驱动程序](../oledb/when-to-use-oledb-driver-for-sql-server.md)  
 讨论适用于 SQL Server 的 OLE DB 驱动程序与 Microsoft 数据访问技术的适应度如何，探讨它与 Windows DAC 和 ADO.NET 相比较如何，同时提供建议，帮助用户决定要采用哪种数据访问技术。  
  
 [适用于 SQL Server 的 OLE DB 驱动程序功能](../oledb/features/oledb-driver-for-sql-server-features.md )  
 介绍 SQL Server 的 OLE DB 驱动程序所支持的功能。  
  
 [使用适用于 SQL Server 的 OLE DB 驱动程序生成应用程序](../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
 简要介绍适用于 SQL Server 的 OLE DB 驱动程序，包括它与 Windows DAC 的差异、其使用的组件，以及如何将其与 ADO 结合。  
  
 本部分还讨论了 SQL Server 安装和部署，包括如何重新发布的 SQL Server 库，OLE DB 驱动程序的 OLE DB 驱动程序。  
  
 [适用于 SQL Server 的 OLE DB 驱动程序的系统要求](../oledb/system-requirements-for-oledb-driver-for-sql-server.md)  
 讨论使用 SQL Server 的 OLE DB 驱动程序所需的系统资源。  
  
 [适用于 SQL Server 的 OLE DB 驱动程序编程](../oledb/ole-db/oledb-driver-for-sql-server-programming.md)  
 提供有关使用用于 SQL Server 的 OLE DB 驱动程序信息。  
  
 [查找有关适用于 SQL Server 的 OLE DB 驱动程序的更多信息](../oledb/finding-more-oledb-driver-for-sql-server-information.md)  
 对于 SQL Server，其中包括指向外部资源和获取进一步帮助提供了有关 OLE DB 驱动程序的其他资源。  
  
  
## <a name="see-also"></a>另请参阅  
 [从 SQL Server 2005 Native Client 更新应用程序](../oledb/applications/updating-an-application-from-sql-server-2005-native-client.md)    
 [OLE DB 操作指南主题](../oledb/ole-db-how-to/ole-db-how-to-topics.md)  
  
  
