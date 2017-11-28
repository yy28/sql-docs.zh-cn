---
title: "MSrepl_errors (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- MSrepl_errors
- MSrepl_errors_TSQL
dev_langs: TSQL
helpviewer_keywords: MSrepl_errors system table
ms.assetid: c6e023c1-2c32-4269-8d76-e442ea309e4b
caps.latest.revision: "16"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 66c276d57f2df480d1d3977304911c2826068cce
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="msreplerrors-transact-sql"></a>MSrepl_errors (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSrepl_errors**表包含与扩展分发代理和合并代理失败信息的行。 此表存储在分发数据库中。  
  
|列名|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**id**|**int**|错误 ID。|  
|**time**|**datetime**|出现错误的时间。|  
|**error_type_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**source_type_id**|**int**|错误源键入 id。|  
|**source_name**|**nvarchar(100)**|错误源名称。|  
|**error_code**|**sysname**|错误代码。|  
|**error_text**|**ntext**|错误消息。|  
|**xact_seqno**|**varbinary(16)**|执行失败的批次的起始事务日志序列号。 仅由分发代理使用，是失败的执行批处理中第一个事务的日志序列号。|  
|**command_id**|**int**|执行失败的批次的命令 ID。 仅由分发代理使用，是执行失败的批次中的第一个命令的 ID。|  
|**session_id**|**int**|出现错误的代理会话 ID。|  
  
## <a name="see-also"></a>另请参阅  
 [复制表 &#40;Transact SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
