---
title: MSrepl_errors (Transact SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- MSrepl_errors
- MSrepl_errors_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSrepl_errors system table
ms.assetid: c6e023c1-2c32-4269-8d76-e442ea309e4b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8aeca48f7958c797a6919951b2c3a32b174a28d1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47806665"
---
# <a name="msreplerrors-transact-sql"></a>MSrepl_errors (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  **MSrepl_errors**表包含具有扩展分发代理和合并代理失败信息的行。 此表存储在分发数据库中。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|错误 ID。|  
|**time**|**datetime**|出现错误的时间。|  
|**error_type_id**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**source_type_id**|**int**|错误源类型 id。|  
|**source_name**|**nvarchar(100)**|错误源名称。|  
|**error_code**|**sysname**|错误代码。|  
|**error_text**|**ntext**|错误消息。|  
|**xact_seqno**|**varbinary(16)**|执行失败的批次的起始事务日志序列号。 仅由分发代理使用，是失败的执行批处理中第一个事务的日志序列号。|  
|**command_id**|**int**|执行失败的批次的命令 ID。 仅由分发代理使用，是执行失败的批次中的第一个命令的 ID。|  
|**session_id**|**int**|出现错误的代理会话 ID。|  
  
## <a name="see-also"></a>请参阅  
 [复制表&#40;Transact SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [复制视图 (Transact-SQL)](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
