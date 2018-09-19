---
title: sys.elastic_pool_resource_stats （Azure SQL 数据库） |Microsoft Docs
ms.custom: ''
ms.date: 09/13/2018
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.component: system-catalog-views
ms.suite: sql
ms.technology: system-objects
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
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 5f7f13ebb5699fc0fe2174e7ee1af9d6c44bcbfb
ms.sourcegitcommit: b8e2e3e6e04368aac54100c403cc15fd4e4ec13a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/13/2018
ms.locfileid: "45563263"
---
# <a name="syselasticpoolresourcestats-azure-sql-database"></a>sys.elastic_pool_resource_stats （Azure SQL 数据库）
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  返回逻辑服务器中的所有弹性数据库池的资源使用情况统计信息。 针对每个弹性数据库池，没有一个行的每个 15 秒的报告窗口 （每分钟四行）。 这包括池中所有数据库的 CPU、 IO、 日志、 存储消耗和并发请求/会话利用率。 此数据将保留 14 天。 
  
||  
|-|  
|**适用于**: [!INCLUDE[ssSDS](../../includes/sssds-md.md)] V12。|  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**start_time**|**datetime2**|指示报告间隔为 15 秒开始的 UTC 时间。|  
|**end_time**|**datetime2**|指示报告间隔为 15 秒结束的 UTC 时间。|  
|**elastic_pool_name**|**nvarchar(128)**|弹性数据库池的名称。|  
|**avg_cpu_percent**|**decimal(5,2)**|平均计算使用率百分比形式表示的池的限制。|  
|**avg_data_io_percent**|**decimal(5,2)**|以基于池限制百分比表示的平均 I/O 使用率。|  
|**avg_log_write_percent**|**decimal(5,2)**|平均写入资源使用率百分比形式表示的池的限制。|  
|**avg_storage_percent**|**decimal(5,2)**|以池的存储限制的百分比表示的平均存储使用率。|  
|**max_worker_percent**|**decimal(5,2)**|最大并发辅助进程 （请求） 以基于池限制百分比表示。|  
|**max_session_percent**|**decimal(5,2)**|以基于池限制百分比表示的最大并发会话。|  
|**elastic_pool_dtu_limit**|**int**|当前最大弹性池 DTU 设置此弹性池在此时间间隔内。|  
|**elastic_pool_storage_limit_mb**|**bigint**|在此间隔期间设置为以兆字节表示此弹性池的当前最大弹性池存储限制。|
|**avg_allocated_storage_percent**|**decimal(5,2)**|分配的弹性池中所有数据库的数据空间的百分比。  这是分配给数据弹性池的最大大小的数据空间的比率。  有关详细信息请参阅： [SQL DB 中的文件空间管理](https://docs.microsoft.com/azure/sql-database/sql-database-file-space-management)|  
  
## <a name="remarks"></a>备注  
 此视图在逻辑服务器的 master 数据库中存在。 您必须连接到 master 数据库查询**sys.elastic_pool_resource_stats**。  
  
## <a name="permissions"></a>Permissions  
 要求的成员身份**dbmanager**角色。  
  
## <a name="examples"></a>示例  
 以下示例返回按当前逻辑服务器中的所有弹性数据库池的最新时间排序的资源使用率数据。  
  
```  
SELECT * FROM sys.elastic_pool_resource_stats   
ORDER BY end_time DESC;  
```  
  
 以下示例计算给定池的平均 DTU 百分比消耗。  
  
```  
SELECT start_time, end_time,      
  (SELECT Max(v)      
FROM (VALUES (avg_cpu_percent), (avg_data_io_percent), (avg_log_write_percent)) AS value(v)) AS [avg_DTU_percent]    
FROM sys.elastic_pool_resource_stats   
WHERE elastic_pool_name = '<your pool name>'   
ORDER BY end_time DESC;  
```  
  
## <a name="see-also"></a>请参阅  
 [使用弹性数据库应对爆炸性增长](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool/)   
 [创建和管理 SQL 数据库弹性数据库池 （预览版）](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool-portal/)   
 [sys.resource_stats &#40;Azure SQL 数据库&#41;](../../relational-databases/system-catalog-views/sys-resource-stats-azure-sql-database.md)   
 [sys.dm_db_resource_stats &#40;Azure SQL 数据库&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-resource-stats-azure-sql-database.md)  
  
  
