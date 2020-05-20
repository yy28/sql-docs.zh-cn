---
title: sys. dm_db_fts_index_physical_stats （Transact-sql） |Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: da91debf86d943e24d998afda2911d000f926525
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/05/2020
ms.locfileid: "82820895"
---
# <a name="sysdm_db_fts_index_physical_stats-transact-sql"></a>sys.dm_db_fts_index_physical_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  为关联有全文或语义索引的每个表中的每个全文或语义索引返回一行。  
  
||||  
|-|-|-|  
|**列名**|**Type**|**说明**|  
|**object_id**|int|包含索引的表的对象 ID。|  
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

在上 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] ，需要 `VIEW SERVER STATE` 权限。   
在 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 高级层上，需要具有 `VIEW DATABASE STATE` 数据库中的权限。 在 [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)] 标准层和基本层上，需要**服务器管理员**或**Azure Active Directory 管理员**帐户。   

## <a name="examples"></a>示例  
 下面的示例说明如何查询关联有全文或语义索引的每个表中的每个全文或语义索引的逻辑大小。  
  
```  
SELECT * FROM sys.dm_db_fts_index_physical_stats;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [管理和监视语义搜索](../../relational-databases/search/manage-and-monitor-semantic-search.md)  
  
  
