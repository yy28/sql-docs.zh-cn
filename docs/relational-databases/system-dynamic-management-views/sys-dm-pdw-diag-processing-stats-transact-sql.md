---
title: sys.dm_pdw_diag_processing_stats (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: pdw
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: df659c55-4f63-45f8-8afe-ce300031bc5b
caps.latest.revision: 7
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: ef951e601b97b4f5de1ebf0675672fe1ff583439
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/07/2018
---
# <a name="sysdmpdwdiagprocessingstats-transact-sql"></a>sys.dm_pdw_diag_processing_stats (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  显示与无法合并到由管理员定义的诊断会话的所有内部的诊断事件相关信息。 查询此视图以了解该驱动器的所有其他 Dmv 填充的诊断和事件处理子系统后面的统计信息。 有一组的每个节点上每个进程的队列。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**pdw_node_id**|**int**|此日志所在的设备节点。|  
|**process_id**|**int**|运行提交此统计信息的进程的标识符。|  
|**target_name**|**nvarchar(255)**|队列的名称。|  
|**queue_size**|**int**|在处理队列中的项的数目。 队列大小通常是 0。 正数表示系统压力下并生成的事件的积压工作。 其他列中的正计数意味着系统已损坏该特定的队列以及任何相关的 Dmv。|  
|**lost_events_count**|**bigint**|丢失的事件数。|  
  
## <a name="see-also"></a>另请参阅  
 [SQL 数据仓库和并行数据仓库动态管理视图&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
