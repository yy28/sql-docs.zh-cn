---
title: "sys.geo_replication_links （Azure SQL 数据库） |Microsoft 文档"
ms.custom: 
ms.date: 10/18/2016
ms.prod: 
ms.prod_service: sql-database
ms.reviewer: 
ms.service: sql-database
ms.component: dmv's
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- dm_geo_replication_links_TSQL
- dm_geo_replication_links
- sys.dm_geo_replication_links
- sys.dm_geo_replication_links_TSQL
helpviewer_keywords:
- sys.dm_geo_replication_links dynamic management view
- dm_geo_replication_links dynamic management view
ms.assetid: 58911798-1d60-4f28-87ab-2def2bfc3de7
caps.latest.revision: 
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5eb8f74023e90966200aca7603b82f685e0eb9db
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2018
---
# <a name="sysgeoreplicationlinks-azure-sql-database"></a>sys.geo_replication_links （Azure SQL 数据库）
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  包含在异地复制合作关系中的主要和辅助数据库之间的每个复制链接的行。 此视图驻留在逻辑 master 数据库中。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|database_id|**int**|Sys.databases 视图中的当前数据库 ID。|  
|start_date|**datetimeoffset**|在区域 SQL 数据库数据中心启动数据库复制时的 UTC 时间|  
|modify_date|**datetimeoffset**|在区域 SQL 数据库的数据中心数据库异地复制完成时的 UTC 时间。 新的数据库与主数据库从此时开始同步。 。|  
|link_guid|**uniqueidentifier**|异地复制链接的唯一 ID。|  
|partner_server|**sysname**|包含异地复制的数据库的逻辑服务器的名称。|  
|partner_database|**sysname**|链接的逻辑服务器上的异地复制数据库名称。|  
|replication_state|**tinyint**|对于此数据库，其中一个的异地复制的状态:。<br /><br /> 0 = 挂起。 计划在创建活动辅助数据库，但必要的准备步骤尚未完成。<br /><br /> 1 = 种子设定。 地域复制目标接受种子设定，但两个数据库不同步。 之前在完成种子设定，你无法连接到辅助数据库。 从主中删除辅助数据库将取消该种子设定操作。<br /><br /> 2 = 弥补性。 辅助数据库处于事务处理方式一致状态，并且正在不断地与主数据库同步。|  
|replication_state_desc|**nvarchar(256)**|PENDING<br /><br /> SEEDING<br /><br /> CATCH_UP|  
|角色 (role)|**tinyint**|地域复制角色，之一：<br /><br /> 0 = 主。 Database_id 指异地复制合作关系中的主数据库。<br /><br /> 1 = 辅助数据库。  Database_id 指异地复制合作关系中的主数据库。|  
|role_desc|**nvarchar(256)**|PRIMARY<br /><br /> SECONDARY|  
|secondary_allow_connections|**tinyint**|辅助数据库类型，之一：<br /><br /> 0 = 否。 故障转移之前，辅助数据库不可访问。<br /><br /> 1 = ReadOnly。 辅助数据库可访问仅向客户端连接使用 ApplicationIntent = ReadOnly。<br /><br /> 2 = 全部。 辅助数据库可访问的任何客户端连接。|  
|secondary_allow_connections _desc|**nvarchar(256)**|否<br /><br /> 全部<br /><br /> 只读|  
  
## <a name="permissions"></a>权限  
 此视图选项仅适用于**master**与服务器级别主体登录名的数据库。  
  
## <a name="example"></a>示例  
 显示具有异地复制链接的所有数据库。  
  
```  
SELECT   
     database_id  
   , start_date  
   , partner_server  
   , partner_database  
   , replication_state  
   , role_desc  
   , secondary_allow_connections_desc   
FROM sys.geo_replication_links;  
```  
  
## <a name="see-also"></a>另请参阅  
 [ALTER DATABASE（Azure SQL 数据库）](../../t-sql/statements/alter-database-azure-sql-database.md)   
 [sys.dm_geo_replication_link_status &#40;Azure SQL Database &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-geo-replication-link-status-azure-sql-database.md)   
 [sys.dm_operation_status &#40;Azure SQL Database &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-operation-status-azure-sql-database.md)  
  
  
