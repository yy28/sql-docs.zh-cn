---
title: sys. dm_os_memory_brokers （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 08/18/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_memory_brokers
- dm_os_memory_brokers_TSQL
- sys.dm_os_memory_brokers_TSQL
- dm_os_memory_brokers
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_memory_brokers dynamic management view
ms.assetid: 48dd6ad9-0d36-4370-8a12-4921d0df4b86
author: stevestein
ms.author: sstein
ms.openlocfilehash: a8e131e2550ffa5078df5e284898ffe936128b7e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "68265866"
---
# <a name="sysdm_os_memory_brokers-transact-sql"></a>sys.dm_os_memory_brokers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的内部分配使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内存管理器。 跟踪进程内存计数器与**sys. dm_os_process_memory**和内部计数器之间的差异可以指示内存空间中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的外部组件的内存使用情况。  
  
 内存中介器基于当前使用量和预测的使用量来公平地在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 内的各种组件之间分布内存分配。 内存中介器不执行分配。 它们只跟踪内存分配以计算分布情况。  
  
 下表提供了有关内存中介器的信息。  
  
> [!NOTE]  
>  若要从[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]或[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]调用此，请使用名称**dm_pdw_nodes_os_memory_brokers**。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**pool_id**|**int**|在资源池与资源调控器池相关联的情况下的资源池 ID。|  
|**memory_broker_type**|**nvarchar(60)**|内存中介器的类型。 当前在中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]有三种类型的内存代理，其说明如下所示。<br /><br /> **MEMORYBROKER_FOR_CACHE** ：分配给缓存的对象使用的内存（非缓冲池缓存）。<br /><br /> **MEMORYBROKER_FOR_STEAL** ：从缓冲池盗用的内存。 这种内存在当前所有者释放它之前，不能供其他组件重新使用。<br /><br /> **MEMORYBROKER_FOR_RESERVE** ：保留供当前正在执行的请求使用的内存。|  
|**allocations_kb**|**bigint**|已分配给这种类型的中介器的内存量（以 KB 为单位）。|  
|**allocations_kb_per_sec**|**bigint**|每秒钟的内存分配速率（以 KB 为单位）。 对于内存释放，该值可以为负值。|  
|**predicted_allocations_kb**|**bigint**|由中介器预测的已分配的内存量。 这基于内存使用模式。|  
|**target_allocations_kb**|**bigint**|基于当前设置和内存使用模式而建议分配的内存量（以 KB 为单位）。 该中介器应增长或缩减到此数目。|  
|**future_allocations_kb**|**bigint**|将在随后几秒内完成的预计分配量（以 KB 为单位）。|  
|**overall_limit_kb**|**bigint**|代理可分配的最大内存量（kb）。|  
|**last_notification**|**nvarchar(60)**|基于当前设置和使用模式的内存使用建议。 以下是有效值：<br /><br /> 增长<br /><br /> 缩减<br /><br /> 稳定|  
|**pdw_node_id**|**int**|**适用**于： [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]、[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> 此分发所在的节点的标识符。|  
  
## <a name="permissions"></a>权限  

在[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]上， `VIEW SERVER STATE`需要权限。   
在[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]高级层上，需要`VIEW DATABASE STATE`具有数据库中的权限。 在[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]标准层和基本层上，需要**服务器管理员**或**Azure Active Directory 管理员**帐户。   
  
## <a name="see-also"></a>另请参阅  

  [&#40;Transact-sql 的与操作系统相关的动态管理视图 SQL Server&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


