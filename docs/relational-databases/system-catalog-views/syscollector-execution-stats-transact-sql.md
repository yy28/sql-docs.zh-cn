---
title: syscollector_execution_stats (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- syscollector_execution_stats
- syscollector_execution_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- syscollector_execution_stats view
- data collector view
ms.assetid: 23e35ac5-fbbf-4922-970c-f4fac44c1263
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b89823af1295b329046395a8f3c345401ca61805
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62760183"
---
# <a name="syscollectorexecutionstats-transact-sql"></a>syscollector_execution_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  提供有关收集组或包的任务执行的信息。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**log_id**|**bigint**|标识收集组的每次执行。 用于将此视图与其他详细日志联接起来。 不可为 null。|  
|**task_name**|**nvarchar(128)**|该信息对应的收集组或包任务的名称。 不可为 null。|  
|**execution_row_count_in**|**int**|在数据流起始位置处理的行数。 可以为 Null。|  
|**execution_row_count_out**|**int**|在数据流结尾位置处理的行数。 可以为 Null。|  
|**execution_row_count_errors**|**int**|在数据流过程中失败的行数。 可以为 Null。|  
|**execution_time_ms**|**int**|完成任务所需的时间（单位为毫秒）。 可以为 Null。|  
|**log_time**|**datetime**|记录此信息的时间。 不可为 null。|  
  
## <a name="permissions"></a>权限  
 要求具有 SELECT 权限的**dc_operator**。  
  
## <a name="see-also"></a>请参阅  
 [数据收集器存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [数据收集器视图 (Transact-SQL)](../../relational-databases/system-catalog-views/data-collector-views-transact-sql.md)   
 [“数据收集”](../../relational-databases/data-collection/data-collection.md)  
  
  
