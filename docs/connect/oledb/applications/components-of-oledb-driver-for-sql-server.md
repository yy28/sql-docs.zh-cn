---
title: 适用于 SQL Server 的 OLE DB 驱动程序的组件 | Microsoft Docs
description: 适用于 SQL Server 的 OLE DB 驱动程序的组件
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- data access [OLE DB Driver for SQL Server], components
- components [OLE DB Driver for SQL Server]
- MSOLEDBSQL, about OLE DB Driver for SQL Server
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 5a5124519bd95ec02e93a007d9881ec80814cfc8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67989317"
---
# <a name="components-of-ole-db-driver-for-sql-server"></a>适用于 SQL Server 的 OLE DB 驱动程序的组件
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  SQL Server OLE DB 驱动程序包含以下组件:  

|组件|描述|  
|---------------|-----------------|  
|msoledbsql.dll|动态链接库 (DLL) 文件, 其中包含 SQL Server 功能的所有 OLE DB 驱动程序。|  
|msoledbsqlr.rll|用于 SQL Server 库的 OLE DB 驱动程序的随附资源文件。|   
|msoledbsql.h|SQL Server 标头文件的 OLE DB 驱动程序, 其中包含使用 SQL Server OLE DB 驱动程序所需的所有新定义。 此标头文件替换 sqloledb 标头文件。<br /><br /> 注意: 只要先定义 sqloledb, 就可以在同一程序中引用 msoledbsql 和 sqloledb。|  
|msoledbsql.lib|直接调用作为 SQL Server OLE DB 驱动程序的一部分的[OpenSqlFilestream](../../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md)函数所需的库文件。<br /><br /> 请注意：如果确实要在编程代码中引用 msoledbsql.lib 文件，需要确保 msoledbsql.dll 文件位于你的系统路径和使用你的应用程序的用户系统路径中。|  

## <a name="see-also"></a>另请参阅  
 [使用适用于 SQL Server 的 OLE DB 驱动程序生成应用程序](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
