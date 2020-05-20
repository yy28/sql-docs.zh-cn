---
title: sys. dm_xe_session_targets （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_xe_session_targets
- dm_xe_session_targets_TSQL
- dm_xe_session_targets
- sys.dm_xe_session_targets_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_xe_session_targets dynamic management view
- extended events [SQL Server], views
ms.assetid: 76fbc3e1-ad88-4a47-8bf1-471c3bee5ad8
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 163efc4d8f2a590c4469f950d56e9fa396e40b9a
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/05/2020
ms.locfileid: "82820769"
---
# <a name="sysdm_xe_session_targets-transact-sql"></a>sys.dm_xe_session_targets (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回有关会话目标的信息。  
  
  |列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|event_session_address|**varbinary(8)**|事件会话的内存地址。 与 sys.dm_xe_sessions.address 之间具有多对一关系。 不可为 null。|  
|target_name|**nvarchar(60)**|会话中目标的名称。 不可为 null。|  
|target_package_guid|**uniqueidentifier**|包含目标的包的 GUID。 不可为 null。|  
|execution_count|**bigint**|已为该会话执行目标的次数。 不可为 null。|  
|execution_duration_ms|**bigint**|目标已经执行的总时间（以毫秒为单位）。 不可为 null。|  
|target_data|**nvarchar(max)**|目标维护的数据，例如事件聚合信息。 可以为 Null。|  
  
## <a name="permissions"></a>权限  
 要求具有服务器的 VIEW SERVER STATE 权限。  
  
### <a name="relationship-cardinalities"></a>关系基数  
  
|From|功能|关系|  
|----------|--------|------------------|  
|sys.dm_xe_session_targets.event_session_address|sys.dm_xe_sessions.address|多对一|  
  
## <a name="change-history"></a>更改历史记录  
  
|更新的内容|  
|---------------------|  
|更正了 target_data 列的数据类型。|  
|更正了对 target_data 列的说明以指示该值可以为 Null。|  
|更正了“关系基数”表。|  
  
## <a name="see-also"></a>另请参阅  
 [动态管理视图和函数 (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  

