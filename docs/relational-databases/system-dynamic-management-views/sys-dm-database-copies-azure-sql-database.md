---
title: sys.dm_database_copies （Azure SQL 数据库） |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- dm_database_copies_TSQL
- sys.dm_database_copies
- dm_database_copies
- sys.dm_database_copies_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dm_database_copies
- sys.dm_database_copies
ms.assetid: d03d4657-86d1-4496-97e6-cc3bc292e0b1
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 6b5a0a656693d66e701642c9c2202c2862136a54
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2019
ms.locfileid: "56031648"
---
# <a name="sysdmdatabasecopies-azure-sql-database"></a>sys.dm_database_copies (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  返回有关数据库副本的信息。  
  
若要返回有关异地复制链接的信息，请使用[sys.geo_replication_links](../../relational-databases/system-dynamic-management-views/sys-geo-replication-links-azure-sql-database.md)或[sys.dm_geo_replication_link_status](../../relational-databases/system-dynamic-management-views/sys-dm-geo-replication-link-status-azure-sql-database.md)视图 （SQL 数据库 V12 中提供）。
  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|`sys.databases` 视图中当前数据库的 ID。|  
|**start_date**|**datetimeoffset**|当启动数据库复制时，区域 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 数据中心的 UTC 时间。|  
|**modify_date**|**datetimeoffset**|当完成数据库复制时，区域 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 数据中心的 UTC 时间。 截至此时，新数据库与主数据库在事务上一致。 更新完成信息每隔 1 分钟。<br /><br />专用于反映将 percent_complete 字段的最后一个更新的 UTC 时间。|  
|**percent_complete**|**real**|已复制的字节的百分比。 值介于 0 到 100 之间。 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 可以自动从某些错误（如故障转移）中恢复，并重新启动数据库复制。 在这种情况下，percent_complete 将从 0 重新开始。|  
|**error_code**|**int**|当大于 0 时，代码指示复制时发生的错误。 如果不发生错误，则值等于 0。|  
|**error_desc**|**nvarchar(4096)**|复制时发生的错误的说明。|  
|**error_severity**|**int**|如果数据库复制失败，则返回 16。|  
|**error_state**|**int**|如果复制恢复，则返回 1。|  
|**copy_guid**|**uniqueidentifier**|复制操作的唯一 ID。|  
|**partner_server**|**sysname**|创建的副本的 SQL 数据库服务器的名称。|  
|**partner_database**|**sysname**|伙伴服务器上的数据库副本的名称。|  
|**replication_state**|**tinyint**|为此数据库的连续复制复制的状态。 值为：<br /><br /> 0 = 挂起。 安排了创建数据库副本，但必要的准备步骤尚未完成或者被种子设定配额临时阻止。<br /><br /> 1 = 种子设定。 被设定为种子的副本数据库尚未完全同步与源数据库。 在此状态下无法连接到该副本。 若要取消种子设定操作正在进行中的，必须删除复制数据库。|  
|**replication_state_desc**|**nvarchar(256)**|replication_state 的说明，它是以下某项：<br /><br /> PENDING<br /><br /> SEEDING<br />|  
|**maximum_lag**|**int**|保留的字段。|  
|**is_continuous_copy**|**bit**|0 = 返回 0|  
|**is_target_role**|**bit**|0 = 源数据库<br /><br /> 1 = 复制数据库|  
|**is_interlink_connected**|bit|保留的字段。|  
|**is_offline_secondary**|bit|保留的字段。|  
  
## <a name="permissions"></a>权限  
 此视图选项仅适用于**主**与服务器级别主体登录名的数据库。  
  
## <a name="remarks"></a>备注  
 可以使用**sys.dm_database_copies**中查看**主**数据库的源或目标[!INCLUDE[ssSDS](../../includes/sssds-md.md)]服务器。 当数据库复制成功完成且新数据库变为 ONLINE 之后中的行**sys.dm_database_copies**自动删除视图。  
  
  
