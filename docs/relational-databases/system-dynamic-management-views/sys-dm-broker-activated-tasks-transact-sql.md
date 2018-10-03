---
title: sys.dm_broker_activated_tasks (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bf3910b432d803ce74e0bf24d83a974072028f33
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47704866"
---
# <a name="sysdmbrokeractivatedtasks-transact-sql"></a>sys.dm_broker_activated_tasks (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  为 Service Broker 激活的每个存储过程返回一行。  
 

|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**spid**|**int**|已激活存储过程的会话的 ID。 可以为 NULL。|  
|**database_id**|**smallint**|定义队列所用数据库的 ID。 可以为 NULL。|  
|**queue_id**|**int**|为其激活存储过程的队列的对象 ID。 可以为 NULL。|  
|**procedure_name**|**nvarchar(650)**|已激活的存储过程的名称。 可以为 NULL。|  
|**execute_as**|**int**|运行存储过程的用户的 ID。 可以为 NULL。|  
  
## <a name="permissions"></a>Permissions  
 要求具有服务器的 VIEW SERVER STATE 权限。  
  
## <a name="physical-joins"></a>物理联接  
 ![Sys.dm_broker_activated_tasks 的联接](../../relational-databases/system-dynamic-management-views/media/join-dm-broker-activated-tasks-1.gif "sys.dm_broker_activated_tasks 的联接")  
  
## <a name="relationship-cardinalities"></a>关系基数  
  
|从|若要|关系|  
|----------|--------|------------------|  
|dm_broker_activated_tasks.spid|dm_exec_sessions.session_id|一对一|  
  
## <a name="see-also"></a>请参阅  
 [动态管理视图和函数 (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [与 Service Broker 有关的动态管理视图 (Transact-SQL)](../../relational-databases/system-dynamic-management-views/service-broker-related-dynamic-management-views-transact-sql.md)  
  
  

