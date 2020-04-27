---
title: 同步请求订阅 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- pull subscriptions [SQL Server replication], synchronizing
- synchronization [SQL Server replication], pull subscriptions
- subscriptions [SQL Server replication], pull
ms.assetid: 3ca24b23-fdc3-408e-8208-a2ace48fc8e3
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c8a7a607221599d599438352eab5add1cc94e5d7
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "63186229"
---
# <a name="synchronize-a-pull-subscription"></a>同步请求订阅
  本主题说明如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]复制代理 [或复制管理对象 (RMO) 在](agents/replication-agents-overview.md)中同步请求订阅。  
  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 订阅由分发代理（对于快照复制和事务复制）或合并代理（对于合并复制）进行同步。 代理可以连续运行、按需运行或按计划运行。 有关如何指定同步计划的详细信息，请参阅[指定同步计划](specify-synchronization-schedules.md)。  
  
 在 **中的** “本地订阅” [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]文件夹中，按需同步订阅。  
  
#### <a name="to-synchronize-a-pull-subscription-on-demand-in-management-studio"></a>在 Management Studio 中按需同步请求订阅  
  
1.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中连接到订阅服务器，然后展开服务器节点。  
  
2.  展开 **“复制”** 文件夹，再展开 **“本地订阅”** 文件夹。  
  
3.  右键单击要同步的订阅，然后单击 **“查看同步状态”**。  
  
4.  在“查看同步状态 - \<订阅服务器>:\<订阅数据库>”对话框中，单击“启动”。******** 完成同步后，将显示消息 **“同步完成”** 。  
  
5.  单击“**关闭**”。  
  
##  <a name="replication-agents"></a><a name="ReplProg"></a>复制代理  
 可通过在命令提示符下调用相应的复制代理可执行文件，以编程方式按需同步请求订阅。 被调用的复制代理可执行文件将取决于请求订阅所属的发布的类型。 有关详细信息，请参阅 [Replication Agents](agents/replication-agents-overview.md)。  
  
> [!NOTE]  
>  复制代理使用通过命令提示符启动该代理的用户的 Windows 身份验证凭据连接到本地服务器。 这些 Windows 凭据还在使用 Windows 集成身份验证连接到远程服务器时使用。  
  
#### <a name="to-start-the-distribution-agent-from-the-command-prompt-or-from-a-batch-file"></a>通过命令提示符或批处理文件启动分发代理  
  
1.  在命令提示符下或批处理文件中，通过运行 [distrib.exe](agents/replication-distribution-agent.md) 并指定下列命令行参数来启动 **复制分发代理**：  
  
    -   **-发布服务器**  
  
    -   **-PublisherDB**  
  
    -   **-分发服务器**  
  
    -   **-Distributorsecuritymode 指定** = **1**  
  
    -   **-订阅服务器**  
  
    -   **-SubscriberDB**  
  
    -   **-SubscriberSecurityMode** = **1**  
  
    -   **-SubscriptionType** = **1**  
  
     如果您使用的是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证，则还必须指定下列参数：  
  
    -   **-DistributorLogin**  
  
    -   **-DistributorPassword**  
  
    -   **-Distributorsecuritymode 指定** = **0**  
  
    -   **-PublisherLogin**  
  
    -   **-PublisherPassword**  
  
    -   **-Publishersecuritymode 指定** = **0**  
  
    -   **-SubscriberLogin**  
  
    -   **-SubscriberPassword**  
  
    -   **-SubscriberSecurityMode** = **0**  
  
#### <a name="to-start-the-merge-agent-from-the-command-prompt-or-from-a-batch-file"></a>在命令提示符下或批处理文件中启动合并代理  
  
1.  在命令提示符下或批处理文件中，通过运行 [replmerg.exe](agents/replication-merge-agent.md) 并指定下列命令行参数来启动 **复制合并代理**：  
  
    -   **-发布服务器**  
  
    -   **-PublisherDB**  
  
    -   **-Publishersecuritymode 指定** = **1**  
  
    -   **-发布**  
  
    -   **-分发服务器**  
  
    -   **-Distributorsecuritymode 指定** = **1**  
  
    -   **-订阅服务器**  
  
    -   **-SubscriberSecurityMode** = **1**  
  
    -   **-SubscriberDB**  
  
    -   **-SubscriptionType** = **1**  
  
     如果您使用的是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证，则还必须指定下列参数：  
  
    -   **-DistributorLogin**  
  
    -   **-DistributorPassword**  
  
    -   **-Distributorsecuritymode 指定** = **0**  
  
    -   **-PublisherLogin**  
  
    -   **-PublisherPassword**  
  
    -   **-Publishersecuritymode 指定** = **0**  
  
    -   **-SubscriberLogin**  
  
    -   **-SubscriberPassword**  
  
    -   **-SubscriberSecurityMode** = **0**  
  
###  <a name="examples-replication-agents"></a><a name="TsqlExample"></a> 示例（复制代理）  
 以下示例启动分发代理以同步请求订阅。 所有连接均使用 Windows 身份验证实现。  
  
 [!code-sql[HowTo#bat_synctranpullsub_10](../../snippets/tsql/SQL15/replication/howto/tsql/synctranpullsub_10.bat)]  
  
 以下示例启动合并代理以同步请求订阅。 所有连接均使用 Windows 身份验证实现。  
  
 [!code-sql[HowTo#bat_syncmergepullsub_10](../../snippets/tsql/SQL15/replication/howto/tsql/syncmergepullsub_10.bat)]  
  
##  <a name="using-replication-management-objects-rmo"></a><a name="RMOProcedure"></a> 使用复制管理对象 (RMO)  
 可以使用复制管理对象 (RMO) 和托管代码对复制代理功能的访问权限，以编程方式同步请求订阅。 用于同步请求订阅的类取决于订阅所属的发布的类型。  
  
> [!NOTE]  
>  如果您要启动一个自主运行而不影响应用程序的订阅，请异步启动代理。 但是，如果您要监视同步的结果并在同步进程期间从代理处接收回调（例如，要显示进度栏），则应当同步启动代理。 对于 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssExpressEd2005](../../includes/ssexpressed2005-md.md)] 订阅服务器，必须同步启动代理。  
  
#### <a name="to-synchronize-a-pull-subscription-to-a-snapshot-or-transactional-publication"></a>将请求订阅与快照或事务发布进行同步  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 类创建与订阅服务器的连接。  
  
2.  创建 <xref:Microsoft.SqlServer.Replication.TransPullSubscription> 类的实例并设置下列属性：  
  
    -   用于 <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>的订阅数据库的名称。  
  
    -   用于 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>的订阅所属的发布的名称。  
  
    -   为 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A>设置发布数据库的名称。  
  
    -   用于 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>的发布服务器的名称。  
  
    -   在步骤 1 中为 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>创建的连接。  
  
3.  调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法以获取其他订阅属性。 如果该方法返回 `false`，则确保订阅存在。  
  
4.  使用下列方法之一在订阅服务器中启动分发代理：  
  
    -   在步骤 2 中的 <xref:Microsoft.SqlServer.Replication.TransPullSubscription.SynchronizeWithJob%2A> 实例上调用 <xref:Microsoft.SqlServer.Replication.TransPullSubscription> 方法。 该方法异步启动分发代理，并在代理作业运行时立即将控制权返回给您的应用程序。 您不能为 [!INCLUDE[ssExpressEd2005](../../includes/ssexpressed2005-md.md)] 订阅服务器调用该方法，如果创建的订阅的 <xref:Microsoft.SqlServer.Replication.PullSubscription.CreateSyncAgentByDefault%2A> 的值为 `false`（默认值），则也不能调用该方法。  
  
    -   获取 <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent> 属性中 <xref:Microsoft.SqlServer.Replication.TransPullSubscription.SynchronizationAgent%2A> 类的实例，然后调用 <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent.Synchronize%2A> 方法。 该方法可以同步启动代理，并且控制权仍属于运行代理作业。 在执行同步期间，您可以在代理仍旧运行的情况下处理 <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent.Status> 事件。  
  
        > [!NOTE]  
        >  如果你在创建请求订阅`false`时<xref:Microsoft.SqlServer.Replication.PullSubscription.CreateSyncAgentByDefault%2A>将的值指定为（默认值），则还需要<xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent.Distributor%2A>指定、 <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent.DistributorSecurityMode%2A>和（可选<xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent.DistributorLogin%2A> ）， <xref:Microsoft.SqlServer.Replication.TransSynchronizationAgent.DistributorPassword%2A>因为订阅的与代理作业相关的元数据在[MSsubscription_properties](/sql/relational-databases/system-tables/mssubscription-properties-transact-sql)中不可用。  
  
#### <a name="to-synchronize-a-pull-subscription-to-a-merge-publication"></a>将请求订阅与合并发布进行同步  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 类创建与订阅服务器的连接。  
  
2.  创建 <xref:Microsoft.SqlServer.Replication.MergePullSubscription> 类的实例并设置下列属性：  
  
    -   用于 <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>的订阅数据库的名称。  
  
    -   用于 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>的订阅所属的发布的名称。  
  
    -   将 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A>设置为已发布的数据库的名称。  
  
    -   用于 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>的发布服务器的名称。  
  
    -   在步骤 1 中为 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>创建的连接。  
  
3.  调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法以获取其他订阅属性。 如果该方法返回 `false`，则确保订阅存在。  
  
4.  使用下列方法之一在订阅服务器中启动合并代理：  
  
    -   在步骤 2 中的 <xref:Microsoft.SqlServer.Replication.MergePullSubscription.SynchronizeWithJob%2A> 实例上调用 <xref:Microsoft.SqlServer.Replication.MergePullSubscription> 方法。 该方法异步启动合并代理，并在代理作业运行时立即将控制权返回给您的应用程序。 您不能为 [!INCLUDE[ssExpressEd2005](../../includes/ssexpressed2005-md.md)] 订阅服务器调用该方法，如果创建的订阅的 <xref:Microsoft.SqlServer.Replication.PullSubscription.CreateSyncAgentByDefault%2A> 的值为 `false`（默认值），则也不能调用该方法。  
  
    -   获取 <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent> 属性中 <xref:Microsoft.SqlServer.Replication.MergePullSubscription.SynchronizationAgent%2A> 类的实例，然后调用 <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.Synchronize%2A> 方法。 该方法可以同步启动合并代理，并且控件仍属于运行代理作业。 在执行同步期间，您可以在代理仍旧运行的情况下处理 <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.Status> 事件。  
  
        > [!NOTE]  
        >  如果你在创建请求订阅`false`时<xref:Microsoft.SqlServer.Replication.PullSubscription.CreateSyncAgentByDefault%2A>将的值指定为（默认值），则还需要指定<xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.Distributor%2A> <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.DistributorSecurityMode%2A>、、 <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.PublisherSecurityMode%2A>、 <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.HostName%2A>、 <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.SubscriptionType%2A>、 <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.ExchangeType%2A>和（可选<xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.DistributorLogin%2A> <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.DistributorPassword%2A> <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.PublisherLogin%2A>）， <xref:Microsoft.SqlServer.Replication.MergeSynchronizationAgent.PublisherPassword%2A>因为订阅的与代理作业相关的元数据在[MSsubscription_properties](/sql/relational-databases/system-tables/mssubscription-properties-transact-sql)中不可用。  
  
###  <a name="examples-rmo"></a><a name="PShellExample"></a> 示例 (RMO)  
 该示例将请求订阅与事务发布进行同步，其中，代理使用代理作业进行异步启动。  
  
 [!code-csharp[HowTo#rmo_SyncTranPullSub_WithJob](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_synctranpullsub_withjob)]  
  
 [!code-vb[HowTo#rmo_vb_SyncTranPullSub_WithJob](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_synctranpullsub_withjob)]  
  
 该示例将请求订阅与事务发布进行同步，其中，代理进行同步启动。  
  
 [!code-csharp[HowTo#rmo_SyncTranPullSub](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_synctranpullsub)]  
  
 [!code-vb[HowTo#rmo_vb_SyncTranPullSub](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_synctranpullsub)]  
  
 该示例将请求订阅与合并发布进行同步，其中，代理使用代理作业进行异步启动。  
  
 [!code-csharp[HowTo#rmo_SyncMergePullSub_WithJob](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_syncmergepullsub_withjob)]  
  
 [!code-vb[HowTo#rmo_vb_SyncMergePullSub_WithJob](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_syncmergepullsub_withjob)]  
  
 该示例将请求订阅与合并发布进行同步，其中，代理进行同步启动。  
  
 [!code-csharp[HowTo#rmo_SyncMergePullSub](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_syncmergepullsub)]  
  
 [!code-vb[HowTo#rmo_vb_SyncMergePullSub](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_syncmergepullsub)]  
  
 该示例使用 Web 同步将请求订阅与合并发布进行同步。 该订阅是在没有代理作业和相关订阅元数据的情况下创建的，因此，必须同步启动代理，并提供更多的订阅信息。  
  
 [!code-csharp[HowTo#rmo_SyncMergePullSub_NoJobWebSync](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_syncmergepullsub_nojobwebsync)]  
  
 [!code-vb[HowTo#rmo_vb_SyncMergePullSub_NoJobWebSync](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_syncmergepullsub_nojobwebsync)]  
  
## <a name="see-also"></a>另请参阅  
 [同步数据](synchronize-data.md)   
 [Create a Pull Subscription](create-a-pull-subscription.md)   
 [复制安全最佳实践](security/replication-security-best-practices.md)  
  
  
