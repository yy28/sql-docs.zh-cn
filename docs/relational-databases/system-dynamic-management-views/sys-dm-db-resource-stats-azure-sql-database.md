---
title: sys.dm_db_resource_stats （Azure SQL 数据库） |Microsoft 文档
ms.custom: ''
ms.date: 04/06/2018
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.component: dmv's
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_db_resource_stats
- sys.dm_db_resource_stats_TSQL
- dm_db_resource_stats
- dm_db_resource_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_resource_stats
- dm_db_resource_stats
ms.assetid: 6e76b39f-236e-4bbf-b0b5-38be190d81e8
caps.latest.revision: 11
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: On Demand
monikerRange: = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 4e67b2e698440789e954e60c25b7aaeb18d04e41
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmdbresourcestats-azure-sql-database"></a>sys.dm_db_resource_stats (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  返回有关 CPU、 I/O 和内存消耗[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]数据库。 每隔 15 秒会显示一行，即使该数据库中没有任何活动也是如此。 历史数据将保留一小时。  
  
|列|数据类型|Description|  
|-------------|---------------|-----------------|  
|end_time|**datetime**|UTC 时间用于指示当前报告间隔的结束时间。|  
|avg_cpu_percent|**十进制 (5,2)**|平均计算使用率（以服务层限制的百分比表示）。|  
|avg_data_io_percent|**十进制 (5,2)**|平均数据输入/输出利用的服务层限制的百分比度量。|  
|avg_log_write_percent|**十进制 (5,2)**|平均写入资源使用率（以服务层限制的百分比表示）。|  
|avg_memory_usage_percent|**十进制 (5,2)**|平均内存使用率（以服务层限制的百分比表示）。<br /><br /> 这包括用于内存中 OLTP 对象的存储的内存。|  
|xtp_storage_percent|**十进制 (5,2)**|存储使用率内存中 OLTP 中的服务层限制的百分比 （报告间隔末尾）。 这包括用于存储以下内存中 OLTP 对象的内存： 内存优化表、 索引和表变量。 它还包括用于处理 ALTER TABLE 操作的内存。<br /><br /> 如果在数据库中未使用内存中 OLTP，则返回 0。|  
|max_worker_percent|**十进制 (5,2)**|最大并发辅助进程 （请求） 中的数据库的服务层限制百分比表示。|  
|max_session_percent|**十进制 (5,2)**|中的数据库的服务层限制百分比表示的最大并发会话。|  
|dtu_limit|**int**|当前最大数据库 DTU 设置为此数据库的在此间隔。 |
|||
  
> [!TIP]  
>  有关这些限制和服务层的更多上下文，请参阅主题[服务层](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/)和[服务层功能和限制](https://azure.microsoft.com/documentation/articles/sql-database-performance-guidance/)。  
  
## <a name="permissions"></a>权限  
 此视图需要拥有 VIEW DATABASE STATE 权限。  
  
## <a name="remarks"></a>注释  
 返回的数据**sys.dm_db_resource_stats**允许你运行的服务层/性能级别限制的最大的百分比表示。
 
 如果已在最后 60 分钟内将数据库故障转移到另一台服务器，该视图将仅返回主数据库故障转移后此时间段内的数据。  
  
 对于此数据的粒度较低视图，使用**sys.resource_stats**目录视图中的**master**数据库。 此视图每 5 分钟捕获一次数据，并将历史数据保留 14 天。  有关详细信息，请参阅[sys.resource_stats &#40;Azure SQL 数据库&#41;](../../relational-databases/system-catalog-views/sys-resource-stats-azure-sql-database.md)。  
  
 如果数据库是弹性池的成员，资源统计信息显示为百分比值，表示为数据库中的弹性池配置设置的最大限制的百分比。  
  
## <a name="example"></a>示例  
  
以下示例将返回当前连接的数据库按最新时间排序的资源利用率数据。  
  
```  
SELECT * FROM sys.dm_db_resource_stats ORDER BY end_time DESC;  
  
```  
  
 以下示例将根据过去几个小时内用户数据库的性能级别所允许的最大 DTU 限制百分比来标识平均 DTU 使用率。 请考虑提高性能级别，因为这些百分比将始终接近于 100%。  
  
```  
SELECT end_time,   
  (SELECT Max(v)    
   FROM (VALUES (avg_cpu_percent), (avg_data_io_percent), (avg_log_write_percent)) AS    
   value(v)) AS [avg_DTU_percent]   
FROM sys.dm_db_resource_stats;  
  
```  
  
 以下示例将返回最近一小时的 CPU 使用率、数据和日志 I/O 以及内存使用率的平均值和最大值。  
  
```  
SELECT    
    AVG(avg_cpu_percent) AS 'Average CPU Utilization In Percent',   
    MAX(avg_cpu_percent) AS 'Maximum CPU Utilization In Percent',   
    AVG(avg_data_io_percent) AS 'Average Data IO In Percent',   
    MAX(avg_data_io_percent) AS 'Maximum Data IO In Percent',   
    AVG(avg_log_write_percent) AS 'Average Log Write Utilization In Percent',   
    MAX(avg_log_write_percent) AS 'Maximum Log Write Utilization In Percent',   
    AVG(avg_memory_usage_percent) AS 'Average Memory Usage In Percent',   
    MAX(avg_memory_usage_percent) AS 'Maximum Memory Usage In Percent'   
FROM sys.dm_db_resource_stats;  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [sys.resource_stats &#40;Azure SQL 数据库&#41;](../../relational-databases/system-catalog-views/sys-resource-stats-azure-sql-database.md)   
 [服务层](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/)   
 [服务层功能和限制](https://azure.microsoft.com/documentation/articles/sql-database-performance-guidance/)  
  
  
