---
title: sys.server_resource_stats （Azure SQL 数据库） |Microsoft Docs
ms.custom: ''
ms.date: 06/28/2018
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: carlrab, edmaca
ms.technology: ''
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
ms.assetid: ''
author: jovanpop-msft
ms.author: jovanpop
manager: craigg
ms.openlocfilehash: 192300903c19913ff3762a744db9f999589e2c53
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47822177"
---
# <a name="sysserverresourcestats-azure-sql-database"></a>sys.server_resource_stats （Azure SQL 数据库）
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

返回 Azure SQL 托管实例 CPU 使用情况、 IO 和存储数据。 在五分钟的间隔内收集和聚合数据。 报告每隔 15 秒都占一行。 返回的数据包括 CPU 使用率、 存储大小、 IO 利用率和托管的实例 SKU。 历史数据保留大约 14 天。

**Sys.server_resource_stats**视图具有不同的定义，具体取决于数据库关联的 Azure SQL 托管实例的版本。 在升级到新的服务器版本时，请考虑这些不同之处和应用程序所需的任何修改。
 
  
 下表介绍 v12 服务器中可用的列：  
  
|“列”|数据类型|Description|  
|----------------------------|---------------|-----------------|  
|start_time|**datetime2**|指示 15 秒的报告间隔的起始的 UTC 时间|  
|end_time|**datetime**|指示 15 秒的报告间隔结束的 UTC 时间|
|resource_type|nvarchar （128)|为其提供指标的资源类型|
|resource_name|nvarchar （128)|资源的名称。|
|sku|nvarchar （128)|托管实例的实例的服务层。 下面是可能的值： <br><ul><li>常规用途</li></ul><ul><li>业务关键型</li></ul>|
|hardware_generation|nvarchar （128)|硬件生成标识符： 例如，第 4 代或第 5 代|
|virtual_core_count|ssNoversion|表示每个实例 （8、 16 或 24 日在公共预览版） 的虚拟内核数|
|avg_cpu_percent|decimal(5,2)|使用过度的实例的托管实例服务层限制的百分比形式表示的平均计算使用率。 它是计算为该实例中的所有数据库的所有资源池的 CPU 时间的总和并除以该层在给定时间间隔内的可用 CPU 时间。|
|reserved_storage_mb|BIGINT|保留每个实例存储 （该客户购买的托管实例的空间量存储）|
|storage_space_used_mb|decimal(18,2)|存储使用的所有托管的实例数据库文件 （包括用户和系统数据库）|
|io_request|BIGINT|I/o 间隔内的物理操作的总数|
|io_bytes_read|BIGINT|物理读取的字节数在时间间隔内|
|io_bytes_written|BIGINT|物理写入的字节数在时间间隔内|

 
> [!TIP]  
>  有关这些限制和服务层的更多上下文，请参阅主题[托管实例服务层](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance#managed-instance-service-tier)。  
    
## <a name="permissions"></a>Permissions  
 此视图可供有权连接到的所有用户角色**主**数据库。  
  
## <a name="remarks"></a>备注  
 返回的数据**sys.server_resource_stats**表示为字节或兆字节 （列名称中所述） 中使用的总以外 avg_cpu，表示为百分比的最大允许服务的限制正在运行的层/性能级别。  
 
## <a name="examples"></a>示例  
 以下示例返回与上周相比平均参与至少 80% 的计算使用率的所有数据库。  
  
```sql  
DECLARE @s datetime;  
DECLARE @e datetime;  
SET @s= DateAdd(d,-7,GetUTCDate());  
SET @e= GETUTCDATE();  
SELECT resource_name, AVG(avg_cpu_percent) AS Average_Compute_Utilization   
FROM sys.server_resource_stats   
WHERE start_time BETWEEN @s AND @e  
GROUP BY resource_name  
HAVING AVG(avg_cpu_percent) >= 80  
```  
    
## <a name="see-also"></a>请参阅  
 [托管实例服务层](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance#managed-instance-service-tier)
