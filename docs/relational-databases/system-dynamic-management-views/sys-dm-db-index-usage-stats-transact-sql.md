---
title: sys.dm_db_index_usage_stats (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_db_index_usage_stats_TSQL
- sys.dm_db_index_usage_stats
- sys.dm_db_index_usage_stats_TSQL
- dm_db_index_usage_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_index_usage_stats dynamic management view
ms.assetid: d06a001f-0f72-4679-bc2f-66fff7958b86
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8d2096243b65573d7d54a372252794976c93d527
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2018
ms.locfileid: "52415332"
---
# <a name="sysdmdbindexusagestats-transact-sql"></a>sys.dm_db_index_usage_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  返回不同类型索引操作的计数以及上次执行每种操作的时间。  
  
 在 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 中，动态管理视图不能公开将影响数据库包含的信息，也不能公开有关用户可以访问的其他数据库的信息。 若要避免公开此类信息，包含不属于已连接租户的数据的每一行都筛选掉。  
  
> [!NOTE]  
>  **sys.dm_db_index_usage_stats**不返回有关内存优化索引的信息。 有关内存优化索引中使用的信息，请参阅[sys.dm_db_xtp_index_stats &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-index-stats-transact-sql.md)。  
  
> [!NOTE]  
>  若要将此视图从命名[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，使用**sys.dm_pdw_nodes_db_index_usage_stats**。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**database_id**|**smallint**|在其中定义表或视图的数据库的 ID。|  
|**object_id**|**int**|为其定义索引的表或视图的 ID。|  
|**index_id**|**int**|索引的 ID。|  
|**user_seeks**|**bigint**|通过用户查询执行的搜索次数。|  
|**user_scans**|**bigint**|通过未使用的用户查询的扫描次数查找谓词。|  
|**user_lookups**|**bigint**|由用户查询执行的书签查找次数。|  
|**user_updates**|**bigint**|通过用户查询执行的更新次数。 这包括 Insert、 Delete 和更新表示操作执行不受影响的实际行数。 例如，如果删除在一个语句中的 1000年行，此计数递增 1|  
|**last_user_seek**|**datetime**|用户上次执行搜索的时间。|  
|**last_user_scan**|**datetime**|用户上次执行扫描的时间。|  
|**last_user_lookup**|**datetime**|用户上次执行查找的时间。|  
|**last_user_update**|**datetime**|用户上次执行更新的时间。|  
|**system_seeks**|**bigint**|通过系统查询执行的搜索次数。|  
|**system_scans**|**bigint**|通过系统查询执行的扫描次数。|  
|**system_lookups**|**bigint**|通过系统查询执行的查找次数。|  
|**system_updates**|**bigint**|通过系统查询执行的更新次数。|  
|**last_system_seek**|**datetime**|系统上次执行搜索的时间。|  
|**last_system_scan**|**datetime**|系统上次执行扫描的时间。|  
|**last_system_lookup**|**datetime**|系统上次执行查找的时间。|  
|**last_system_update**|**datetime**|系统上次执行更新的时间。|  
|pdw_node_id|**int**|**适用于**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]， [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 对于此分布的节点标识符。|  
  
## <a name="remarks"></a>备注  
 由一个查询执行对指定索引所进行的每个单独的搜索、扫描、查找或更新都被计为对该索引的一次使用，并使此视图中的相应计数器递增。 对于由用户提交的查询所引发的操作以及由内部生成的查询所引发的操作（例如为收集统计信息而进行的扫描），都将报告相应的信息。  
  
 **User_updates**计数器指示的级别引起的插入的索引维护、 更新或删除对基础表或视图的操作。 可以使用此视图确定应用程序极少使用的索引。 还可以使用此视图确定引发维护开销的索引。 您可能要删除引发维护开销但不用于查询或只是偶尔用于查询的索引。  
  
 只要启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (MSSQLSERVER) 服务，计数器就初始化为空。 而且，当分离或关闭数据库时（例如，由于 AUTO_CLOSE 设置为 ON），便会删除与该数据库关联的所有行。  
  
 使用索引时，将行添加到**sys.dm_db_index_usage_stats**如果某行的索引尚不存在。 当添加该行时，它的计数器会初始设置为零。  
  
 在升级到[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]， [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]，或[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]，sys.dm_db_index_usage_stats 中的项会被删除。 开头[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]，就像之前保留条目[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]。  
  
## <a name="permissions"></a>权限  
上[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`权限。   
上[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]，需要`VIEW DATABASE STATE`数据库中的权限。  
  
## <a name="see-also"></a>请参阅  

 [与索引相关的动态管理视图和函数 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/index-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_db_index_physical_stats (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)   
 [sys.dm_db_index_operational_stats (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md)   
 [sys.indexes (Transact-SQL)](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.objects (Transact-SQL)](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [监视和优化性能](../../relational-databases/performance/monitor-and-tune-for-performance.md)  
  
  


