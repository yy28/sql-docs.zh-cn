---
title: sys. dm_resource_governor_external_resource_pools （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 07/24/2019
ms.prod: sql
ms.technology: machine-learning
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_resource_governor_external_resource_pools_TSQL
- sys.dm_resource_governor_external_resource_pools
- dm_resource_governor_external_resource_pools
- dm_resource_governor_external_resource_pools_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dm_resource_governor_external_resource_pools
- sys.dm_resource_governor_external_resource_pools
author: dphansen
ms.author: davidph
manager: cgronlun
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: cf77a073a1432df839bfd13046c66018496e79f1
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "68468515"
---
# <a name="sysdm_resource_governor_external_resource_pools-transact-sql"></a>sys. dm_resource_governor_external_resource_pools （Transact-sql）
[!INCLUDE[tsql-appliesto-ss-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss-xxxx-xxxx-xxx-md.md)]

返回有关当前外部资源池状态、资源池的当前配置以及资源池统计信息的信息。 
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)。  
  
|Colmn 名称      |数据类型      |说明|  
|----------------|---------------|-----------------| 
| external_pool_id|**int**|资源池的 ID。 不可为 null。 |
| name|**sysname**|资源池的名称。 不可为 null。 
| pool_version|**int**|内部版本号。|
| max_cpu_percent|**int**|存在 CPU 争用时允许此资源池中的所有请求使用的最大平均 CPU 带宽的当前配置。 不可为 null。 |
| max_processes|**int**|并发外部进程的最大数量。 默认值为 0，指定没有限制。 不可为 null。|
| max_memory_percent|**int**|此资源池中的请求可使用的总服务器内存百分比的当前配置。 不可为 null。 |
| statistics_start_time|**datetime**|为该池重置统计信息的时间。 不可为 null。 
| peak_memory_kb|**bigint**|资源池使用的最大内存量（kb）。 不可为 null。 |
| write_io_count|**int**|自重置资源调控器统计信息以来发出的写入 IO 总数。 不可为 null。 |
| read_io_count|**int**|自重置资源调控器统计信息以来发出的读取 IO 总数。 不可为 null。 |
| total_cpu_kernel_ms|**bigint**|重置资源调控器统计信息以来的累计 CPU 用户内核时间（以毫秒为单位）。 不可为 null。 |
| total_cpu_user_ms|**bigint**|重置资源调控器统计信息以来的累计 CPU 用户时间（以毫秒为单位）。 不可为 null。 |
| active_processes_count|**int**|请求时运行的外部进程数。 不可为 null。 |

 
## <a name="permissions"></a>权限

需要 `VIEW SERVER STATE` 权限。

## <a name="see-also"></a>另请参阅  
 [sys.dm_resource_governor_external_resource_pool_affinity (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md)  
  
  
