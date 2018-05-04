---
title: sys.dm_geo_replication_link_status （Azure SQL 数据库） |Microsoft 文档
ms.custom: ''
ms.date: 10/13/2016
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.component: dmv's
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
caps.latest.revision: 15
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 187a873e72570db11d19812a9bcc95927d577ec0
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmgeoreplicationlinkstatus-azure-sql-database"></a>sys.dm_geo_replication_link_status （Azure SQL 数据库）
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  包含在异地复制合作关系中的主要和辅助数据库之间的每个复制链接的行。 这包括主和辅助数据库。 如果给定的主数据库已存在多个连续复制链接，此表为每个关系包含一行。 在所有数据库，包括逻辑 master 中创建视图。 但是，在主数据库中查询此视图将返回空集合。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|link_guid|**uniqueidentifier**|复制链接的唯一 ID。|  
|partner_server|**sysname**|包含链接的数据库的逻辑服务器的名称。|  
|partner_database|**sysname**|链接的逻辑服务器上链接的数据库的名称。|  
|last_replication|**datetimeoffset**|由辅助基于主数据库时钟的最后一个事务确认的时间戳。 此值是主数据库上。|  
|replication_lag_sec|**int**|Last_replication 值和基于主数据库时钟在主计算机上的该事务的提交的时间戳之间的时间差异以秒为单位。  此值是主数据库上。|  
|replication_state|**tinyint**|对于此数据库，其中一个的异地复制的状态:。<br /><br /> 1 = 种子设定。 地域复制目标接受种子设定，但两个数据库不同步。 之前在完成种子设定，你无法连接到辅助数据库。 从主中删除辅助数据库将取消该种子设定操作。<br /><br /> 2 = 弥补性。 辅助数据库处于事务处理方式一致状态，并且正在不断地与主数据库同步。<br /><br /> 4 = 已挂起。 这不是活动的连续复制关系。 此状态通常指示可用的互连带宽不足，无法满足主数据库上事务活动的水平。 但是，连续复制关系仍保持不变。|  
|replication_state_desc|**nvarchar(256)**|PENDING<br /><br /> SEEDING<br /><br /> CATCH_UP|  
|角色 (role)|**tinyint**|地域复制角色，之一：<br /><br /> 0 = 主。 Database_id 指异地复制合作关系中的主数据库。<br /><br /> 1 = 辅助数据库。  Database_id 指异地复制合作关系中的主数据库。|  
|role_desc|**nvarchar(256)**|PRIMARY<br /><br /> SECONDARY|  
|secondary_allow_connections|**tinyint**|辅助数据库类型，之一：<br /><br /> 0 = 不能直接允许连接到辅助数据库并且数据库不是可用于读访问。<br /><br /> 2 = 所有允许连接到辅助 repl; 中的数据库进行只读访问 ication。|  
|secondary_allow_connections_desc|**nvarchar(256)**|否<br /><br /> 全部|  
|last_commit|**datetimeoffset**|提交到数据库的最后一个事务的时间。 如果检索主数据库上，它指示在主数据库上的最后一个提交时间。 如果检索辅助数据库上，它指示在辅助数据库上的最后一个提交时间。 如果检索辅助数据库上的复制链接的主出现故障时，它指示直到辅助的哪一阶段已捕捉到正在。|
  
> [!NOTE]  
>  如果通过删除辅助数据库 （部分 4.2） 中，在该数据库所在的行终止复制关系**sys.dm_geo_replication_link_status**视图中消失。  
  
## <a name="permissions"></a>权限  
 具备 view_database_state 权限的任何帐户可以查询**sys.dm_geo_replication_link_status**。  
  
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
  
## <a name="see-also"></a>另请参阅  
 [ALTER DATABASE &#40;Azure SQL 数据库&#41;](../../t-sql/statements/alter-database-azure-sql-database.md)   
 [sys.geo_replication_links &#40;Azure SQL 数据库&#41;](../../relational-databases/system-dynamic-management-views/sys-geo-replication-links-azure-sql-database.md)   
 [sys.dm_operation_status &#40;Azure SQL 数据库&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-operation-status-azure-sql-database.md)  
  
  
