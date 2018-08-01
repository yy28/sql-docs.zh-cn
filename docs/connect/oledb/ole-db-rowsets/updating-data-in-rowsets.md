---
title: 更新行集中的数据 |Microsoft Docs
description: 更新使用 SQL Server 的 OLE DB 驱动程序的行集中的数据
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-rowsets
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- updating data [SQL Server]
- rowsets [OLE DB], updating data
- OLE DB Driver for SQL Server, rowsets
- OLE DB rowsets, updating data
- OLE DB Driver for SQL Server, data updates
- data updates [SQL Server], OLE DB
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 20484bce71d0e776b4090f743c65e3a78d655a70
ms.sourcegitcommit: 50838d7e767c61dd0b5e677b6833dd5c139552f2
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 07/18/2018
ms.locfileid: "39108809"
---
# <a name="updating-data-in-rowsets"></a>更新行集中的数据
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  适用于 SQL Server 的 OLE DB 驱动程序在使用者更新包含该数据的可修改行集时更新 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 数据。 当使用者请求支持 IRowsetChange 或 IRowsetUpdate 接口时，将创建一个可修改的行集。  
  
 所有 OLE DB 驱动程序的 SQL Server 的可修改的行集使用[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]游标以支持行集。 行集属性 DBPROP_LOCKMODE 更改游标中的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 并发控制行为，并确定在可更新行集中提取行集的行和生成数据完整性错误的行为。  
  
 SQL Server 的 OLE DB 驱动程序支持在更新前后同步行。  
  
> [!NOTE]  
>  可使用 IRowChange::SetColumns 设置行对象的一个或多个指定列的值。  
  
## <a name="in-this-section"></a>本节内容  
  
-   [更新 SQL Server 游标中的数据](../../oledb/ole-db-rowsets/updating-data-in-sql-server-cursors.md)  
  
-   [重新同步行](../../oledb/ole-db-rowsets/updating-data-in-rowsets-resynchronizing-rows.md)  
  
## <a name="see-also"></a>另请参阅  
 [行集](../../oledb/ole-db-rowsets/rowsets.md)  
  
  
