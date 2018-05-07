---
title: sys.all_columns (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- all_columns_TSQL
- all_columns
- sys.all_columns_TSQL
- sys.all_columns
dev_langs:
- TSQL
helpviewer_keywords:
- sys.all_columns catalog view
ms.assetid: 40e04fe9-0b64-4799-84c0-57f128b2bdc2
caps.latest.revision: 48
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 3b8daabfa5975e52c6c3f13bdb6c4bd8f791e3ec
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="sysallcolumns-transact-sql"></a>sys.all_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  显示属于用户定义对象和系统对象的所有列的联合。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|object_id|**int**|此列所属对象的 ID。|  
|name|**sysname**|列的名称。 在对象中是唯一的。|  
|column_id|**int**|列的 ID。 在对象中是唯一的。<br /><br /> 列 ID 可以不按顺序排列。|  
|system_type_id|**tinyint**|列的系统类型 ID。|  
|user_type_id|**int**|用户定义的列类型的 ID。<br /><br /> 若要返回的类型名称，将联接到[sys.types](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)目录在此列的视图。|  
|max_length|**int**|列的最大长度（字节）。<br /><br /> 为-1 = 的列数据类型为**varchar （max)**， **nvarchar (max)**， **varbinary （max)**，或**xml**。<br /><br /> 有关**文本**列，max_length 值将是 16 或 sp_tableoption 'text in row 设置的值。|  
|精度|**tinyint**|如果基于数值; 列的精度否则为为 0。|  
|小数位数|**tinyint**|如果列包含的是数值，则为列的小数位数；否则为 0。|  
|collation_name|**sysname**|如果基于字符的; 列的排序规则的名称否则，为 NULL。|  
|is_nullable|**bit**|1 = 列可为空。|  
|is_ansi_padded|**bit**|1 = 如果列为字符、二进制或变量类型，则该列使用 ANSI_PADDING ON 行为。<br /><br /> 0 = 列不是字符、二进制或变量类型。|  
|is_rowguidcol|**bit**|1 = 列为声明的 ROWGUIDCOL。|  
|is_identity|**bit**|1 = 列具有标识值|  
|is_computed|**bit**|1 = 列为计算列。|  
|is_filestream|**bit**|1 = 列声明使用 Filestream 存储。|  
|is_replicated|**bit**|1 = 列已复制。|  
|is_non_sql_subscribed|**bit**|1 = 列具有非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 订阅服务器。|  
|is_merge_published|**bit**|1 = 列已合并发布。|  
|is_dts_replicated|**bit**|1 = 使用 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 复制列。|  
|is_xml_document|**bit**|1 = 内容为完整的 XML 文档。<br /><br /> 0 = 内容是文档片段，或列的数据类型不是 XML。|  
|xml_collection_id|**int**|非零的列的数据类型是否为**xml**和类型化 XML。 该值将是包含列的验证 XML 架构命名空间的集合的 ID。<br /><br /> 0 = 没有任何 XML 架构集合。|  
|default_object_id|**int**|默认对象，无论它是独立 ID [sys.sp_bindefault](../../relational-databases/system-stored-procedures/sp-bindefault-transact-sql.md)，或在行、 列级默认约束。 内联列级默认对象的 parent_object_id 列是对该表本身的反引用。<br /><br /> 0 = 无默认值。|  
|rule_object_id|**int**|使用 sys.sp_bindrule 绑定到列的独立规则的 ID。<br /><br /> 0 = 无独立规则。<br /><br /> 列级检查约束，请参阅[sys.check_constraints &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-check-constraints-transact-sql.md)。|  
|is_sparse|bit|1 = 列为稀疏列。 有关详细信息，请参阅 [使用稀疏列](../../relational-databases/tables/use-sparse-columns.md)。|  
|is_column_set|bit|1 = 列为列集。 有关详细信息，请参阅 [使用列集](../../relational-databases/tables/use-column-sets.md)。|  
|将 generated_always_type|**tinyint**|**适用范围**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 表示列的类型的数字值：<br /><br /> 0 = NOT_APPLICABLE<br /><br /> 1 = AS_ROW_START<br /><br /> 2 = AS_ROW_END|  
|generated_always_type_desc|**nvarchar(60)**|**适用范围**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 列的类型的文本说明：<br /><br /> NOT_APPLICABLE<br /><br /> AS_ROW_START<br /><br /> AS_ROW_END|  
  
## <a name="permissions"></a>权限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另请参阅  
 [对象目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [查询的 SQL Server 系统目录常见问题](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [sys.columns (Transact-SQL)](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys.system_columns &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/sys-system-columns-transact-sql.md)   
 [sys.computed_columns &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/sys-computed-columns-transact-sql.md)  
  
  
