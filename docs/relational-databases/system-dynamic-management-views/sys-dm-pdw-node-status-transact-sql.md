---
title: sys. dm_pdw_node_status （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 8e263b65-81d0-49d0-8873-62ef424369d6
author: CarlRabeler
ms.author: carlrab
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 8e13043774528228eaa46e70abe5ee00f9e51ac9
ms.sourcegitcommit: df1f0f2dfb9452f16471e740273cd1478ff3100c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/29/2020
ms.locfileid: "87395927"
---
# <a name="sysdm_pdw_node_status-transact-sql"></a>sys. dm_pdw_node_status （Transact-sql）
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  保存有关所有设备节点的性能和状态的附加信息（高于[sys.databases dm_pdw_nodes &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-transact-sql.md)）。 它为设备中的每个节点列出一行。  
  
|列名|数据类型|说明|范围|  
|-----------------|---------------|-----------------|-----------|  
|pdw_node_id|**int**|与节点关联的唯一数字 id。<br /><br /> 此视图的键。|在设备中唯一，而不考虑类型。|  
|process_id|**int**|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]||  
|process_name|**nvarchar(255)**|[!INCLUDE[ssInfoNA](../../includes/ssinfona-md.md)]||  
|allocated_memory|**bigint**|此节点上已分配的内存总量。||  
|available_memory|**bigint**|此节点上的可用内存总量。||  
|process_cpu_usage|**bigint**|总进程 CPU 使用率（以计时周期为单位）。||  
|total_cpu_usage|**bigint**|总 CPU 使用率（以刻度为单位）。||  
|thread_count|**bigint**|在此节点上使用的线程的总数。||  
|handle_count|**bigint**|在此节点上使用的句柄总数。||  
|total_elapsed_time|**bigint**|自系统启动或重新启动以来经过的总时间。|自系统启动或重新启动以来经过的总时间。 如果 total_elapsed_time 超过了整数的最大值24.8 （以毫秒为单位），则会导致具体化失败，因为溢出。<br /><br /> 最大值（以毫秒为单位）等效于24.8 天。|  
|is_available|**bit**|指示此节点是否可用的标志。||  
|sent_time|**datetime**|此节点上次发送网络包的时间。||  
|received_time|**datetime**|此节点上次收到网络包的时间。||  
|error_id|**nvarchar （36）**|此节点上发生的最后一个错误的唯一标识符。||  
  
## <a name="see-also"></a>另请参阅  
 [SQL 数据仓库和并行数据仓库动态管理视图 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
