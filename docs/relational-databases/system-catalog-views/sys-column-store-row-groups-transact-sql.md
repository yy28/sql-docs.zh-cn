---
title: sys.column_store_row_groups (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.column_store_row_groups_TSQL
- column_store_row_groups
- sys.column_store_row_groups
- column_store_row_groups_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.column_store_row_groups catalog view
ms.assetid: 76e7fef2-d1a4-4272-a2bb-5f5dcd84aedc
caps.latest.revision: 17
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: ef19c029232369de3a2da590e17f97a8bdb13655
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "38029787"
---
# <a name="syscolumnstorerowgroups-transact-sql"></a>sys.column_store_row_groups (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  在各个段的基础上提供聚集列存储索引信息，以便帮助管理员作出系统管理决定。 **sys.column_store_row_groups**包含列 （包括那些已标记为已删除） 以物理方式存储的行的总数和标记为已删除的行数的列。 使用**sys.column_store_row_groups**来确定哪些行组具有较高百分比的已删除的行和应重新生成。  
   
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|对其定义此索引的表的 ID。|  
|**index_id**|**int**|具有此列存储索引的表的索引 ID。|  
|**partition_number**|**int**|保留行组 row_group_id 的表分区的 ID。 您可以使用 partition_number 将此 DMV 联接到 sys.partitions。|  
|**row_group_id**|**int**|与此行组关联的行组编号。 这在分区中是唯一的。<br /><br /> -1 = 内存中表的结尾。|  
|**delta_store_hobt_id**|**bigint**|增量存储区中打开的行组的 hobt_id。<br /><br /> 如果在增量存储行组不为 NULL。<br /><br /> 对于内存中表的结尾为 NULL。|  
|State|**tinyint**|与 state_description 关联的 ID 号。<br /><br /> 0 = INVISIBLE<br /><br /> 1 = OPEN<br /><br /> 2 = CLOSED<br /><br /> 3 = COMPRESSED <br /><br /> 4 = 逻辑删除|  
|**state_description**|**nvarchar(60)**|行组的持久状态的说明：<br /><br /> INVISIBLE - 从增量存储区中的数据进行生成过程中的隐藏压缩段。 读操作将使用增量存储区，直至完成不可见的压缩段。 然后，新段变为可见，并删除源增量存储区。<br /><br /> OPEN – 正在接受新记录的读/写行组。 开放的行组仍采用行存储格式，并且尚未压缩成列存储格式。<br /><br /> CLOSED – 一个已填充的行组，但尚未由元组搬运者进程压缩。<br /><br /> COMPRESSED – 已填充和压缩的行组。|  
|**total_rows**|**bigint**|行组中物理存储的总行数。 一些行可能已删除，但它们仍被存储。 一个行组中的最大行数为 1,048,576（十六进制 FFFFF）。|  
|**deleted_rows**|**bigint**|行组中标记为已删除的总行数。 对于 DELTA 行组，此值始终为 0。|  
|**size_in_bytes**|**bigint**|对于 DELTA 和 COLUMNSTORE 行组，指的是此行组中所有数据的大小（不包括元数据和共享字典），以字节为单位。|  
  
## <a name="remarks"></a>Remarks  
 针对每个表中具有聚合或非聚合列存储索引的每个列存储行组返回一行。  
  
 使用**sys.column_store_row_groups**以确定包含在行组和行组的大小的行数。  
  
 当行组中的已删除行数量增长到占总行数的较大百分比时，该表的效率将下降。 重新生成列存储索引以减少表的大小，同时减少读取该表所需的磁盘 I/O。 若要重新生成列存储索引使用**重新生成**的选项**ALTER INDEX**语句。  
  
 可更新列存储首先将新数据插入**打开**行组，这是采用行存储格式，有时也称为 delta 表。  一旦打开的行组已满，其状态更改为**已关闭**。 已关闭行组将由元组搬运者进程压缩为列存储格式和状态将变为**压缩**。  元组搬运者是一个后台进程，它定期唤醒并检查是否有任何关闭的行组正准备要压缩成列存储行组。  元组搬运者还取消分配其中已删除每个行的行组。 已解除分配的行组标记为**逻辑删除**。 若要立即运行元组搬运者进程，请使用**REORGANIZE**的选项**ALTER INDEX**语句。  
  
 如果列存储行组已填充，它将进行压缩并停止接受新行。 当从压缩组中删除行时，这些行将保留但标记为已删除。 对压缩组的更新将实现为压缩组中的删除以及对打开组的插入。  
  
## <a name="permissions"></a>权限  
 返回表的信息，如果用户具有**VIEW DEFINITION**表的权限。  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="examples"></a>示例  
 下面的示例联接**sys.column_store_row_groups**表与其他系统表，以返回有关特定表的信息。 计算的 `PercentFull` 列是对行组效率的估计。 若要查找有关单个表删除的注释连字符的前面**其中**子句，并提供表名称。  
  
```  
SELECT i.object_id, object_name(i.object_id) AS TableName,   
i.name AS IndexName, i.index_id, i.type_desc,   
CSRowGroups.*,   
100*(total_rows - ISNULL(deleted_rows,0))/total_rows AS PercentFull    
FROM sys.indexes AS i  
JOIN sys.column_store_row_groups AS CSRowGroups  
    ON i.object_id = CSRowGroups.object_id  
AND i.index_id = CSRowGroups.index_id   
--WHERE object_name(i.object_id) = '<table_name>'   
ORDER BY object_name(i.object_id), i.name, row_group_id;  
```  
  
## <a name="see-also"></a>请参阅  
 [对象目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [查询 SQL Server 系统目录常见问题](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [sys.columns (Transact-SQL)](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys.all_columns &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-all-columns-transact-sql.md)   
 [sys.computed_columns &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-computed-columns-transact-sql.md)   
 [列存储索引指南](~/relational-databases/indexes/columnstore-indexes-overview.md)     
 [sys.column_store_dictionaries &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-column-store-dictionaries-transact-sql.md)   
 [sys.column_store_segments (Transact-SQL)](../../relational-databases/system-catalog-views/sys-column-store-segments-transact-sql.md)  
  
  

