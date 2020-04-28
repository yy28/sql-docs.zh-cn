---
title: sys. dm_db_partition_stats （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 05/31/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_db_partition_stats
- dm_db_partition_stats_TSQL
- sys.dm_db_partition_stats_TSQL
- sys.dm_db_partition_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_partition_stats dynamic management view
ms.assetid: 9db9d184-b3a2-421e-a804-b18ebcb099b7
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: cb9ab9e3cbf5948e5e832171c179d6daa2c0bc28
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "68096277"
---
# <a name="sysdm_db_partition_stats-transact-sql"></a>sys.dm_db_partition_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  返回当前数据库中每个分区的页和行计数信息。  
  
> [!NOTE]  
>  若要从[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]调用此，请使用名称**dm_pdw_nodes_db_partition_stats**。 Dm_pdw_nodes_db_partition_stats sys.databases 中的 partition_id 不同于 Azure SQL 数据仓库的 sys.databases 目录视图中的 partition_id。
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**partition_id**|**bigint**|分区 ID。 在数据库中是唯一的。 除了 Azure SQL 数据仓库以外，此值与**sys.databases**目录视图中**partition_id**的值相同。|  
|**object_id**|**int**|包含该分区的表或索引视图的对象 ID。|  
|**index_id**|**int**|包含该分区的堆或索引的 ID。<br /><br /> 0 = 堆<br /><br /> 1 = 聚集索引。<br /><br /> > 1 = 非聚集索引|  
|**partition_number**|**int**|索引或堆中从 1 开始的分区号。|  
|**in_row_data_page_count**|**bigint**|分区中存储行内数据所用的页数。 如果分区是堆的一部分，则该值为堆中的数据页数。 如果分区是索引的一部分，则该值为叶级别中的页数。 （B 树中的非叶页不包含在计数中。）在这两种情况下，不包括 IAM （索引分配映射）页。 对于 xVelocity 内存优化列存储索引，始终为 0。|  
|**in_row_used_page_count**|**bigint**|用于存储和管理分区中的行内数据的总页数。 该计数包括非叶 B 树页、IAM 页以及 **in_row_data_page_count** 列包含的全部页。 对列存储索引始终为 0。|  
|**in_row_reserved_page_count**|**bigint**|为存储和管理该分区中的行内数据而保留的总页数，包括已使用的和未使用的页。 对列存储索引始终为 0。|  
|**lob_used_page_count**|**bigint**|用于存储和管理分区中的行外 **text**、**ntext**、**image**、**varchar(max)**、**nvarchar(max)**、**varbinary(max)** 和 **xml** 列的页数。 包含 IAM 页。<br /><br /> 用于存储和管理分区中的列存储索引的 LOB 总数。|  
|**lob_reserved_page_count**|**bigint**|为存储和管理分区中的行外 **text**、**ntext**、**image**、**varchar(max)**、**nvarchar(max)**、**varbinary(max)** 和 **xml** 列而保留的页数，包括使用的和未使用的页。 包含 IAM 页。<br /><br /> 为存储和管理分区中的列存储索引而保留的 LOB 总数。|  
|**row_overflow_used_page_count**|**bigint**|用于保存和管理分区中行溢出 **varchar**、**nvarchar**、**varbinary** 和 **sql_variant** 列的页数。 包含 IAM 页。<br /><br /> 对列存储索引始终为 0。|  
|**row_overflow_reserved_page_count**|**bigint**|为保存和管理分区中行溢出 **varchar**、**nvarchar**、**varbinary** 和 **sql_variant** 列而保留的页数，包括已使用的和未使用的页。 包含 IAM 页。<br /><br /> 对列存储索引始终为 0。|  
|**used_page_count**|**bigint**|用于分区的总页数。 计算为**in_row_used_page_count** + **lob_used_page_count** + **row_overflow_used_page_count**。|  
|**reserved_page_count**|**bigint**|为分区保留的总页数。 计算为**in_row_reserved_page_count** + **lob_reserved_page_count** + **row_overflow_reserved_page_count**。|  
|**row_count**|**bigint**|分区中的大约行数。|  
|**pdw_node_id**|**int**|**适用**于： [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 此分发所在的节点的标识符。|  
|**distribution_id**|**int**|**适用**于： [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 与分布关联的唯一数字 id。|  
  
## <a name="remarks"></a>备注  
 **sys.dm_db_partition_stats** 显示用于存储和管理数据库中全部分区的行内数据 LOB 数据和行溢出数据的空间的有关信息。 每个分区对应一行。  
  
 作为输出数据依据的计数缓存在内存中，或存储在磁盘中的各种系统表中。  
  
 行内数据、LOB 数据以及行溢出数据表示构成分区的三个分配单元。 可以在 [sys.allocation_units](../../relational-databases/system-catalog-views/sys-allocation-units-transact-sql.md) 目录视图中查询数据库中每个分配单元的元数据。  
  
 如果堆或索引未分区，则它由一个分区（分区号为 1）组成，因而只会为该堆或索引返回一行。 可以在 [sys.partitions](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md) 目录视图中查询有关数据库中全部表和索引的每个分区的元数据。  
  
 可以通过求全部相关分区计数的和来获取单个表或单个索引的总计数。  
  
## <a name="permissions"></a>权限  
 查询 **sys.dm_db_partition_stats** 动态管理视图要求具备 VIEW DATABASE STATE 权限。 有关动态管理视图权限的详细信息，请参阅[&#40;transact-sql&#41;中的动态管理视图和函数](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)。  
  
## <a name="examples"></a>示例  
  
### <a name="a-returning-all-counts-for-all-partitions-of-all-indexes-and-heaps-in-a-database"></a>A. 返回数据库中全部索引和堆的全部分区的所有计数  
 以下示例演示了 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 数据库中全部索引和堆的全部分区的所有计数。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT * FROM sys.dm_db_partition_stats;  
GO  
```  
  
### <a name="b-returning-all-counts-for-all-partitions-of-a-table-and-its-indexes"></a>B. 返回表及其索引的全部分区的所有计数  
 以下示例演示了 `HumanResources.Employee` 表及其索引的全部分区的所有计数。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT * FROM sys.dm_db_partition_stats   
WHERE object_id = OBJECT_ID('HumanResources.Employee');  
GO  
```  
  
### <a name="c-returning-total-used-pages-and-total-number-of-rows-for-a-heap-or-clustered-index"></a>C. 返回堆或聚集索引使用的总页数和总行数  
 以下示例返回 `HumanResources.Employee` 表的堆或聚集索引使用的总页数和总行数。 因为默认情况不对 `Employee` 表分区，请注意和仅包含一个分区。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT SUM(used_page_count) AS total_number_of_used_pages,   
    SUM (row_count) AS total_number_of_rows   
FROM sys.dm_db_partition_stats  
WHERE object_id=OBJECT_ID('HumanResources.Employee')    AND (index_id=0 or index_id=1);  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [动态管理视图和函数 &#40;Transact-sql&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [与数据库相关的动态管理视图 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  
  
  


