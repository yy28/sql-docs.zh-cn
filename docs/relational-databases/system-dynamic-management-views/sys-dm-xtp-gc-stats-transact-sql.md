---
title: sys. dm_xtp_gc_stats （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_xtp_gc_stats
- dm_xtp_gc_stats_TSQL
- sys.dm_xtp_gc_stats_TSQL
- sys.dm_xtp_gc_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_xtp_gc_stats dynamic management view
ms.assetid: 8287d611-50e3-43e1-ba8d-3e3793d3ba0e
author: stevestein
ms.author: sstein
ms.openlocfilehash: 28d98f7f95d9e9c2af967976b875f61388342583
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "68090176"
---
# <a name="sysdm_xtp_gc_stats-transact-sql"></a>sys.dm_xtp_gc_stats (Transact-SQL)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  提供有关 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 垃圾回收进程的当前行为的信息（总体统计信息）。  
  
 行在常规事务处理过程中或是由主垃圾回收线程（称为空闲工作线程）进行垃圾回收。 在用户事务提交后，它取消排队从垃圾回收队列（[sys.databases. dm_xtp_gc_queue_stats &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xtp-gc-queue-stats-transact-sql.md)）中一个工作项。 可以进行垃圾回收但是未由主用户事务访问的任何行都在灰尘角扫描（针对较少访问的索引区域的扫描）过程中由空闲工作线程进行垃圾回收。  
  
 有关详细信息，请参阅[内存中 OLTP&#40;内存中优化&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)。  
  
|列名称|类型|说明|  
|-----------------|----------|-----------------|  
|rows_examined|**bigint**|自启动服务器以来垃圾回收子系统检查的行数。|  
|rows_no_sweep_needed|**bigint**|已在未进行灰尘角扫描的情况下删除的行数。|  
|rows_first_in_bucket|**bigint**|垃圾回收检查的作为哈希桶中第一行的行数。|  
|rows_first_in_bucket_removed|**bigint**|垃圾回收检查的、已删除的、作为哈希桶中第一行的行数。|  
|rows_marked_for_unlink|**bigint**|垃圾回收检查的在其索引中已标记为已取消链接且 ref count =0 的行数。|  
|parallel_assist_count|**bigint**|用户事务处理的行数。|  
|idle_worker_count|**bigint**|空闲工作线程处理的垃圾行数。|  
|sweep_scans_started|**bigint**|垃圾回收子系统执行的灰尘角扫描数。|  
|sweep_scans_retries|**bigint**|垃圾回收子系统执行的灰尘角扫描数。|  
|sweep_rows_touched|**bigint**|灰尘角处理读取的行。|  
|sweep_rows_expiring|**bigint**|灰尘角处理读取的即将到期的行。|  
|sweep_rows_expired|**bigint**|灰尘角处理读取的过期行。|  
|sweep_rows_expired_removed|**bigint**|灰尘角处理删除的过期行。|  
  
## <a name="permissions"></a>权限  
 要求对实例具有 VIEW SERVER STATE 权限。  
  
## <a name="usage-scenario"></a>使用方案  
 下面是示例输出：  
  
```  
rows_examined        rows_no_sweep_needed rows_first_in_bucket rows_first_in_bucket_removed  
280085               209512               69905  
rows_first_in_bucket_removed rows_marked_for_unlink parallel_assist_count idle_worker_count  
69905                        0                      8953  
  
idle_worker_count    sweep_scans_started  sweep_scan_retries   sweep_rows_touched  
10306473             670                  0                    1343  
  
sweep_rows_expiring  sweep_rows_expired   sweep_rows_expired_removed  
               0                 673673  
```  
  
## <a name="see-also"></a>另请参阅  
 [内存优化表动态管理视图 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  
