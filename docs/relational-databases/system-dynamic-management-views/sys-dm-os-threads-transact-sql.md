---
title: sys.dm_os_threads (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_os_threads_TSQL
- sys.dm_os_threads
- dm_os_threads
- sys.dm_os_threads_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_threads dynamic management view
ms.assetid: a5052701-edbf-4209-a7cb-afc9e65c41c1
caps.latest.revision: 35
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: ef4180180b6a5ebab95ccc3cc1ebe879a495fcf7
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="sysdmosthreads-transact-sql"></a>sys.dm_os_threads (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  返回在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 进程中运行的所有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 操作系统线程的列表。  
  
> [!NOTE]  
>  若要从我们称之为[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，使用名称**sys.dm_pdw_nodes_os_threads**。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|thread_address|**varbinary(8)**|线程的内存地址（主键）。|  
|started_by_sqlservr|**bit**|指示线程发起方。<br /><br /> 1 = [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 启动了线程。<br /><br /> 0 = 其他组件启动了线程，例如，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的扩展存储过程。|  
|os_thread_id|**int**|操作系统分配的线程 ID。|  
|status|**int**|内部状态标志。|  
|instruction_address|**varbinary(8)**|当前执行的指令的地址。|  
|creation_time|**datetime**|该线程的创建时间。|  
|kernel_time|**bigint**|该线程占用的内核时间。|  
|usermode_time|**bigint**|该线程占用的用户时间。|  
|stack_base_address|**varbinary(8)**|该线程的最高堆栈地址在内存中的位置。|  
|stack_end_address|**varbinary(8)**|该线程的最低堆栈地址在内存中的位置。|  
|stack_bytes_committed|**int**|在堆栈中提交的字节数。|  
|stack_bytes_used|**int**|线程目前使用的字节数。|  
|affinity|**bigint**|该线程运行时使用的 CPU 掩码。 这取决于配置的值**ALTER SERVER CONFIGURATION SET PROCESS AFFINITY**语句。 在软关联的情况下，可能与计划程序不同。|  
|Priority|**int**|该线程的优先级值。|  
|区域设置|**int**|线程的缓存区域设置 LCID。|  
|标记|**varbinary(8)**|线程的缓存模拟令牌句柄。|  
|is_impersonating|**int**|指示该线程是否使用 Win32 模拟。<br /><br /> 1 = 该线程使用与进程默认的安全凭据不同的安全凭据。 这表明线程正在模拟创建该进程的实体以外的其他实体。|  
|is_waiting_on_loader_lock|**int**|指示线程是否正在等待加载程序锁的操作系统状态。|  
|fiber_data|**varbinary(8)**|线程当前运行的 Win32 纤程。 只有在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置了轻型池时，这才适用。|  
|thread_handle|**varbinary(8)**|仅限内部使用。|  
|event_handle|**varbinary(8)**|仅限内部使用。|  
|scheduler_address|**varbinary(8)**|与该线程关联的计划程序的内存地址。 有关详细信息，请参阅[sys.dm_os_schedulers &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-schedulers-transact-sql.md)。|  
|worker_address|**varbinary(8)**|绑定到该线程的工作线程的内存地址。 有关详细信息，请参阅[sys.dm_os_workers &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-workers-transact-sql.md)。|  
|fiber_context_address|**varbinary(8)**|内部纤程上下文地址。 只有在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置了轻型池时，这才适用。|  
|self_address|**varbinary(8)**|内部一致性指针。|  
|processor_group|**int**|**适用范围**： [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 处理器组 ID。|  
|pdw_node_id|**int**|**适用于**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]， [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 此分布的节点标识符。|  
  
## <a name="permissions"></a>权限

上[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`权限。   
上[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]，需要`VIEW DATABASE STATE`数据库中的权限。   

## <a name="examples"></a>示例  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 在启动时将启动线程，然后将工作与这些线程进行关联。 但是，外部组件（如扩展存储过程）可以在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 进程中启动线程。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 无法控制这些线程。 sys.dm_os_threads 可以提供有关使用中的资源的恶意线程信息[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]过程。  
  
 下面的查询用于查找正在运行非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 启动的线程的工作以及执行的时间。  
  
> [!NOTE]  
>  为清晰起见，下面的查询在 `*` 语句中使用星号 (`SELECT`)。 应避免使用星号 (*)，尤其是对目录视图、动态管理视图和系统表值函数。 将来的升级和版本的[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]可能添加列并将列的顺序更改为这些视图和函数。 这些更改可能会中断需要特定顺序和列数的应用程序。  
  
```  
SELECT *  
  FROM sys.dm_os_threads  
  WHERE started_by_sqlservr = 0;  
```  
  
## <a name="see-also"></a>另请参阅  
  [sys.dm_os_workers &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-workers-transact-sql.md)   
 [SQL Server 操作系统相关的动态管理视图&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


