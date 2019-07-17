---
title: sys.dm_db_fts_index_physical_stats (Transact SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_db_fts_index_physical_stats_TSQL
- dm_db_fts_index_physical_stats
- dm_db_fts_index_physical_stats_TSQL
- sys.dm_db_fts_index_physical_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_fts_index_physical_stats dynamic management view
ms.assetid: 997c3278-3630-47f6-ada3-190b6c16ce0e
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 4394483cd17510c998126a70c12f4d669c9282aa
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/16/2019
ms.locfileid: "68264490"
---
# <a name="sysdmdbftsindexphysicalstats-transact-sql"></a>sys.dm_db_fts_index_physical_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  为关联有全文或语义索引的每个表中的每个全文或语义索引返回一行。  
  
||||  
|-|-|-|  
|**列名**|**类型**|**说明**|  
|**object_id**|INT|包含索引的表的对象 ID。|  
|**fulltext_index_page_count**|**bigint**|提取的逻辑大小（用索引页数表示）。|  
|**keyphrase_index_page_count**|**bigint**|提取的逻辑大小（用索引页数表示）。|  
|**similarity_index_page_count**|**bigint**|提取的逻辑大小（用索引页数表示）。|  
  
## <a name="general-remarks"></a>一般备注  
 有关详细信息，请参阅[管理和监视语义搜索](../../relational-databases/search/manage-and-monitor-semantic-search.md)。  
  
## <a name="metadata"></a>元数据  
 有关语义索引状态的信息，请查询以下动态管理视图：  
  
-   [sys.dm_fts_index_population (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql.md)  
  
-   [sys.dm_fts_semantic_similarity_population (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-fts-semantic-similarity-population-transact-sql.md)  
  
## <a name="permissions"></a>权限

上[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`权限。   
上[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]高级层，需要`VIEW DATABASE STATE`数据库中的权限。 上[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]标准版和基本层，需要**服务器管理员**或**Azure Active Directory 管理员**帐户。   

## <a name="examples"></a>示例  
 下面的示例说明如何查询关联有全文或语义索引的每个表中的每个全文或语义索引的逻辑大小。  
  
```  
SELECT * FROM sys.dm_db_fts_index_physical_stats;  
GO  
```  
  
## <a name="see-also"></a>请参阅  
 [管理和监视语义搜索](../../relational-databases/search/manage-and-monitor-semantic-search.md)  
  
  
