---
title: sys.internal_partitions (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- Azure SQL Database
- SQL Server 2016 Preview
dev_langs:
- TSQL
ms.assetid: 0262df2b-5ba7-4715-b17b-3d9ce470a38e
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a3280403d6194bd3f5370985d31e672752ed8c25
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2018
---
# <a name="sysinternalpartitions-transact-sql"></a>sys.internal_partitions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  返回为每个跟踪基于磁盘的表的列存储索引的内部数据的行集的一行。 这些行集是列存储索引的内部和跟踪删除行、 行组映射和增量存储行组。 他们可以为每个表分区; 每个跟踪数据每个表有至少一个分区。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]它会重新生成列存储索引每次重新创建行集。   
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|partition_id|**bigint**|此分区的分区 ID。 在数据库中是唯一的。|  
|object_id|**int**|包含分区的表的对象 ID。|  
|index_id|**int**|在表上定义的列存储索引的索引 ID。<br /><br /> 1 = 聚集列存储索引<br /><br /> 2 = 非聚集列存储索引|  
|partition_number|**int**|分区数。<br /><br /> 1 = 第一分区的已分区表或未分区表的单个分区。<br /><br /> 2 = 第二个分区，依此类推。|  
|internal_object_type|**tinyint**|跟踪列存储索引的内部数据的行集对象。<br /><br /> 2 = COLUMN_STORE_DELETE_BITMAP<br /><br /> 3 = COLUMN_STORE_DELTA_STORE<br /><br /> 4 = COLUMN_STORE_DELETE_BUFFER<br /><br /> 5 = COLUMN_STORE_MAPPING_INDEX|  
|internal_object_type_desc|**nvarchar(60)**|COLUMN_STORE_DELETE_BITMAP – 此位图索引跟踪标记为从列存储中删除的行。 因为分区可以有多个行组中的行，位图是每个行组。 行是仍以物理方式存在并已占用空间正在列存储。<br /><br /> COLUMN_STORE_DELTA_STORE – 的行，存储组称为行组，不具有将被压缩到列存储。 每个表分区可以有零个或多个增量存储行组。<br /><br /> COLUMN_STORE_DELETE_BUFFER – 用于维护可更新非聚集列存储索引删除。 当查询从基础的行存储表中删除行时，删除缓冲区将跟踪从列存储的删除。 当已删除的行数超过 1048576 时，它们将合并回删除位图中，后台元组发动机线程或显式的 Reorganize 命令。  在任何给定时间点，删除位图的删除缓冲区的并集表示所有已删除的行。<br /><br /> COLUMN_STORE_MAPPING_INDEX – 使用只在聚集列存储索引已辅助的非聚集的索引。 这会将非聚集索引键映射到正确的行组和列存储中的行 ID。 它只存储密钥的行，然后迁移到不同的行组;在增量行组压缩到列存储，以及合并操作合并两个不同的行组中的行时，将发生这种情况。|  
|Row_group_id|**int**|增量存储行组 ID。 每个表分区可以有零个或多个增量存储行组。|  
|hobt_id|**bigint**|内部行集合对象的 ID。 这是与其他 Dmv 以获取有关内部行集的物理特征的详细信息的良好键。|  
|rows|**bigint**|此分区中的大约行数。|  
|data_compression|**tinyint**|压缩的行集的状态：<br /><br /> 0 = NONE<br /><br /> 1 = ROW<br /><br /> 2 = PAGE|  
|data_compression_desc|**nvarchar(60)**|为每个分区的压缩状态。 行存储表的可能值为 NONE、ROW 和 PAGE。 列存储表的可能值为 COLUMNSTORE 和 COLUMNSTORE_ARCHIVE。|  
  
## <a name="permissions"></a>权限  
 要求 **公共** 角色具有成员身份。 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="general-remarks"></a>一般备注  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 它将创建或重新生成列存储索引的每次重新创建新的列存储内部索引。  
  
## <a name="examples"></a>示例  
  
### <a name="a-view-all-of-the-internal-rowsets-for-a-table"></a>A. 查看所有表的内部行集  
 此示例返回所有表的内部列存储行集。 Hobt_id 还可用于查找有关特定行集的详细信息。  
  
```  
SELECT i.object_id, i.index_id, i.name, p.hobt_id, p.internal_object_type_id, p.internal_object_type_desc  
FROM sys.internal_partitions AS p  
JOIN sys.indexes AS i  
on i.object_id = p.object_id  
WHERE p.object_id = OBJECT_ID ( '<table name' ) ;  
```  
  
## <a name="see-also"></a>另请参阅  
 [对象目录视图 &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [查询 SQL Server 系统目录常见问题解答](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
