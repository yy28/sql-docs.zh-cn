---
title: sys. server_resource_stats （Azure SQL Database） |Microsoft Docs
ms.custom: ''
ms.date: 06/28/2018
ms.service: sql-database
ms.reviewer: carlrab, edmaca
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
monikerRange: =azuresqldb-current||=sqlallproducts-allversions
ms.openlocfilehash: e85a74b203d270223d215ace08a58a0eea980fa1
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85772986"
---
# <a name="sysserver_resource_stats-azure-sql-database"></a>sys. server_resource_stats （Azure SQL Database）
[!INCLUDE[Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/asdb-asdbmi.md)]

返回 Azure SQL 托管实例的 CPU 使用情况、IO 和存储数据。 在五分钟的间隔内收集和聚合数据。 每15秒报告一次。 返回的数据包括 CPU 使用率、存储大小、IO 利用率和托管实例 SKU。 历史数据保留大约 14 天。

**Sys. server_resource_stats**视图的定义不同，具体取决于与数据库关联的 Azure SQL 托管实例的版本。 在升级到新的服务器版本时，请考虑这些不同之处和应用程序所需的任何修改。
 
  
 下表介绍 v12 服务器中可用的列：  
  
|列|数据类型|说明|  
|----------------------------|---------------|-----------------|  
|start_time|**datetime2**|指示15秒报表间隔开始时间的 UTC 时间|  
|end_time|**datetime**|指示15秒报表间隔结束的 UTC 时间|
|resource_type|Nvarchar(128)|为其提供指标的资源的类型|
|resource_name|nvarchar(128)|资源的名称。|
|sku|nvarchar(128)|托管实例实例的服务层。 下面是可能的值： <br><ul><li>常规用途</li></ul><ul><li>业务关键</li></ul>|
|hardware_generation|nvarchar(128)|硬件生成标识符：例如 Gen 4 或 Gen 5|
|virtual_core_count|int|表示每个实例的虚拟核心数（公共预览版中为8、16或24）|
|avg_cpu_percent|decimal （5，2）|平均计算使用率（以该实例使用托管实例服务层限制的百分比表示）。 它计算为实例中所有数据库的所有资源池的 CPU 时间的总和，并在给定的时间间隔内除以该层的可用 CPU 时间。|
|reserved_storage_mb|bigint|每个实例保留的存储（客户为托管实例购买的存储空间量）|
|storage_space_used_mb|decimal （18，2）|所有托管实例数据库文件使用的存储（包括用户数据库和系统数据库）|
|io_request|bigint|间隔内的 i/o 物理操作数总数|
|io_bytes_read|bigint|在时间间隔内读取的物理字节数|
|io_bytes_written|bigint|在间隔中写入的物理字节数|

 
> [!TIP]  
>  有关这些限制和服务层的详细信息，请参阅主题[托管实例的服务层](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance#managed-instance-service-tiers)。  
    
## <a name="permissions"></a>权限  
 此视图可用于具有连接到**master**数据库的权限的所有用户角色。  
  
## <a name="remarks"></a>备注  
 **Sys. server_resource_stats**返回的数据表示为除 avg_cpu 之外的字节或兆字节（在列名中指定）中使用的总大小，这表示为运行的服务层/性能级别所允许的最大限制的百分比。  
 
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
    
## <a name="see-also"></a>另请参阅  
 [托管实例的服务层](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance#managed-instance-service-tiers)
