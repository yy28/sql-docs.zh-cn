---
title: sys.dm_db_rda_schema_update_status (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: language-reference
f1_keywords:
- sys.dm_db_rda_schema_update_status
- sys.dm_db_rda_schema_update_status_TSQL
- dm_db_rda_schema_update_status
- dm_db_rda_schema_update_status_TSQL
helpviewer_keywords:
- sys.dm_db_rda_schema_update_status dynamic management view
ms.assetid: 364e3caa-a7c6-4be5-a029-0b19da34de3e
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 930e717767c44f5d8151cd94c29f9b6aaa205fa4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47755795"
---
# <a name="stretch-database---sysdmdbrdaschemaupdatestatus"></a>Stretch Database-sys.dm_db_rda_schema_update_status
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  包含为当前数据库中的每个已启用延伸的表的远程数据存档每个架构更新任务行。 任务通过任务 id 标识。  
  
 **dm_db_rda_schema_update_status**的范围限定为当前数据库上下文。 请确保你想要查看架构更新状态的已启用延伸的表的数据库上下文中。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**table_id**|**int**|正在更新本地已启用延伸的表的远程数据存档架构的 ID。|  
|**database_id**|**int**|包含本地启用延伸的表的数据库的 ID。|  
|**task_id**|**bigint**|远程数据存档架构更新任务的 ID。|  
|**task_type**|**int**|远程数据存档架构更新任务的类型。|  
|**task_type_desc**|**nvarchar**|远程数据存档架构更新任务的类型的说明。|  
|**task_state**|**int**|远程数据存档架构更新任务的状态。|  
|**task_state_des**|**nvarchar**|远程数据存档架构更新任务的状态的说明。|  
|**start_time_utc**|**datetime**|UTC 时间的远程数据存档已开始的架构更新。|  
|**end_time_utc**|**datetime**|已完成的远程数据存档架构更新的 UTC 时间。|  
|**error_number**|**int**|如果远程数据存档架构更新失败，出现，则该错误的错误号否则，为 null。|  
|**error_severity**|**int**|如果远程数据存档架构更新失败，发生错误的严重级别否则，为 null。|  
|**error_state**|**int**|如果远程数据存档架构更新失败，出现，则该错误的状态否则，为 null。 Error_state 指示条件或发生错误的位置。|  
  
## <a name="see-also"></a>请参阅  
 [Stretch 数据库](../../sql-server/stretch-database/stretch-database.md)  
  
  
