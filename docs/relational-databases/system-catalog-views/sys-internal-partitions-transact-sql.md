---
title: sys.internal_partitions (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/26/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 0262df2b-5ba7-4715-b17b-3d9ce470a38e
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5795ec9feaef483dd3ee9b5f3e31dbb619a89331
ms.sourcegitcommit: ce5770d8b91c18ba5ad031e1a96a657bde4cae55
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67388341"
---
# <a name="sysinternalpartitions-transact-sql"></a>sys.internal_partitions (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  返回为每个跟踪基于磁盘的表的列存储索引的内部数据的行集的一行。 这些行集是列存储索引的内部并跟踪已删除行、 行组映射和增量存储行组。 它们为每个表分区; 每个跟踪数据每个表具有至少一个分区。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 每次重新生成列存储索引将重新创建行集。   
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|partition_id|**bigint**|此分区的分区 ID。 在数据库中是唯一的。|  
|object_id|**int**|包含分区的表的对象 ID。|  
|index_id|**int**|对表定义的列存储索引的索引 ID。<br /><br /> 1 = 聚集列存储索引<br /><br /> 2 = 非聚集列存储索引|  
|partition_number|**int**|分区数。<br /><br /> 1 = 已分区表的第一个分区或未分区表的单个分区。<br /><br /> 2 = 第二个分区中，依次类推。|  
|internal_object_type|**tinyint**|跟踪列存储索引的内部数据的行集对象。<br /><br /> 2 = COLUMN_STORE_DELETE_BITMAP<br /><br /> 3 = COLUMN_STORE_DELTA_STORE<br /><br /> 4 = COLUMN_STORE_DELETE_BUFFER<br /><br /> 5 = COLUMN_STORE_MAPPING_INDEX|  
|internal_object_type_desc|**nvarchar(60)**|COLUMN_STORE_DELETE_BITMAP-此位图索引跟踪标记为删除从列存储中的行。 由于分区可以具有多个行组中的行，位图是为每个行组。 行是仍以物理方式存在并已满空间位于在列存储中。<br /><br /> COLUMN_STORE_DELTA_STORE-存储组的行，调用的尚未压缩成列存储行组。 每个表分区可以包含零个或多个增量存储行组。<br /><br /> COLUMN_STORE_DELETE_BUFFER-用于维护到可更新非聚集列存储索引删除。 查询从基础的行存储表中删除行，删除缓冲区将跟踪从列存储中删除。 当已删除的行数超过 1048576 时，它们合并成删除位图背景元组发动机线程或显式的 Reorganize 命令。  在任何给定时间点，删除位图的删除缓冲区的并集表示所有已删除的行。<br /><br /> COLUMN_STORE_MAPPING_INDEX-只有在聚集列存储索引具有辅助的非聚集的索引时使用。 这将非聚集索引键映射到正确的行组和列存储中的行 ID。 它只存储密钥的行，然后迁移到不同的行组;增量行组压缩到列存储中，以及合并操作将两个不同的行组中的行时，将发生这种情况。|  
|Row_group_id|**int**|增量存储行组 ID。 每个表分区可以包含零个或多个增量存储行组。|  
|hobt_id|**bigint**|内部行集对象的 ID。 这是一个很好密钥来加入其他 Dmv 来获取有关内部行集的物理特征的详细信息。|  
|rows|**bigint**|此分区中的大约行数。|  
|data_compression|**tinyint**|压缩的行集的状态：<br /><br /> 0 = NONE<br /><br /> 1 = ROW<br /><br /> 2 = PAGE|  
|data_compression_desc|**nvarchar(60)**|为每个分区的压缩状态。 行存储表的可能值为 NONE、ROW 和 PAGE。 列存储表的可能值为 COLUMNSTORE 和 COLUMNSTORE_ARCHIVE。|  
|optimize_for_sequential_key|**bit**|1 = 分区最后一页插入启用了优化。<br><br>0 = 默认值。 分区具有禁用的最后一页插入优化。|
  
## <a name="permissions"></a>权限  
 要求 **公共** 角色具有成员身份。 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="general-remarks"></a>一般备注  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 每次创建或重新生成列存储索引将重新创建新的列存储内部索引。  
  
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
  
## <a name="see-also"></a>请参阅  
 [对象目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [查询 SQL Server 系统目录常见问题解答](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
