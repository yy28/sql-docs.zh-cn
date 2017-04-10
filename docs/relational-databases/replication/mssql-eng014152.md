---
title: "MSSQL_ENG014152 | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "MSSQL_ENG014152 错误"
ms.assetid: 4215e2b1-cd30-441f-9671-9afc742adf6e
caps.latest.revision: 11
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 11
---
# MSSQL_ENG014152
    
## 消息详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|14152|  
|事件源|MSSQLSERVER|  
|组件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符号名称||  
|消息正文|复制 - %s：代理 %s 计划重试。 %s|  
  
## 解释  
 指定的复制代理已计划重试请求的操作。 进程继续重试，直到达到配置的最大作业步骤重试次数。  
  
 通常由于下列原因之一发生重试：  
  
-   超过了 **QueryTimeout** 值。  
  
-   超过了 **LoginTimeout** 值。  
  
-   将复制进程选为了死锁牺牲品。  
  
## 用户操作  
 如果重试消息很少出现，则不需要用户操作。  
  
 使用 [sp_help_jobstep](../../relational-databases/system-stored-procedures/sp-help-jobstep-transact-sql.md) 若要查看的最大次数的当前设置 **运行代理程序** 步骤指定的复制代理程序将重试。 您可以使用 **@retry_attempts** 参数 [sp_update_jobstep](../../relational-databases/system-stored-procedures/sp-update-jobstep-transact-sql.md) 存储过程来调整作业步骤重试次数。  
  
 如果重试消息频繁重复出现，则应根据错误消息排除导致重试的问题。 对于指示为何必须计划重试的消息，检查代理的历史记录。 某些情况下，您可能需要对复制代理启用更详细的日志记录。 有关如何配置复制日志记录的详细信息，请参阅 Microsoft 知识库文章 [312292](http://support.microsoft.com/kb/312292)。  
  
## 另请参阅  
 [错误和事件参考 & #40;复制和 #41;](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  