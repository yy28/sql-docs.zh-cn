---
title: 监视 Always On 可用性组的性能 (SQL Server) | Microsoft Docs
ms.custom: ag-guide
ms.date: 06/13/2017
ms.prod: sql-server-2016
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: dfd2b639-8fd4-4cb9-b134-768a3898f9e6
caps.latest.revision: 13
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 6ad77dc80e9c54dffba133e06428dca24f2f704b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="monitor-performance-for-always-on-availability-groups"></a>监视 Always On 可用性组的性能
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Always On 可用性组的性能方面对维护任务关键型数据库的服务级别协议 (SLA) 至关重要。 了解可用性组如何将日志传送到次要副本有助于估计可用性实现的恢复时间目标 (RTO) 和恢复点目标 (RPO)，并识别执行效果不佳的可用性组或副本中的瓶颈。 本文介绍同步过程，演示如何计算一些关键指标，并提供一些常见性能故障排除方案的链接。  
  
 所涉及的主题如下：  
  
-   [数据同步过程](#BKMK_DATA_SYNC_PROCESS)  
  
-   [流控制门](#BKMK_FLOW_CONTROL_GATES)  
  
-   [估计故障转移时间 (RTO)](#BKMK_RTO)  
  
-   [估计可能的数据丢失 (RPO)](#BKMK_RPO)  
  
-   [监视 RTO 和 RPO](#BKMK_Monitoring_for_RTO_and_RPO)  
  
-   [性能故障排除方案](#BKMK_SCENARIOS)  
  
-   [有用的扩展事件](#BKMK_XEVENTS)  
  
##  <a name="BKMK_DATA_SYNC_PROCESS"></a>数据同步过程  
 若要估计完全同步的时间并识别瓶颈，需要了解同步过程。 性能瓶颈可能出现在过程中的任何位置，查找瓶颈有助于更深入发掘潜在的问题。 下图和下表说明了数据同步过程：  
  
 ![可用性组数据同步](media/always-onag-datasynchronization.gif "可用性组数据同步")  
  
|||||  
|-|-|-|-|  
|**序列**|**步骤说明**|**注释**|**有用的指标**|  
|@shouldalert|日志生成|日志数据已刷新到磁盘。 必须将此日志复制到次要副本。 日志记录会进入发送队列。|[SQL Server:Database > Log bytes flushed\sec](~/relational-databases/performance-monitor/sql-server-databases-object.md)|  
|2|捕获|捕获每个数据库的日志，并将其发送到相应的伙伴队列（每个数据库/副本对一个）。 只要已连接可用性副本且数据移动未因任何原因暂停，此捕获进程便会持续运行，并且数据库/副本对显示为“正在同步”或“已同步”。 如果捕获进程不能以足够快的速度扫描消息并将其排入队列，则会构建日志发送队列。|[SQL Server:Availability Replica > Bytes Sent to Replica\sec](~/relational-databases/performance-monitor/sql-server-availability-replica.md)，这是为该可用性副本排队的所有数据库消息总和的聚合。<br /><br /> 主要副本上的 [log_send_queue_size](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md) (KB) 和 [log_bytes_send_rate](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md)（KB/秒）。|  
|3|Send|每个数据库副本队列中的消息均取消排队，并跨网络发送到相应的次要副本。|[SQL Server:Availability Replica > Bytes sent to transport\sec](~/relational-databases/performance-monitor/sql-server-availability-replica.md) 和 [SQL Server:Availability Replica > Message Acknowledgement Time](~/relational-databases/performance-monitor/sql-server-availability-replica.md)（毫秒）|  
|4|接收和缓存|每个辅助副本都会接收并缓存消息。|性能计数器 [SQL Server:Availability Replica > Log Bytes Received/sec](~/relational-databases/performance-monitor/sql-server-availability-replica.md)|  
|5|强化|在次要副本上刷新日志以进行强化。 日志刷新后，会将确认发送回主要副本。<br /><br /> 强化日志后，即可避免数据丢失。|性能计数器 [SQL Server:Database > Log Bytes Flushed/sec](~/relational-databases/performance-monitor/sql-server-databases-object.md)<br /><br /> 等待类型 [HADR_LOGCAPTURE_SYNC](~/relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)|  
|6|重做|重做次要副本上的刷新页面。 页面在等待重做时会保留在重做队列中。|[SQL Server:Database Replica > Redone Bytes/sec](~/relational-databases/performance-monitor/sql-server-database-replica.md)<br /><br /> [redo_queue_size](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md) (KB) 和 [redo_rate](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md)。<br /><br /> 等待类型 [REDO_SYNC](~/relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)|  
  
##  <a name="BKMK_FLOW_CONTROL_GATES"></a>流控制门  
 可用性组在主要副本上设计有流控制门，可避免所有可用性副本上的资源（例如网络和内存资源）过度消耗。 这些流控制门不会影响可用性副本同步运行状况的状态，但它们会影响可用性数据库（包括 RPO）的整体性能。  
  
 在主要副本上捕获日志后，它们会受制于两个级别的流控制，如下表所示。  
  
|||||  
|-|-|-|-|  
|**Level**|**门数**|**消息数量**|**有用的指标**|  
|Transport|每个可用性副本 1 个|8192|扩展事件 database_transport_flow_control_action|  
|“数据库”|每个可用性数据库 1 个|11200 (x64)<br /><br /> 1600 (x86)|[DBMIRROR_SEND](~/relational-databases/system-dynamic-management-views/sys-dm-os-wait-stats-transact-sql.md)<br /><br /> 扩展事件 hadron_database_flow_control_action|  
  
 达到任一门的消息阈值后，则不再向特定副本或为特定数据库发送消息日志。 接收到已发送消息的确认消息，以使发送的消息数量低于阈值后，可以发送消息。  
  
 除了流控制门，还有另一个因素可阻止发送日志消息。 副本同步可确保按日志序列号 (LSN) 的顺序来发送和应用消息。 发送日志消息前，其 LSN 还会检查最低已确认的 LSN 号，确保其小于阈值之一（具体取决于消息类型）。 如果两个 LSN 号之间的差距大于阈值，则不会发送消息。 差距再次低于阈值后，则会发送消息。  
  
 两个有用的性能计数器，即 [SQL Server:Availability Replica > Flow control/sec](~/relational-databases/performance-monitor/sql-server-availability-replica.md) 和 [SQL Server:Availability Replica > Flow Control Time (ms/sec)](~/relational-databases/performance-monitor/sql-server-availability-replica.md)，会在最后一秒钟内显示激活流控制的次数以及等待流控制所花费的时间。 流控制的等待时间越长，转换的 RPO 越高。 有关导致流控制等待时间较长这一类型问题的详细信息，请参阅[故障排除：可用性组超过了 RPO](troubleshoot-availability-group-exceeded-rpo.md)。  
  
##  <a name="BKMK_RTO"></a>估计故障转移时间 (RTO)  
 SLA 中的 RTO 取决于 Always On 实现在任何给定时间的故障转移时间，可使用以下公式表示：  
  
 ![可用性组 RTO 计算](media/always-on-rto.gif "可用性组 RTO 计算")  
  
> [!IMPORTANT]  
>  如果可用性组包含多个可用性数据库，则具有最高 Tfailover 的可用性数据库会成为 RTO 符合性的限制值。  
  
 故障检测时间（即 Tdetection）是系统检测到故障所用的时间。 此时间取决于群集级别设置，而不是各个可用性副本。 根据配置的自动故障转移条件，可触发故障转移，作为对关键 SQL Server 内部错误（如孤立的自旋锁）的即时反应。 在这种情况下，检测速度可能与 [ sp_server_diagnostics &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-server-diagnostics-transact-sql.md) 错误报告发送到 WSFC 群集的速度相同（默认间隔为运行状况检查超时的 1/3）。 也可能因超时而触发故障转移，例如群集运行状况检查超时已过期（默认为 30 秒）或资源 DLL 和 SQL Server 实例之间的租约已过期（默认为 20 秒）。 在这种情况下，检测时间与超时间隔一样长。 有关详细信息，请参阅[针对可用性组的自动故障转移的灵活的故障转移策略 &#40;SQL Server&#41;](https://msdn.microsoft.com/library/hh710061(SQL.120).aspx)。  
  
 如果准备进行故障转移，次要副本唯一需要做的是让重做赶上日志的末尾。 重做时间（即 Tredo）使用以下公式进行计算：  
  
 ![可用性组重做时间计算](media/always-on-redo.gif "可用性组重做时间计算")  
  
 其中，redo_queue 是 [redo_queue_size](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md) 中的值，redo_rate 是 [redo_rate](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md) 中的值。  
  
 故障转移系统开销时间（即 Toverhead）包括对 WSFC 群集进行故障转移和将数据库联机所用的时间。 此时间通常较短且比较固定。  
  
##  <a name="BKMK_RPO"></a>估计可能的数据丢失 (RPO)  
 SLA 中的 RPO 取决于 Always On 实现在任何给定时间可能的数据丢失。 此可能的数据丢失可以使用以下公式进行表示：  
  
 ![可用性组 RPO 计算](media/always-on-rpo.gif "可用性组 RPO 计算")  
  
 其中，log_send_queue 是 [log_send_queue_size](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md) 的值，日志生成速率是 [SQL Server:Database > Log Bytes Flushed/sec](~/relational-databases/performance-monitor/sql-server-databases-object.md) 的值。  
  
> [!WARNING]  
>  如果可用性组包含多个可用性数据库，则具有最高 Tdata_loss 的可用性数据库会成为 RPO 符合性的限制值。  
  
 日志发送队列表示可能因灾难性故障而丢失的所有数据。 初看上去，使用日志生成速率而不是日志发送速率很奇怪（请参阅 [log_send_rate](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md)）。 但请记住，使用日志发送速率仅提供同步时间，而 RPO 基于其生成速度（而不是同步速度）来衡量数据丢失。  
  
 估计 Tdata_loss 更为简单的方法是使用 [last_commit_time](~/relational-databases/system-dynamic-management-views/sys-dm-hadr-database-replica-states-transact-sql.md)。 主要副本上的 DMV 会为所有副本报告此值。 可以计算主要副本的值与次要副本的值之间的差值，从而估计次要副本上的日志追赶主要副本的速度。 如前面所述，此计算并不会根据生成日志的速度告知可能的数据丢失，但应为一个近似值。  
  
##  <a name="BKMK_Monitoring_for_RTO_and_RPO"></a>监视 RTO 和 RPO  
 本部分演示如何监视可用性组的 RTO 和 RPO 指标。 此演示类似于 [The Always On health model, part 2: Extending the health model](http://blogs.msdn.com/b/sqlalwayson/archive/2012/02/13/extending-the-alwayson-health-model.aspx)（Always On 运行状况模型，第二部分：扩展运行状况模型）中给出的 GUI 教程。  
  
 [估计故障转移时间 (RTO)](#BKMK_RTO) 和[估计可能的数据丢失 (RPO)](#BKMK_RPO) 中的故障转移时间和可能的数据丢失计算的元素，可方便地用作策略管理方面数据库副本状态中的性能指标（请参阅[查看 SQL Server 对象上基于策略的管理方面](~/relational-databases/policy-based-management/view-the-policy-based-management-facets-on-a-sql-server-object.md)）。 可以按计划监视这两个指标，并在指标分别超过 RTO 和 RPO 时发出警报。  
  
 演示的脚本创建了两个系统策略，它们按各自计划运行，并具有以下特征：  
  
-   估计的故障转移时间超过 10 分钟时，RTO 策略会失败，每 5 分钟评估一次  
  
-   估计的数据丢失超过 1 小时时，RPO 策略会失败，每 30 分钟评估一次  
  
-   两个策略在所有可用性副本上的配置相同  
  
-   所有服务器上都将评估策略，但仅在本地可用性副本是主要副本的可用性组上进行评估。 如果本地可用性副本不是主要副本，则不会评估策略。  
  
-   在主要副本上查看时，Always On 仪表板中可以很方便地显示策略失败情况。  

若要创建策略，请在参与可用性组的所有服务器实例上按照以下说明操作：  

1.  如果尚未启动，请[启动 SQL Server 代理服务](~/ssms/agent/start-stop-or-pause-the-sql-server-agent-service.md)。  
  
2.  在 SQL Server Management Studio 中，从“工具”菜单中，单击“选项”。  
  
3.  在“SQL Server Always On”选项卡上，选择“启用用户定义的 Always On 策略”，然后单击“确定”。  
  
     通过此设置，可在 Always On 仪表板中显示正确配置的自定义策略。  
  
4.  使用以下规范创建[基于策略的管理条件](~/relational-databases/policy-based-management/create-a-new-policy-based-management-condition.md)：  
  
    -   **名称**：`RTO`  
  
    -   **Facet**：数据库副本状态  
  
    -   **字段**：`Add(@EstimatedRecoveryTime, 60)`  
  
    -   **运算符**：<=  
  
    -   **值**：`600`  
  
     如果潜在故障转移时间超过 10 分钟（包含用于故障检测和故障转移的 60 秒开销），此条件会失败。  
  
5.  使用以下规范创建第二个[基于策略的管理条件](~/relational-databases/policy-based-management/create-a-new-policy-based-management-condition.md)：  
  
    -   **名称**：`RPO`  
  
    -   **Facet**：数据库副本状态  
  
    -   **字段**：`@EstimatedDataLoss`  
  
    -   **运算符**：<=  
  
    -   **值**：`3600`  
  
     如果可能的数据丢失超过 1 小时，则此条件会失败。  
  
6.  使用以下规范创建第三个[基于策略的管理条件](~/relational-databases/policy-based-management/create-a-new-policy-based-management-condition.md)：  
  
    -   **名称**：`IsPrimaryReplica`  
  
    -   **Facet**可用性组  
  
    -   **字段**：`@LocalReplicaRole`  
  
    -   **运算符**：=  
  
    -   **值**：`Primary`  
  
     此条件会检查给定的可用性组的本地可用性副本是否为主要副本。  
  
7.  使用以下规范创建[基于策略的管理策略](~/relational-databases/policy-based-management/create-a-policy-based-management-policy.md)：  
  
    -   “常规”页：  
  
        -   **名称**：`CustomSecondaryDatabaseRTO`  
  
        -   **检查条件**：`RTO`  
  
        -   **针对目标**：IsPrimaryReplica AvailabilityGroup 中的每个 DatabaseReplicaState  
  
             此设置确保仅在本地可用性副本是其主要副本的可用性组上对策略进行评估。  
  
        -   **评估模式**：按计划  
  
        -   **计划**：CollectorSchedule_Every_5min  
  
        -   **已启用**：已选中  
  
    -   “说明”页：  
  
        -   **类别**：可用性数据库警告  
  
             通过此设置，策略评估结果可显示在 Always On 仪表板中。  
  
        -   **说明**：当前副本的 RTO 超过 10 分钟，假定发现和故障转移的开销为 1 分钟。应立即调查相应服务器实例上的性能问题。  
  
        -   **要显示的文本**：RTO 已超出！  
  
8.  使用以下规范创建第二个[基于策略的管理策略](~/relational-databases/policy-based-management/create-a-policy-based-management-policy.md)：  
  
    -   “常规”页：  
  
        -   **名称**：`CustomAvailabilityDatabaseRPO`  
  
        -   **检查条件**：`RPO`  
  
        -   **针对目标**：IsPrimaryReplica AvailabilityGroup 中的每个 DatabaseReplicaState  
  
        -   **评估模式**：按计划  
  
        -   **计划**：CollectorSchedule_Every_30min  
  
        -   **已启用**：已选中  
  
    -   “说明”页：  
  
        -   **类别**：可用性数据库警告  
  
        -   **说明**：可用性数据库已超过时间为 1 小时的 RPO。应立即调查可用性副本上的性能问题。  
  
        -   **要显示的文本**：RPO 已超出！  
  
 操作完成后，会创建两个新的 SQL Server 代理作业，每个策略评估计划都会有一个作业。 这些作业的名称应以“syspolicy_check_schedule”开头。  
  
 可以查看作业历史记录，以检查评估结果。 评估失败情况还记录在事件为 ID 34052 的 Windows 应用程序日志中（事件查看器中）。 还可以配置 SQL Server 代理以发送有关策略失败的警报。 有关详细信息，请参阅[配置警报以通知策略管理员策略失败情况](~/relational-databases/policy-based-management/configure-alerts-to-notify-policy-administrators-of-policy-failures.md)。  
  
##  <a name="BKMK_SCENARIOS"></a>性能故障排除方案  
 下表列出了常见的与性能相关的故障排除方案。  
  
|应用场景|Description|  
|--------------|-----------------|  
|[疑难解答：可用性组超过了 RTO](troubleshoot-availability-group-exceeded-rto.md)|进行自动故障转移或计划的手动故障转移（无数据丢失）后，故障转移时间超过 RTO。 或者，在估计同步提交次要副本（如自动故障转移伙伴）的故障转移时间时，发现该时间超过 RTO。|  
|[疑难解答：可用性组超过了 RPO](troubleshoot-availability-group-exceeded-rpo.md)|执行强制手动故障转移后，数据丢失超过 RPO。 或者，在计算异步提交次要副本可能丢失的数据时，发现它超过了 RPO。|  
|[故障排除：主要副本的更改未反映在次要副本上](troubleshoot-primary-changes-not-reflected-on-secondary.md)|客户端应用程序在主要副本上成功完成更新，但查询次要副本显示更改未得到反映。|  
  
##  <a name="BKMK_XEVENTS"></a>有用的扩展事件  
 在对“正在同步”状态下的副本进行故障排除时，以下扩展事件很有用。  
  
|事件名称|类别|Channel|可用性副本|  
|----------------|--------------|-------------|--------------------------|  
|redo_caught_up|事务|调试|辅助副本|  
|redo_worker_entry|事务|调试|辅助副本|  
|hadr_transport_dump_message|`alwayson`|调试|主|  
|hadr_worker_pool_task|`alwayson`|调试|主|  
|hadr_dump_primary_progress|`alwayson`|调试|主|  
|hadr_dump_log_progress|`alwayson`|调试|主|  
|hadr_undo_of_redo_log_scan|`alwayson`|分析|辅助副本|  
  
  