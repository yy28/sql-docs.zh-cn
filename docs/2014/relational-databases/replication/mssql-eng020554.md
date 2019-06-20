---
title: MSSQL_ENG020554 | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG020554 error
ms.assetid: ef1a1b88-b2ab-43e8-99cd-163a973262d6
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 744ab7a10db83cffa098bc97aa0ceb2c615481fd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63057115"
---
# <a name="mssqleng020554"></a>MSSQL_ENG020554
    
## <a name="message-details"></a>消息详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|20554|  
|事件源|MSSQLSERVER|  
|组件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符号名称||  
|消息正文|复制代理在 %ld 分钟内没有记录任何进度消息。 这表明代理已停止响应或系统活动过多。 请确保正在将记录复制到目标，并且与订阅服务器、发布服务器和分发服务器的连接仍然是活动的。|  
  
## <a name="explanation"></a>解释  
 复制代理检查  作业以指定的时间间隔运行（默认为 10 分钟），检查每个复制代理的状态。 如果自上次代理检查作业运行后，代理未记录任何进度消息，将引发错误 MSSQL_ENG020554。 即使未发生其他复制活动，代理至少应该记录历史记录消息。 虽然复制代理未按预期响应，但其未必已停止或失败（如果代理失败，将引发错误 MSSQL_ENG020536）。  
  
 下列问题可导致引发错误 MSSQL_ENG020554：  
  
-   代理正忙。  
  
     当代理检查作业轮询时，如果代理因为过于繁忙而无法响应，则代理检查作业无法报告复制代理运行是否正常。 有很多原因可导致复制代理忙：可能有大量数据正在复制，或者由于应用程序设计或配置问题而导致进程长时间运行。  
  
-   代理无法登录到拓扑中的某台计算机。  
  
     所有代理都有参数 **-LoginTimeOut** （默认设置为 15 秒），此参数管理代理尝试登录到复制节点的所用时间，如合并代理登录到发布服务器。 如果将 **-LoginTimeOut** 值设置为高于复制代理检查作业运行的时间间隔，则登录问题可能是导致该错误的根本原因：错误 MSSQL_ENG020554 引发后，该代理才会引发更具体的错误。  
  
## <a name="user-action"></a>用户操作  
 所需操作取决于错误的原因：  
  
-   对于引发此错误的所有情况：  
  
     检查复制监视器中的错误详细信息，如果代理已停止，请重新启动它。 错误详细信息可能提供关于代理为何无法正常运行的附加信息。 如果代理正在运行，请不要停止和重新启动代理，因为这样会使问题恶化。 有关在复制监视器中查看代理状态和错误详细资料的信息，请参阅以下主题：  
  
    -   有关快照代理、 日志读取器代理和队列读取器代理，请参阅[查看信息和执行其任务使用复制监视器](monitor/view-information-and-perform-tasks-replication-monitor.md)。  
  
    -   有关分发代理和合并代理，请参阅[查看信息和执行其任务使用复制监视器](monitor/view-information-and-perform-tasks-replication-monitor.md)。  
  
-   如果由于代理忙而频频引发此错误：  
  
     可能需要重新设计应用程序，以便减少代理进行处理所花费的时间。  
  
     可以通过 **“作业属性”** 对话框来加大检查代理状态的时间间隔。 有关访问此对话框复制作业的信息，请参阅[查看信息和执行其任务使用复制监视器](monitor/view-information-and-perform-tasks-replication-monitor.md)。  
  
-   如果代理无法登录到拓扑中的某台计算机：  
  
     建议将 **-LoginTimeOut** 的值设置为低于复制代理检查作业运行的时间间隔值。 在某些情况下，由于导致登录超时的网络问题，需要将 **-LoginTimeOut** 的值设置得更高。如果将 **-LoginTimeOut** 设置得较低，复制会报告更为具体的错误，使你可以解决可能因权限、网络问题或其他问题而导致的登录问题。 代理参数可以在代理配置文件和命令行中指定。 有关详细信息，请参阅：  
  
    -   [处理复制代理配置文件](agents/replication-agent-profiles.md)  
  
    -   [查看和修改复制代理命令提示符参数 (SQL Server Management Studio)](agents/view-and-modify-replication-agent-command-prompt-parameters.md)  
  
    -   [Replication Agent Executables Concepts](concepts/replication-agent-executables-concepts.md)的最小和最大内存量。  
  
## <a name="see-also"></a>请参阅  
 [复制代理管理](agents/replication-agent-administration.md)   
 [错误和事件参考（复制）](errors-and-events-reference-replication.md)   
 [复制分发代理](agents/replication-distribution-agent.md)   
 [复制日志读取器代理](agents/replication-log-reader-agent.md)   
 [复制合并代理](agents/replication-merge-agent.md)   
 [复制队列读取器代理](agents/replication-queue-reader-agent.md)   
 [复制快照代理](agents/replication-snapshot-agent.md)  
  
  
