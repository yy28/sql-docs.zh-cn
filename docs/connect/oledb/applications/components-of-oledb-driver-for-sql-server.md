---
title: 用于 SQL Server 的 OLE DB 驱动程序的组件 |Microsoft 文档
description: 用于 SQL Server 的 OLE DB 驱动程序的组件
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|applications
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- data access [OLE DB Driver for SQL Server], components
- components [OLE DB Driver for SQL Server]
- MSOLEDBSQL, about OLE DB Driver for SQL Server
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 2548d1c3830611f9b9fddb556d8711ca7039b9ed
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="components-of-ole-db-driver-for-sql-server"></a>用于 SQL Server 的 OLE DB 驱动程序的组件
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB 驱动程序的 SQL Server 包含以下组件：  

|组件|Description|  
|---------------|-----------------|  
|msoledbsql.dll|包含所有 SQL Server 功能的 OLE DB 驱动程序动态链接库 (DLL) 文件。|  
|msoledbsqlr.rll|用于 SQL Server 库 OLE DB 驱动程序附带资源文件。|   
|msoledbsql.h|为 SQL Server 标头文件包含的所有新定义 OLE DB 驱动程序所需使用用于 SQL Server 的 OLE DB 驱动程序。 此标头文件将替换 sqloledb.h 标头文件。<br /><br /> 注意： 你可以引用 msoledbsql.h 和 sqloledb.h 同一程序中的，只要 sqloledb.h 首先定义。|  
|msoledbsql.lib|库文件需要直接调用[OpenSqlFilestream](../../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md)是 SQL Server 的 OLE DB 驱动程序的一部分的函数。<br /><br /> 注意： 如果你确实在编程代码中引用 msoledbsql.lib 文件，你需要确保 msoledbsql.dll 文件是在你的系统路径，并使用户在系统路径中使用你的应用程序。|  

## <a name="see-also"></a>另请参阅  
 [使用适用于 SQL Server 的 OLE DB 驱动程序生成应用程序](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
