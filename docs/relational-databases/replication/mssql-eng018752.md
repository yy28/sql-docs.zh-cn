---
title: MSSQL_ENG018752 | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- MSSQL_ENG018752 error
ms.assetid: 405b2655-acb4-4e15-bcc6-b8f86bb22b37
caps.latest.revision: 15
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 929c5e1c6205ab46b89ce4818183bb5ba9084fbe
ms.lasthandoff: 04/11/2017

---
# <a name="mssqleng018752"></a>MSSQL_ENG018752
    
## <a name="message-details"></a>消息详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|18752|  
|事件源|MSSQLSERVER|  
|组件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符号名称||  
|消息正文|一次只能有一个日志读取器代理或日志相关过程(sp_repldone、sp_replcmds 和 sp_replshowcmds)连接到某个数据库。 如果执行了一个日志相关过程，那么在启动日志读取器代理或者执行另一个日志相关过程之前，请删除执行第一个过程时所用的连接，或者在该连接上执行 sp_replflush。|  
  
## <a name="explanation"></a>解释  
 有多个当前连接正在尝试执行以下任一日志相关过程: **sp_repldone**、 **sp_replcmds**或 **sp_replshowcmds**。 存储过程 [sp_repldone &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-repldone-transact-sql.md) 和 [sp_replcmds &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md) 是日志读取器代理用来在已发布数据库中查找和更新已复制事务的相关信息的存储过程。 存储过程 [sp_replshowcmds &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replshowcmds-transact-sql.md) 用于解决事务性复制发生的某些类型的问题。  
  
 在以下情形下将引发此错误：  
  
-   如果某个已发布数据库的日志读取器代理正在运行，而另一个日志读取器代理试图在同一个数据库上运行，则对第二个代理引发此错误，并且此错误将出现在代理历史记录中。  
  
     有时看起来像是有多个代理，则可能其中一个代理是执行孤立进程的结果。  
  
-   如果启动了已发布数据库的日志读取器代理，而用户在同一个数据库上执行 **sp_repldone**、 **sp_replcmds**或 **sp_replshowcmds** ，则在执行存储过程的应用程序（如 **sqlcmd**）中将引发此错误。  
  
-   如果已发布数据库的日志读取器代理不在运行状态，而用户在执行 **sp_repldone**、 **sp_replcmds**或 **sp_replshowcmds** 后没有关闭用于执行此过程的连接，则当日志读取器代理尝试连接到数据库时将引发此错误。  
  
## <a name="user-action"></a>用户操作  
 以下步骤可以帮助您解决这个问题。 如果任何一个步骤能正确启动日志读取器代理，则没有必要完成剩余的步骤。  
  
-   检查日志读取器代理的历史记录，查找可能导致此错误的其他任何错误。 有关在复制监视器中查看代理状态和错误详细资料的信息，请参阅[查看与发布关联的代理的信息和执行其任务（复制监视器）](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-publication-agents.md)。  
  
-   检查 [sp_who &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md) 的输出，查找连接到已发布数据库的具体进程标识号(SPID)。 关闭所有可能运行 **sp_repldone**、 **sp_replcmds**或 **sp_replshowcmds**的连接。  
  
-   重新启动日志读取器代理。 有关详细信息，请参阅[启动和停止复制代理 (SQL Server Management Studio)](../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md).  
  
-   在分发服务器上重新启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务（使之在群集中脱机或联机）。 如果计划的作业有可能在任何其他 **实例中执行了**sp_repldone **、**sp_replcmds **或** sp_replshowcmds [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，则也要为那些实例重新启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理。 有关详细信息，请参阅[启动、停止或暂停 SQL Server 代理服务](http://msdn.microsoft.com/library/c95a9759-dd30-4ab6-9ab0-087bb3bfb97c)。  
  
-   对发布服务器上的发布数据库执行 [sp_replflush &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-replflush-transact-sql.md)，然后重新启动日志读取器代理。  
  
-   如果错误继续出现，请增加代理的日志记录并指定日志的输出文件。 此操作可能会提供找到该错误和/或其他错误消息的步骤，具体取决于错误的上下文。  
  
## <a name="see-also"></a>另请参阅  
 [错误和事件参考（复制）](../../relational-databases/replication/errors-and-events-reference-replication.md)   
 [复制日志读取器代理](../../relational-databases/replication/agents/replication-log-reader-agent.md)  
  
  
