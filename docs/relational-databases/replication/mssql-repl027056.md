---
title: MSSQL_REPL027056 | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_REPL027056 error
ms.assetid: 92d62f3c-b8ae-482e-a348-2e9a8ee9786e
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 88b30abba50e8bdf1a350d882a3053f965a3da6e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68020192"
---
# <a name="mssqlrepl027056"></a>MSSQL_REPL027056
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="message-details"></a>消息详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|27056|  
|事件源|MSSQLSERVER|  
|组件|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|符号名称||  
|消息正文|合并进程无法更改“%1”上的生成历史记录。 进行故障排除时，请使用详细的历史日志记录来重新启动同步，并指定要写入的输出文件。|  
  
## <a name="explanation"></a>解释  
 此错误通常是由增长过大的合并复制系统表中的争用所引起。 大型系统表通常是由于发布保持期过长造成的，因为在到达保持期之前，元数据必须一直存储在这些表中。  
  
## <a name="user-action"></a>用户操作  
 **若要解决此问题：**  
  
1.  减小合并代理的 -**DownloadGenerationsPerBatch** 和 **-UploadGenerationsPerBatch** 参数的值，使进程在你解决引起错误的潜在问题时能够继续执行。 代理参数可以在代理配置文件和命令行中指定。 有关详细信息，请参阅：  
  
    -   [处理复制代理配置文件](../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)  
  
    -   [查看和修改复制代理命令提示符参数 (SQL Server Management Studio)](../../relational-databases/replication/agents/view-and-modify-replication-agent-command-prompt-parameters.md)  
  
    -   [Replication Agent Executables Concepts](../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)的最小和最大内存量。  
  
2.  为发布保持期指定尽可能低的设置。 有关详细信息，请参阅 [Subscription Expiration and Deactivation](../../relational-databases/replication/subscription-expiration-and-deactivation.md)。  
  
3.  在维护合并复制过程中，应不定期检查与合并复制关联的系统表的增长：MSmerge_contents、MSmerge_genhistory，以及 MSmerge_tombstone、MSmerge_current_partition_mappings，以及 MSmerge_past_partition_mappings。 定期对这些表重建索引。 有关详细信息，请参阅 [重新组织和重新生成索引](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)。  
  
## <a name="see-also"></a>另请参阅  
 [错误和事件参考（复制）](../../relational-databases/replication/errors-and-events-reference-replication.md)  
  
  
