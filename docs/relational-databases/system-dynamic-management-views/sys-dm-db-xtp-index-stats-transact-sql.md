---
title: sys.dm_db_xtp_index_stats (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 08/29/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_db_xtp_index_stats
- dm_db_xtp_index_stats
- sys.dm_db_xtp_index_stats_TSQL
- dm_db_xtp_index_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_xtp_index_stats dynamic management view
ms.assetid: 8d0a50b8-2015-4576-930f-e3307dfc888e
caps.latest.revision: 25
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: ab42288073de559c6f691fd18672a7a4adc3f60e
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="sysdmdbxtpindexstats-transact-sql"></a>sys.dm_db_xtp_index_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-asdb-xxxx-xxx-md.md)]

  包含上次重新启动数据库后收集的统计信息。   
  
 有关详细信息，请参阅[内存中 OLTP&#40;内存中优化&#41;](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)和[对于使用内存优化表的索引的指导原则](http://msdn.microsoft.com/library/16ef63a4-367a-46ac-917d-9eebc81ab29b)。  

  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|object_id|**bigint**|该索引所属对象的 ID。|  
|xtp_object_id|**bigint**|与当前版本的对象相对应的内部 ID。<br /><br /> 注意： 适用于[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]。|  
|index_id|**bigint**|索引的 ID。 该 index_id 只在该对象中是唯一的。|  
|scans_started|**bigint**|执行的内存中 OLTP 索引扫描的次数。 每次进行选择、插入、更新或删除时都需要进行索引扫描。|  
|scans_retries|**bigint**|需要重试的索引扫描次数，|  
|rows_returned|**bigint**|自表创建或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 启动以来返回的累计行数。|  
|rows_touched|**bigint**|自表创建或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 启动以来访问的累计行数。|  
|rows_expiring|**bigint**|仅限内部使用。|  
|rows_expired|**bigint**|仅限内部使用。|  
|rows_expired_removed|**bigint**|仅限内部使用。|  
|phantom_scans_started|**bigint**|仅限内部使用。|  
|phatom_scans_retries|**bigint**|仅限内部使用。|  
|phantom_rows_touched|**bigint**|仅限内部使用。|  
|phantom_expiring_rows_encountered|**bigint**|仅限内部使用。|  
|phantom_expired_rows_encountered|**bigint**|仅限内部使用。|  
|phantom_expired_removed_rows_encountered|**bigint**|仅限内部使用。|  
|phantom_expired_rows_removed|**bigint**|仅限内部使用。|  
|object_address|**varbinary(8)**|仅限内部使用。|  
  
## <a name="permissions"></a>权限  
 要求对当前数据库拥有 VIEW DATABASE STATE 权限。  
  
## <a name="see-also"></a>另请参阅  
 [内存优化表的动态管理视图&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)  
  
  
