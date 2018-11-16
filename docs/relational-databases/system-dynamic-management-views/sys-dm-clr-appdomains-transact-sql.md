---
title: sys.dm_clr_appdomains (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_clr_appdomains
- sys.dm_clr_appdomains
- dm_clr_appdomains_TSQL
- sys.dm_clr_appdomains_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_clr_appdomains dynamic management dynamic management view
ms.assetid: 9fe0d4fd-950a-4274-a493-85e776278045
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d7e1c3534e510e2a18929331918db7b6cf3efa60
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/15/2018
ms.locfileid: "51657456"
---
# <a name="sysdmclrappdomains-transact-sql"></a>sys.dm_clr_appdomains (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  为服务器中的每个应用程序域返回一行。 应用程序域 (**AppDomain**) 是在构造[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]公共语言运行时 (CLR) 是应用程序的隔离单元。 此视图可用于了解和解决问题中正在执行的 CLR 集成对象[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
 有多种类型的 CLR 集成托管数据库对象。 有关这些对象的常规信息，请参阅[使用公共语言运行时 (CLR) 集成生成数据库对象](../../relational-databases/clr-integration/database-objects/building-database-objects-with-common-language-runtime-clr-integration.md)。 执行这些对象，每当[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]创建**AppDomain**在其下程序可以加载并执行所需的代码。 隔离级别**AppDomain**是一个**AppDomain**每个数据库的每位所有者。 也就是说，用户拥有的所有 CLR 对象始终都执行在同一个**AppDomain**每个数据库 （如果用户在不同数据库中，CLR 数据库对象将运行在不同的应用程序域中注册 CLR 数据库对象）。 **AppDomain**在代码完成执行后才会被销毁。 而是缓存在内存中以备将来执行， 这可以提高性能。  
  
 有关详细信息，请参阅[应用程序域](https://go.microsoft.com/fwlink/p/?LinkId=299658)。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**appdomain_address**|**varbinary(8)**|地址**AppDomain**。 所有托管的数据库的用户拥有的对象始终加载在同一个**AppDomain**。 可以使用此列以查找在此当前加载的所有程序集**AppDomain**中**sys.dm_clr_loaded_assemblies**。|  
|**appdomain_id**|**int**|ID **AppDomain**。 每个**AppDomain**都有唯一的 id。|  
|**appdomain_name**|**varchar(386)**|名称**AppDomain**由分配[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。|  
|**creation_time**|**datetime**|时间**AppDomain**已创建。 因为**Appdomain**缓存并重复使用以更好性能**creation_time**不一定执行代码时的时间。|  
|**db_id**|**int**|此数据库的 ID **AppDomain**已创建。 在两个不同数据库中存储的代码无法共享同一个**AppDomain**。|  
|**user_id**|**int**|在此可以执行其对象的用户 ID **AppDomain**。|  
|State|**nvarchar(128)**|当前状态的描述符**AppDomain**。 AppDomain 可以处于从创建到删除的不同状态中。 有关详细信息，请参阅本主题的“备注”部分。|  
|**strong_refcount**|**int**|此强引用的数目**AppDomain**。 这反映了当前正在执行的使用此批处理的数目**AppDomain**。 请注意，将创建此视图执行**强引用计数**; 即使当前正在执行，没有代码**strong_refcount**将具有值为 1。|  
|**weak_refcount**|**int**|此弱引用的数目**AppDomain**。 这表示对象数目**AppDomain**缓存。 当执行托管的数据库对象，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]将其缓存在**AppDomain**供将来重复使用。 这可以提高性能。|  
|**cost**|**int**|成本**AppDomain**。 开销越大，更有可能这**AppDomain**内存压力下卸载。 成本通常取决于重新创建此所需的内存量**AppDomain**。|  
|**value**|**int**|值**AppDomain**。 值越低，更有可能这**AppDomain**内存压力下卸载。 值通常依赖于连接或批次数量使用此**AppDomain**。|  
|**total_processor_time_ms**|**bigint**|自进程启动后在当前应用程序域中执行的过程中所有线程所用的处理器总时间（毫秒）。 这相当于**System.AppDomain.MonitoringTotalProcessorTime**。|  
|**total_allocated_memory_kb**|**bigint**|应用程序域自创建以来进行的所有内存分配的总大小 (KB)（不减去已收集的内存大小）。 这相当于**System.AppDomain.MonitoringTotalAllocatedMemorySize**。|  
|**survived_memory_kb**|**bigint**|在已知当前应用程序域所引用的最近一次全面的阻塞收集之后仍剩余的字节数 (KB)。 这相当于**System.AppDomain.MonitoringSurvivedMemorySize**。|  
  
## <a name="remarks"></a>备注  
 没有之间的一个对多关系**dm_clr_appdomains.appdomain_address**并**dm_clr_loaded_assemblies.appdomain_address**。  
  
 下表列出了可能**状态**值，它们的说明，当它们发生在**AppDomain**生命周期。 可以使用此信息要遵循的生命周期**AppDomain**及监视可疑或重复性**AppDomain**实例卸载，而无需分析 Windows 事件日志。  
  
## <a name="appdomain-initialization"></a>AppDomain 初始化  
  
|State|Description|  
|-----------|-----------------|  
|E_APPDOMAIN_CREATING|**AppDomain**正在创建。|  
  
## <a name="appdomain-usage"></a>AppDomain 使用情况  
  
|State|Description|  
|-----------|-----------------|  
|E_APPDOMAIN_SHARED|在运行时**AppDomain**随时可供多个用户使用。|  
|E_APPDOMAIN_SINGLEUSER|**AppDomain**供 DDL 操作中使用。 此行为不同于 E_APPDOMAIN_SHARED，在后者中，共享的 AppDomain 用于 CLR 集成执行，而非 DDL 操作。 此类 AppDomain 独立于其他并发操作。|  
|E_APPDOMAIN_DOOMED|**AppDomain**计划无法卸载，但当前线程正在其中。|  
  
## <a name="appdomain-cleanup"></a>AppDomain 的清除  
  
|State|Description|  
|-----------|-----------------|  
|E_APPDOMAIN_UNLOADING|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 已请求 CLR 卸载**AppDomain**，通常是因为包含托管的数据库对象的程序集已更改或删除。|  
|E_APPDOMAIN_UNLOADED|CLR 已卸载**AppDomain**。 这通常是由于升级过程的结果**ThreadAbort**， **OutOfMemory**，或在用户代码中未经处理的异常。|  
|E_APPDOMAIN_ENQUEUE_DESTROY|**AppDomain**已在 CLR 中卸载并设置被破坏[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。|  
|E_APPDOMAIN_DESTROY|**AppDomain**通过处于销毁过程中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。|  
|E_APPDOMAIN_ZOMBIE|**AppDomain**已由销毁[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]; 但是，并非所有对引用**AppDomain**已清除。|  
  
## <a name="permissions"></a>Permissions  
 需要对数据库具有 VIEW SERVER STATE 权限。  
  
## <a name="examples"></a>示例  
 下面的示例演示如何查看的详细信息**AppDomain**给定程序集：  
  
```  
select appdomain_id, creation_time, db_id, user_id, state  
from sys.dm_clr_appdomains a  
where appdomain_address =   
(select appdomain_address   
 from sys.dm_clr_loaded_assemblies  
   where assembly_id = 500);  
```  
  
 下面的示例演示如何查看中的所有程序集给定**AppDomain**:  
  
```  
select a.name, a.assembly_id, a.permission_set_desc, a.is_visible, a.create_date, l.load_time   
from sys.dm_clr_loaded_assemblies as l   
inner join sys.assemblies as a  
on l.assembly_id = a.assembly_id  
where l.appdomain_address =   
(select appdomain_address   
from sys.dm_clr_appdomains  
where appdomain_id = 15);  
```  
  
## <a name="see-also"></a>请参阅  
 [sys.dm_clr_loaded_assemblies &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-clr-loaded-assemblies-transact-sql.md)   
 [公共语言运行时与相关的动态管理视图&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/common-language-runtime-related-dynamic-management-views-transact-sql.md)  
  
  
