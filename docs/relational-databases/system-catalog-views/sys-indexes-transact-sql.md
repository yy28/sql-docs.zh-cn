---
title: sys.indexes (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 04/18/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.indexes
- indexes
- sys.indexes_TSQL
- indexes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.indexes catalog view
ms.assetid: 066bd9ac-6554-4297-88fe-d740de1f94a8
caps.latest.revision: 48
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: f251924f2e13c8834ff01f1f5ecc66b884c22675
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="sysindexes-transact-sql"></a>sys.indexes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  每个表格对象（例如，表、视图或表值函数）的索引或堆都包含一行。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|该索引所属对象的 ID。|  
|**名称**|**sysname**|索引的名称。 **名称**仅在对象中是唯一。<br /><br /> NULL = 堆|  
|**index_id**|**int**|索引的 ID。 **index_id**仅在对象中是唯一。<br /><br /> 0 = 堆<br /><br /> 1 = 聚集索引<br /><br /> > 1 = 非聚集索引|  
|**类型**|**tinyint**|索引的类型：<br /><br /> 0 = 堆<br /><br /> 1 = 聚集<br /><br /> 2 = 非聚集<br /><br /> 3 = XML<br /><br /> 4 = 空间<br /><br /> 5 = 聚集列存储索引。 **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 6 = 非聚集列存储索引。 **适用范围**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 7 = 非聚集哈希索引。 **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|  
|**type_desc**|**nvarchar(60)**|索引类型的说明：<br /><br /> HEAP<br /><br /> CLUSTERED<br /><br /> NONCLUSTERED<br /><br /> XML<br /><br /> SPATIAL<br /><br /> 聚集列存储-**适用于**:[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 非聚集列存储-**适用于**:[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 非聚集哈希： 仅在内存优化表上支持非聚集哈希索引。 sys.hash_indexes 视图显示当前哈希索引和哈希属性。 有关详细信息，请参阅[sys.hash_indexes &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-hash-indexes-transact-sql.md)。 **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|  
|**is_unique**|**bit**|1 = 索引是唯一的。<br /><br /> 0 = 索引不是唯一的。<br /><br /> 对于聚集列存储索引始终为 0。|  
|**data_space_id**|**int**|此索引的数据空间的 ID。 数据空间是文件组或分区方案。<br /><br /> 0 = **object_id**是表值函数或内存中索引。|  
|**ignore_dup_key**|**bit**|1 = IGNORE_DUP_KEY 是 ON。<br /><br /> 0 = IGNORE_DUP_KEY 是 OFF。|  
|**is_primary_key**|**bit**|1 = 索引是 PRIMARY KEY 约束的一部分。<br /><br /> 对于聚集列存储索引始终为 0。|  
|**is_unique_constraint**|**bit**|1 = 索引是 UNIQUE 约束的一部分。<br /><br /> 对于聚集列存储索引始终为 0。|  
|**fill_factor**|**tinyint**|> 0 = 创建或重新生成索引时使用的 FILLFACTOR 百分比。<br /><br /> 0 = 默认值<br /><br /> 对于聚集列存储索引始终为 0。|  
|**is_padded**|**bit**|1 = PADINDEX 是 ON。<br /><br /> 0 = PADINDEX 是 OFF。<br /><br /> 对于聚集列存储索引始终为 0。|  
|**is_disabled**|**bit**|1 = 禁用索引。<br /><br /> 0 = 不禁用索引。|  
|**is_hypothetical**|**bit**|1 = 索引是假设的，不能直接用作数据访问路径。 假设的索引包含列级统计信息。<br /><br /> 0 = 索引不是假设的。|  
|**allow_row_locks**|**bit**|1 = 索引允许行锁。<br /><br /> 0 = 索引不允许行锁。<br /><br /> 对于聚集列存储索引始终为 0。|  
|**allow_page_locks**|**bit**|1 = 索引允许页锁。<br /><br /> 0 = 索引不允许页锁。<br /><br /> 对于聚集列存储索引始终为 0。|  
|**has_filter**|**bit**|1 = 索引具有一个筛选器，且仅包含符合筛选器定义的行。<br /><br /> 0 = 索引不具有筛选器。|  
|**filter_definition**|**nvarchar(max)**|包含在筛选索引中的行子集的表达式。<br /><br /> 对于堆或非筛选索引，其值为 NULL。|  
|**auto_created**|**bit**|1 = 已通过自动优化创建索引。<br /><br />0 = 已由用户创建索引。
  
## <a name="permissions"></a>权限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="examples"></a>示例  
 下面的示例返回 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 数据库中 `Production.Product` 表的所有索引。  
  
```  
  
SELECT i.name AS index_name  
    ,i.type_desc  
    ,is_unique  
    ,ds.type_desc AS filegroup_or_partition_scheme  
    ,ds.name AS filegroup_or_partition_scheme_name  
    ,ignore_dup_key  
    ,is_primary_key  
    ,is_unique_constraint  
    ,fill_factor  
    ,is_padded  
    ,is_disabled  
    ,allow_row_locks  
    ,allow_page_locks  
FROM sys.indexes AS i  
INNER JOIN sys.data_spaces AS ds ON i.data_space_id = ds.data_space_id  
WHERE is_hypothetical = 0 AND i.index_id <> 0   
AND i.object_id = OBJECT_ID('Production.Product');  
GO  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [对象目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sys.index_columns (Transact-SQL)](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)   
 [sys.xml_indexes (Transact-SQL)](../../relational-databases/system-catalog-views/sys-xml-indexes-transact-sql.md)   
 [sys.objects (Transact-SQL)](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.key_constraints &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/sys-key-constraints-transact-sql.md)   
 [sys.filegroups (Transact-SQL)](../../relational-databases/system-catalog-views/sys-filegroups-transact-sql.md)   
 [sys.partition_schemes (Transact-SQL)](../../relational-databases/system-catalog-views/sys-partition-schemes-transact-sql.md)   
 [查询的 SQL Server 系统目录常见问题](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [内存中 OLTP（内存中优化）](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
