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
ms.openlocfilehash: fbc52a9e982da45586ce7ace5e58e8985869e552
ms.sourcegitcommit: 8f1d1363e18e0c32ff250617ab6cb2da2147bf8e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/03/2018
---
# <a name="ole-db-driver-for-sql-server"></a>用于 SQL Server 的 OLE DB 驱动程序
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

MSOLEDBSQL 或 OLE DB 驱动程序对于 SQL Server，是一个术语，互换用于 SQL Server，请参阅 OLE DB 驱动程序。

## <a name="different-generations-of-ole-db-drivers"></a>不同代的 OLE DB 驱动程序

有三个不同级别的 SQL server 的 Microsoft OLE DB 提供程序。

### <a name="1-microsoft-ole-db-provider-for-sql-server-sqloledb"></a>1.Microsoft OLE DB Provider for SQL Server (SQLOLEDB)
[Microsoft OLE DB Provider for SQL Server](../../ado/guide/appendixes/microsoft-ole-db-provider-for-sql-server.md) (SQLOLEDB) 仍作为的一部分附带[Windows 数据访问组件](https://msdn.microsoft.com/en-us/library/ms692897.aspx)。 它不不再保留，并且不建议新的开发使用该驱动程序。 


### <a name="2-sql-server-native-client-snac"></a>2.SQL Server Native Client (SNAC)
从开始[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]、 [SQL Server Native Client (SNAC)](../../relational-databases/native-client/sql-server-native-client.md)包含 OLE DB 提供程序接口 (SQLNCLI)，并且附带的 OLE DB 访问接口[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]通过[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]。

它是[宣布弃用在 2011 年](https://blogs.msdn.microsoft.com/sqlnativeclient/2011/08/29/microsoft-is-aligning-with-odbc-for-native-relational-data-access/)，不建议新的开发使用该驱动程序。 有关 SNAC 生命周期和可用的下载的详细信息，请参阅[SNAC 生命周期所述](https://blogs.msdn.microsoft.com/sqlreleaseservices/snac-lifecycle-explained/)。

### <a name="3-microsoft-ole-db-driver-for-sql-server-msoledbsql"></a>3.Microsoft OLE DB Driver for SQL Server (MSOLEDBSQL)
OLE DB 已[undeprecated](https://blogs.msdn.microsoft.com/sqlnativeclient/2017/10/06/announcing-the-new-release-of-ole-db-driver-for-sql-server/)和发布 2018，并且可以下载[此处](https://go.microsoft.com/fwlink/?linkid=871294)。

新的 OLE DB 访问接口称为 Microsoft OLE DB 驱动程序的 SQL Server (MSOLEDBSQL)。 新的提供程序将更新与今后的最新的服务器功能。

> [!NOTE]
> 若要使用适用于 SQL Server 的新 Microsoft OLE DB 驱动程序，在现有应用程序中，你应计划将你的连接字符串从 SQLOLEDB 或 SQLNCLI，转换为 MSOLEDBSQL。   

SQL Server 功能 OLE DB 驱动程序的信息：

-   [适用于 SQL Server 的 OLE DB 驱动程序对 LocalDB 的支持](../oledb/features/oledb-driver-for-sql-server-support-for-localdb.md)  

-   [元数据发现](../oledb/features/metadata-discovery.md)  

-   [适用于 SQL Server 的 OLE DB 驱动程序的 UTF-16 支持](../oledb/features/utf-16-support-in-oledb-driver-for-sql-server.md)  

-   [适用于 SQL Server 的 OLE DB 驱动程序对高可用性和灾难恢复的支持](../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md)  

-   [访问扩展事件日志中的诊断信息](../oledb/features/accessing-diagnostic-information-in-the-extended-events-log.md)  

## <a name="see-also"></a>另请参阅  
[安装 SQL Server 的 OLE DB 驱动程序](../oledb/applications/installing-oledb-driver-for-sql-server.md)     
[适用于 SQL Server 的 OLE DB 驱动程序功能](../oledb/features/oledb-driver-for-sql-server-features.md )     
