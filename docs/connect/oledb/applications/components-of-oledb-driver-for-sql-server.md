---
title: 适用于 SQL Server 的 OLE DB 驱动程序的组件 |Microsoft Docs
description: 适用于 SQL Server 的 OLE DB 驱动程序的组件
ms.custom: ''
ms.date: 06/12/2018
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
ms.openlocfilehash: b1b46e57b3be42fa93f8a246db528a5f85709d9e
ms.sourcegitcommit: 50838d7e767c61dd0b5e677b6833dd5c139552f2
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2018
ms.locfileid: "39109829"
---
# <a name="components-of-ole-db-driver-for-sql-server"></a>适用于 SQL Server 的 OLE DB 驱动程序的组件
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB 驱动程序适用于 SQL Server 包含以下组件：  

|组件|描述|  
|---------------|-----------------|  
|msoledbsql.dll|包含所有 SQL Server 功能，OLE DB 驱动程序动态链接库 (DLL) 文件。|  
|msoledbsqlr.rll|SQL Server 库，OLE DB 驱动程序附带的资源文件。|   
|msoledbsql.h|使用用于 SQL Server 的 OLE DB 驱动程序所需的 SQL Server 标头文件，其中包含的所有新定义，OLE DB 驱动程序。 此标头文件取代了 sqloledb.h 头文件。<br /><br /> 注意： 你可以引用 msoledbsql.h 和 sqloledb.h 同一程序中的，只要先定义了 sqloledb.h。|  
|msoledbsql.lib|库文件需要直接调用[OpenSqlFilestream](../../../relational-databases/blob/access-filestream-data-with-opensqlfilestream.md)是 SQL Server 的 OLE DB 驱动程序的一部分的函数。<br /><br /> 如果确实要在编程代码中引用 sqlncli11.lib 文件，您需要确保 sqlncli11.dll 文件位于您的系统路径和使用您的应用程序的用户的系统路径中。|  

## <a name="see-also"></a>另请参阅  
 [使用适用于 SQL Server 的 OLE DB 驱动程序生成应用程序](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
