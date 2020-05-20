---
title: sys. dm_pdw_query_stats_xe （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.technology: system-objects
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 5d551241-db35-4958-b60f-55e996f95c1f
author: CarlRabeler
ms.author: carlrab
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: ba136f705c57fcd5ffbef1433d70ceaefe4e3ae9
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/05/2020
ms.locfileid: "82829260"
---
# <a name="sysdm_pdw_query_stats_xe-transact-sql"></a>sys. dm_pdw_query_stats_xe （Transact-sql）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  此 DMV 已弃用，并将在将来的版本中删除。 在此版本中，它返回0行。  
  
|列名|数据类型|说明|范围|  
|-----------------|---------------|-----------------|-----------|  
|event|**nvarchar(60)**|此视图的键。||  
|event_id|**nvarchar （36）**|||  
|create_time|**datetime**|||  
|session_id|**int**|会话的 id。|请参阅 dm_pdw_exec_sessions sys.databases 中的 session_id [&#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md)。|  
|cpu|**int**|||  
|reads|**int**|自事件开始后的逻辑读取次数。||  
|Writes|**int**|自事件开始后的逻辑写入次数。||  
|sql_text|**nvarchar(4000)**|||  
|client_app_name|**nvarchar(255)**|||  
|tsql_stack|**nvarchar(255)**|||  
|pdw_node_id|**int**|此 Xevent 实例正在其上运行的节点。|  
  
## <a name="see-also"></a>另请参阅  
 [SQL 数据仓库和并行数据仓库动态管理视图 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)  
  
  
