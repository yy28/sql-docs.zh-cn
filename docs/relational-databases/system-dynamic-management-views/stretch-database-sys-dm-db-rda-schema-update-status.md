---
title: sys.dm_db_rda_schema_update_status (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-stretch
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_db_rda_schema_update_status
- sys.dm_db_rda_schema_update_status_TSQL
- dm_db_rda_schema_update_status
- dm_db_rda_schema_update_status_TSQL
helpviewer_keywords:
- sys.dm_db_rda_schema_update_status dynamic management view
ms.assetid: 364e3caa-a7c6-4be5-a029-0b19da34de3e
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: b694361a46673208e52134e9c5becf2e491c9584
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="stretch-database---sysdmdbrdaschemaupdatestatus"></a>Stretch Database-sys.dm_db_rda_schema_update_status
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  包含为当前数据库中每个已启用延伸的表的远程数据存档每个架构更新任务的一行。 任务由及其任务 id 标识。  
  
 **dm_db_rda_schema_update_status**范围限定为当前数据库上下文。 请确保你想要查看架构更新状态的已启用延伸的表的数据库上下文中。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**table_id**|**int**|正在更新其远程数据存档架构本地已启用延伸的表的 ID。|  
|**database_id**|**int**|包含本地已启用延伸的表的数据库的 ID。|  
|**task_id**|**bigint**|远程数据存档架构更新任务的 ID。|  
|**task_type**|**int**|远程数据存档架构更新任务的类型。|  
|**task_type_desc**|**nvarchar**|远程数据存档架构更新任务的类型的说明。|  
|**task_state**|**int**|远程数据存档架构更新任务的状态。|  
|**task_state_des**|**nvarchar**|远程数据存档架构更新任务的状态说明。|  
|**start_time_utc**|**datetime**|从该处的远程数据存档架构更新已开始的 UTC 时间。|  
|**end_time_utc**|**datetime**|从该处的远程数据存档架构更新的 UTC 时间完成。|  
|**error_number**|**int**|如果远程数据存档架构更新失败，发生的错误; 错误号否则，为 null。|  
|**error_severity**|**int**|如果远程数据存档架构更新失败，出现; 错误的严重级别否则，为 null。|  
|**error_state**|**int**|如果远程数据存档架构更新失败，发生的错误; 的状态否则，为 null。 Error_state 指示的条件或发生错误的位置。|  
  
## <a name="see-also"></a>另请参阅  
 [Stretch 数据库](../../sql-server/stretch-database/stretch-database.md)  
  
  
