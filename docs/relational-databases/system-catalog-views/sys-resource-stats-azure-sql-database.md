---
title: "sys.resource_stats （Azure SQL 数据库） |Microsoft 文档"
ms.custom: 
ms.date: 05/23/2016
ms.prod: 
ms.prod_service: sql-database
ms.reviewer: 
ms.service: sql-database
ms.component: system-catalog-views
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- resource_stats
- sys.resource_stats
- sys.resource_stats_TSQL
- resource_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.resource_stats
- resource_stats
ms.assetid: 02379a1b-3622-4578-8c59-a1b8f1a17914
caps.latest.revision: 
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 72b0dc0c526198dc49047f44be0cce47ea7f3455
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2018
---
# <a name="sysresourcestats-azure-sql-database"></a>sys.resource_stats (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  返回 Azure SQL 数据库的 CPU 使用率和存储数据。 在五分钟的间隔内收集和聚合数据。 对于每个用户数据库，对于资源消耗情况有变化的每个五分钟报告时段都有一行。 这包括 CPU 使用率、存储大小更改或数据库 SKU 修改。 没有更改的闲置数据库可能没有对应于每五分钟间隔的行。 历史数据保留大约 14 天。  
  
 **Sys.resource_stats**视图都有不同的定义，具体取决于数据库与 Azure SQL 数据库服务器的版本。 在升级到新的服务器版本时，请考虑这些不同之处和应用程序所需的任何修改。  
  
 下表介绍 v12 服务器中可用的列：  
  
|列（v12 服务器）|数据类型|Description|  
|----------------------------|---------------|-----------------|  
|start_time|**datetime**|指示 5 分钟报告间隔的开始时间的 UTC 时间。|  
|end_time|**datetime**|指示 5 分钟的报告间隔结束的 UTC 时间。|  
|database_name|**varchar**|用户数据库的名称。|  
|sku|**varchar**|数据库的服务层。 下面是可能的值：<br /><br /> 基本<br /><br /> Standard<br /><br /> Premium|  
|storage_in_megabytes|**float**|时间段的最大存储大小 (MB)，包括数据库数据、索引、存储过程和元数据。|  
|avg_cpu_percent|**numeric**|平均计算使用率（以服务层限制的百分比表示）。|  
|avg_data_io_percent|**numeric**|平均 I/O 使用率（以基于服务层限制的百分比表示）。|  
|avg_log_write_percent|**numeric**|平均写入资源使用率（以服务层限制的百分比表示）。|  
|max_worker_percent|**decimal(5,2)**|最大并发辅助进程 （请求） 中基于数据库的服务层的限制数的百分比。<br /><br /> 基于 15 第二个示例的并发工作项计数的 5 分钟时间间隔内当前计算最大值。|  
|max_session_percent|**decimal(5,2)**|在基于数据库的服务层的限制数的百分比的最大并发会话。<br /><br /> 基于并发会话计数 15 第二个示例 5 分钟时间间隔内当前计算最大值。|  
|dtu_limit|**int**|当前最大数据库 DTU 设置为此数据库的在此间隔。|  
  
> [!TIP]  
>  有关这些限制和服务层的更多上下文，请参阅主题[服务层](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/)和[服务层功能和限制](https://azure.microsoft.com/documentation/articles/sql-database-performance-guidance/)。  
  
 下表介绍 v11 服务器中可用的列：  
  
|列（v11 服务器）|数据类型|Description|  
|----------------------------|---------------|-----------------|  
|start_time|**datetime**|指示 5 分钟报告间隔的开始时间的 UTC 时间。|  
|end_time|**datetime**|指示 5 分钟的报告间隔结束的 UTC 时间。|  
|database_name|**nvarchar**|数据库的名称。|  
|sku|**nvarchar**|数据库的服务层。 下面是可能的值：<br /><br /> Web<br /><br /> Business<br /><br /> 基本<br /><br /> Standard<br /><br /> Premium|  
|usage_in_seconds|**int**|*注意： 此列已弃用的 v11，其值始终设置为 0。*<br /><br /> 自上次测量后使用的 CPU 时间。<br /><br /> 对于 CPU 度量，我们建议你使用**avg_cpu_cores_used**列而不是此列。|  
|storage_in_megabytes|**decimal**|时间段的最大存储大小 (MB)，包括数据库数据、索引、存储过程和元数据。|  
|avg_cpu_cores_used|**decimal**|*注意： 此列已弃用的 v11，其值始终设置为 0。*<br /><br /> 此间隔中使用的平均 CPU 内核数。|  
|avg_physical_read_iops|**decimal**|*注意： 此列已弃用的 v11，其值始终设置为 0。*<br /><br /> 此间隔中的平均读取 IOPS。|  
|avg_physical_write_iops|**decimal**|*注意： 此列已弃用的 v11，其值始终设置为 0。*<br /><br /> 此间隔中的平均写入 IOPS。|  
|active_memory_used_kb|**bigint**|*注意： 此列已弃用的 v11，其值始终设置为 0。*<br /><br /> 在此时间间隔结束正在使用的活动内存的计数。|  
|active_session_count|**int**|在此间隔末尾的活动会话计数。|  
|active_worker_count|**int**|在此间隔末尾的活动工作线程的计数。|  
|avg_cpu_percent|**decimal**|平均计算使用率（以服务层限制的百分比表示）。|  
|avg_physical_data_read_percent|**decimal**|平均 I/O 使用率（以基于服务层限制的百分比表示）。|  
|avg_log_write_percent|**decimal**|平均写入资源使用率（以服务层限制的百分比表示）。|  
  
## <a name="permissions"></a>权限  
 此视图可供所有用户角色有权连接到虚拟**master**数据库。  
  
## <a name="remarks"></a>注释  
 返回的数据**sys.resource_stats**允许你运行的基本、 标准和高级数据库的服务层/性能级别的 DTU 限制的最大的百分比表示。  对于 Web 层和业务层，这些数字表示 Standard S2 性能层限制的百分比。  例如，对 Web 数据库执行操作时，如果 avg_cpu_percent 返回 70%，则表示 S2 层限制的 70%。 此外，对于 Web 层和业务层，这些百分比可能会反映大于 100% 的数字，这类数字同样基于 S2 层限制。  
  
 如果数据库是弹性池的成员，资源统计信息显示为百分比值，表示为数据库中的弹性池配置设置的最大 DTU 限制的百分比。  
  
 对于此数据的更精细视图，使用**sys.dm_db_resource_stats**在用户数据库中的动态管理视图。 此视图每 15 秒钟捕获一次数据，并将历史数据保留 1 个小时。  有关详细信息，请参阅[sys.dm_db_resource_stats &#40;Azure SQL Database &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-resource-stats-azure-sql-database.md).  

## <a name="examples"></a>示例  
 以下示例返回与上周相比平均参与至少 80% 的计算使用率的所有数据库。  
  
```  
DECLARE @s datetime;  
DECLARE @e datetime;  
SET @s= DateAdd(d,-7,GetUTCDate());  
SET @e= GETUTCDATE();  
SELECT database_name, AVG(avg_cpu_percent) AS Average_Compute_Utilization   
FROM sys.resource_stats   
WHERE start_time BETWEEN @s AND @e  
GROUP BY database_name  
HAVING AVG(avg_cpu_percent) >= 80  
```  
  
 以下示例计算给定数据库的平均 DTU 百分比消耗。 （此查询仅在对 v11 服务器运行时才有效。）  
  
```  
SELECT start_time, end_time,      
  (SELECT Max(v)      
   FROM (VALUES (avg_cpu_percent), (avg_physical_data_read_percent), (avg_log_write_percent)) AS value(v)) AS [avg_DTU_percent]    
FROM sys.resource_stats   
WHERE database_name = '<your db name>'   
ORDER BY end_time DESC;  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [服务层](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/)   
 [服务层功能和限制](https://azure.microsoft.com/documentation/articles/sql-database-performance-guidance/)  
  
  
