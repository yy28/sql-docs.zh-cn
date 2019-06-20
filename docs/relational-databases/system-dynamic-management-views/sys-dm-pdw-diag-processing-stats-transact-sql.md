---
title: sys.dm_pdw_diag_processing_stats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: df659c55-4f63-45f8-8afe-ce300031bc5b
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: f96dd7be6de1415abb8a71425b083c58e7012d9d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62691370"
---
# <a name="sysdmpdwdiagprocessingstats-transact-sql"></a>sys.dm_pdw_diag_processing_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  显示与所有无法合并到由管理员定义的诊断会话的内部诊断事件相关的信息。 查询此视图，以了解该驱动器的所有其他 Dmv 填充的背后的诊断和事件处理子系统的统计信息。 有一组的每个节点上每个进程的队列。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**pdw_node_id**|**int**|此日志所在的设备节点。|  
|**process_id**|**int**|运行提交此统计信息的进程的标识符。|  
|**target_name**|**nvarchar(255)**|队列的名称。|  
|**queue_size**|**int**|在处理队列中的项的数目。 队列大小通常是 0。 正数表示系统在压力下并生成积压工作的事件。 其他列中的正值意味着系统已损坏该特定队列以及任何相关的 Dmv。|  
|**lost_events_count**|**bigint**|丢失的事件数。|  
  
## <a name="see-also"></a>请参阅  
 [SQL 数据仓库和并行数据仓库动态管理视图&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
