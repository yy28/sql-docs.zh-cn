---
title: sys.dm_pdw_node_status (Transact SQL) |Microsoft 文档
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
ms.assetid: 8e263b65-81d0-49d0-8873-62ef424369d6
caps.latest.revision: 7
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 6e9e36fc384bcf4a20a73a460f80ad0c73d983e9
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/07/2018
---
# <a name="sysdmpdwnodestatus-transact-sql"></a>sys.dm_pdw_node_status (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  保存的其他信息 (通过[sys.dm_pdw_nodes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)) 有关的性能和状态的所有设备节点。 它列出每个设备中的节点的一行。  
  
|列名|数据类型|Description|范围|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|与节点关联的唯一数字 id。<br /><br /> 此视图的键。|唯一的设备，无论何种类型。|  
|process_id|**int**|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]||  
|process_name|**nvarchar(255)**|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]||  
|allocated_memory|**bigint**|分配此节点上的内存的总数。||  
|available_memory|**bigint**|在此节点上的总可用内存。||  
|process_cpu_usage|**bigint**|总进程 CPU 使用率，以刻度为单位。||  
|total_cpu_usage|**bigint**|总 CPU 使用率，以刻度为单位。||  
|thread_count|**bigint**|在此节点上使用的线程的总数。||  
|handle_count|**bigint**|使用此节点上的句柄的总数。||  
|total_elapsed_time|**bigint**|系统启动或重新启动后经过的总时间。|系统启动或重新启动后经过的总时间。 如果 total_elapsed_time 超过一个整数 （以毫秒为单位的 24.8 天） 的最大值，它将导致具体化失败由于溢出。<br /><br /> 以毫秒为单位的最大值相当于 24.8 天。|  
|is_available|**bit**|指示此节点是否可用的标志。||  
|sent_time|**datetime**|最后一次此节点发送网络包。||  
|received_time|**datetime**|上次接收网络数据包的此节点的时间。||  
|error_id|**nvarchar(36)**|此节点发生的最后一个错误的唯一标识符。||  
  
## <a name="see-also"></a>另请参阅  
 [SQL 数据仓库和并行数据仓库动态管理视图&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
