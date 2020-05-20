---
title: sys. index_resumable_operations （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 11/12/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.index_resumable_operations_TSQL
- sys.indexes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.indexes
- sys.index_resumable_operations
ms.assetid: ''
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 143ed8e5487772a39e4e98c92f8f07d78de7f370
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/05/2020
ms.locfileid: "82823367"
---
# <a name="sysindex_resumable_operations-transact-sql"></a>sys. index_resumable_operations （Transact-sql）

[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]
**sys. index_resumable_operations**是一个系统视图，用于监视和检查当前执行状态以实现可恢复索引重新生成。  
**适用**于： SQL Server （2017和更高版本）和 Azure SQL 数据库
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|此索引所属的对象的 ID （不可为 null）。|  
|**index_id**|**int**|索引的 ID （不可为 null）。 **index_id**仅在对象中是唯一的。|
|**name**|**sysname**|索引的名称。 **名称**仅在对象中是唯一的。|  
|**sql_text**|**nvarchar(max)**|DDL T-sql 语句文本|
|**last_max_dop**|**smallint**|上次使用的 MAX_DOP （默认值 = 0）|
|**partition_number**|**int**|所属索引或堆中的分区号。 对于未分区的表和索引，或者如果正在重新生成所有分区，则此列的值为 NULL。|
|State |**tinyint**|可恢复索引的操作状态：<br /><br />0 = 正在运行<br /><br />1 = 暂停|
|**state_desc**|**nvarchar(60)**|可恢复索引的操作状态的说明（正在运行或已暂停）|  
|**start_time**|**datetime**|索引操作开始时间（不可为 null）|
|**last_pause_time**|**datatime**| 索引操作上次暂停时间（可以为 null）。 如果操作正在运行且从未暂停，则为 NULL。|
|**total_execution_time**|**int**|开始时间的总执行时间（分钟）（不可为 null）|
|**percent_complete**|**real**|索引操作进度完成百分比（不可为 null）。|
|**page_count**|**bigint**|索引生成操作为新索引和映射索引（不可为 null）分配的索引页的总数。

## <a name="permissions"></a>权限

[!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  

## <a name="example"></a>示例

 列出处于暂停状态的所有可恢复索引创建或重新生成操作。

```sql
SELECT * FROM  sys.index_resumable_operations WHERE STATE = 1;  
```

## <a name="see-also"></a>另请参阅

- [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md)
- [CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md)
- [目录视图](catalog-views-transact-sql.md)
- [对象目录视图](object-catalog-views-transact-sql.md)
- [sys.indexes](sys-xml-indexes-transact-sql.md)
- [sys.index_columns](sys-index-columns-transact-sql.md)
- [sys.xml_indexes](sys-xml-indexes-transact-sql.md)
- [sys.objects](sys-index-columns-transact-sql.md)
- [sys.key_constraints](sys-key-constraints-transact-sql.md)
- [sys.filegroups](sys-filegroups-transact-sql.md)
- [sys.partition_schemes](sys-partition-schemes-transact-sql.md)
- [查询 SQL Server 系统目录常见问题](querying-the-sql-server-system-catalog-faq.md)
