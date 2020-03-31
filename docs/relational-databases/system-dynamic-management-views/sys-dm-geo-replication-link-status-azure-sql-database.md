---
title: sys.dm_geo_replication_link_status
titleSuffix: Azure SQL Database
ms.date: 01/28/2019
ms.service: sql-database
ms.reviewer: ''
ms.topic: conceptual
f1_keywords:
- dm_geo_replication_link_status
- dm_geo_replication_link_status_TSQL
- sys.dm_geo_replication_link_status
- sys.dm_geo_replication_link_status_TSQL
helpviewer_keywords:
- dm_geo_replication_link_status dynamic management view
- sys.dm_geo_replication_link_status dynamic management view
ms.assetid: d763d679-470a-4c21-86ab-dfe98d37e9fd
author: mashamsft
ms.author: mathoma
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.custom: seo-dt-2019
ms.openlocfilehash: 8bdf74e6ee774d9a0cc8e3d9128c659b75287511
ms.sourcegitcommit: d1f6da6f0f5e9630261cf733c64958938a3eb859
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/12/2020
ms.locfileid: "79198224"
---
# <a name="sysdm_geo_replication_link_status-azure-sql-database"></a>sys.dm_geo_replication_link_status（Azure SQL 数据库）

[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  包含异地复制伙伴关系中主数据库和辅助数据库之间的每个复制链接的行。 这包括主数据库和辅助数据库。 如果给定主数据库有多个连续复制链接，此表将对每种关系包含一行。 将在所有数据库（包括逻辑 master）中创建该视图。 但是，在主数据库中查询此视图将返回空集合。  
  
|列名称|数据类型|描述|  
|-----------------|---------------|-----------------|  
|link_guid|**唯一标识符**|复制链接的唯一 ID。|  
|partner_server|**sysname**|包含链接数据库的 SQL 数据库服务器的名称。|  
|partner_database|**sysname**|链接 SQL Database 服务器上链接数据库的名称。|  
|last_replication|**日期时间偏移**|辅助数据库时钟确认最后一个事务的时号。 此值仅在主数据库上可用。|  
|replication_lag_sec|**Int**|last_replication值与该事务提交在主数据库时钟上提交的时间戳之间的时差（以秒为单位）。  此值仅在主数据库上可用。|  
|replication_state|**小金特**|此数据库的异地复制状态，其中一个：<br /><br /> 1 = 播种。 正在设定异地复制目标的种子，但两个数据库尚未同步。 在种子设定完成之前，您不能连接到辅助数据库。 从主数据库中删除辅助数据库将取消种子设定操作。<br /><br /> 2 = 追赶。 辅助数据库处于事务一致性状态，并且不断与主数据库同步。<br /><br /> 4 = 挂起。 这不是有效的连续复制关系。 此状态通常指示可用的互连带宽不足，无法满足主数据库上事务活动的水平。 但是，连续复制关系仍保持不变。|  
|replication_state_desc|**nvarchar(256)**|PENDING<br /><br /> SEEDING<br /><br /> CATCH_UP|  
|角色 (role)|**小金特**|异地复制角色，其中之一：<br /><br /> 0 = 主。 database_id是指异地复制伙伴关系中的主数据库。<br /><br /> 1 = 辅助。  database_id是指异地复制伙伴关系中的主数据库。|  
|role_desc|**nvarchar(256)**|PRIMARY<br /><br /> SECONDARY|  
|secondary_allow_connections|**小金特**|辅助类型，其中之一：<br /><br /> 0 = 不允许直接连接到辅助数据库，并且数据库不能进行读取访问。<br /><br /> 2 = 允许所有连接到数据库的辅助复读;用于只读访问。|  
|secondary_allow_connections_desc|**nvarchar(256)**|否<br /><br /> All|  
|last_commit|**日期时间偏移**|提交到数据库的最后一个事务的时间。 如果在主数据库上检索，则指示主数据库上的最后一个提交时间。 如果在辅助数据库上检索，则指示辅助数据库上的最后一个提交时间。 如果在复制链接的主数据库关闭时在辅助数据库上检索，则指示辅助数据库的点已赶上。|
  
> [!NOTE]  
>  如果通过删除辅助数据库（第 4.2 节）终止复制关系，则**sys.dm_geo_replication_link_status**视图中该数据库的行将消失。  
  
## <a name="permissions"></a>权限  
 具有view_database_state权限的任何帐户都可以查询**sys.dm_geo_replication_link_status**。  
  
## <a name="example"></a>示例  
 显示辅助数据库的复制延迟和上次复制时间。  
  
```  
SELECT   
     link_guid  
   , partner_server  
   , last_replication  
   , replication_lag_sec   
FROM sys.dm_geo_replication_link_status;  
```  
  
## <a name="see-also"></a>另请参阅  
 [更改数据库&#40;Azure SQL 数据库&#41;](../../t-sql/statements/alter-database-azure-sql-database.md)   
 [系统geo_replication_links&#40;Azure SQL 数据库&#41;](../../relational-databases/system-dynamic-management-views/sys-geo-replication-links-azure-sql-database.md)   
 [系统dm_operation_status&#40;Azure SQL 数据库&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-operation-status-azure-sql-database.md)   
 [sp_wait_for_database_copy_sync](../system-stored-procedures/active-geo-replication-sp-wait-for-database-copy-sync.md)
  
