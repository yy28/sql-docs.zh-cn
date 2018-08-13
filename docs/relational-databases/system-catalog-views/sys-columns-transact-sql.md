---
title: sys.columns (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 11/21/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.columns_TSQL
- sys.columns
- columns_TSQL
- columns
dev_langs:
- TSQL
helpviewer_keywords:
- sys.columns catalog view
ms.assetid: 323ac9ea-fc52-4b8c-8a7e-e0e44f8ed86c
caps.latest.revision: 57
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 5672a062fdab79cf7a903e5dfac2d1f369bd70de
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/06/2018
ms.locfileid: "39550347"
---
# <a name="syscolumns-transact-sql"></a>sys.columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  为包含列的对象（如视图或表）的每一列返回一行。 下面是包含列的对象类型的列表。  
  
-   表值程序集函数 (FT)  
  
-   内联表值 SQL 函数 (IF)  
  
-   内部表 (IT)  
  
-   系统表 (S)  
  
-   表值 SQL 函数 (TF)  
  
-   用户表 (U)  
  
-   视图 (V)  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|object_id|**int**|此列所属对象的 ID。|  
|NAME|**sysname**|列的名称。 在对象中是唯一的。|  
|column_id|**int**|列的 ID。 在对象中是唯一的。<br /><br /> 列 ID 可以不按顺序排列。|  
|system_type_id|**tinyint**|系统类型的列的 ID。|  
|user_type_id|**int**|用户定义的列类型的 ID。<br /><br /> 若要返回的类型名称，将联接到[sys.types](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)目录对此列的视图。|  
|max_length|**smallint**|列的最大长度（字节）。<br /><br /> -1 = 的列数据类型为**varchar （max)**， **nvarchar （max)**， **varbinary （max)**，或者**xml**。<br /><br /> 有关**文本**列，max_length 值将是 16 或 sp_tableoption 'text in row' 设置的值。|  
|精度|**tinyint**|如果基于数值; 列的精度否则为为 0。|  
|小数位数|**tinyint**|如果基于数值，则为列的小数位数；否则为 0。|  
|collation_name|**sysname**|如果基于字符的; 的列的排序规则名称否则，为 NULL。|  
|is_nullable|**bit**|1 = 列可为空。|  
|is_ansi_padded|**bit**|1 = 如果列为字符、二进制或变量类型，则该列使用 ANSI_PADDING ON 行为。<br /><br /> 0 = 列不是字符、二进制或变量类型。|  
|is_rowguidcol|**bit**|1 = 列为声明的 ROWGUIDCOL。|  
|is_identity|**bit**|1 = 列具有标识值|  
|is_computed|**bit**|1 = 列为计算列。|  
|is_filestream|**bit**|1 = 列为 FILESTREAM 列。|  
|is_replicated|**bit**|1 = 列已复制。|  
|is_non_sql_subscribed|**bit**|1 = 列具有非 SQL Server 订阅服务器。|  
|is_merge_published|**bit**|1 = 列已合并发布。|  
|is_dts_replicated|**bit**|1 = 使用 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 复制列。|  
|is_xml_document|**bit**|1 = 内容为完整的 XML 文档。<br /><br /> 0 = 内容是文档片段或列数据类型不是**xml**。|  
|xml_collection_id|**int**|如果列的数据类型为非零**xml**和类型化 XML。 该值将为包含列的验证 XML 架构命名空间的集合的 ID。<br /><br /> 0 = 没有 XML 架构集合。|  
|default_object_id|**int**|默认对象，而不管它是一个独立的对象 ID [sys.sp_bindefault](../../relational-databases/system-stored-procedures/sp-bindefault-transact-sql.md)，还是内联列级 DEFAULT 约束。 内联列级默认对象的 parent_object_id 列是对该表本身的反引用。<br /><br /> 0 = 无默认值。|  
|rule_object_id|**int**|使用 sys.sp_bindrule 绑定到列的独立规则的 ID。<br /><br /> 0 = 无独立规则。 列级 CHECK 约束，请参阅[sys.check_constraints &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-check-constraints-transact-sql.md)。|  
|is_sparse|**bit**|1 = 列为稀疏列。 有关详细信息，请参阅 [使用稀疏列](../../relational-databases/tables/use-sparse-columns.md)。|  
|is_column_set|**bit**|1 = 列为列集。 有关详细信息，请参阅 [使用稀疏列](../../relational-databases/tables/use-sparse-columns.md)。|  
|将 generated_always_type|**tinyint**|适用范围：[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]。<br /><br /> 标识列的值生成时 （始终为 0 表示系统表中的列）：<br /><br /> 0 = NOT_APPLICABLE<br /><br /> 1 = AS_ROW_START<br /><br /> 2 = AS_ROW_END<br /><br /> 有关详细信息，请参阅[临时表&#40;关系数据库&#41;](../../relational-databases/tables/temporal-tables.md)。|  
|generated_always_type_desc|**nvarchar(60)**|适用范围：[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]。<br /><br /> 文本说明的`generated_always_type`的值 (始终 NOT_APPLICABLE 系统表中的列) <br /><br /> NOT_APPLICABLE<br /><br /> AS_ROW_START<br /><br /> AS_ROW_END|  
|encryption_type|**int**|适用范围：[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]。<br /><br /> 加密类型：<br /><br /> 1 = 确定性加密<br /><br /> 2 = 随机的加密|  
|encryption_type_desc|**nvarchar(64)**|适用范围：[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]。<br /><br /> 加密类型说明：<br /><br /> 随机化<br /><br /> DETERMINISTIC|  
|encryption_algorithm_name|**sysname**|适用范围：[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]。<br /><br /> 加密算法的名称。<br /><br /> 支持仅 AEAD_AES_256_CBC_HMAC_SHA_512。|  
|column_encryption_key_id|**int**|适用范围：[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]。<br /><br /> CEK 的 ID。|  
|column_encryption_key_database_name|**sysname**|适用范围：[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、[!INCLUDE[ssSDW_md](../../includes/sssds-md.md)]。<br /><br /> 如果不同于列的数据库列加密密钥所在的数据库的名称。 如果与列相同的数据库中存在该密钥为 NULL。|  
|is_hidden|**bit**|适用范围：[!INCLUDE[ssCurrentLong](../../includes/sscurrentlong-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]。<br /><br /> 指示是否隐藏列：<br /><br /> 0 = 常规、 非隐藏、 可见列<br /><br /> 1 = 隐藏的列|  
|is_masked|**bit**|适用范围：[!INCLUDE[ssCurrentLong](../../includes/sscurrentlong-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]。<br /><br /> 指示是否通过动态数据掩码来屏蔽列：<br /><br /> 0 = 不屏蔽的正则列<br /><br /> 1 = 列被屏蔽|  


 
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>请参阅  
 [系统视图&#40;Transact SQL&#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [对象目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [查询 SQL Server 系统目录常见问题](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [sys.all_columns &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-all-columns-transact-sql.md)   
 [sys.system_columns &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-system-columns-transact-sql.md)  
  
  
