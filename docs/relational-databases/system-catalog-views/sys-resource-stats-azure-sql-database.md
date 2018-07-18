---
title: sys.resource_stats （Azure SQL 数据库） |Microsoft Docs
ms.custom: ''
ms.date: 04/06/2018
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.component: system-catalog-views
ms.suite: sql
ms.technology: system-objects
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
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: c2f8a0e0cebcf64bedac33861184e806f322d7d1
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "38038846"
---
# <a name="sysresourcestats-azure-sql-database"></a>sys.resource_stats (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  返回 Azure SQL 数据库的 CPU 使用率和存储数据。 在五分钟的间隔内收集和聚合数据。 对于每个用户数据库，对于资源消耗情况有变化的每个五分钟报告时段都有一行。 返回的数据包括 CPU 使用情况、 存储大小更改或数据库 SKU 修改。 无需更改的闲置数据库可能没有对应于每五分钟时间间隔内行。 历史数据保留大约 14 天。  
  
 **Sys.resource_stats**视图具有不同的定义，具体取决于数据库关联的 Azure SQL 数据库服务器版本。 在升级到新的服务器版本时，请考虑这些不同之处和应用程序所需的任何修改。  
  
 下表介绍 v12 服务器中可用的列：  
  
|“列”|数据类型|Description|  
|----------------------------|---------------|-----------------|  
|start_time|**datetime**|指示 5 分钟报告间隔的起始的 UTC 时间。|  
|end_time|**datetime**|指示五分钟报告间隔结束的 UTC 时间。|  
|database_name|**varchar**|用户数据库的名称。|  
|sku|**varchar**|数据库的服务层。 下面是可能的值：<br /><br /> “基本”<br /><br /> Standard<br /><br /> Premium<br /><br />常规用途<br /><br />业务关键型|  
|storage_in_megabytes|**float**|最大存储大小以兆字节为单位的时间段，包括数据库数据、 索引、 存储的过程和元数据。|  
|avg_cpu_percent|**numeric**|平均计算使用率（以服务层限制的百分比表示）。|  
|avg_data_io_percent|**numeric**|平均 I/O 使用率（以基于服务层限制的百分比表示）。|  
|avg_log_write_percent|**numeric**|平均写入资源使用率（以服务层限制的百分比表示）。|  
|max_worker_percent|**decimal(5,2)**|最大并发辅助进程 （请求） 以基于数据库的服务层限制的百分比表示。<br /><br /> 基于并发工作线程计数的 15 秒样本的五分钟间隔当前计算最大值。|  
|max_session_percent|**decimal(5,2)**|基于数据库的服务层限制百分比形式表示的最大并发会话。<br /><br /> 基于并发会话计数的 15 秒样本的五分钟间隔当前计算最大值。|  
|dtu_limit|**int**|当前最大数据库 DTU 设置为此数据库的在此时间间隔内。 |  
  
> [!TIP]  
>  有关这些限制和服务层的更多上下文，请参阅主题[服务层](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/)。  
    
## <a name="permissions"></a>权限  
 此视图可供所有用户角色有权连接到虚拟**主**数据库。  
  
## <a name="remarks"></a>Remarks  
 返回的数据**sys.resource_stats**表示为百分比的最大允许运行的服务层/性能级别的限制。  
  
 如果数据库是弹性池的成员，资源统计信息显示为百分比值，表示为数据库中的弹性池配置设置的最大限制的百分比。  
  
 对于此数据的更精细视图，使用**sys.dm_db_resource_stats**用户数据库中的动态管理视图。 此视图每隔 15 秒捕获数据和历史数据保留 1 小时。  有关详细信息，请参阅[sys.dm_db_resource_stats &#40;Azure SQL 数据库&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-resource-stats-azure-sql-database.md)。  

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
    
## <a name="see-also"></a>请参阅  
 [服务层](https://azure.microsoft.com/documentation/articles/sql-database-service-tiers/)   
 [服务层功能和限制](https://azure.microsoft.com/documentation/articles/sql-database-performance-guidance/)  
  
  
