---
title: "以编程方式监视复制 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "TSQL"
helpviewer_keywords: 
  - "sp_replmonitorhelppublisher"
  - "sp_replmonitorhelpmergesessiondetail"
  - "监视性能 [SQL Server 复制], 发布状态"
  - "sp_replmonitorhelpmergesession"
  - "sp_replmonitorhelppublicationthresholds"
  - "监视性能 [SQL Server 复制], 订阅状态"
  - "监视性能 [SQL Server 复制], Transact-SQL 编程"
  - "sp_replmonitorsubscriptionpendingcmds"
  - "sp_replmonitorchangepublicationthreshold"
  - "事务复制, 监视"
  - "sp_replmonitorhelppublication"
  - "sp_replmonitorhelpsubscription"
  - "监视性能 [SQL Server 复制], 阈值和警告"
  - "合并复制监视 [SQL Server 复制]"
  - "快照复制 [SQL Server], 监视"
ms.assetid: e8bf8850-8da5-4a4f-a399-64232b4e476d
caps.latest.revision: 34
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 34
---
# 以编程方式监视复制
  复制监视器是一种可用于监视复制拓扑的图形化工具。 可以使用 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 复制存储过程或复制管理对象 (RMO) 以编程方式访问相同的监视数据。 您可以利用这些对象对以下任务进行编程：  
  
-   监视发布服务器、发布和订阅的状态。  
  
-   监视一个或多个订阅服务器上的合并代理会话。  
  
-   监视等待在一个或多个订阅服务器上应用的事务处理命令。  
  
-   定义用于确定发布何时需要干预的阈值标准。  
  
-   监视跟踪令牌的状态。  
  
 **本主题内容：**  
  
 [Transact-SQL](#Tsql)  
  
 [复制管理对象 (RMO)](#RMO)  
  
##  <a name="Tsql"></a> Transact-SQL  
  
#### 从分发服务器监视发布服务器、发布和订阅  
  
1.  在分发数据库上分发服务器上，执行 [sp_replmonitorhelppublisher](../../../relational-databases/system-stored-procedures/sp-replmonitorhelppublisher-transact-sql.md)。 这将返回使用此分发服务器的所有发布服务器的监视信息。 若要将结果集限制在单个发布服务器范围之内，请指定 **@publisher**。  
  
2.  在分发数据库上分发服务器上，执行 [sp_replmonitorhelppublication](../../../relational-databases/system-stored-procedures/sp-replmonitorhelppublication-transact-sql.md)。 这将返回使用此分发服务器的所有发布的监视信息。 若要限制到单个发布服务器、 发布或已发布的数据库的结果集，请指定 **@publisher**, ，**@publication**, ，或 **@publisher_db**, 分别。  
  
3.  在分发数据库上分发服务器上，执行 [sp_replmonitorhelpsubscription](../../../relational-databases/system-stored-procedures/sp-replmonitorhelpsubscription-transact-sql.md)。 这将返回使用此分发服务器的所有订阅的监视信息。 若要限制结果集属于单个发布服务器订阅，发布或已发布的数据库中，指定 **@publisher**, ，**@publication**, ，或 **@publisher_db**, 分别。  
  
#### 监视等待在订阅服务器上应用的事务处理命令  
  
1.  在分发数据库上分发服务器上，执行 [sp_replmonitorsubscriptionpendingcmds](../../../relational-databases/system-stored-procedures/sp-replmonitorsubscriptionpendingcmds-transact-sql.md)。 这将返回为使用此分发服务器的所有订阅挂起的所有命令的监视信息。 若要限制结果集为属于单个发布服务器订阅的挂起的命令，订阅服务器、 发布或已发布的数据库指定 **@publisher**, ，**@subscriber**, ，**@publication**, ，或 **@publisher_db**, 分别。  
  
#### 监视等待上载或下载的合并更改  
  
1.  在发布服务器上对发布数据库中，执行 [sp_showpendingchanges](../../../relational-databases/system-stored-procedures/sp-showpendingchanges-transact-sql.md)。 这将返回一个结果集，其中显示了有关等待复制到订阅服务器的更改的信息。 若要将结果集限制在属于单个发布或项目的更改范围之内，请分别指定 **@publication** 或 **@article**。  
  
2.  在订阅数据库上的订阅服务器上，执行 [sp_showpendingchanges](../../../relational-databases/system-stored-procedures/sp-showpendingchanges-transact-sql.md)。 这将返回一个结果集，其中显示了有关等待复制到发布服务器的更改的信息。 若要将结果集限制在属于单个发布或项目的更改范围之内，请分别指定 **@publication** 或 **@article**。  
  
#### 监视合并代理会话  
  
1.  在分发数据库上分发服务器上，执行 [sp_replmonitorhelpmergesession](../../../relational-databases/system-stored-procedures/sp-replmonitorhelpmergesession-transact-sql.md)。 这将返回监视信息，包括 **Session_id**, ，有关使用此分发服务器的所有订阅的所有合并代理会话。 您还可以获取 **Session_id** 通过查询 [MSmerge_sessions](../../../relational-databases/system-tables/msmerge-sessions-transact-sql.md) 系统表。  
  
2.  在分发数据库上分发服务器上，执行 [sp_replmonitorhelpmergesessiondetail](../../../relational-databases/system-stored-procedures/sp-replmonitorhelpmergesessiondetail-transact-sql.md)。 指定 **Session_id** 步骤 1 中的值 **@session_id**。 这将显示有关该会话的详细监视信息。  
  
3.  为每个相关会话重复步骤 2。  
  
#### 从订阅服务器监视请求订阅的合并代理会话  
  
1.  在订阅服务器上的订阅数据库上，执行 [sp_replmonitorhelpmergesession](../../../relational-databases/system-stored-procedures/sp-replmonitorhelpmergesession-transact-sql.md)。 对于给定的订阅，指定 **@publisher**, ，**@publication**, ，和发布数据库的名称 **@publisher_db**。 这将为此订阅的最后五个合并代理会话返回监视信息。 记下的值 **Session_id** 对于结果中的相关会话的设置。  
  
2.  在订阅服务器上的订阅数据库上，执行 [sp_replmonitorhelpmergesessiondetail](../../../relational-databases/system-stored-procedures/sp-replmonitorhelpmergesessiondetail-transact-sql.md)。 指定 **Session_id** 步骤 1 中的值 **@session_id**。 这将显示有关该会话的详细监视信息。  
  
3.  为每个相关会话重复步骤 2。  
  
#### 查看和修改发布的监视阈值标准  
  
1.  在分发数据库上分发服务器上，执行 [sp_replmonitorhelppublicationthresholds](../../../relational-databases/system-stored-procedures/sp-replmonitorhelppublicationthresholds-transact-sql.md)。 这将返回为使用此分发服务器的所有发布设置的监视阈值。 若要限制结果集以监视阈值属于单个发布服务器或已发布的数据库或属于单个发布，请指定 **@publisher**, ，**@publisher_db**, ，或 **@publication**, 分别。 记下的值 **Metric_id** 必须更改任何阈值。 有关详细信息，请参阅 [Set Thresholds and Warnings in Replication Monitor](../../../relational-databases/replication/monitor/set-thresholds-and-warnings-in-replication-monitor.md)。  
  
2.  在分发数据库上分发服务器上，执行 [sp_replmonitorchangepublicationthreshold](../../../relational-databases/system-stored-procedures/sp-replmonitorchangepublicationthreshold-transact-sql.md)。 根据需要指定下列参数：  
  
    -    **Metric_id** 在步骤 1 中获取值 **@metric_id**。  
  
    -   为 **@value**指定监视阈值标准的新值。  
  
    -   将 **@shouldalert** 的值指定为 **1** 以在达到此阈值时记录警报；如果不需要警报，则指定为 **0** 。  
  
    -   将 **@mode** 的值指定为 **1** 以启用监视阈值指标，或指定为 **2** 以禁用它。  
  
##  <a name="RMO"></a> 复制管理对象 (RMO)  
  
#### 监视对订阅服务器上的合并发布的订阅  
  
1.  通过使用创建连接到订阅服务器 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 类。  
  
2.  创建的实例 <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor> 类，并将设置 <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.Publisher%2A>, ，<xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.Publication%2A>, ，<xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.PublisherDB%2A>, ，<xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.SubscriberDB%2A> 属性的订阅，并设置 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 属性设置为 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 步骤 1 中创建。  
  
3.  调用以下方法之一返回有关该订阅的合并代理会话的信息：  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetSessionsSummary%2A> -返回一组 <xref:Microsoft.SqlServer.Replication.MergeSessionSummary> 上最多最后五个合并代理会话对象的信息。 请注意 <xref:Microsoft.SqlServer.Replication.MergeSessionSummary.SessionId%2A> 感兴趣的任何会话的值。  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetSessionsSummary%2A> -返回一组 <xref:Microsoft.SqlServer.Replication.MergeSessionSummary> 对象的前面几个小时作为传入过程中已发生的合并代理会话的信息与 *小时* （最多最后五个会话） 的参数。 请注意 <xref:Microsoft.SqlServer.Replication.MergeSessionSummary.SessionId%2A> 感兴趣的任何会话的值。  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetLastSessionSummary%2A> -返回 <xref:Microsoft.SqlServer.Replication.MergeSessionSummary> 对象上的最后一个合并代理会话的信息。 请注意 <xref:Microsoft.SqlServer.Replication.MergeSessionSummary.SessionId%2A> 此会话的值。  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetSessionsSummaryDataSet%2A> -返回 <xref:System.Data.DataSet> 最多最后五个合并代理会话，每行上对象的信息。 记下的值 **Session_id** 感兴趣的任何会话的列。  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetLastSessionSummaryDataRow%2A> -返回 <xref:System.Data.DataRow> 对象上的最后一个合并代理会话的信息。 记下的值 **Session_id** 此会话的列。  
  
4.  （可选）调用 <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.RefreshSessionSummary%2A> 若要刷新的数据 <xref:Microsoft.SqlServer.Replication.MergeSessionSummary> 对象作为传递 *mss，* 或致电 <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.RefreshSessionSummary%2A> 刷新中的数据 <xref:System.Data.DataRow> 对象作为传递 *drRefresh*。  
  
5.  使用步骤 3 中获取的会话 ID 调用以下方法之一，以返回有关特定会话的详细信息：  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetSessionDetails%2A> -返回一组 <xref:Microsoft.SqlServer.Replication.MergeSessionDetail> 对象提供 *SessionId*。  
  
    -   <xref:Microsoft.SqlServer.Replication.MergeSubscriberMonitor.GetSessionDetailsDataSet%2A> -返回 <xref:System.Data.DataSet> 信息指定对象 *SessionId*。  
  
#### 监视分发服务器上所有发布的复制属性  
  
1.  通过使用创建连接到分发服务器 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 类。  
  
2.  创建的实例 <xref:Microsoft.SqlServer.Replication.ReplicationMonitor> 类。  
  
3.  设置 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 属性设置为 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 步骤 1 中创建。  
  
4.  调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法以获取该对象的属性。  
  
5.  执行以下一种或多种方法返回使用该分发服务器的所有发布服务器的复制信息。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumDistributionAgents%2A> -返回 <xref:System.Data.DataSet> 对象，其中包含有关此分发服务器上的所有分发代理的信息。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumErrorRecords%2A> -返回 <xref:System.Data.DataSet> 对象，其中包含有关分发服务器上存储的错误的信息。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumLogReaderAgents%2A> -返回 <xref:System.Data.DataSet> 对象，其中包含有关分发服务器上的所有日志读取器代理的信息。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumMergeAgents%2A> -返回 <xref:System.Data.DataSet> 对象，其中包含有关分发服务器上的所有合并代理的信息。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumMiscellaneousAgents%2A> -返回 <xref:System.Data.DataSet> 对象，其中包含有关分发服务器上的所有其他复制代理的信息。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumPublishers%2A> -返回 <xref:System.Data.DataSet> 对象，其中包含有关此分发服务器上的所有发布服务器的信息。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumPublishers2%2A> -返回 <xref:System.Data.DataSet> 返回使用此分发服务器的发布者的对象。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumQueueReaderAgents%2A> -返回 <xref:System.Data.DataSet> 对象，其中包含有关分发服务器上的所有队列读取器代理的信息。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumQueueReaderAgentSessionDetails%2A> -返回 <xref:System.Data.DataSet> 对象，其中包含有关指定的队列读取器代理和会话的详细信息。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumQueueReaderAgentSessions%2A> -返回 <xref:System.Data.DataSet> 对象，其中包含有关指定的队列读取器代理会话信息。  
  
    -   <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.EnumSnapshotAgents%2A> -返回 <xref:System.Data.DataSet> 对象，其中包含有关分发服务器上的所有快照代理的信息。  
  
#### 监视分发服务器上特定发布服务器的发布属性  
  
1.  通过使用创建连接到分发服务器 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 类。  
  
2.  获取 <xref:Microsoft.SqlServer.Replication.PublisherMonitor> 中通过以下方式之一的对象。  
  
    -   创建的实例 <xref:Microsoft.SqlServer.Replication.PublisherMonitor> 类。 设置 <xref:Microsoft.SqlServer.Replication.PublisherMonitor.Name%2A> 属性的发布服务器上，并设置 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 属性设置为 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 步骤 1 中创建。 调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法以获取该对象的属性。 如果该方法返回 **false**，则表示发布服务器名称定义不正确或表示该发布不存在。  
  
    -   从 <xref:Microsoft.SqlServer.Replication.PublisherMonitorCollection> 访问通过 <xref:Microsoft.SqlServer.Replication.ReplicationMonitor.PublisherMonitors%2A> 属性的现有 <xref:Microsoft.SqlServer.Replication.ReplicationMonitor> 对象。  
  
3.  执行以下一种或多种方法返回有关属于该发布服务器的所有发布的复制信息。  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumDistributionAgentSessionDetails%2A> -返回 <xref:System.Data.DataSet> 对象，其中包含有关指定分发代理和会话的详细信息。  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumDistributionAgentSessions%2A> -返回 <xref:System.Data.DataSet> 对象，其中包含有关指定的分发代理会话信息。  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumErrorRecords%2A> -返回 <xref:System.Data.DataSet> 对象，其中包含有关指定的错误的错误记录信息。  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumLogReaderAgentSessionDetails%2A> -返回 <xref:System.Data.DataSet> 对象，其中包含指定的日志读取器代理和会话的详细信息。  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumLogReaderAgentSessions%2A> -返回 <xref:System.Data.DataSet> 对象，其中包含指定的日志读取器代理会话信息。  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumMergeAgentSessionDetails%2A> -返回 <xref:System.Data.DataSet> 对象，其中包含有关指定的合并代理和会话的详细信息。  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumMergeAgentSessionDetails2%2A> -返回 <xref:System.Data.DataSet> 对象，其中包含有关指定的合并代理和会话的其他详细信息。  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumMergeAgentSessions%2A> -返回 <xref:System.Data.DataSet> 对象，其中包含指定的合并代理会话信息。  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumMergeAgentSessions2%2A> -返回 <xref:System.Data.DataSet> 对象，其中包含指定的合并代理的其他会话信息。  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumPublications%2A> -返回 <xref:System.Data.DataSet> 对象，其中包含有关此分发服务器上的所有发布的信息。  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumPublications2%2A> -返回 <xref:System.Data.DataSet> 对象，其中包含有关此分发服务器上的所有发布的其他信息。  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumSnapshotAgentSessionDetails%2A> -返回 <xref:System.Data.DataSet> 对象，其中包含有关指定快照代理和会话的详细信息。  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumSnapshotAgentSessions%2A> -返回 <xref:System.Data.DataSet> 对象，其中包含指定的快照代理会话信息。  
  
    -   <xref:Microsoft.SqlServer.Replication.PublisherMonitor.EnumSubscriptions%2A> -返回 <xref:System.Data.DataSet> 对象，其中包含有关对此分发服务器上发布的所有订阅的信息。  
  
#### 监视分发服务器上的特定发布的属性  
  
1.  通过使用创建连接到分发服务器 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 类。  
  
2.  获取 <xref:Microsoft.SqlServer.Replication.PublicationMonitor> 中通过以下方式之一的对象。  
  
    -   创建的实例 <xref:Microsoft.SqlServer.Replication.PublicationMonitor> 类。 设置 <xref:Microsoft.SqlServer.Replication.PublicationMonitor.DistributionDBName%2A>, ，<xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublisherName%2A>, ，<xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublicationDBName%2A>, ，和 <xref:Microsoft.SqlServer.Replication.PublicationMonitor.Name%2A> 属性的发布，并设置 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 属性设置为 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 步骤 1 中创建。 调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法以获取该对象的属性。 如果该方法返回 **false**，则表示发布属性定义不正确，或表示该发布不存在。  
  
    -   从 <xref:Microsoft.SqlServer.Replication.PublicationMonitorCollection> 访问通过 <xref:Microsoft.SqlServer.Replication.PublisherMonitor.PublicationMonitors%2A> 属性的现有 <xref:Microsoft.SqlServer.Replication.PublisherMonitor> 对象。  
  
3.  执行以下一种或多种方法返回有关此发布的信息。  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumErrorRecords%2A> -返回 <xref:System.Data.DataSet> 对象，其中包含有关指定的错误的错误记录。  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumLogReaderAgent%2A> -返回 <xref:System.Data.DataSet> 对象，其中包含有关此发布的日志读取器代理的信息。  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumMonitorThresholds%2A> -返回 <xref:System.Data.DataSet> 为此发布的对象，其中包含有关监视器警告阈值的信息设置。  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumQueueReaderAgent%2A> -返回 <xref:System.Data.DataSet> 对象，其中包含有关使用此发布的队列读取器代理的信息。  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumSnapshotAgent%2A> -返回 <xref:System.Data.DataSet> 对象，其中包含有关此发布的快照代理的信息。  
  
    -   <xref:Microsoft.SqlServer.Replication.Publication.EnumSubscriptions%2A> -返回 <xref:System.Data.DataSet> 对象，其中包含有关对此发布的订阅的信息。  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumSubscriptions2%2A> -返回 <xref:System.Data.DataSet> 对象，其中包含有关对此发布的订阅的其他信息基于提供 <xref:Microsoft.SqlServer.Replication.SubscriptionResultOption>。  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumTracerTokenHistory%2A> -返回 <xref:System.Data.DataSet> 对象，其中包含指定的跟踪令牌的滞后时间信息。  
  
    -   <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumTracerTokens%2A> -返回 <xref:System.Data.DataSet> 对象，其中包含有关插入到此发布的所有跟踪令牌的信息。  
  
#### 监视正等待在订阅服务器上应用的事务处理命令  
  
1.  通过使用创建连接到分发服务器 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 类。  
  
2.  获取 <xref:Microsoft.SqlServer.Replication.PublicationMonitor> 中通过以下方式之一的对象。  
  
    -   创建的实例 <xref:Microsoft.SqlServer.Replication.PublicationMonitor> 类。 设置 <xref:Microsoft.SqlServer.Replication.PublicationMonitor.DistributionDBName%2A>, ，<xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublisherName%2A>, ，<xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublicationDBName%2A>, ，和 <xref:Microsoft.SqlServer.Replication.PublicationMonitor.Name%2A> 属性的发布，并设置 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 属性设置为 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 步骤 1 中创建。 调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法以获取该对象的属性。 如果该方法返回 **false**，则表示发布属性定义不正确，或表示该发布不存在。  
  
    -   从 <xref:Microsoft.SqlServer.Replication.PublicationMonitorCollection> 访问通过 <xref:Microsoft.SqlServer.Replication.PublisherMonitor.PublicationMonitors%2A> 属性的现有 <xref:Microsoft.SqlServer.Replication.PublisherMonitor> 对象。  
  
3.  执行 <xref:Microsoft.SqlServer.Replication.PublicationMonitor.TransPendingCommandInfo%2A> 方法，它返回 <xref:Microsoft.SqlServer.Replication.PendingCommandInfo> 对象。  
  
4.  使用此属性 <xref:Microsoft.SqlServer.Replication.PendingCommandInfo> 对象，以确定的挂起命令的估计的数和所需完成的这些命令传递的时间长度。  
  
#### 为发布设置监视器警告阈值  
  
1.  通过使用创建连接到分发服务器 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 类。  
  
2.  获取 <xref:Microsoft.SqlServer.Replication.PublicationMonitor> 中通过以下方式之一的对象。  
  
    -   创建的实例 <xref:Microsoft.SqlServer.Replication.PublicationMonitor> 类。 设置 <xref:Microsoft.SqlServer.Replication.PublicationMonitor.DistributionDBName%2A>, ，<xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublisherName%2A>, ，<xref:Microsoft.SqlServer.Replication.PublicationMonitor.PublicationDBName%2A>, ，和 <xref:Microsoft.SqlServer.Replication.PublicationMonitor.Name%2A> 属性的发布，并设置 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 属性设置为 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 步骤 1 中创建。 调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法以获取该对象的属性。 如果该方法返回 **false**，则表示发布属性定义不正确，或表示该发布不存在。  
  
    -   从 <xref:Microsoft.SqlServer.Replication.PublicationMonitorCollection> 访问通过 <xref:Microsoft.SqlServer.Replication.PublisherMonitor.PublicationMonitors%2A> 属性的现有 <xref:Microsoft.SqlServer.Replication.PublisherMonitor> 对象。  
  
3.  执行 <xref:Microsoft.SqlServer.Replication.PublicationMonitor.EnumMonitorThresholds%2A> 方法。 请注意在返回的当前阈值设置 <xref:System.Collections.ArrayList> 的 <xref:Microsoft.SqlServer.Replication.MonitorThreshold> 对象。  
  
4.  执行 <xref:Microsoft.SqlServer.Replication.PublicationMonitor.ChangeMonitorThreshold%2A> 方法。 传递以下参数：  
  
    -   *metricID* - <xref:System.Int32> 值，该值表示从下表中的监视阈值指标︰  
  
        |值|说明|  
        |-----------|-----------------|  
        |1|**过期** -监视对事务发布的订阅是否即将过期。|  
        |2|**延迟** -监视对事务发布的订阅的性能。|  
        |4|**mergeexpiration** -监视的订阅是否即将过期合并发布。|  
        |5|**mergeslowrunduration** -监视通过低带宽 （拨号） 连接的合并同步的持续时间。|  
        |6|**mergefastrunduration** -监视通过高带宽 (LAN) 连接的合并同步的持续时间。|  
        |7|**mergefastrunspeed** -监视通过高带宽 (LAN) 连接的合并同步的同步速率。|  
        |8|**mergeslowrunspeed** -监视通过低带宽 （拨号） 连接进行的合并同步的同步速率。|  
  
    -   *启用* - <xref:System.Boolean> 值，该值指示是否为发布启用指标。  
  
    -   *thresholdValue* -设置的阈值的整数值。  
  
    -   *shouldAlert* 的整数，指示此阈值是否应生成警报。  
  
  