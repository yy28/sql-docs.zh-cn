---
title: "sys.dm_xe_session_targets (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: dmv's
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cdc4dd3ffa39c7d245b25a895f189aaaaa6cd332
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2018
---
# <a name="sysdmxesessiontargets-transact-sql"></a>sys.dm_xe_session_targets (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回有关会话目标的信息。  
  
  |列名|数据类型|Description|  
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
  
|从|若要|关系|  
|----------|--------|------------------|  
|sys.dm_xe_session_targets.event_session_address|sys.dm_xe_sessions.address|多对一|  
  
## <a name="change-history"></a>更改历史记录  
  
|更新内容|  
|---------------------|  
|更正了 target_data 列的数据类型。|  
|更正了对 target_data 列的说明以指示该值可以为 Null。|  
|更正了“关系基数”表。|  
  
## <a name="see-also"></a>另请参阅  
 [动态管理视图和函数 (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)  
  
  

