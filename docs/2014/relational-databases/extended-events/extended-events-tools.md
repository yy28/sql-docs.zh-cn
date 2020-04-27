---
title: 扩展事件工具 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xevents
ms.topic: conceptual
helpviewer_keywords:
- extended events [SQL Server], using
- extended events [SQL Server], options for using
ms.assetid: d312a9ff-50ba-4721-baef-50bfd3169d38
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e26bc62f0e6b81b7b4ac8e1361d0a1ac31513ef6
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "63137052"
---
# <a name="extended-events-tools"></a>扩展事件工具
  您可以使用以下工具创建和管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 扩展事件会话：  
  
-   数据定义语言 (DDL) 语句。 这些语句可用于创建和修改扩展事件会话。  
  
-   动态管理视图、目录视图和系统表。 这些视图和表可用于通过使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句获取会话数据和元数据。 这些系统表可帮助您确定用于 SQL 跟踪事件类和列的现有扩展事件等效项。  
  
-   对象资源管理器的 **“扩展事件”** 节点。 该节点可用于启动、停止或删除会话，或者用于导入和导出会话模板。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell 提供程序。 这是一个强大的工具，可用于创建、更改和管理扩展事件会话。 有关详细信息，请参阅 [对扩展事件使用 PowerShell 提供程序](use-the-powershell-provider-for-extended-events.md)。  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. 该工具可用于创建和执行在扩展事件主题中提供的代码示例。 有关详细信息，请参阅 [对象资源管理器](../../ssms/object/object-explorer.md)。  
  
 除了您创建的会话之外，在服务器上存在一个默认的系统运行状况会话。 该会话收集的系统数据可用于帮助解决性能问题。 有关详细信息，请参阅[使用 System_health 会话](use-the-ssms-xe-profiler.md)。  
  
## <a name="ddl-statements"></a>DDL 语句  
 请以下 DDL 语句可以创建、更改和删除扩展事件会话。  
  
|名称|说明|  
|----------|-----------------|  
|[CREATE EVENT SESSION (Transact-SQL)](/sql/t-sql/statements/create-event-session-transact-sql)|创建用于标识事件源、事件会话目标和事件会话参数的扩展事件会话对象。|  
|[ALTER EVENT SESSION (Transact-SQL)](/sql/t-sql/statements/alter-event-session-transact-sql)|启动或停止事件会话，或更改事件会话配置。|  
|[DROP EVENT SESSION (Transact-SQL)](/sql/t-sql/statements/drop-event-session-transact-sql)|删除事件会话。|  
  
## <a name="catalog-views"></a>目录视图  
 使用下面的目录视图可获取创建事件会话时所创建的元数据。  
  
|名称|说明|  
|----------|-----------------|  
|[sys.server_event_sessions (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-server-event-sessions-transact-sql)|列出所有事件会话定义。|  
|[sys.server_event_session_actions (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-server-event-session-actions-transact-sql)|返回针对事件会话的每个事件执行的每个操作所对应的行。|  
|[sys.server_event_session_events (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-server-event-session-events-transact-sql)|返回事件会话中每个事件所对应的行。|  
|[sys.server_event_session_fields (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-server-event-session-fields-transact-sql)|对在事件和目标上显式设置的每个可自定义列都返回一行。|  
|[sys.server_event_session_targets (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-server-event-session-targets-transact-sql)|返回事件会话的每个事件目标所对应的行。|  
  
## <a name="dynamic-management-views"></a>动态管理视图  
 使用下面的动态管理视图可以获取会话元数据和会话数据。 将从目录视图中获取元数据，当启动并运行事件会话时即创建会话数据。  
  
> [!NOTE]  
>  直到会话启动，这些视图中才会包含会话数据。  
  
|名称|说明|  
|----------|-----------------|  
|[sys.dm_os_dispatcher_pools (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-dispatcher-pools-transact-sql)|返回有关会话调度程序池的信息。|  
|[sys.dm_xe_objects (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-objects-transact-sql)|对事件包显示的每个对象都返回一行。|  
|[sys.dm_xe_object_columns (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-object-columns-transact-sql)|返回所有对象的架构信息。|  
|[sys.dm_xe_packages (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-packages-transact-sql)|列出向扩展事件引擎注册的所有包。|  
|[sys.dm_xe_sessions (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-sessions-transact-sql)|返回有关处于活动状态的扩展事件会话的信息。|  
|[sys.dm_xe_session_targets (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-session-targets-transact-sql)|返回有关会话目标的信息。|  
|[sys.dm_xe_session_events (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-session-events-transact-sql)|返回有关会话事件的信息。|  
|[sys.dm_xe_session_event_actions (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-session-event-actions-transact-sql)|返回有关事件会话操作的信息。|  
|[sys.dm_xe_map_values (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-map-values-transact-sql)|提供一个从内部数字键到可读文本的映射。|  
|[sys.dm_xe_session_object_columns (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-session-object-columns-transact-sql)|显示绑定到会话的对象的配置值。|  
  
## <a name="system-tables"></a>系统表  
 使用下面的系统表可以获取与 SQL 跟踪事件类和列的扩展事件等效项有关的信息。  
  
|名称|说明|  
|----------|-----------------|  
|[trace_xe_event_map (Transact-SQL)](/sql/relational-databases/system-tables/extended-events-tables-trace-xe-event-map)|映射到 SQL 跟踪事件类的每个扩展事件各占一行。|  
|[trace_xe_action_map (Transact-SQL)](/sql/relational-databases/system-tables/extended-events-tables-trace-xe-action-map)|映射到 SQL 跟踪列 ID 的每个扩展事件操作各占一行。|  
  
## <a name="see-also"></a>另请参阅  
 [动态管理视图和函数 &#40;Transact-sql&#41;](../views/views.md)   
 [Transact-sql&#41;的目录视图 &#40;](/sql/relational-databases/system-catalog-views/catalog-views-transact-sql)   
 [&#40;Transact-sql&#41;SQL Server 扩展事件表](/sql/relational-databases/system-tables/system-tables-transact-sql)   
 [使用 system_health 会话](use-the-ssms-xe-profiler.md)   
 [对扩展事件使用 PowerShell 提供程序](use-the-powershell-provider-for-extended-events.md)  
  
  
