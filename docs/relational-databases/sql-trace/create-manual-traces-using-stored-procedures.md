---
title: "使用存储过程创建手动跟踪 | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f6f47fa2-7c17-41d4-9f69-9be144d56832
caps.latest.revision: 7
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 1ee7ef604dc518fb4765ca5bd944c7fe01500035
ms.lasthandoff: 04/11/2017

---
# <a name="create-manual-traces-using-stored-procedures"></a>使用存储过程创建手动跟踪
  Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供 [!INCLUDE[tsql](../../includes/tsql-md.md)] 系统存储过程来创建对 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]实例的跟踪。 可以不使用 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]，而使用这些系统存储过程从您自己的应用程序中手动创建跟踪。 这样，您就可以针对企业的特定需求编写自定义应用程序。  
  
## <a name="in-this-section"></a>本节内容  
 下表列出了用于跟踪 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]实例的系统存储过程。  
  
|存储过程|执行的任务|  
|----------------------|--------------------|  
|[sys.fn_trace_geteventinfo (Transact-SQL)](../../relational-databases/system-functions/sys-fn-trace-geteventinfo-transact-sql.md)|返回跟踪中包含的事件的相关信息。|  
|[sys.fn_trace_getinfo (Transact-SQL)](../../relational-databases/system-functions/sys-fn-trace-getinfo-transact-sql.md)|返回有关指定跟踪或所有现有跟踪的信息。|  
|[sp_trace_create (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-trace-create-transact-sql.md)|创建跟踪定义。 新的跟踪将处于停止状态。|  
|[sp_trace_generateevent (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-trace-generateevent-transact-sql.md)|创建用户定义事件。|  
|[sp_trace_setevent (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)|将事件类或数据列添加到跟踪，或从跟踪中删除事件类或数据列。|  
|[sp_trace_setstatus (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql.md)|启动、停止或关闭跟踪。|  
|[sys.fn_trace_getfilterinfo (Transact-SQL)](../../relational-databases/system-functions/sys-fn-trace-getfilterinfo-transact-sql.md)|返回有关应用于跟踪的筛选器的信息。|  
|[sp_trace_setfilter (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql.md)|将新的或已修改的筛选器应用于跟踪。|  
  
 **使用存储过程定义自己的跟踪**  
  
1.  使用 **sp_trace_setevent**指定要捕获的事件。  
  
2.  指定任何事件筛选器。 有关详细信息，请参阅[设置跟踪筛选器 (Transact SQL)](../../relational-databases/sql-trace/set-a-trace-filter-transact-sql.md)。  
  
3.  使用 **sp_trace_create** 为捕获的事件数据指定目的。  
  
 有关使用跟踪存储过程的示例，请参阅[创建跟踪 (Transact-SQL)](../../relational-databases/sql-trace/create-a-trace-transact-sql.md)。  
  
 **设置跟踪定义默认值**  
  
 [SQL Server 事件探查器](../../tools/sql-server-profiler/set-trace-definition-defaults-sql-server-profiler.md)  
  
 **设置跟踪显示默认值**  
  
 [SQL Server 事件探查器](../../tools/sql-server-profiler/set-trace-display-defaults-sql-server-profiler.md)  
  
 **创建跟踪**  
  
 [SQL Server 事件探查器](../../tools/sql-server-profiler/create-a-trace-sql-server-profiler.md)  
  
 [Transact-SQL](../../relational-databases/sql-trace/create-a-trace-transact-sql.md)  
  
 **向跟踪模板添加或从中删除事件**  
  
 [SQL Server 事件探查器](../../tools/sql-server-profiler/specify-events-and-data-columns-for-a-trace-file-sql-server-profiler.md)  
  
 [Transact-SQL](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)  
  
  
