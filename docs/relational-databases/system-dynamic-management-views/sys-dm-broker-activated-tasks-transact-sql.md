---
title: sys.dm_broker_activated_tasks (TRANSACT-SQL) |Microsoft 文档
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
- sys.dm_broker_activated_tasks
- sys.dm_broker_activated_tasks_TSQL
- dm_broker_activated_tasks
- dm_broker_activated_tasks_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_broker_activated_tasks dynamic management view
ms.assetid: 17e6f87f-8f56-489d-9aed-216afc8ef310
caps.latest.revision: 22
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5b678ec74e729a66dc2546cce855d8d2145c9621
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="sysdmbrokeractivatedtasks-transact-sql"></a>sys.dm_broker_activated_tasks (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  为 Service Broker 激活的每个存储过程返回一行。  
 

|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**spid**|**int**|已激活存储过程的会话的 ID。 可以为 NULL。|  
|**database_id**|**int**|定义队列所用数据库的 ID。 可以为 NULL。|  
|**queue_id**|**int**|为其激活存储过程的队列的对象 ID。 可以为 NULL。|  
|**procedure_name**|**nvarchar(650)**|已激活的存储过程的名称。 可以为 NULL。|  
|**execute_as**|**int**|运行存储过程的用户的 ID。 可以为 NULL。|  
  
## <a name="permissions"></a>权限  
 要求具有服务器的 VIEW SERVER STATE 权限。  
  
## <a name="physical-joins"></a>物理联接  
 ![联接的 sys.dm_broker_activated_tasks](../../relational-databases/system-dynamic-management-views/media/join-dm-broker-activated-tasks-1.gif "为 sys.dm_broker_activated_tasks 联接")  
  
## <a name="relationship-cardinalities"></a>关系基数  
  
|从|若要|关系|  
|----------|--------|------------------|  
|dm_broker_activated_tasks.spid|dm_exec_sessions.session_id|一对一|  
  
## <a name="see-also"></a>另请参阅  
 [动态管理视图和函数 (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Service Broker 相关的动态管理视图 & #40;Transact SQL & #41;](../../relational-databases/system-dynamic-management-views/service-broker-related-dynamic-management-views-transact-sql.md)  
  
  

