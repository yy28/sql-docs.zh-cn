---
title: sys.resource_stats （Azure SQL 数据库） |Microsoft 文档
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
caps.latest.revision: 28
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
monikerRange: = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 7b8087839e5ea151d69a18cdf46d19fa5c917e66
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="sysresourcestats-azure-sql-database"></a>sys.resource_stats (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  返回 Azure SQL 数据库的 CPU 使用率和存储数据。 在五分钟的间隔内收集和聚合数据。 对于每个用户数据库，对于资源消耗情况有变化的每个五分钟报告时段都有一行。 返回的数据包括 CPU 使用情况、 存储大小的变化或数据库 SKU 修改。 不进行任何更改的空闲数据库可能具有的每五分钟时间间隔内的行。 历史数据保留大约 14 天。  
  
 **Sys.resource_stats**视图都有不同的定义，具体取决于数据库与 Azure SQL 数据库服务器的版本。 在升级到新的服务器版本时，请考虑这些不同之处和应用程序所需的任何修改。  
  
 下表介绍 v12 服务器中可用的列：  
  
|列|数据类型|Description|  
|----------------------------|---------------|-----------------|  
|start_time|**datetime**|UTC 指示五分钟报告间隔的起始时间。|  
|end_time|**datetime**|该值指示五分钟报告间隔结束的 UTC 时间。|  
|database_name|**varchar**|用户数据库的名称。|  
|sku|**varchar**|数据库的服务层。 下面是可能的值：<br /><br /> 基本<br /><br /> Standard<br /><br /> Premium<br /><br />常规用途<br /><br />业务关键型|  
|storage_in_megabytes|**float**|以兆字节为时间段，包括数据库数据、 索引、 存储的过程和元数据的最大存储大小。|  
|avg_cpu_percent|**numeric**|平均计算使用率（以服务层限制的百分比表示）。|  
|avg_data_io_percent|**numeric**|平均 I/O 使用率（以基于服务层限制的百分比表示）。|  
|avg_log_write_percent|**numeric**|平均写入资源使用率（以服务层限制的百分比表示）。|  
|max_worker_percent|**decimal(5,2)**|最大并发辅助进程 （请求） 中基于数据库的服务层的限制数的百分比。<br /><br /> 基于并发工作计数的 15 秒示例五分钟间隔的当前计算最大值。|  
|max_session_percent|**decimal(5,2)**|在基于数据库的服务层的限制数的百分比的最大并发会话。<br /><br /> 基于并发会话计数的 15 秒示例五分钟间隔的当前计算最大值。|  
|dtu_limit|**int**|当前最大数据库 DTU 设置为此数据库的在此间隔。 |  
  
> [!TIP]  
>  有关这些限制和服务层的更多上下文，请参阅主题[服务层](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/)。  
    
## <a name="permissions"></a>权限  
 此视图可供所有用户角色有权连接到虚拟**master**数据库。  
  
## <a name="remarks"></a>注释  
 返回的数据**sys.resource_stats**允许你运行的服务层/性能级别限制的最大的百分比表示。  
  
 如果数据库是弹性池的成员，资源统计信息显示为百分比值，表示为数据库中的弹性池配置设置的最大限制的百分比。  
  
 对于此数据的更精细视图，使用**sys.dm_db_resource_stats**在用户数据库中的动态管理视图。 此视图捕获每隔 15 秒的数据，并将历史数据保留 1 个小时。  有关详细信息，请参阅[sys.dm_db_resource_stats &#40;Azure SQL 数据库&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-resource-stats-azure-sql-database.md)。  

## <a name="examples"></a>示例  
 以下示例返回与上周相比平均参与至少 80% 的计算使用率的所有数据库。  
  
```sql  
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
    
## <a name="see-also"></a>另请参阅  
 [服务层](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/)   
 [服务层功能和限制](https://azure.microsoft.com/documentation/articles/sql-database-performance-guidance/)  
  
  
