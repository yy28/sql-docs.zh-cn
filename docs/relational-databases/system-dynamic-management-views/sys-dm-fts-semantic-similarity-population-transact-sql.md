---
title: sys.dm_fts_semantic_similarity_population (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_fts_semantic_similarity_population_TSQL
- sys.dm_fts_semantic_similarity_population
- dm_fts_semantic_similarity_population
- sys.dm_fts_semantic_similarity_population_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_fts_semantic_similarity_population dynamic management view
ms.assetid: 33666f28-c370-47e2-a932-190316ed5f69
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b98333366f5c929d6324d103e5638b7e69ff1d56
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmftssemanticsimilaritypopulation-transact-sql"></a>sys.dm_fts_semantic_similarity_population (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  为关联有语义索引的每个表中的每个相似性索引返回一行关于文档相似性索引填充状态的信息。  
  
 填充步骤紧随提取步骤。 相似性提取步骤的状态信息，请参阅[sys.dm_fts_index_population &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql.md)。  
    
||||  
|-|-|-|  
|**列名**|**类型**|**Description**|  
|**database_id**|**int**|包含正在填充的全文索引的数据库 ID。|  
|**catalog_id**|**int**|包含此全文索引的全文目录的 ID。|  
|**table_id**|**int**|其全文索引正在被填充的表的 ID。|  
|**document_count**|**int**|填充中的文档总数|  
|**document_processed_count**|**int**|自此填充周期开始以来处理的文档数|  
|**completion_type**|**int**|有关填充完成的状态。|  
|**completion_type_description**|**nvarchar(120)**|完成类型的说明。|  
|**worker_count**|**int**|与相似性提取关联的工作线程数|  
|**status**|**int**|此填充的状态。 说明：某些状态是暂时的。 可以是以下类型之一：<br /><br /> 3 = 正在启动<br /><br /> 5 = 正常处理<br /><br /> 7 = 已停止处理<br /><br /> 11 = 已中止填充|  
|**status_description**|**nvarchar(120)**|对填充状态的说明。|  
|**start_time**|**datetime**|填充开始的时间。|  
|**incremental_timestamp**|**timestamp**|表示完全填充的开始时间戳。 对于所有其他填充类型，该值是表示填充进度的上次提交的检查点。|  
  
## <a name="general-remarks"></a>一般备注  
 有关详细信息，请参阅[管理和监视语义搜索](../../relational-databases/search/manage-and-monitor-semantic-search.md)。  
  
## <a name="metadata"></a>元数据  
 语义索引编制的状态的详细信息，请查询[sys.dm_fts_index_population &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql.md)。  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>权限  
 要求具有服务器的 VIEW SERVER STATE 权限。  
  
## <a name="examples"></a>示例  
 下面的示例说明如何为关联有语义索引的所有表查询文档相似性索引填充的状态：  
  
```  
SELECT * FROM sys.dm_fts_semantic_similarity_population;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [管理和监视语义搜索](../../relational-databases/search/manage-and-monitor-semantic-search.md)  
  
  
