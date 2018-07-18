---
title: sys.geo_replication_links （Azure SQL 数据库） |Microsoft Docs
ms.custom: ''
ms.date: 10/18/2016
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- dm_geo_replication_links_TSQL
- dm_geo_replication_links
- sys.dm_geo_replication_links
- sys.dm_geo_replication_links_TSQL
helpviewer_keywords:
- sys.dm_geo_replication_links dynamic management view
- dm_geo_replication_links dynamic management view
ms.assetid: 58911798-1d60-4f28-87ab-2def2bfc3de7
caps.latest.revision: 14
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 5e59dcd6550c006b5a1e0f3e3be6440669e05021
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "37997739"
---
# <a name="sysgeoreplicationlinks-azure-sql-database"></a>sys.geo_replication_links （Azure SQL 数据库）
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  包含每个异地复制合作关系中的主要和辅助数据库之间的复制链接的行。 此视图驻留在逻辑 master 数据库中。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|database_id|**int**|当前数据库中的 sys.databases 视图的 ID。|  
|start_date|**datetimeoffset**|区域 SQL 数据库数据中心启动数据库复制时的 UTC 时间|  
|modify_date|**datetimeoffset**|在区域的 SQL 数据库数据中心完成数据库异地复制时的 UTC 时间。 新的数据库与主数据库从此时开始同步。 实例时都提供 SQL Server 登录名。|  
|link_guid|**uniqueidentifier**|异地复制链接的唯一 ID。|  
|partner_server|**sysname**|包含的异地复制数据库的逻辑服务器的名称。|  
|partner_database|**sysname**|异地复制链接的逻辑服务器上数据库的名称。|  
|replication_state|**tinyint**|对于此数据库，其中一个异地复制的状态:。<br /><br /> 0 = 挂起。 安排了创建活动辅助数据库但尚未完成必要的准备步骤。<br /><br /> 1 = 种子设定。 异地复制目标正在设定种子，但尚未同步两个数据库。 直到设定种子完毕后，您不能连接到辅助数据库。 从主数据库中删除辅助数据库将取消种子设定操作。<br /><br /> 2 = 弥补。 辅助数据库处于事务一致的状态，并且正在不断地与主数据库同步。|  
|replication_state_desc|**nvarchar(256)**|PENDING<br /><br /> SEEDING<br /><br /> CATCH_UP|  
|角色 (role)|**tinyint**|异地复制角色，其中一个：<br /><br /> 0 = 主数据库。 Database_id 是指的异地复制合作关系中的主数据库。<br /><br /> 1 = 辅助数据库。  Database_id 是指的异地复制合作关系中的主数据库。|  
|role_desc|**nvarchar(256)**|PRIMARY<br /><br /> SECONDARY|  
|secondary_allow_connections|**tinyint**|辅助数据库类型，其中一个：<br /><br /> 0 = 否。 故障转移之前，辅助数据库不可访问。<br /><br /> 1 = ReadOnly。 辅助数据库是只能访问客户端连接使用 ApplicationIntent = ReadOnly。<br /><br /> 2 = 全部。 辅助数据库都可以访问任何客户端连接。|  
|secondary_allow_connections _desc|**nvarchar(256)**|“否”<br /><br /> All<br /><br /> 只读的|  
  
## <a name="permissions"></a>权限  
 此视图选项仅适用于**主**与服务器级别主体登录名的数据库。  
  
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
  
## <a name="see-also"></a>请参阅  
 [ALTER DATABASE（Azure SQL 数据库）](../../t-sql/statements/alter-database-azure-sql-database.md)   
 [sys.dm_geo_replication_link_status &#40;Azure SQL 数据库&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-geo-replication-link-status-azure-sql-database.md)   
 [sys.dm_operation_status &#40;Azure SQL 数据库&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-operation-status-azure-sql-database.md)  
  
  
