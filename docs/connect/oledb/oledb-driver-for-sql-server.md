---
title: 用于 SQL Server 的 OLE DB 驱动程序 |Microsoft 文档
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb
ms.reviewer: ''
ms.suite: sql
description: ''
ms.custom: ''
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: article
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 89e66fe2c61ae17a43e2a58071ba04374f33ea04
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2018
---
# <a name="ole-db-driver-for-sql-server"></a>用于 SQL Server 的 OLE DB 驱动程序
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

MSOLEDBSQL 或 OLE DB 驱动程序对于 SQL Server，是一个术语，它已用于互换的 SQL Server，请参阅 OLE DB 驱动程序。

## <a name="different-incarnations-of-ole-db-drivers"></a>OLE DB 驱动程序的不同一直伴随

有三个不同版本的 SQL server 的 Microsoft OLE DB 提供程序。


### <a name="1-microsoft-ole-db-provider-for-sql-server-sqloledb"></a>1.Microsoft OLE DB Provider for SQL Server (SQLOLEDB)

[Microsoft OLE DB Provider for SQL Server](../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md) (SQLOLEDB) 仍作为的一部分附带[Windows 数据访问组件](https://msdn.microsoft.com/en-us/library/ms692897.aspx)。 不建议新的开发使用该驱动程序。


### <a name="2-sql-server-native-client-snac"></a>2.SQL Server Native Client (SNAC)

从 SQL Server 2005 开始[SQL Server Native Client (SNAC)](../../relational-databases/native-client/sql-server-native-client.md)包含 OLE DB 提供程序接口 (SQLNCLI)，并且随 SQL Server 2017 通过 SQL Server 2005 的 OLE DB 访问接口。

它是[宣布弃用在 2011 年](https://blogs.msdn.microsoft.com/sqlnativeclient/2011/08/29/microsoft-is-aligning-with-odbc-for-native-relational-data-access/)，不建议新的开发使用该驱动程序。


### <a name="3-microsoft-ole-db-driver-for-sql-server-msoledbsql"></a>3.Microsoft OLE DB Driver for SQL Server (MSOLEDBSQL)

OLE DB 已[宣布为在 2017 undeprecated](https://blogs.msdn.microsoft.com/sqlnativeclient/2017/10/06/announcing-the-new-release-of-ole-db-driver-for-sql-server/)。 2018 已宣布新计划的发布。

新的 OLE DB 访问接口称为 Microsoft OLE DB 驱动程序的 SQL Server (MSOLEDBSQL)。 新的提供程序将更新与今后的最新的服务器功能。

SQL Server 功能 OLE DB 驱动程序的信息：

-   [For SQL Server 对 LocalDB 的支持的 OLE DB 驱动程序](../oledb/features/oledb-driver-for-sql-server-support-for-localdb.md)  

-   [元数据发现](../oledb/features/metadata-discovery.md)  

-   [OLE DB 驱动程序中的 SQL Server 的 utf-16 支持](../oledb/features/utf-16-support-in-oledb-driver-for-sql-server.md)  

-   [用于高可用性、 灾难恢复的 SQL Server 支持的 OLE DB 驱动程序](../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)  

-   [访问扩展事件日志中的诊断信息](../oledb/features/accessing-diagnostic-information-in-the-extended-events-log.md)  

## <a name="see-also"></a>另请参阅  
[安装 SQL Server 的 OLE DB 驱动程序](../oledb/applications/installing-oledb-driver-for-sql-server.md)  
 [用于 SQL Server 功能的 OLE DB 驱动程序](../oledb/features/oledb-driver-for-sql-server-features.md )  
