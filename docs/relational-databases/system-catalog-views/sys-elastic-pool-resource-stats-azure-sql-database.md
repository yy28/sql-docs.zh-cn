---
title: sys.elastic_pool_resource_stats
titleSuffix: Azure SQL Database
ms.date: 01/28/2019
ms.service: sql-database
ms.prod_service: sql-database
ms.reviewer: ''
ms.topic: reference
f1_keywords:
- sys.elastic_pool_resource_stats catalog view
helpviewer_keywords:
- sys.elastic_pool_resource_stats_TSQL
- sys.elastic_pool_resource_stats
- elastic_pool_resource_stats_TSQL
- elastic_pool_resource_stats
ms.assetid: f242c1bd-3cc8-4c8b-8aaf-c79b6a8a0329
author: stevestein
ms.author: sstein
ms.custom: seo-dt-2019
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 0712785a5af3e8cc3c606a597ba02e0075c88dd9
ms.sourcegitcommit: f688a37bb6deac2e5b7730344165bbe2c57f9b9c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/08/2019
ms.locfileid: "73843873"
---
# <a name="syselastic_pool_resource_stats-azure-sql-database"></a>sys. elastic_pool_resource_stats （Azure SQL Database）
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  返回 SQL 数据库服务器中所有弹性池的资源使用情况统计信息。 对于每个弹性池，每15秒的报告窗口（每分钟四行）都有一行。 这包括池中所有数据库的 CPU、IO、日志、存储消耗和并发请求/会话利用率。 此数据将保留14天。 
  
||  
|-|  
|**适用**于： [!INCLUDE[ssSDS](../../includes/sssds-md.md)] V12。|  
  
|列名|数据类型|描述|  
|-----------------|---------------|-----------------|  
|**start_time**|**datetime2**|指示15秒报告间隔的开始时间的 UTC 时间。|  
|**end_time**|**datetime2**|指示15秒报表间隔结束时间的 UTC 时间。|  
|**elastic_pool_name**|**nvarchar(128)**|弹性数据库池的名称。|  
|**avg_cpu_percent**|**decimal(5,2)**|平均计算使用率（以池限制的百分比表示）。|  
|**avg_data_io_percent**|**decimal(5,2)**|平均 i/o 利用率（以百分比表示），基于池的限制。|  
|**avg_log_write_percent**|**decimal(5,2)**|平均写入资源使用率（以池限制的百分比表示）。|  
|**avg_storage_percent**|**decimal(5,2)**|池的存储限制的平均存储利用率（以百分比表示）。|  
|**max_worker_percent**|**decimal(5,2)**|以百分比表示的最大并发工作线程数（以百分比表示）。|  
|**max_session_percent**|**decimal(5,2)**|基于池的限制的最大并发会话数（以百分比表示）。|  
|**elastic_pool_dtu_limit**|**int**|此弹性池的当前最大弹性池 DTU 设置。|  
|**elastic_pool_storage_limit_mb**|**bigint**|此弹性池的当前最大弹性池存储限制设置（以 mb 为单位）。|
|**avg_allocated_storage_percent**|**decimal(5,2)**|弹性池中所有数据库分配的数据空间百分比。  这是为弹性池分配的数据空间与数据最大大小的比率。  有关详细信息，请参阅[SQL DB 中的文件空间管理](https://docs.microsoft.com/azure/sql-database/sql-database-file-space-management)|  
  
## <a name="remarks"></a>Remarks

 此视图存在于 SQL 数据库服务器的 master 数据库中。 您必须连接到 master 数据库才能查询**sys.databases elastic_pool_resource_stats**。  
  
## <a name="permissions"></a>Permissions

 要求具有**dbmanager**角色的成员身份。  
  
## <a name="examples"></a>示例

 下面的示例返回当前 SQL 数据库服务器中所有弹性数据库池的最近时间排序的资源利用率数据。  
  
```sql
SELECT * FROM sys.elastic_pool_resource_stats
ORDER BY end_time DESC;  
```

 下面的示例计算给定池的平均 DTU 百分比消耗量。  

```sql
SELECT start_time, end_time,
  (SELECT Max(v)
FROM (VALUES (avg_cpu_percent), (avg_data_io_percent), (avg_log_write_percent)) AS value(v)) AS [avg_DTU_percent]
FROM sys.elastic_pool_resource_stats
WHERE elastic_pool_name = '<your pool name>'
ORDER BY end_time DESC;  
```

## <a name="see-also"></a>另请参阅

 [利用弹性数据库应对爆炸性增长](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool/)   
 [创建和管理 SQL 数据库弹性数据库池（预览版）](https://azure.microsoft.com/documentation/articles/sql-database-elastic-pool-portal/)   
 [resource_stats &#40;Azure SQL 数据库&#41; ](../../relational-databases/system-catalog-views/sys-resource-stats-azure-sql-database.md)   
 [dm_db_resource_stats &#40;Azure SQL 数据库&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-resource-stats-azure-sql-database.md)  
  
  
