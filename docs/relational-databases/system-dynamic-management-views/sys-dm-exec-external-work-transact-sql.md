---
title: sys.dm_exec_external_work (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DM_EXEC_EXTERNAL_WORK
- DM_EXEC_EXTERNAL_WORK_TSQL
- SYS.DM_EXEC_EXTERNAL_WORK_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_external_work management view
- dm_exec_external_work management view
- PolyBase,views
- PolyBase
ms.assetid: 7597d97b-1fde-4135-ac35-4af12968f300
caps.latest.revision: 8
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 79de7b54f8d662107014d740ca157055f0085c78
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmexecexternalwork-transact-sql"></a>sys.dm_exec_external_work (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  返回有关每个辅助进程的工作负荷每个计算节点上的信息。  
  
 查询 sys.dm_exec_external_work 来标识增减与外部数据源 （例如 Hadoop 或外部的 SQL Server） 进行通信的工作。  
  
|列名|数据类型|Description|范围|  
|-----------------|---------------|-----------------|-----------|  
|execution_id|**nvarchar(32)**|关联的 PolyBase 查询的唯一标识符。|请参阅*request_ID*中[sys.dm_exec_requests &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)。|  
|step_index|**int**|此辅助进程正在执行的请求。|请参阅*step_index*中[sys.dm_exec_requests &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)。|  
|dms_step_index|**int**|在执行此辅助进程 DMS 计划中的步骤。|请参阅[sys.dm_exec_dms_workers &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-dms-workers-transact-sql.md)。|  
|compute_node_id|**int**|工作线程的节点运行。|请参阅[sys.dm_exec_compute_nodes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-compute-nodes-transact-sql.md)。|  
|type|**nvarchar(60)**|外部工作的类型。|File 拆分|  
|work_id|**int**|实际拆分的 ID。|大于或等于 0。|  
|input_name|**nvarchar(4000)**|要读取的输入的名称|使用 Hadoop 时的文件名称。|  
|read_location|**bigint**|偏移量或读取位置。|要读取的文件偏移量。|  
|bytes_processed|**bigint**|此工作线程处理的总字节数。|大于或等于 0。|  
|长度|**bigint**|拆分或发生 Hadoop HDFS 块的长度|用户可定义。 默认值为 64 M|  
|status|**nvarchar(32)**|工作线程的状态|挂起，处理、 完成、 失败、 已中止|  
|start_time|**datetime**|工作的开头||  
|end_time|**datetime**|工作的末尾||  
|total_elapsed_time|**int**|总时间 （毫秒）||  
  
## <a name="see-also"></a>另请参阅  
 [PolyBase 使用动态管理视图进行故障排除](http://msdn.microsoft.com/library/ce9078b7-a750-4f47-b23e-90b83b783d80)   
 [动态管理视图和函数 (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [与数据库相关的动态管理视图&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  
