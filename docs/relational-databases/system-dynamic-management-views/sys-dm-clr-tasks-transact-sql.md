---
title: sys.dm_clr_tasks (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.dm_clr_tasks
- sys.dm_clr_tasks_TSQL
- dm_clr_tasks
- dm_clr_tasks_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_clr_tasks dynamic management view
ms.assetid: 462b9061-09fa-4858-9707-03d6cc19c769
caps.latest.revision: 21
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: fa0d98e2d3c5a0d3b0754646ef6c3f2a19036306
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmclrtasks-transact-sql"></a>sys.dm_clr_tasks (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  对于当前正在运行的所有公共语言运行时 (CLR) 任务，相应地返回一行。 如果 [!INCLUDE[tsql](../../includes/tsql-md.md)] 批中包含对 CLR 例程的引用，那么这个批将创建单独的任务，以执行该批中的所有托管代码。 如果批中的多个语句需要执行托管代码，那么这些批将使用相同的 CLR 任务。 CLR 任务负责维护执行托管代码所涉及的对象和状态，以及在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例和公共语言运行时之间的转换。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**task_address**|**varbinary(8)**|CLR 任务的地址。|  
|**sos_task_address**|**varbinary(8)**|基础 [!INCLUDE[tsql](../../includes/tsql-md.md)] 批任务的地址。|  
|**appdomain_address**|**varbinary(8)**|此任务在其中运行的应用程序域的地址。|  
|**状态**|**nvarchar(128)**|任务的当前状态。|  
|**abort_state**|**nvarchar(128)**|中止任务时当前所处的状态（如果取消任务）。中止任务时涉及多个状态。|  
|**类型**|**nvarchar(128)**|任务类型。|  
|**affinity_count**|**int**|任务的关联。|  
|**forced_yield_count**|**int**|强制产生任务的次数。|  
  
## <a name="permissions"></a>权限  

上[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`权限。   
上[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]，需要`VIEW DATABASE STATE`数据库中的权限。   
  
## <a name="see-also"></a>另请参阅  
 [动态管理视图和函数 (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [公共语言运行时相关的动态管理视图&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/common-language-runtime-related-dynamic-management-views-transact-sql.md)  
  
  

