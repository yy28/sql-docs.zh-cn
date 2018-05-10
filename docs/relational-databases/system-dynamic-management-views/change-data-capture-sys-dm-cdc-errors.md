---
title: sys.dm_cdc_errors (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_cdc_errors_TSQL
- dm_cdc_errors
- sys.dm_cdc_errors
- sys.dm_cdc_errors_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_cdc_errors dynamic management view
- change data capture [SQL Server], error reporting
ms.assetid: 898f2d76-9e63-45ef-94da-8034e86004ab
caps.latest.revision: 14
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 2b12ebd0edae5efc061ce49ed7d2986f6710c775
ms.sourcegitcommit: d2573a8dec2d4102ce8882ee232cdba080d39628
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/07/2018
---
# <a name="change-data-capture---sysdmcdcerrors"></a>变更数据捕获的 sys.dm_cdc_errors
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  为变更数据捕获日志扫描会话中遇到的每个错误返回一行。  
 
 
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|会话的 ID。<br /><br /> 0 = 在日志扫描会话中未发生错误。|  
|**phase_number**|**int**|表示发生错误时会话所在的阶段的数字。 有关每个阶段的说明，请参阅[sys.dm_cdc_log_scan_sessions &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/change-data-capture-sys-dm-cdc-log-scan-sessions.md)。|  
|**entry_time**|**datetime**|记录错误的日期和时间。 此值对应于 SQL 错误日志中的时间戳。|  
|**error_number**|**int**|错误消息的 ID。|  
|**error_severity**|**int**|消息的严重级别，在 1 到 25 之间。|  
|**error_state**|**int**|错误的状态号。|  
|**error_message**|**nvarchar(1024)**|错误的消息正文。|  
|**start_lsn**|**nvarchar(23)**|发生错误时正在处理的行的起始 LSN 值。<br /><br /> 0 = 在日志扫描会话中未发生错误。|  
|**begin_lsn**|**nvarchar(23)**|发生错误时正在处理的事务的起始 LSN 值。<br /><br /> 0 = 在日志扫描会话中未发生错误。|  
|**sequence_value**|**nvarchar(23)**|发生错误时正在处理的行的 LSN 值。<br /><br /> 0 = 在日志扫描会话中未发生错误。|  
  
## <a name="remarks"></a>注释  
 **sys.dm_cdc_errors**包含前几个 32 会话信息时出错。  
  
## <a name="permissions"></a>权限  
 要求对查询的 VIEW DATABASE STATE 权限**sys.dm_cdc_errors**动态管理视图。 有关动态管理视图权限的详细信息，请参阅[动态管理视图和函数&#40;TRANSACT-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)。  
  
## <a name="see-also"></a>另请参阅  
 [sys.dm_cdc_log_scan_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/change-data-capture-sys-dm-cdc-log-scan-sessions.md)   
 [sys.dm_repl_traninfo &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-repl-traninfo-transact-sql.md)  
  
  

