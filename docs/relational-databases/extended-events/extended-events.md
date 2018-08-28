---
title: 扩展事件 | Microsoft Docs
ms.custom: ''
ms.date: 10/23/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: xevents
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- extended events [SQL Server]
- xe
ms.assetid: bf3b98a6-51ed-4f2d-9c26-92f07f1fa947
caps.latest.revision: 48
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 240832f889c11a7896c67bfb60660bce7035d68c
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43087741"
---
# <a name="extended-events"></a>扩展事件
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 扩展事件具有高度可伸缩且高度可配置的体系结构，使用户能够按需收集解决性能问题或确定性能问题所需的信息。  

可在此处找到扩展事件的详细信息：

- [快速入门：SQL Server 中的扩展事件](../../relational-databases/extended-events/quick-start-extended-events-in-sql-server.md)
- 博客： [SQL Server 扩展事件](http://blogs.msdn.com/b/extended_events/)

  
## <a name="benefits-of-includessnoversionincludesssnoversion-mdmd-extended-events"></a>[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 扩展事件的优点  
 扩展事件是使用非常少的性能资源的轻型性能监视系统。 扩展事件提供两个图形用户界面（“新建会话向导”和“新建会话”），以便创建、修改、显示和分析你的会话数据。  
  
## <a name="extended-events-concepts"></a>扩展事件概念  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 扩展事件 (Extended Events) 是在现有概念（例如事件或事件使用者）的基础上建立的，它使用了 Windows 事件跟踪的概念并引入了新概念。  
  
 下表描述了扩展事件中的概念。  
  
|主题|描述|  
|-----------|-----------------|  
|[SQL Server 扩展事件包](../../relational-databases/extended-events/sql-server-extended-events-packages.md)|介绍了扩展事件包，扩展事件会话运行期间这些包中的对象将用于获取和处理数据。|  
|[SQL Server 扩展事件目标](http://msdn.microsoft.com/library/e281684c-40d1-4cf9-a0d4-7ea1ecffa384)|介绍了在事件会话期间可接收数据的事件使用者。|  
|[SQL Server 扩展事件引擎](../../relational-databases/extended-events/sql-server-extended-events-engine.md)|介绍了可实现和管理扩展事件会话的引擎。|  
|[SQL Server 扩展事件会话](../../relational-databases/extended-events/sql-server-extended-events-sessions.md)|介绍了扩展事件会话。|  
  
## <a name="extended-events-architecture"></a>扩展事件体系结构  
 扩展事件 (Extended Events) 是用于服务器系统的常规事件处理系统。 扩展事件基础结构支持 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中数据的关联，并且在某些情况下，还支持操作系统和数据库应用程序中数据的关联。 对于后一种情况，必须将扩展事件输出定向到 Windows 事件跟踪 (ETW)，才能使事件数据与操作系统或应用程序事件数据建立关联。  
  
 所有应用程序都具有在应用程序外部和内部均有用的执行点。 在应用程序内部，可以使用任务初始执行期间收集到的信息对异步处理进行排队。 在应用程序外部，执行点为监视实用工具提供被监视应用程序的行为和性能特征的有关信息。  
  
 扩展事件支持在进程外部使用事件数据。 此类数据通常由以下工具或用户使用：  
  
-   跟踪工具，如 SQL 跟踪和系统监视器。  
  
-   日志记录工具，如 Windows 事件日志或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误日志。  
  
-   管理某个产品或为某个产品开发应用程序的用户。  
  
 扩展事件的设计涉及以下主要方面：  
  
-   扩展事件引擎是不识别事件的。 因此，该引擎可以将任何事件绑定到任何目标，因为该引擎不受事件内容约束。 有关扩展事件引擎的详细信息，请参阅 [SQL Server Extended Events Engine](../../relational-databases/extended-events/sql-server-extended-events-engine.md)。  
  
-    事件与事件使用者不同，后者在扩展事件中称为“目标”。 也就是说任何目标可以接收任何事件。 此外，引发的任何事件均可供目标自动使用，这样可以记录或提供额外的事件上下文。 有关详细信息，请参阅 [SQL Server Extended Events Targets](http://msdn.microsoft.com/library/e281684c-40d1-4cf9-a0d4-7ea1ecffa384)。  
  
-   事件不同于在事件发生时要执行的操作。 因此，任何操作可以与任何事件相关联。  
  
-   谓词可以在应捕获事件数据时动态进行筛选。 这增加了扩展事件基础结构的灵活性。 有关详细信息，请参阅 [SQL Server Extended Events Packages](../../relational-databases/extended-events/sql-server-extended-events-packages.md)。  
  
 扩展事件可以同步生成事件数据（并异步处理该数据），这为事件处理提供了灵活的解决方案。 此外，扩展事件提供以下功能：  
  
-   一种跨服务器系统处理事件的统一方法，同时使用户可以隔离特定的事件进行故障排除。  
  
-   与现有的 ETW 工具集成并支持现有的 ETW 工具。  
  
-   基于 [!INCLUDE[tsql](../../includes/tsql-md.md)]的完全可配置的事件处理机制。  
  
-   可以动态监视活动进程，同时对这些进程的影响最小。  
  
-   运行时不会对性能造成任何明显影响的默认系统运行状况会话。 该会话收集的系统数据可用于帮助解决性能问题。 有关详细信息，请参阅 [使用 system_health 会话](../../relational-databases/extended-events/use-the-system-health-session.md)。  
  
## <a name="extended-events-tasks"></a>扩展事件任务  

使用 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 或 [!INCLUDE[tsql](../../includes/tsql-md.md)] 执行 [!INCLUDE[tsql](../../includes/tsql-md.md)] 数据定义语言 (DDL) 语句、动态管理视图和功能或目录视图，可以针对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 环境创建简单或复杂的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 扩展事件排除故障解决方案。  
  
|任务说明|主题|  
|----------------------|-----------|  
|使用 **“对象资源管理器”** 管理事件会话。|[在对象资源管理器中管理事件会话](../../relational-databases/extended-events/manage-event-sessions-in-the-object-explorer.md)|  
|介绍如何创建扩展事件会话。|[创建扩展事件会话](http://msdn.microsoft.com/library/34b1e95a-a80e-4aca-9201-abde47f2ca74)|  
|介绍如何查看和刷新目标数据。| [SQL Server 中扩展事件的目标数据的高级查看功能](../../relational-databases/extended-events/advanced-viewing-of-target-data-from-extended-events-in-sql-server.md)|  
|介绍如何使用扩展事件工具创建和管理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 扩展事件会话。|[扩展事件工具](../../relational-databases/extended-events/extended-events-tools.md)|  
|介绍如何更改扩展事件会话。|[更改扩展事件会话](../../relational-databases/extended-events/alter-an-extended-events-session.md)|  
|介绍如何获取与事件关联的字段的信息。|[获取所有事件的字段](http://msdn.microsoft.com/library/4e4ee03f-5bca-42ed-a37c-db1c82e3aad2)|  
|介绍如何找到在已注册的包中有哪些事件可用。|[查看已注册包的事件](http://msdn.microsoft.com/library/9a90b1a2-aa69-43f6-bdeb-cc5f57a26c6f)|  
|介绍如何确定在已注册的包中有哪些扩展事件目标可用。|[查看已注册包的扩展事件目标](http://msdn.microsoft.com/library/4985aa5f-ac99-49f6-852c-9d25916549e9)|  
|介绍如何查看与各 SQL 跟踪事件及其关联列等效的扩展事件和操作。|[查看与 SQL 跟踪事件类等效的扩展事件](../../relational-databases/extended-events/view-the-extended-events-equivalents-to-sql-trace-event-classes.md)|  
|介绍如何找到在 CREATE EVENT SESSION 或 ALTER EVENT SESSION 中使用 ADD TARGET 参数时可设置的参数。|[获取 ADD TARGET 实参的可配置形参](http://msdn.microsoft.com/library/08454543-c5c8-4ca3-9af9-f1d82264471c)|  
|介绍如何将现有 SQL 跟踪脚本转换为扩展事件会话。|[将现有 SQL 跟踪脚本转换为扩展事件会话](../../relational-databases/extended-events/convert-an-existing-sql-trace-script-to-an-extended-events-session.md)|  
|介绍如何确定持有锁的查询、查询的计划以及取锁时的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 堆栈。|[确定持有锁的查询](../../relational-databases/extended-events/determine-which-queries-are-holding-locks.md)|  
|介绍如何识别影响数据库性能的锁来源。|[查找具有最多锁定的对象](../../relational-databases/extended-events/find-the-objects-that-have-the-most-locks-taken-on-them.md)|  
|介绍如何将扩展事件和 Windows 事件跟踪配合使用来监视系统活动。|[使用扩展事件监视系统活动](../../relational-databases/extended-events/monitor-system-activity-using-extended-events.md)|  
| 为扩展事件使用目录视图和动态管理视图 (DMV) | [SQL Server 中扩展事件系统视图中的 SELECT 和 JOIN](../../relational-databases/extended-events/selects-and-joins-from-system-views-for-extended-events-in-sql-server.md) |

  
## <a name="see-also"></a>另请参阅  
 [数据层应用程序](../../relational-databases/data-tier-applications/data-tier-applications.md)   
 [DAC 对 SQL Server 对象和版本的支持](../../relational-databases/data-tier-applications/dac-support-for-sql-server-objects-and-versions.md)   
 [部署数据层应用程序](../../relational-databases/data-tier-applications/deploy-a-data-tier-application.md)   
 [监视数据层应用程序](../../relational-databases/data-tier-applications/monitor-data-tier-applications.md)   
 [扩展事件动态管理视图](../../relational-databases/system-dynamic-management-views/extended-events-dynamic-management-views.md)   
 [扩展事件目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/extended-events-catalog-views-transact-sql.md)  
  
  
