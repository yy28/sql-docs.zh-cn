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
ms.openlocfilehash: c88ef12d636dd5b10e1b7b3cd9418df3e058325b
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "86007053"
---
# <a name="components-of-ole-db-driver-for-sql-server"></a>适用于 SQL Server 的 OLE DB 驱动程序的组件
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB Driver for SQL Server 包含以下组件：  

|组件|说明|  
|---------------|-----------------|  
|msoledbsql.dll|包含 OLE DB Driver for SQL Server 所有功能的动态链接库 (DLL) 文件。|  
|msoledbsqlr.rll|OLE DB Driver for SQL Server 库的附带资源文件。|   
|msoledbsql.h|包含使用 OLE DB Driver for SQL Server 所需的所有新定义的 OLE DB Driver for SQL Server 头文件。 该头文件取代了 sqloledb.h 头文件。<br /><br /> 注意：只要先定义了 sqloledb.h，就可以在同一个程序中引用 msoledbsql.h 和 sqloledb.h。|  
|msoledbsql.lib|直接调用属于 OLE DB Driver for SQL Server 的一部分的 [OpenSqlFilestream](../../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md) 函数所需的库文件。<br /><br /> 注意：如果确实要在编程代码中引用 msoledbsql.lib 文件，需要确保 msoledbsql.dll 文件位于你的系统路径和使用你的应用程序的用户系统路径中。|  

## <a name="see-also"></a>另请参阅  
 [使用适用于 SQL Server 的 OLE DB 驱动程序生成应用程序](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
