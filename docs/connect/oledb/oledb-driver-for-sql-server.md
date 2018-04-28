---
title: 用于 SQL Server 的 OLE DB 驱动程序 |Microsoft 文档
description: 用于 SQL Server 的 OLE DB 驱动程序
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: OLE DB Driver
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
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
ms.author: Pedro.Lopes
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 40458d9c9c3b547a40be170e390344d8bb5f181a
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="ole-db-driver-for-sql-server"></a>用于 SQL Server 的 OLE DB 驱动程序
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../includes/driver_oledb_download.md)]

  OLE DB 驱动程序的 SQL Server 是独立的数据访问应用程序编程接口 (API)，用于 OLE DB 中引入[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]。 OLE DB 驱动程序的 SQL Server 提供了一个动态链接库 (DLL) 中的 SQL OLE DB 驱动程序。 除 Windows 数据访问组件（Windows DAC，以前为 Microsoft 数据访问组件或 MDAC）提供的功能之外，它还提供新的功能。 OLE DB 驱动程序的 SQL Server 可以用于创建新的应用程序或增强现有应用程序需要利用中引入的功能[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]，如多个活动结果集 (MARS)、 用户定义的数据类型 (UDT)、 查询支持通知、 快照隔离和 XML 数据类型。  
  
> [!NOTE]  
>  有关 OLE DB 驱动程序的 SQL Server 和 Windows DAC，以及有关问题的信息更新到 OLE DB 驱动程序为 Windows DAC 应用程序适用于 SQL Server 之前要考虑之间的差异的列表，请参阅[sql 更新为 OLE DB 驱动程序的应用程序服务器从 MDAC](../oledb/applications/updating-an-application-to-oledb-driver-for-sql-server-from-mdac.md)。  
  
 SQL Server 的 OLE DB 驱动程序可以与结合使用 OLE DB 核心服务提供与 Windows DAC，但这不是要求;选择使用核心服务，或不依赖于单个应用程序 （例如，如果是必需的连接池） 的要求。  
  
 ActiveX 数据对象 (ADO) 应用程序可能使用的 SQL Server 的 OLE DB 驱动程序，但建议结合使用 ADO **DataTypeCompatibility**连接字符串关键字 (或其对应**数据源**属性)。 ADO 应用程序时使用用于 SQL Server 的 OLE DB 驱动程序，可以利用这些新功能中引入[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]可通过 SQL Server 的 OLE DB 驱动程序通过连接字符串关键字或 OLE DB 属性或[!INCLUDE[tsql](../../includes/tsql-md.md)]。 用 ADO 这些功能使用的详细信息，请参阅[与 OLE DB 驱动程序的 SQL Server 使用 ADO](../oledb/applications/using-ado-with-oledb-driver-for-sql-server.md)。  
  
 OLE DB 驱动程序的 SQL Server 旨在提供简化的方法，获取对使用 OLE DB 的 SQL Server 的本机数据访问权限。 它提供一种创新和发展新数据访问功能，而无需更改现在是 Microsoft Windows 平台的一部分的当前 Windows DAC 组件方法。  
  
 虽然 OLE DB 驱动程序的 SQL Server 使用 Windows DAC 中的组件，它不显式依赖于 Windows DAC 的特定版本。 你可以使用 OLE DB 驱动程序适用于 SQL Server 使用任何适用于 SQL Server 的 OLE DB 驱动程序支持的操作系统安装的 Windows DAC 的版本。  

 ## <a name="different-generations-of-ole-db-drivers"></a>不同代的 OLE DB 驱动程序

有三个不同级别的 SQL server 的 Microsoft OLE DB 提供程序。

### <a name="1-microsoft-ole-db-provider-for-sql-server-sqloledb"></a>1.Microsoft OLE DB Provider for SQL Server (SQLOLEDB)
[Microsoft OLE DB Provider for SQL Server](../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md) (SQLOLEDB) 仍作为的一部分附带[Windows 数据访问组件](https://msdn.microsoft.com/en-us/library/ms692897.aspx)。 它不不再保留，并且不建议新的开发使用该驱动程序。

### <a name="2-sql-server-native-client-snac"></a>2.SQL Server Native Client (SNAC)
从开始[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]、 [SQL Server Native Client (SNAC)](../../relational-databases/native-client/sql-server-native-client.md)包含 OLE DB 提供程序接口 (SQLNCLI)，并且附带的 OLE DB 访问接口[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]通过[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]。

它是[宣布弃用在 2011 年](https://blogs.msdn.microsoft.com/sqlnativeclient/2011/08/29/microsoft-is-aligning-with-odbc-for-native-relational-data-access/)，不建议新的开发使用该驱动程序。 有关 SNAC 生命周期和可用的下载的详细信息，请参阅[SNAC 生命周期所述](https://blogs.msdn.microsoft.com/sqlreleaseservices/snac-lifecycle-explained/)。

### <a name="3-microsoft-ole-db-driver-for-sql-server-msoledbsql"></a>3.Microsoft OLE DB Driver for SQL Server (MSOLEDBSQL)
OLE DB 已[undeprecated](https://blogs.msdn.microsoft.com/sqlnativeclient/2017/10/06/announcing-the-new-release-of-ole-db-driver-for-sql-server/)并且在 2018年发布。

新的 OLE DB 访问接口称为 Microsoft OLE DB 驱动程序的 SQL Server (MSOLEDBSQL)。 新的提供程序将更新与今后的最新的服务器功能。

> [!NOTE]
> 若要使用适用于 SQL Server 的新 Microsoft OLE DB 驱动程序，在现有应用程序中，你应计划将你的连接字符串从 SQLOLEDB 或 SQLNCLI，转换为 MSOLEDBSQL。
  
## <a name="in-this-section"></a>本節內容  
[何时使用适用于 SQL Server 的 OLE DB 驱动程序](../oledb/when-to-use-oledb-driver-for-sql-server.md)  
 讨论如何 OLE DB 驱动程序的 SQL Server 适应 Microsoft 数据访问技术，如何它将与 Windows DAC 和 ADO.NET，进行比较并提供数据访问技术，可使用指针来确定。  
  
 [适用于 SQL Server 的 OLE DB 驱动程序功能](../oledb/features/oledb-driver-for-sql-server-features.md )  
 描述适用于 SQL Server 的 OLE DB 驱动程序支持的功能。  
  
 [使用适用于 SQL Server 的 OLE DB 驱动程序生成应用程序](../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
 对于 SQL Server 的开发，包括如何与 Windows DAC，它使用的组件以及如何可与它使用 ADO 提供 OLE DB 驱动程序的概述。  
  
 本部分还讨论 OLE DB 驱动程序对于 SQL Server 安装和部署，包括如何重新发布用于 SQL Server 库 OLE DB 驱动程序。  
  
 [适用于 SQL Server 的 OLE DB 驱动程序的系统要求](../oledb/system-requirements-for-oledb-driver-for-sql-server.md)  
 讨论使用 SQL Server 的 OLE DB 驱动程序所需的系统资源。  
  
 [适用于 SQL Server 的 OLE DB 驱动程序编程](../oledb/ole-db/oledb-driver-for-sql-server-programming.md)  
 提供有关使用用于 SQL Server 的 OLE DB 驱动程序的信息。  
  
 [查找有关适用于 SQL Server 的 OLE DB 驱动程序的更多信息](../oledb/finding-more-oledb-driver-for-sql-server-information.md)  
 对于 SQL Server，包括外部资源的链接和获取进一步帮助提供有关 OLE DB 驱动程序的其他资源。  
  
  
## <a name="see-also"></a>另请参阅  
 [更新应用程序从 SQL Server 2005 的本机客户端](../oledb/applications/updating-an-application-from-sql-server-2005-native-client.md)    
 [OLE DB 操作指南主题](../oledb/ole-db-how-to/ole-db-how-to-topics.md)  
  
  
