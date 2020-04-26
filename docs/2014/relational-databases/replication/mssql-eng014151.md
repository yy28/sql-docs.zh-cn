---
title: MSSQL_ENG014151 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG014151 error
ms.assetid: 54b45e70-46b3-4c7a-a5bf-06f6dd028ceb
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1f292841c227db26f1c518b2eaef896f7ce3570c
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/25/2020
ms.locfileid: "63191457"
---
# <a name="mssql_eng014151"></a>MSSQL_ENG014151
    
## <a name="message-details"></a>消息详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|14151|  
|事件源|MSSQLSERVER|  
|组件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符号名称||  
|消息正文|复制 - %s: 代理 %s 失败。 %s|  
  
## <a name="explanation"></a>说明  
 此错误可由任何复制代理失败引发。 消息结尾的文本取决于失败的上下文。  
  
## <a name="user-action"></a>用户操作  
 此错误可能在多种情况下发生；请根据需要使用下列方法：  
  
-   重新启动失败的代理，以查看此代理现在是否能正常运行。 有关详细信息，请参阅[启动和停止复制代理 (SQL Server Management Studio)](agents/start-and-stop-a-replication-agent-sql-server-management-studio.md) 和[复制代理可执行文件概念](concepts/replication-agent-executables-concepts.md)。  
  
-   查看代理历史记录和作业历史记录，寻找同时发生的其他错误。 有关在复制监视器中查看代理状态和错误详细资料的信息，请参阅[使用复制监视器查看信息和执行任务](monitor/view-information-and-perform-tasks-replication-monitor.md)。  
  
-   验证代理所访问的各计算机之间的基本连接是否正常，然后用实用工具（如 [sqlcmd Utility](../../tools/sqlcmd-utility.md)）连接到每台计算机。 连接时，请使用代理建立连接使用的同一帐户。 有关每个代理帐户所需权限的详细信息，请参阅 [Replication Agent Security Model](security/replication-agent-security-model.md)。  
  
-   如果在创建或应用快照发生错误时，请检查快照目录中的文件以查找错误。  
  
-   如果错误继续出现，请增加代理的日志记录并指定日志的输出文件。 此操作可能会提供找到该错误和/或其他错误消息的步骤，具体取决于错误的上下文。  
  
## <a name="see-also"></a>另请参阅  
 [复制代理管理](agents/replication-agent-administration.md)   
 [错误和事件参考（复制）](errors-and-events-reference-replication.md)   
 [Replication Distribution Agent](agents/replication-distribution-agent.md)   
 [Replication Log Reader Agent](agents/replication-log-reader-agent.md)   
 [Replication Merge Agent](agents/replication-merge-agent.md)   
 [复制队列读取器代理](agents/replication-queue-reader-agent.md)   
 [Replication Snapshot Agent](agents/replication-snapshot-agent.md)  
  
  
