---
title: sys.dm_resource_governor_external_resource_pools (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 05/02/2018
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
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: c6dde8b57112785bde5377d77cdb1d57f2767e3b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47624145"
---
# <a name="sysdmresourcegovernorexternalresourcepools-transact-sql"></a>sys.dm_resource_governor_external_resource_pools (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

返回有关当前的外部资源池状态、 资源池和资源池统计信息的当前配置的信息。 
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)。  
  
|Colmn 名称      |数据类型      |Description|  
|----------------|---------------|-----------------| 
| external_pool_id|**int**|资源池的 ID。 不可为 null。 |
| NAME|**sysname**|资源池的名称。 不可为 null。 
| pool_version|**int**|内部版本号。|
| max_cpu_percent|**int**|存在 CPU 争用时允许此资源池中的所有请求使用的最大平均 CPU 带宽的当前配置。 不可为 null。 |
| max_processes|**int**|最大并发外部进程数。 默认值为 0，指定没有限制。 不可为 null。|
| max_memory_percent|**int**|此资源池中的请求可使用的总服务器内存百分比的当前配置。 不可为 null。 |
| statistics_start_time|**datetime**|为该池重置统计信息的时间。 不可为 null。 
| peak_memory_kb|**bigint**|最大使用，以千字节，资源池的内存量。 不可为 null。 |
| write_io_count|**int**|自重置资源调控器统计信息以来发出的写入 IO 总数。 不可为 null。 |
| read_io_count|**int**|自重置资源调控器统计信息以来发出的读取 IO 总数。 不可为 null。 |
| total_cpu_kernel_ms|**bigint**|中的累计 CPU 用户内核时间自重置资源调控器统计信息以来的毫秒。 不可为 null。 |
| total_cpu_user_ms|**bigint**|以毫秒为单位自重置资源调控器统计信息以来累积 CPU 用户时间。 不可为 null。 |
| active_processes_count|**int**|在请求的时间点运行的外部进程数。 不可为 null。 |

 
## <a name="permissions"></a>Permissions

需要 `VIEW SERVER STATE` 权限。

## <a name="see-also"></a>请参阅  
 [sys.dm_resource_governor_external_resource_pool_affinity (Transact SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-resource-governor-external-resource-pool-affinity-transact-sql.md)  
  
  
