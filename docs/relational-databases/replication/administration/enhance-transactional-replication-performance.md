---
title: "增强事务复制性能 | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- publications [SQL Server replication], design and performance
- performance [SQL Server replication], transactional replication
- designing databases [SQL Server], replication performance
- performance [SQL Server replication], snapshot replication
- snapshot replication [SQL Server], performance
- subscriptions [SQL Server replication], performance considerations
- agents [SQL Server replication], performance
- Distribution Agent, performance
- transactional replication, performance
- Log Reader Agent, performance
ms.assetid: 67084a67-43ff-4065-987a-3b16d1841565
caps.latest.revision: "39"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ac5c385cfdff8c4c024c02534d8c040534c400ca
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="enhance-transactional-replication-performance"></a>增强事务复制性能
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]在考虑[增强常规复制性能](../../../relational-databases/replication/administration/enhance-general-replication-performance.md)中介绍的常规性能提示后，还需要考虑特定于事务复制的其他几个方面。  
  
## <a name="database-design"></a>数据库设计  
  
-   在应用程序设计中，最大限度地减小事务大小。  
  
     默认情况下，事务复制根据事务边界传播更改。 如果事务越小，则分发代理因网络问题而重新发送事务的可能性就越小。 如果重新发送事务需要代理，则发送的数据量会较小。  
  
## <a name="distributor-configuration"></a>分发服务器配置  
  
-   在专用服务器上配置分发服务器。  
  
     通过配置远程分发服务器可以减少发布服务器的处理开销。 有关详细信息，请参阅[配置分发](../../../relational-databases/replication/configure-distribution.md)。  
  
-   适当调整分发数据库的大小。  
  
     在系统承受典型负载的情况下对复制进行测试，以确定存储命令需要多少空间。 确保数据库足以存储命令，而无需频繁地自动增大。 有关更改数据库大小的详细信息，请参阅 [ALTER DATABASE (Transact-SQL)](../../../t-sql/statements/alter-database-transact-sql.md)。  
  
## <a name="publication-design"></a>发布设计  
  
-   在对已发布的表进行批更新时，复制存储过程执行。  
  
     如果所做的批处理更新有时会影响订阅服务器上的大量行，则应考虑使用存储过程更新已发布的表，并发布存储过程的执行。 分发代理不是为每个受影响的行都发送一个更新或删除，而是在订阅服务器上用相同的参数值执行相同的过程。 有关详细信息，请参阅 [Publishing Stored Procedure Execution in Transactional Replication](../../../relational-databases/replication/transactional/publishing-stored-procedure-execution-in-transactional-replication.md)。  
  
-   将项目分布在多个发布上。  
  
     如果不能使用 **-SubscriptionStreams** 参数（将在本主题的后面部分进行介绍），请考虑创建多个发布。 将项目分布在这些发布上使复制可以并行地将更改应用到订阅服务器。  
  
## <a name="subscription-considerations"></a>订阅注意事项  
  
-   如果在相同的发布服务器中拥有多个发布（这是新建发布向导中的默认情况），则使用独立代理而非共享代理。  
  
-   连续运行而不是按非常频繁的计划运行代理。  
  
     将代理设置为连续运行而不是创建频繁的计划（如每分钟）会提高复制性能，因为代理不必启动和停止。 将分发代理设置为连续运行后，以低滞后时间将更改传播到拓扑中连接的其他服务器。 有关详细信息，请参阅：  
  
    -   [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]：[指定同步计划](../../../relational-databases/replication/specify-synchronization-schedules.md)  
  
## <a name="distribution-agent-and-log-reader-agent-parameters"></a>分发代理和日志读取器代理参数  
  
-   要解决意外、一次性瓶颈，请使用日志读取器代理的 **–MaxCmdsInTran** 参数。  
  
     **–MaxCmdsInTran** 参数指定日志读取器向分发数据库写入命令时组成一个事务的语句的最大数量。 使用此参数能够使日志读取器代理和分发代理在订阅服务器上应用命令时将发布服务器上的大事务（由许多命令组成）分成若干个较小的事务。 指定此参数可以减少分发服务器的争用问题并缩短发布服务器与订阅服务器之间的滞后时间。 由于初始事务是以较小的单元应用的，订阅服务器可以在初始事务结束之前访问一个较大的逻辑发布服务器事务的行，因而会破坏事务的原子性。 默认值为 0 ，这将保持发布服务器的事务边界。 此参数不适用于 Oracle 发布服务器。  
  
    > [!WARNING]  
    >  **MaxCmdsInTran** 并非始终开启。 其之所以存在，是为了解决某人在单个事务中意外执行了大量 DML 操作（在整个事务进入分发数据库并持有锁之前，导致命令分发延迟等）的问题。 如果您经常遇到这种情况，则应审查应用程序并找到减少事务大小的方法。  
  
-   为分发代理使用 **–SubscriptionStreams** 参数。  
  
     **–SubscriptionStreams** 参数可以显著提高聚合复制吞吐量。 它使到一台订阅服务器的多个连接可以并行应用批量更改，同时在使用单线程时保持多个事务特征的存在。 如果有一个连接无法执行或提交，则所有连接将中止当前批处理，而且代理将用单独的流重试失败的批处理。 在重试阶段完成之前，订阅服务器上会存在临时事务不一致。 失败的批处理成功提交后，订阅服务器将恢复到事务一致状态。  
  
     可以使用 [sp_addsubscription (Transact-SQL)](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md) 的 **@subscriptionstreams** 来指定此代理参数的值。  
  
-   增大日志读取器代理的 **-ReadBatchSize** 参数的值。  
  
     日志读取器代理和分发代理支持事务读取和提交操作的批大小。 批大小的默认值为 500 个事务。 日志读取器代理从日志中读取特定数量的事务，而不管这些事务是否标记为复制。 将大量事务写入发布数据库，而其中只有一小部分标记为复制时，则应使用 **-ReadBatchSize** 参数增加日志读取器代理的读取批大小。 此参数不适用于 Oracle 发布服务器。  
  
-   增大分发代理的 **-CommitBatchSize** 参数的值。  
  
     提交一组事务的开销是固定的；通过不经常提交大量事务，就可以将开销分散在大量数据上。 但是，增大此参数的优势因应用更改的开销由其他因素（例如包含日志的最大磁盘 I/O）限制而降低。 另外，需要考虑以下权衡问题：必须回滚任何导致分发代理重新开始的失败并重新应用大量事务。 对于不可靠的网络，越小的值导致失败的几率越小，如果导致失败，将回滚并重新应用较少量事务。  
  
-   减小日志读取器代理的 **-PollingInterval** 参数的值。  
  
     **-PollingInterval** 参数指定为要复制的事务查询已发布数据库的事务日志的频率。 默认值为 5 秒。 如果减小此值，日志的轮询将更加频繁，这会使事务从发布数据库传递到分发数据库的滞后时间较低。 但是，应该对较低滞后时间的需要和因频繁轮询导致的服务器上增加的负荷之间进行平衡。  
  
 代理参数可以在代理配置文件和命令行中指定。 有关详细信息，请参阅：  
  
-   [处理复制代理配置文件](../../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)  
  
-   [查看和修改复制代理命令提示符参数 &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/view-and-modify-replication-agent-command-prompt-parameters.md)  
  
-   [复制代理可执行文件概念](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)  
  
  
