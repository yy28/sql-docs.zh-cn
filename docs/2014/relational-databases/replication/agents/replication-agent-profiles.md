---
title: 复制代理配置文件 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Distribution Agent, profiles
- replication [SQL Server], agents and profiles
- replication agent profiles [SQL Server]
- Merge Agent, profiles
- agents [SQL Server replication], profiles
- Queue Reader Agent, profiles
- profiles [SQL Server], replication agents
- Snapshot Agent, profiles
- Log Reader Agent, profiles
ms.assetid: 0e980725-e42f-4283-94cb-d8a6dba5df62
caps.latest.revision: 43
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: f17c7ae974704ba42ad4653f1f560497f7bd9061
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36126062"
---
# <a name="replication-agent-profiles"></a>复制代理配置文件
  在配置复制时，将在分发服务器上安装一组代理配置文件。 代理配置文件包含一组在代理每次运行时都要使用的参数：在代理启动过程中，每个代理都会登录到分发服务器，并查询其配置文件中的参数。 对于使用 Web 同步的合并订阅，配置文件会下载并存储在订阅服务器中。 如果配置文件发生了更改，订阅服务器中的配置文件将在合并代理下次运行时更新。 有关 Web 同步的详细信息，请参阅 [Web Synchronization for Merge Replication](../web-synchronization-for-merge-replication.md)。  
  
 复制为每个代理提供一个默认的配置文件，同时还为日志读取器代理、分发代理和合并代理提供附加的预定义配置文件。 除了所提供的配置文件之外，您还可以创建符合自己应用程序要求的配置文件。 使用代理配置文件可以轻松地更改与该配置文件关联的所有代理的键参数。 例如，如果您有 20 个快照代理并且需要更改查询超时值（ **-QueryTimeout** 参数），则可以更新这些快照代理使用的配置文件，这样该此类型的所有代理将在下次运行时自动开始使用新值。  
  
 您也可能对代理的不同实例拥有不同的配置文件。 例如，以拨号连接方式连接到发布服务器和分发服务器的合并代理可以通过使用“慢速链接”  配置文件而采用一组更适合慢速通信链接的参数。  
  
> [!NOTE]  
>  如果在命令行中为代理参数指定了值，则该值将覆盖代理配置文件中为同一参数设置的值。  
  
 **使用和修改代理配置文件**  
  
-   [处理复制代理配置文件](replication-agent-profiles.md)  
  
## <a name="snapshot-agent-profiles"></a>快照代理配置文件  
 下表显示了快照代理的默认配置文件中定义的参数。 有关这些参数的详细信息，请参阅 [Replication Snapshot Agent](replication-snapshot-agent.md)。  
  
||默认值|  
|-|-------------|  
|**-BcpBatchSize**|100000|  
|**-HistoryVerboseLevel**|2|  
|**-LoginTimeout**|15|  
|**-QueryTimeout**|1800|  
  
## <a name="log-reader-agent-profiles"></a>日志读取器代理配置文件  
 下表显示了日志读取器代理的配置文件中定义的参数。 表中的每一列都表示一个已命名的配置文件。 有关这些参数的详细信息，请参阅 [Replication Log Reader Agent](replication-log-reader-agent.md)。  
  
||默认值|详细历史记录|  
|-|-------------|---------------------|  
|**-HistoryVerboseLevel**|@shouldalert|2|  
|**-LoginTimeout**|15|15|  
|**-LogScanThreshold**|500000|500000|  
|**-PollingInterval**|5|5|  
|**-QueryTimeout**|1800|1800|  
|**-ReadBatchSize**|500|500|  
  
## <a name="distribution-agent-profiles"></a>分发代理配置文件  
 下表显示了分发代理的配置文件中定义的参数。 表中的每一列都表示一个已命名的配置文件。 有关这些参数的详细信息，请参阅 [Replication Distribution Agent](replication-distribution-agent.md)。  
  
||默认值|详细历史记录|Windows 同步管理器|出现数据一致性错误时继续|OLEDB 流的分发配置文件|  
|-|-------------|---------------------|-------------------------------------|-----------------------------------------|----------------------------------------------|  
|**-BcpBatchSize**|100000|100000|1000|100000|2147473647|  
|**-CommitBatchSize**|100|100|100|100|100|  
|**-CommitBatchThreshold**|1000|1000|1000|1000|1000|  
|**-HistoryVerboseLevel**|@shouldalert|2|@shouldalert|@shouldalert|@shouldalert|  
|**-KeepAliveMessageInterval**|300|300|300|300|300|  
|**-LoginTimeout**|15|15|15|15|15|  
|**-MaxBcpThreads**|@shouldalert|@shouldalert|@shouldalert|@shouldalert|@shouldalert|  
|**-MaxDeliveredTransactions**|0|0|0|0|0|  
|**-OledbStreamThreshold**|NULL|NULL|NULL|NULL|32768|  
|**-PacketSize**|NULL|NULL|NULL|NULL|32768|  
|**-PollingInterval**|5|5|5|5|5|  
|**-QueryTimeout**|1800|1800|1800|1800|1800|  
|**-SkipErrors**|NULL|NULL|NULL|**-SkipErrors** 2601:2627:20598|NULL|  
|**-TransactionsPerHistory**|100|100|100|100|100|  
|**-UseOledbStreaming**|NULL|NULL|NULL|NULL|**-UseOledbStreaming**|  
  
## <a name="merge-agent-profiles"></a>合并代理配置文件  
 下表显示了合并代理的配置文件中定义的参数。 表中的每一列都表示一个已命名的配置文件。 有关这些参数的详细信息，请参阅 [Replication Merge Agent](replication-merge-agent.md)。  
  
||默认值|详细历史记录|Windows 同步管理器|行计数验证|行计数和校验和验证|慢速链接|高卷服务器对服务器|  
|-|-------------|---------------------|-------------------------------------|-------------------------|--------------------------------------|---------------|------------------------------------|  
|**-BcpBatchSize**|100000|100000|1000|100000|100000|100000|100000|  
|**-ChangesPerHistory**|100|50|50|100|100|100|1000|  
|**-DestThreads**|2|@shouldalert|@shouldalert|@shouldalert|@shouldalert|@shouldalert|4|  
|**-DownloadGenerationsPerBatch**|50|50|50|50|50|@shouldalert|500|  
|**-DownloadReadChangesPerBatch**|100|100|100|100|100|100|100|  
|**-DownloadWriteChangesPerBatch**|100|100|100|100|100|100|100|  
|**-FastRowCount**|@shouldalert|@shouldalert|@shouldalert|@shouldalert|@shouldalert|@shouldalert|@shouldalert|  
|**-HistoryVerboseLevel**|2|3|@shouldalert|@shouldalert|2|@shouldalert|2|  
|**-KeepAliveMessageInterval**|300|300|300|300|300|300|300|  
|**-LoginTimeout**|15|15|15|15|15|15|15|  
|**-MaxDownloadChanges**|0|0|0|0|0|0|0|  
|**-MaxUploadChanges**|0|0|0|0|0|0|0|  
|**-MetadataRetentionCleanup**|@shouldalert|@shouldalert|@shouldalert|@shouldalert|@shouldalert|@shouldalert|@shouldalert|  
|**-NumDeadlockRetries**|5|5|5|5|5|5|5|  
|**-ParallelUploadDownload**|NULL|NULL|NULL|NULL|NULL|NULL|@shouldalert|  
|**-PollingInterval**|60|60|60|60|60|60|60|  
|**-QueryTimeout**|300|300|300|300|300|300|600|  
|**-QueueSizeMultiplier**|NULL|NULL|NULL|NULL|NULL|NULL|5|  
|**-SrcThreads**|2|2|2|2|2|@shouldalert|3|  
|**-StartQueueTimeout**|0|0|0|0|0|0|0|  
|**-UploadGenerationsPerBatch**|50|50|50|50|50|@shouldalert|500|  
|**-UploadReadChangesPerBatch**|100|100|100|100|100|100|100|  
|**-UploadWriteChangesPerBatch**|100|100|100|100|100|100|100|  
|**-Validate**|0|0|0|@shouldalert|3|0|0|  
|**-ValidateInterval**|60|60|60|60|60|60|60|  
  
## <a name="queue-reader-agent-profiles"></a>队列读取器代理配置文件  
 下表显示了队列读取器代理的默认配置文件中定义的参数。 有关这些参数的详细信息，请参阅 [Replication Queue Reader Agent](replication-queue-reader-agent.md)。  
  
||默认值|  
|-|-------------|  
|**-HistoryVerboseLevel**|@shouldalert|  
|**-LoginTimeout**|15|  
|**-PollingInterval**|5|  
|**-QueryTimeout**|1800|  
  
## <a name="see-also"></a>请参阅  
 [复制代理管理](replication-agent-administration.md)   
 [查看和修改复制代理命令提示符参数 (SQL Server Management Studio)](view-and-modify-replication-agent-command-prompt-parameters.md)   
 [Replication Agent Executables Concepts](../concepts/replication-agent-executables-concepts.md)  
  
  