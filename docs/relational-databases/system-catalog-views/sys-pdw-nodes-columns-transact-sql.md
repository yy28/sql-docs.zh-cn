---
title: sys.pdw_nodes_columns (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/03/2017
ms.prod: ''
ms.prod_service: sql-data-warehouse, pdw
ms.service: sql-data-warehouse
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 268c77b7-1d71-4197-a2ed-5e2b2b8fc260
caps.latest.revision: 7
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: aab0463f2fcc2a6ae24e716fd502c91eb8f9f867
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="syspdwnodescolumns-transact-sql"></a>sys.pdw_nodes_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-pdw-md.md)]

  显示用户定义的表和用户定义的视图的列。  
  
|列名|数据类型|Description|范围|  
|-----------------|---------------|-----------------|-----------|  
|object_id|**int**|此列所属对象的 ID。||  
|name|**sysname**|列的名称。 在对象中唯一。||  
|column_id|**int**|列的 ID。 在对象中唯一。||  
|system_type_id|**tinyint**|列的系统类型的 ID。||  
|user_type_id|**int**|用户定义的列类型的 ID。||  
|max_length|**int**|列的最大长度（字节）。|包括有关受支持的列类型 （无效）-1。|  
|精度|**tinyint**|如果基于数值; 列的精度否则为为 0。||  
|小数位数|**tinyint**|如果基于数值，则为列的小数位数；否则为 0。||  
|collation_name|**sysname**|如果基于字符的; 列的排序规则的名称否则，为 NULL。||  
|is_nullable|**bit**|1 = 列可为空。||  
|is_ansi_padded|**bit**|1 = 如果列为字符、二进制或变量类型，则该列使用 ANSI_PADDING ON 行为。|始终为 0。|  
|is_rowguidcol|**bit**|1 = 列为声明的 ROWGUIDCOL。|始终为 0。|  
|is_identity|**bit**|1 = 列具有标识值。|始终为 0。|  
|is_computed|**bit**|1 = 列为计算列。|始终为 0。|  
|is_filestream|**bit**|1 = 列为 FILESTREAM 列。|始终为 0。|  
|is_replicated|**bit**|1 = 列已复制。|始终为 0。|  
|is_non_sql_subscribed|**bit**|1 = 列具有非 SQL 订阅服务器。|始终为 0。|  
|is_merge_published|**bit**|1 = 列已合并发布。|始终为 0。|  
|is_dts_replicated|**bit**|1 = 通过使用 SSIS 复制列。|始终为 0。|  
|is_xml_document|**bit**|1 = 内容为完整的 XML 文档。|始终为 0。|  
|xml_collection_id|**int**|0 = 没有 XML 架构集合。|始终为 0。|  
|default_object_id|**int**|默认对象; ID0 = 无默认值。|始终为 0。|  
|rule_object_id|**int**|独立的规则绑定到列的 ID。 <br />0 = 无独立规则。|始终为 0。|  
|is_sparse|**bit**|1 = 列为稀疏列。|始终为 0。|  
|is_column_set|**bit**|1 = 列为列集。|始终为 0。|  
|pdw_node_id|**int**|唯一标识符[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]节点。|NOT NULL|  
  
## <a name="permissions"></a>权限  
 需要 CONTROL SERVER 权限。  
  
## <a name="see-also"></a>另请参阅  
 [SQL 数据仓库和并行数据仓库目录视图](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
 [sys.all_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-all-columns-transact-sql.md)  
  
  
