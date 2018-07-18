---
title: sys.dm_db_missing_index_details (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_db_missing_index_details
- dm_db_missing_index_details
- sys.dm_db_missing_index_details_TSQL
- dm_db_missing_index_details_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- missing indexes feature [SQL Server], sys.dm_db_missing_index_details dynamic management view
- sys.dm_db_missing_index_details dynamic management view
ms.assetid: ced484ae-7c17-4613-a3f9-6d8aba65a110
caps.latest.revision: 37
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 7d3b07692b4e12ab4bdd0be15566cf115ad71b76
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2018
ms.locfileid: "34465623"
---
# <a name="sysdmdbmissingindexdetails-transact-sql"></a>sys.dm_db_missing_index_details (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  返回有关缺失索引的详细信息，不包括空间索引。  
  
 在 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 中，动态管理视图不能公开将影响数据库包含的信息，也不能公开有关用户可以访问的其他数据库的信息。 要避免公开此类信息，需要将包含不属于已连接租户的数据的每一行都筛选掉。  

  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**index_handle**|**int**|标识特定的缺失索引。 该标识符在服务器中是唯一的。 **index_handle**是此表的密钥。|  
|**database_id**|**int**|标识带有缺失索引的表所驻留的数据库。|  
|**object_id**|**int**|标识索引缺失的表。|  
|**equality_columns**|**nvarchar(4000)**|构成相等谓词的列的逗号分隔列表，谓词的形式如下：<br /><br /> *table.column* =*constant_value*|  
|**inequality_columns**|**nvarchar(4000)**|构成不等谓词的列的逗号分隔列表，例如以下形式的谓词：<br /><br /> *table.column* > *constant_value*<br /><br /> “=”之外的任何比较运算符都表示不相等。|  
|**included_columns**|**nvarchar(4000)**|用于查询的涵盖列的逗号分隔列表。 有关涵盖的详细信息或包含的列，请参阅[Create Indexes with Included Columns](../../relational-databases/indexes/create-indexes-with-included-columns.md)。<br /><br /> 对于内存优化索引 (哈希和内存优化非聚集)，忽略**included_columns**。 每个内存优化索引中均包含表的所有列。|  
|**语句**|**nvarchar(4000)**|索引缺失的表的名称。|  
  
## <a name="remarks"></a>注释  
 返回的信息**sys.dm_db_missing_index_details**时查询查询优化器优化，而且不具有持久性，会更新。 缺失索引信息只保留到重新启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 前。 如果数据库管理员要在服务器回收后保留缺失索引信息，则应定期制作缺失索引信息的备份副本。  
  
 若要确定哪些缺失索引组特定的缺失索引是的一部分，您可以查询**sys.dm_db_missing_index_groups**动态管理视图，方法是其与**sys.dm_db_missing_index_details**基于**index_handle**列。  
  
## <a name="using-missing-index-information-in-create-index-statements"></a>在 CREATE INDEX 语句中使用缺失索引信息  
 若要返回的信息转换**sys.dm_db_missing_index_details**到内存优化索引和基于磁盘的索引都 CREATE INDEX 语句中，相等列应该进行之前是否不相等列，以及组合在一起它们应索引的键。 应该使用 INCLUDE 子句将包含列添加到 CREATE INDEX 语句。 若要确定相等列的有效顺序，请基于其选择性排序：首先列出选择性最强的列（列列表中的最左侧）。  
  
 有关内存优化索引的详细信息，请参阅[内存优化表的索引](../../relational-databases/in-memory-oltp/indexes-for-memory-optimized-tables.md)。  
  
## <a name="transaction-consistency"></a>事务一致性  
 如果事务创建或删除了一个表，则包含有关已删除对象的缺失索引信息的行将从此动态管理对象中删除，以保持事务一致性。  
  
## <a name="permissions"></a>权限

上[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`权限。   
上[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]，需要`VIEW DATABASE STATE`数据库中的权限。   

## <a name="see-also"></a>另请参阅  
 [sys.dm_db_missing_index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-columns-transact-sql.md)   
 [sys.dm_db_missing_index_groups &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-groups-transact-sql.md)   
 [sys.dm_db_missing_index_group_stats &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-group-stats-transact-sql.md)  
  
  
