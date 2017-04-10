---
title: "MSSQL_ENG018752 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "MSSQL_ENG018752 错误"
ms.assetid: 405b2655-acb4-4e15-bcc6-b8f86bb22b37
caps.latest.revision: 15
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 15
---
# MSSQL_ENG018752
    
## 消息详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|18752|  
|事件源|MSSQLSERVER|  
|组件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符号名称||  
|消息正文|一次只能有一个日志读取器代理或日志相关过程(sp_repldone、sp_replcmds 和 sp_replshowcmds)连接到某个数据库。 如果执行了一个日志相关过程，那么在启动日志读取器代理或者执行另一个日志相关过程之前，请删除执行第一个过程时所用的连接，或者在该连接上执行 sp_replflush。|  
  
## 解释  
 多个当前连接正在尝试执行以下任何项︰ **sp_repldone**, ，**sp_replcmds**, ，或 **sp_replshowcmds**。 存储的过程 [sp_repldone & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-repldone-transact-sql.md) 和 [sp_replcmds & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-replcmds-transact-sql.md) 存储的过程使用由日志读取器代理来查找和更新有关已发布数据库中复制的事务的信息。 存储的过程 [sp_replshowcmds & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-replshowcmds-transact-sql.md) 用于排除某些类型的事务复制的问题。  
  
 在以下情形下将引发此错误：  
  
-   如果某个已发布数据库的日志读取器代理正在运行，而另一个日志读取器代理试图在同一个数据库上运行，则对第二个代理引发此错误，并且此错误将出现在代理历史记录中。  
  
     有时看起来像是有多个代理，则可能其中一个代理是执行孤立进程的结果。  
  
-   如果发布的数据库的日志读取器代理已启动，并且用户执行 **sp_repldone**, ，**sp_replcmds**, ，或 **sp_replshowcmds** 针对该数据库，则会引发错误的存储的过程已执行的应用程序中 (如 **sqlcmd**)。  
  
-   如果没有日志读取器代理正在运行已发布数据库，并且用户执行 **sp_repldone**, ，**sp_replcmds**, ，或 **sp_replshowcmds** 和后没有关闭的连接对其执行此过程，该错误日志读取器代理试图连接到数据库时引发。  
  
## 用户操作  
 以下步骤可以帮助您解决这个问题。 如果任何一个步骤能正确启动日志读取器代理，则没有必要完成剩余的步骤。  
  
-   检查日志读取器代理的历史记录，查找可能导致此错误的其他任何错误。 在复制监视器中查看代理状态和错误详细资料的信息，请参阅 [查看信息并执行任务的代理相关联的发布 & #40;复制监视器 & #41;](../../relational-databases/replication/monitor/view information and perform tasks for publication agents.md)。  
  
-   输出中检查 [sp_who & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md) 有关具体进程标识号 (Spid) 连接到已发布的数据库。 关闭可能已用的任何连接 **sp_repldone**, ，**sp_replcmds**, ，或 **sp_replshowcmds**。  
  
-   重新启动日志读取器代理。 有关详细信息，请参阅 [启动和停止复制代理 & #40;SQL Server Management Studio & #41;](../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)。  
  
-   在分发服务器上重新启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理服务（使之在群集中脱机或联机）。 如果没有计划的作业无法执行了 **sp_repldone**, ，**sp_replcmds**, ，或 **sp_replshowcmds** 从任何其他 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例时，重新启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 也要为这些实例的代理。 有关详细信息，请参阅 [启动、 停止或暂停 SQL Server 代理服务](../../ssms/agent/start-stop-or-pause-the-sql-server-agent-service.md)。  
  
-   执行 [sp_replflush & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-replflush-transact-sql.md) 在发布服务器上的发布数据库中，然后重新启动日志读取器代理。  
  
-   如果错误继续出现，请增加代理的日志记录并指定日志的输出文件。 此操作可能会提供找到该错误和/或其他错误消息的步骤，具体取决于错误的上下文。  
  
## 另请参阅  
 [错误和事件参考 & #40;复制和 #41;](../../relational-databases/replication/errors-and-events-reference-replication.md)   
 [复制日志读取器代理](../../relational-databases/replication/agents/replication-log-reader-agent.md)  
  
  