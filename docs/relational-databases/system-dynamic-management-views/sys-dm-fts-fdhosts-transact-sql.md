---
title: sys.dm_fts_fdhosts (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_fts_fdhosts
- dm_fts_fdhosts_TSQL
- sys.dm_fts_fdhosts
- sys.dm_fts_fdhosts_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_fts_fdhosts dynamic management view
- troubleshooting [SQL Server], full-text search
ms.assetid: d42a6334-4362-4361-83da-f8324fe55ec7
caps.latest.revision: 13
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 9671d5a411b12b2cdc7225f215a43c27d19de10c
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2018
---
# <a name="sysdmftsfdhosts-transact-sql"></a>sys.dm_fts_fdhosts (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  返回有关服务器实例中筛选器后台程序宿主的当前活动的信息。  
  
 
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**fdhost_id**|**int**|筛选器后台程序宿主的 ID。|  
|**fdhost_name**|**nvarchar(120)**|筛选器后台程序宿主的名称。|  
|**fdhost_process_id**|**int**|筛选器后台程序宿主的 Windows 进程 ID。|  
|**fdhost_type**|**nvarchar(120)**|筛选器后台程序宿主正在处理的文档的类型，为如下类型之一：<br /><br /> 单线程<br /><br /> 多线程<br /><br /> 大文档|  
|**max_thread**|**int**|筛选器后台程序宿主中线程的最大数。|  
|**batch_count**|**int**|筛选器后台程序宿主中要处理的批次的数量。|  
  
## <a name="permissions"></a>权限  

上[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`权限。   
上[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]，需要`VIEW DATABASE STATE`数据库中的权限。   

## <a name="examples"></a>示例  
 下面的示例返回筛选器后台程序宿主的名称以及其中的线程的最大数目。 它还监视筛选器后台程序当前正在处理的批次数量。 此信息可用于诊断性能。  
  
```  
SELECT fdhost_name, batch_count, max_thread FROM sys.dm_fts_fdhosts;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [全文搜索和语义搜索动态管理视图和函数&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)   
 [全文搜索](../../relational-databases/search/full-text-search.md)  
  
  
