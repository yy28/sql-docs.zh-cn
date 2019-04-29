---
title: sys.fulltext_index_fragments (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fulltext_index_fragments
- sys.fulltext_index_fragments_TSQL
- fulltext_index_fragments_TSQL
- sys.fulltext_index_fragments
dev_langs:
- TSQL
helpviewer_keywords:
- full-text indexes [SQL Server], fragments
- full-text indexes [SQL Server], metadata
- troubleshooting [SQL Server], full-text search
- sys.fulltext_index_fragments catalog view
ms.assetid: a82e5018-5d88-45c0-9a47-c251e17a6cdb
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: dbf3affc922eeddd0b27d15df1177bad30bb185f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63006124"
---
# <a name="sysfulltextindexfragments-transact-sql"></a>sys.fulltext_index_fragments (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  全文索引使用内部表称为*全文索引片段*来存储倒排的索引数据。 可以使用此视图来查询有关这些片断的元数据。 在此视图中，每个全文索引片断在每个包含全文索引的表中各占一行。  
 
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|table_id|**int**|包含全文索引片断的表的对象 ID。|  
|fragment_object_id|**int**|与片断关联的内部表的对象 ID。|  
|fragment_id|**int**|全文索引片断的逻辑 ID。 它在该表的所有片断中是唯一的。|  
|TIMESTAMP|**timestamp**|与片断创建关联的时间戳。 较新片断的时间戳大于较早片断的时间戳。|  
|data_size|**int**|片断的逻辑大小（以字节为单位）。|  
|row_count|**int**|片断中的行数。|  
|status|**int**|片断状态，其中包括：<br /><br /> 0 = 新创建，尚未使用<br /><br /> 1 = 在全文索引填充或合并过程中正在用于插入<br /><br /> 4 = 关闭。 准备用于查询<br /><br /> 6 = 正在用于合并输入并准备用于查询<br /><br /> 8 = 标记为删除。 将不会用于查询和合并源。<br /><br /> 状态为 4 或 6 表示片断是逻辑全文索引的一部分，并且可以查询;也就是说，正是*可查询*片段。|  
  
## <a name="remarks"></a>备注  
 可以使用 sys.fulltext_index_fragments 目录视图来查询组成全文索引的片断数。 如果全文查询速度较慢，可使用 sys.fulltext_index_fragments 查询全文索引中的可查询片断（状态 = 4 或 6）数，如下所示：  
  
```  
SELECT table_id, status FROM sys.fulltext_index_fragments  
   WHERE status=4 OR status=6;  
```  
  
 如果存在多个可查询的片断，Microsoft 建议您重新组织包含全文索引的全文目录，以便将这些片断合并在一起。 若要重新组织的全文目录，请使用[ALTER FULLTEXT CATALOG](../../t-sql/statements/alter-fulltext-catalog-transact-sql.md)*catalog_name*重新组织。 例如，若要重新组织 `ftCatalog` 数据库中名为 `AdventureWorks2012` 的全文目录，请输入：  
  
```  
USE AdventureWorks2012;  
GO  
ALTER FULLTEXT CATALOG ftCatalog REORGANIZE;  
GO  
```  
  
## <a name="permissions"></a>权限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [对象目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [填充全文索引](../../relational-databases/search/populate-full-text-indexes.md)  
  
  
