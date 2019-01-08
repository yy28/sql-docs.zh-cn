---
title: sys.fulltext_index_columns (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.fulltext_index_columns
- fulltext_index_columns
- sys.fulltext_index_columns_TSQL
- fulltext_index_columns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- full-text indexes [SQL Server], columns
- sys.fulltext_index_columns catalog view
- full-text indexes [SQL Server], properties
ms.assetid: c34b8625-e53c-4281-ace6-d46230d5cb84
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e7f95e82acaff4fdb2e1186817b9e12be14904c9
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52543683"
---
# <a name="sysfulltextindexcolumns-transact-sql"></a>sys.fulltext_index_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  对构成全文索引的每列都包含一行。    
 
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|此对象所属对象的 ID。|  
|**column_id**|**int**|构成全文索引的列的 ID。|  
|**type_column_id**|**int**|将用户提供文档文件扩展名-".doc"、".xls"和等的文档存储给定行中的类型列的 ID。 类型列仅针对全文索引期间需要筛选其数据的列指定。 如果不适用，则为 NULL。 有关详细信息，请参阅 [配置和管理搜索筛选器](../../relational-databases/search/configure-and-manage-filters-for-search.md)。|  
|**language_id**|**int**|其断字符用于对该全文列创建索引的语言 LCID。<br /><br /> 0 = 非特定语言。<br /><br /> 有关详细信息，请参阅[sys.fulltext_languages &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md)。|  
|**statistical_semantics**|**int**|1 = 此列在全文索引之外还启用了统计语义索引。|  
  
## <a name="permissions"></a>权限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)]  
  
## <a name="see-also"></a>请参阅  
 [对象目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
