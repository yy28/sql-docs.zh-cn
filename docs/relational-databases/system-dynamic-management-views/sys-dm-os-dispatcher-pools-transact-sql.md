---
title: sys.dm_os_dispatcher_pools (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 08/18/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_os_dispatcher_pools_TSQL
- dm_os_dispatcher_pools
- sys.dm_os_dispatcher_pools
- sys.dm_os_dispatcher_pools_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- extended events [SQL Server], views
- sys.dm_os_dispatcher_pools DMV
ms.assetid: b9edbc83-c6bc-4753-9bb5-a454cfe7d6bf
caps.latest.revision: 25
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7ceaad5d07730720f9aef590762f062cf1832a07
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="sysdmosdispatcherpools-transact-sql"></a>sys.dm_os_dispatcher_pools (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回有关会话调度程序池的信息。 调度程序池是由系统组件用来执行后台处理的线程池。  
  
> [!NOTE]  
>  若要从我们称之为[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，使用名称**sys.dm_pdw_nodes_os_dispatcher_pools**。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|dispatcher_pool_address|**varbinary(8)**|调度程序池的地址。 dispatcher_pool_address 是唯一的。 不可为 null。|  
|type|**nvarchar(256)**|调度程序池的类型。 不可为 null。 有两种类型的调度程序池：<br /><br /> DISP_POOL_XE_ENGINE<br /><br /> DISP_POOL_XE_SESSION<br /><br /> 查询的完整列表 DMV|  
|name|**nvarchar(256)**|调度程序池的名称。 不可为 null。|  
|dispatcher_count|**int**|处于活动状态的调度程序线程数。 不可为 null。|  
|dispatcher_ideal_count|**int**|调度程序池通过增大可使用的调度程序线程数。 不可为 null。|  
|dispatcher_timeout_ms|**int**|调度程序将在退出之前等待新工作的时间（以毫秒为单位）。 不可为 null。|  
|dispatcher_waiting_count|**int**|空闲的调度程序线程数。 不可为 null。|  
|queue_length|**int**|等待由调度程序池处理的工作项数。 不可为 null。|  
|pdw_node_id|**int**|**适用于**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]， [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 此分布的节点标识符。|  
  
## <a name="permissions"></a>权限

上[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`权限。   
上[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]，需要`VIEW DATABASE STATE`数据库中的权限。   

## <a name="see-also"></a>另请参阅  
  
  


