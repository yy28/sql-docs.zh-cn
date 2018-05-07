---
title: trace_xe_action_map (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- trace_xe_action_map_TSQL
- trace_xe_action_map
dev_langs:
- TSQL
helpviewer_keywords:
- extended events [SQL Server], tables
- trace_xe_action_map
ms.assetid: 208a1413-ce7f-4521-b765-d74723627302
caps.latest.revision: 11
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 29fba0bc16dc42798ecd37d234dd79e30e9db856
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="extended-events-tables---tracexeactionmap"></a>扩展事件表-trace_xe_action_map
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  映射到 SQL 跟踪列 ID 的每个扩展事件操作各占一行。 此表存储在 master 数据库中，sys 架构中。  
  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|trace_column_id|**int**|正在映射的 SQL 跟踪列的 ID。|  
|package_name|**nvarchar(60)**|映射操作所在的扩展事件包的名称。|  
|xe_action_name|**nvarchar(60)**|映射到 SQL 跟踪列的扩展事件操作的名称。|  
  
## <a name="remarks"></a>注释  
 您可以使用以下查询确定与 SQL 跟踪列等效的扩展事件操作：  
  
```  
SELECT tc.name AS trace_column, am.package_name, am.xe_action_name  
FROM sys.trace_columns AS tc  
INNER JOIN sys.trace_xe_action_map AS am  
   ON tc.trace_column_id = am.trace_column_id  
```  
  
 不映射到表中不包括的操作的 SQL 跟踪列。  
  
## <a name="see-also"></a>另请参阅  
 [trace_xe_event_map (Transact-SQL)](../../relational-databases/system-tables/extended-events-tables-trace-xe-event-map.md)  
  
  
