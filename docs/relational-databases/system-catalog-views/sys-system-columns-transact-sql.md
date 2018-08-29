---
title: sys.system_columns (TRANSACT-SQL) |Microsoft Docs
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
- system_columns_TSQL
- system_columns
- sys.system_columns
- sys.system_columns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.system_columns catalog view
ms.assetid: 4ab1d48a-d57a-4e76-a08c-9627eeaf4588
caps.latest.revision: 46
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 80cf322c0a5835274afffc8d8c48e217b63d75dd
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43084999"
---
# <a name="syssystemcolumns-transact-sql"></a>sys.system_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  具有列的系统对象的每列都对应一行。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|此列所属对象的 ID。|  
|**名称**|**sysname**|列的名称。 在对象中是唯一的。|  
|**column_id**|**int**|列的 ID。 在对象中是唯一的。<br /><br /> 列 ID 可以不按顺序排列。|  
|**system_type_id**|**tinyint**|列的系统类型的 ID。|  
|**user_type_id**|**int**|用户定义的列类型的 ID。<br /><br /> 若要返回的类型名称，将联接到[sys.types](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)目录对此列的视图。|  
|**max_length**|**smallint**|列的最大长度（以字节为单位）。<br /><br /> -1 = 的列数据类型为**varchar （max)**， **nvarchar （max)**， **varbinary （max)**，或者**xml**。<br /><br /> 有关**文本**列， **max_length**值将是 16，或者设置的值**sp_tableoption** 'text in row。|  
|**精度**|**tinyint**|如果基于数值; 列的精度否则为为 0。|  
|**scale**|**tinyint**|如果列包含的是数值，则为列的小数位数；否则为 0。|  
|**collation_name**|**sysname**|如果基于字符的; 的列的排序规则名称否则，为 NULL。|  
|**is_nullable**|**bit**|1 = 列可为空。|  
|**is_ansi_padded**|**bit**|1 = 如果列为字符、二进制或变量类型，则该列使用 ANSI_PADDING ON 行为。<br /><br /> 0 = 列不是字符、二进制或变量类型。|  
|**is_rowguidcol**|**bit**|1 = 列为声明的 ROWGUIDCOL。|  
|**is_identity**|**bit**|1 = 列具有标识值。|  
|**is_computed**|**bit**|1 = 列为计算列。|  
|**is_filestream**|**bit**|1 = 列声明使用 Filestream 存储。|  
|**is_replicated**|**bit**|1 = 列已复制。|  
|**is_non_sql_subscribed**|**bit**|1 = 列具有非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 订阅服务器。|  
|**is_merge_published**|**bit**|1 = 列已合并发布。|  
|**is_dts_replicated**|**bit**|1 = 使用 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 复制列。|  
|**is_xml_document**|**bit**|1 = 内容为完整的 XML 文档。<br /><br /> 0 = 内容是文档片段或列数据类型不是**xml**。|  
|**xml_collection_id**|**int**|非零的列数据类型是否**xml**和类型化 XML。 该值将为包含列的验证 XML 架构命名空间的集合的 ID。<br /><br /> 0 = 没有 XML 架构集合。|  
|**default_object_id**|**int**|默认对象，而不管它是独立的 ID [sys.sp_bindefault](../../relational-databases/system-stored-procedures/sp-bindefault-transact-sql.md)，还是内联列级 DEFAULT 约束。 **Parent_object_id**的内联列级默认对象的列是对该表本身的引用。 或者，如果没有默认值，则其值为 0。|  
|**rule_object_id**|**int**|独立规则绑定到的 ID 列使用**sys.sp_bindrule**。<br /><br /> 0 = 无独立规则。<br /><br /> 列级 CHECK 约束，请参阅[sys.check_constraints &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-check-constraints-transact-sql.md)。|  
|is_sparse|**bit**|1 = 列为稀疏列。 有关详细信息，请参阅 [使用稀疏列](../../relational-databases/tables/use-sparse-columns.md)。|  
|is_column_set|**bit**|1 = 列为列集。 有关详细信息，请参阅 [使用列集](../../relational-databases/tables/use-column-sets.md)。|  
|将 generated_always_type|**tinyint**|表示列的类型的数值：<br /><br /> 0 = NOT_APPLICABLE<br /><br /> 1 = AS_ROW_START<br /><br /> 2 = AS_ROW_END|  
|generated_always_type_desc|**nvarchar(60)**|列的类型的文本说明：<br /><br /> NOT_APPLICABLE<br /><br /> AS_ROW_START<br /><br /> AS_ROW_END<br /><br /> **适用范围**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>请参阅  
 [对象目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [查询 SQL Server 系统目录常见问题](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [sys.columns (Transact-SQL)](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)   
 [sys.all_columns &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-all-columns-transact-sql.md)   
 [sys.computed_columns &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-computed-columns-transact-sql.md)  
  
  
