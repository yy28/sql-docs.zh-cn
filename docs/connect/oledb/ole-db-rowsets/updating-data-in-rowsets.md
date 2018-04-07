---
title: 更新行集合中的数据 |Microsoft 文档
description: 更新行集使用的 SQL Server OLE DB 驱动程序中的数据
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: ole-db-rowsets
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
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
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: cc8816993330718218631335db1611cc0581d594
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2018
---
# <a name="updating-data-in-rowsets"></a>更新行集中的数据
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  SQL Server 更新 OLE DB 驱动程序[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]数据时使用者更新可修改的行集包含的数据。 当使用者请求支持时创建的可修改的行集**IRowsetChange**或**IRowsetUpdate**接口。  
  
 所有 OLE DB 驱动程序的 SQL Server 的可修改的行集使用[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]游标来支持行集。 行集属性 DBPROP_LOCKMODE 更改游标中的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 并发控制行为，并确定在可更新行集中提取行集的行和生成数据完整性错误的行为。  
  
 SQL Server 的 OLE DB 驱动程序支持行同步之前或之后更新。  
  
> [!NOTE]  
>  可使用 IRowChange::SetColumns 设置行对象的一个或多个指定列的值。  
  
## <a name="in-this-section"></a>本節內容  
  
-   [更新 SQL Server 游标中的数据](../../oledb/ole-db-rowsets/updating-data-in-sql-server-cursors.md)  
  
-   [重新同步的行](../../oledb/ole-db-rowsets/updating-data-in-rowsets-resynchronizing-rows.md)  
  
## <a name="see-also"></a>另请参阅  
 [行集](../../oledb/ole-db-rowsets/rowsets.md)  
  
  
