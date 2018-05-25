---
title: sys.dm_clr_appdomains (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
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
caps.latest.revision: 24
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: e37769be6369fe1a18b8c6fb03dbecd534df502a
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2018
---
# <a name="sysdmclrappdomains-transact-sql"></a>sys.dm_clr_appdomains (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  为服务器中的每个应用程序域返回一行。 应用程序域 (**AppDomain**) 是中的构造[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]公共语言运行时 (CLR) 是为应用程序隔离的单位。 此视图可用于了解和解决在中执行的 CLR 集成对象[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
 有多种类型的 CLR 集成托管数据库对象。 有关这些对象的常规信息，请参阅[生成数据库对象所具有公共语言运行时 (CLR) 集成](../../relational-databases/clr-integration/database-objects/building-database-objects-with-common-language-runtime-clr-integration.md)。 每当执行这些对象，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]创建**AppDomain**下它程序可以加载并执行所需的代码。 隔离级别**AppDomain**是**AppDomain**每个数据库的每位所有者。 即用户所拥有的所有 CLR 对象始终都执行在同一个**AppDomain**每个数据库 （如果用户注册 CLR 数据库对象，在不同数据库中，CLR 数据库对象将在不同应用程序域中运行）。 **AppDomain**代码完成执行后才会被销毁。 而是缓存在内存中以备将来执行， 这提高了性能。  
  
 有关详细信息，请参阅[应用程序域](http://go.microsoft.com/fwlink/p/?LinkId=299658)。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**appdomain_address**|**varbinary(8)**|地址**AppDomain**。 在同一个始终加载用户所拥有的对象的所有托管的数据库**AppDomain**。 你可以使用此列来查找此当前加载的所有程序集**AppDomain**中**sys.dm_clr_loaded_assemblies**。|  
|**appdomain_id**|**int**|ID **AppDomain**。 每个**AppDomain**具有唯一的 id。|  
|**appdomain_name**|**varchar(386)**|名称**AppDomain**分配[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。|  
|**creation_time**|**datetime**|时间**AppDomain**已创建。 因为**AppDomains**缓存和重用为了提高性能， **creation_time**不一定是执行的代码时的时间。|  
|**db_id**|**int**|在此数据库 ID **AppDomain**已创建。 存储在两个不同的数据库中的代码不能共享一个**AppDomain**。|  
|**user_id**|**int**|在此可以执行其对象的用户 ID **AppDomain**。|  
|**状态**|**nvarchar(128)**|当前状态的描述符**AppDomain**。 AppDomain 可以处于从创建到删除的不同状态中。 有关详细信息，请参阅本主题的“备注”部分。|  
|**strong_refcount**|**int**|强引用数目**AppDomain**。 这反映当前正在执行使用此选项的批处理数**AppDomain**。 请注意，将创建此视图执行**强引用计数**; 即使当前正在执行，没有代码**strong_refcount**将具有值为 1。|  
|**weak_refcount**|**int**|弱引用数目**AppDomain**。 这表示多少对象内**AppDomain**进行缓存。 当您执行托管的数据库对象，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]将其内部缓存**AppDomain**以备将来再使用。 这提高了性能。|  
|**cost**|**int**|成本的**AppDomain**。 成本较高、 更有可能此**AppDomain**是卸载内存压力下。 成本通常依赖于需要多少内存来重新创建此**AppDomain**。|  
|**值**|**int**|值**AppDomain**。 值越低，更有可能此**AppDomain**是卸载内存压力下。 值通常依赖于多少连接或批处理正在使用此**AppDomain**。|  
|**total_processor_time_ms**|**bigint**|自进程启动后在当前应用程序域中执行的过程中所有线程所用的处理器总时间（毫秒）。 这相当于**System.AppDomain.MonitoringTotalProcessorTime**。|  
|**total_allocated_memory_kb**|**bigint**|应用程序域自创建以来进行的所有内存分配的总大小 (KB)（不减去已收集的内存大小）。 这相当于**System.AppDomain.MonitoringTotalAllocatedMemorySize**。|  
|**survived_memory_kb**|**bigint**|在已知当前应用程序域所引用的最近一次全面的阻塞收集之后仍剩余的字节数 (KB)。 这相当于**System.AppDomain.MonitoringSurvivedMemorySize**。|  
  
## <a name="remarks"></a>注释  
 没有之间的一个可能关系**dm_clr_appdomains.appdomain_address**和**dm_clr_loaded_assemblies.appdomain_address**。  
  
 下面的表列表可能**状态**值、 及其说明，以及时，它们会在**AppDomain**生命周期。 你可以使用此信息要遵循的生命周期**AppDomain**和要监视的可疑或重复**AppDomain**卸载，而无需分析 Windows 事件日志的实例。  
  
## <a name="appdomain-initialization"></a>AppDomain 初始化  
  
|State|Description|  
|-----------|-----------------|  
|E_APPDOMAIN_CREATING|**AppDomain**正在创建。|  
  
## <a name="appdomain-usage"></a>AppDomain 使用情况  
  
|State|Description|  
|-----------|-----------------|  
|E_APPDOMAIN_SHARED|运行时**AppDomain**随时可供由多个用户使用。|  
|E_APPDOMAIN_SINGLEUSER|**AppDomain**随时可供在 DDL 操作中使用。 此行为不同于 E_APPDOMAIN_SHARED，在后者中，共享的 AppDomain 用于 CLR 集成执行，而非 DDL 操作。 此类 AppDomain 独立于其他并发操作。|  
|E_APPDOMAIN_DOOMED|**AppDomain**计划会被卸载，但当前有在其中执行的线程。|  
  
## <a name="appdomain-cleanup"></a>AppDomain 的清除  
  
|State|Description|  
|-----------|-----------------|  
|E_APPDOMAIN_UNLOADING|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 已请求 CLR 卸载**AppDomain**，通常是由于更改包含托管的数据库对象的程序集或将其删除。|  
|E_APPDOMAIN_UNLOADED|已卸载 CLR **AppDomain**。 这通常是由于升级过程的结果**ThreadAbort**， **OutOfMemory**，或在用户代码中未经处理的异常。|  
|E_APPDOMAIN_ENQUEUE_DESTROY|**AppDomain**已卸载的 CLR 和设置被破坏[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。|  
|E_APPDOMAIN_DESTROY|**AppDomain**处于销毁通过[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。|  
|E_APPDOMAIN_ZOMBIE|**AppDomain**已通过销毁[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]; 但是，并非所有对引用**AppDomain**已清除了。|  
  
## <a name="permissions"></a>权限  
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
  
## <a name="see-also"></a>另请参阅  
 [sys.dm_clr_loaded_assemblies &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-clr-loaded-assemblies-transact-sql.md)   
 [公共语言运行时相关的动态管理视图&#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/common-language-runtime-related-dynamic-management-views-transact-sql.md)  
  
  
