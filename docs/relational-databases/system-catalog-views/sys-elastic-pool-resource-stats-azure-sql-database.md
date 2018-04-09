---
title: sys.elastic_pool_resource_stats （Azure SQL 数据库） |Microsoft 文档
ms.custom: ''
ms.date: 04/06/2018
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.component: system-catalog-views
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- Azure SQL Database
f1_keywords:
- sys.elastic_pool_resource_stats catalog view
helpviewer_keywords:
- sys.elastic_pool_resource_stats_TSQL
- sys.elastic_pool_resource_stats
- elastic_pool_resource_stats_TSQL
- elastic_pool_resource_stats
ms.assetid: f242c1bd-3cc8-4c8b-8aaf-c79b6a8a0329
caps.latest.revision: 18
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: c1e77bcfcfd4e27981f63fd2802fd6b76c18fe1f
ms.sourcegitcommit: d6b1695c8cbc70279b7d85ec4dfb66a4271cdb10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2018
---
# <a name="syselasticpoolresourcestats-azure-sql-database"></a>sys.elastic_pool_resource_stats （Azure SQL 数据库）
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  在逻辑服务器中返回所有弹性数据库池的资源使用情况统计信息。 对于每个弹性数据库池，则都占一行 reporting 窗口 （每分钟的四个行） 每 15 秒。 这包括 CPU、 IO、 日志、 存储消耗和并发请求/会话使用率池中所有数据库。 此数据将保留 14 天。 
  
||  
|-|  
|**适用于**: [!INCLUDE[ssSDS](../../includes/sssds-md.md)] V12。|  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**start_time**|**datetime2**|指示的报告间隔为 15 秒起始的 UTC 时间。|  
|**end_time**|**datetime2**|该值指示的报告间隔为 15 秒结束的 UTC 时间。|  
|**elastic_pool_name**|**nvarchar(128)**|弹性数据库池的名称。|  
|**avg_cpu_percent**|**decimal(5,2)**|平均计算利用率，以百分比表示的池的限制。|  
|**avg_data_io_percent**|**decimal(5,2)**|在基于池的限制数的百分比的平均 I/O 使用率。|  
|**avg_log_write_percent**|**decimal(5,2)**|平均写入资源使用率的池限制百分比。|  
|**avg_storage_percent**|**decimal(5,2)**|在池的存储限制的百分比的平均存储使用率。|  
|**max_worker_percent**|**decimal(5,2)**|最大并发辅助进程 （请求） 中基于池的限制数的百分比。|  
|**max_session_percent**|**decimal(5,2)**|在基于池的限制数的百分比的最大并发会话。|  
|**elastic_pool_dtu_limit**|**int**|当前最大的弹性池 DTU 设置此弹性池在此间隔。|  
|**elastic_pool_storage_limit_mb**|**bigint**|在此时间间隔设置为以兆字节表示此弹性池的当前最大的弹性池存储上限。|  
  
## <a name="remarks"></a>注释  
 此视图在逻辑服务器的 master 数据库中存在。 你必须连接到 master 数据库查询**sys.elastic_pool_resource_stats**。  
  
## <a name="permissions"></a>权限  
 要求的成员身份**dbmanager**角色。  
  
## <a name="examples"></a>示例  
 下面的示例返回按当前逻辑服务器中的所有弹性数据库池的最新时间排序的资源利用率数据。  
  
```  
SELECT * FROM sys.elastic_pool_resource_stats   
ORDER BY end_time DESC;  
```  
  
 下面的示例计算的平均 DTU 消耗百分比为给定的池。  
  
```  
SELECT start_time, end_time,      
  (SELECT Max(v)      
FROM (VALUES (avg_cpu_percent), (avg_data_io_percent), (avg_log_write_percent)) AS value(v)) AS [avg_DTU_percent]    
FROM sys.elastic_pool_resource_stats   
WHERE elastic_pool_name = '<your pool name>'   
ORDER BY end_time DESC;  
```  
  
## <a name="see-also"></a>另请参阅  
 [使用弹性数据库缓解爆炸性增长](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool/)   
 [创建和管理 SQL 数据库弹性数据库池 （预览版）](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool-portal/)   
 [sys.resource_stats &#40;Azure SQL 数据库&#41;](../../relational-databases/system-catalog-views/sys-resource-stats-azure-sql-database.md)   
 [sys.dm_db_resource_stats &#40;Azure SQL 数据库&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-resource-stats-azure-sql-database.md)  
  
  
