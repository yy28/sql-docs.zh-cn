---
title: sys. dm_pdw_diag_processing_stats （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: df659c55-4f63-45f8-8afe-ce300031bc5b
author: CarlRabeler
ms.author: carlrab
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: a765e591e3b55bb4be2e2b6d7431873702910f6f
ms.sourcegitcommit: df1f0f2dfb9452f16471e740273cd1478ff3100c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/29/2020
ms.locfileid: "87394348"
---
# <a name="sysdm_pdw_diag_processing_stats-transact-sql"></a>sys. dm_pdw_diag_processing_stats （Transact-sql）
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  显示与可以合并到管理员定义的诊断会话中的所有内部诊断事件相关的信息。 查询此视图，以了解诊断所用的统计信息，以及驱动所有其他 Dmv 总体的事件子系统。 每个节点上的每个进程都有一组队列。  
  
|列名|数据类型|说明|  
|-----------------|---------------|-----------------|  
|pdw_node_id|**int**|此日志来自的设备节点。|  
|**process_id**|**int**|正在提交此统计信息的进程的标识符。|  
|**target_name**|**nvarchar(255)**|队列的名称。|  
|**queue_size**|**int**|进程队列中的项数。 队列大小通常为0。 正数指示系统正在压力上并且正在生成事件积压工作（backlog）。 其他列中的正计数表示该特定队列的系统已损坏，以及任何相关的 Dmv。|  
|**lost_events_count**|**bigint**|丢失的事件数。|  
  
## <a name="see-also"></a>另请参阅  
 [SQL 数据仓库和并行数据仓库动态管理视图 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
