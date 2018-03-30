---
title: 用于 SQL Server 的 OLE DB 驱动程序的组件 |Microsoft 文档
description: 用于 SQL Server 的 OLE DB 驱动程序的组件
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|applications
ms.reviewer: ''
ms.suite: sql
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- data access [OLE DB Driver for SQL Server], components
- components [OLE DB Driver for SQL Server]
- MSOLEDBSQL, about OLE DB Driver for SQL Server
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 18b0f0e13fefefe5e3be09d7538150cfccbfcb21
ms.sourcegitcommit: 9f4330a4b067deea396b8567747a6771f35e6eee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2018
---
# <a name="components-of-ole-db-driver-for-sql-server"></a>用于 SQL Server 的 OLE DB 驱动程序的组件
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  OLE DB 驱动程序的 SQL Server 包含以下组件：  

|组件|Description|  
|---------------|-----------------|  
|msoledbsql.dll|包含所有 SQL Server 功能的 OLE DB 驱动程序动态链接库 (DLL) 文件。|  
|msoledbsqlr.rll|用于 SQL Server 库 OLE DB 驱动程序附带资源文件。|   
|msoledbsql.h|为 SQL Server 标头文件包含的所有新定义 OLE DB 驱动程序所需使用用于 SQL Server 的 OLE DB 驱动程序。 此标头文件将替换 sqloledb.h 标头文件。<br /><br /> 注意： 你可以引用 msoledbsql.h 和 sqloledb.h 同一程序中的，只要 sqloledb.h 首先定义。|  
|msoledbsql.lib|库文件需要直接调用**bcp**属于 SQL Server 的 OLE DB 驱动程序的实用工具函数。<br /><br /> 注意： 如果你确实在编程代码中引用 msoledbsql.lib 文件，你需要确保 msoledbsql.dll 文件是在你的系统路径，并使用户在系统路径中使用你的应用程序。|  

## <a name="see-also"></a>另请参阅  
 [使用 OLE DB 驱动程序的 SQL Server 的生成应用程序](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
