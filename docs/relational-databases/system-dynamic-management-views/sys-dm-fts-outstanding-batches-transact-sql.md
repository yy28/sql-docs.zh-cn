---
title: sys.dm_fts_outstanding_batches (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_fts_outstanding_batches
- dm_fts_outstanding_batches_TSQL
- sys.dm_fts_outstanding_batches_TSQL
- sys.dm_fts_outstanding_batches
dev_langs:
- TSQL
helpviewer_keywords:
- troubleshooting [SQL Server], full-text search
- sys.dm_fts_outstanding_batches dynamic management view
ms.assetid: c4d697ed-c906-4c28-b137-036a25e13c84
caps.latest.revision: 13
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: fc924c085044b92deadca30b13f693b041fa39d7
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sysdmftsoutstandingbatches-transact-sql"></a>sys.dm_fts_outstanding_batches (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  返回有关每个全文索引批次的信息。  
  
  |列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|database_id|**int**|数据库 ID|  
|catalog_id|**int**|全文目录的 ID|  
|table_id|**int**|包含此全文索引的表 ID 的 ID|  
|batch_id|**int**|批次 ID|  
|memory_address|**varbinary(8)**|批次对象内存地址|  
|crawl_memory_address|**varbinary(8)**|爬网对象内存地址（父对象）|  
|memregion_memory_address|**varbinary(8)**|筛选器后台程序宿主 (fdhost.exe) 的出站共享内存的内存区域内存地址|  
|hr_batch|**int**|批次的最新错误代码|  
|is_retry_batch|**bit**|指示是否为重试批次：<br /><br /> 0 = 否<br /><br /> 1 = 是|  
|retry_hints|**int**|批次所需重试的类型：<br /><br /> 0 = 不重试<br /><br /> 1 = 多线程重试<br /><br /> 2 = 单线程重试<br /><br /> 3 = 单线程和多线程重试<br /><br /> 5 = 多线程最终重试<br /><br /> 6 = 单线程最终重试<br /><br /> 7 = 单线程和多线程最终重试|  
|retry_hints_description|**nvarchar(120)**|所需重试类型的说明：<br /><br /> NO RETRY<br /><br /> MULTI THREAD RETRY<br /><br /> SINGLE THREAD RETRY<br /><br /> SINGLE AND MULTI THREAD RETRY<br /><br /> MULTI THREAD FINAL RETRY<br /><br /> SINGLE THREAD FINAL RETRY<br /><br /> SINGLE AND MULTI THREAD FINAL RETRY|  
|doc_failed|**bigint**|批次中失败的文档的数目|  
|batch_timestamp|**timestamp**|创建批次时获取的时间戳值|  
  
## <a name="permissions"></a>权限  

上[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`权限。   
上[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]，需要`VIEW DATABASE STATE`数据库中的权限。   
  
## <a name="examples"></a>示例  
 下面的示例确定服务器实例中每个表当前正在处理的批次的数目。  
  
```  
SELECT database_id, table_id, COUNT(*) AS batch_count FROM sys.dm_fts_outstanding_batches GROUP BY database_id, table_id ;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [全文搜索和语义搜索动态管理视图和函数&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)   
 [全文搜索](../../relational-databases/search/full-text-search.md)  
  
  
