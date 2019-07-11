---
title: sys.dm_geo_replication_link_status （Azure SQL 数据库） |Microsoft Docs
ms.custom: ''
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
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: e94406cf30d1a942581f5fcfd30438c84ea2b159
ms.sourcegitcommit: aeb2273d779930e76b3e907ec03397eab0866494
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/10/2019
ms.locfileid: "67716701"
---
# <a name="sysdmgeoreplicationlinkstatus-azure-sql-database"></a>sys.dm_geo_replication_link_status（Azure SQL 数据库）

[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  包含每个异地复制合作关系中的主要和辅助数据库之间的复制链接的行。 这包括主和辅助数据库。 如果给定主数据库存在多个连续复制链接，此表为每个关系包含一行。 在所有数据库，包括逻辑 master 中创建视图。 但是，在主数据库中查询此视图将返回空集合。  
  
|列名|数据类型|描述|  
|-----------------|---------------|-----------------|  
|link_guid|**uniqueidentifier**|复制链接的唯一 ID。|  
|partner_server|**sysname**|包含链接的数据库的 SQL 数据库服务器的名称。|  
|partner_database|**sysname**|链接 SQL Database 服务器上链接数据库的名称。|  
|last_replication|**datetimeoffset**|最后一个事务由主数据库制辅助确认的时间戳。 此值是可在主数据库上。|  
|replication_lag_sec|**int**|以秒为单位和之间的时差 last_replication 值的主数据库制在主计算机上的该事务的提交时间戳。  此值是可在主数据库上。|  
|replication_state|**tinyint**|对于此数据库，其中一个异地复制的状态:。<br /><br /> 1 = 种子设定。 异地复制目标正在设定种子，但尚未同步两个数据库。 直到设定种子完毕后，您不能连接到辅助数据库。 从主数据库中删除辅助数据库将取消种子设定操作。<br /><br /> 2 = 弥补。 辅助数据库处于事务一致的状态，并且正在不断地与主数据库同步。<br /><br /> 4 = 已挂起。 这不是活动的连续复制关系。 此状态通常指示可用的互连带宽不足，无法满足主数据库上事务活动的水平。 但是，连续复制关系仍保持不变。|  
|replication_state_desc|**nvarchar(256)**|PENDING<br /><br /> SEEDING<br /><br /> CATCH_UP|  
|角色 (role)|**tinyint**|异地复制角色，其中一个：<br /><br /> 0 = 主数据库。 Database_id 是指的异地复制合作关系中的主数据库。<br /><br /> 1 = 辅助数据库。  Database_id 是指的异地复制合作关系中的主数据库。|  
|role_desc|**nvarchar(256)**|PRIMARY<br /><br /> SECONDARY|  
|secondary_allow_connections|**tinyint**|辅助数据库类型，其中一个：<br /><br /> 0 = 不能直接允许连接到辅助数据库并且数据库不是可用于读访问。<br /><br /> 2 = all 允许连接到辅助 repl; 中的数据库进行只读访问 ication。|  
|secondary_allow_connections_desc|**nvarchar(256)**|否<br /><br /> All|  
|last_commit|**datetimeoffset**|提交到数据库的最后一个事务的时间。 如果检索主数据库上，它指示在主数据库上的最后一个提交时间。 如果检索辅助数据库上，它指示在辅助数据库上的最后一个提交时间。 如果检索辅助数据库上的复制链接的主数据库出现故障时，它指示哪一点辅助数据库赶上之前。|
  
> [!NOTE]  
>  如果通过删除辅助数据库 （部分 4.2） 中，该数据库中的行终止复制关系**sys.dm_geo_replication_link_status**视图将消失。  
  
## <a name="permissions"></a>权限  
 任何具有 view_database_state 权限帐户可以查询**sys.dm_geo_replication_link_status**。  
  
## <a name="example"></a>示例  
 显示复制延迟和我的辅助数据库的上次复制时间。  
  
```  
SELECT   
     link_guid  
   , partner_server  
   , last_replication  
   , replication_lag_sec   
FROM sys.dm_geo_replication_link_status;  
```  
  
## <a name="see-also"></a>请参阅  
 [ALTER DATABASE &#40;Azure SQL Database&#41;](../../t-sql/statements/alter-database-azure-sql-database.md)   
 [sys.geo_replication_links &#40;Azure SQL 数据库&#41;](../../relational-databases/system-dynamic-management-views/sys-geo-replication-links-azure-sql-database.md)   
 [sys.dm_operation_status &#40;Azure SQL 数据库&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-operation-status-azure-sql-database.md)  
  
  
