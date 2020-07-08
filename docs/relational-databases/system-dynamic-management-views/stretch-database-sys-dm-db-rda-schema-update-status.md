---
title: sys. dm_db_rda_schema_update_status （Transact-sql） |Microsoft Docs
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
author: pmasl
ms.author: pelopes
ms.openlocfilehash: b74f408bdb2be61076d5034478dc6743259fed6a
ms.sourcegitcommit: 703968b86a111111a82ef66bb7467dbf68126051
ms.contentlocale: zh-CN
ms.lasthandoff: 07/07/2020
ms.locfileid: "86053643"
---
# <a name="stretch-database---sysdm_db_rda_schema_update_status"></a>Stretch Database-sys. dm_db_rda_schema_update_status
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  当前数据库中每个已启用延伸的表的远程数据存档的每个架构更新任务在表中占一行。 任务由其任务 id 标识。  
  
 **dm_db_rda_schema_update_status**的作用域限定为当前数据库上下文。 请确保在已启用延伸的表的数据库上下文中，要查看其架构更新状态。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|table_id****|**int**|正在更新其远程数据存档架构的本地 Stretch 已启用表的 ID。|  
|**database_id**|**int**|包含启用了延伸的本地表的数据库的 ID。|  
|**task_id**|**bigint**|远程数据存档架构更新任务的 ID。|  
|**task_type**|**int**|远程数据存档架构更新任务的类型。|  
|**task_type_desc**|**nvarchar**|远程数据存档架构更新任务的类型说明。|  
|**task_state**|**int**|远程数据存档架构更新任务的状态。|  
|**task_state_des**|**nvarchar**|远程数据存档架构更新任务的状态说明。|  
|**start_time_utc**|**datetime**|远程数据存档架构更新开始的 UTC 时间。|  
|**end_time_utc**|**datetime**|远程数据存档架构更新完成时的 UTC 时间。|  
|error_number |**int**|如果远程数据存档架构更新失败，则表明出现了错误的错误号;否则为 null。|  
|**error_severity**|**int**|如果远程数据存档架构更新失败，则表明出现了错误的严重性;否则为 null。|  
|**error_state**|**int**|如果远程数据存档架构更新失败，则表明出现了错误的状态;否则为 null。 Error_state 指示发生错误的条件或位置。|  
  
## <a name="see-also"></a>另请参阅  
 [Stretch 数据库](../../sql-server/stretch-database/stretch-database.md)  
  
  
