---
title: "重新初始化订阅 | Microsoft Docs"
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
  - "初始化订阅 [SQL Server 复制], 重新初始化"
  - "订阅 [SQL Server 复制], 重新初始化"
  - "重新初始化订阅"
ms.assetid: ca3625c5-c62e-4ab7-9829-d511f838e385
caps.latest.revision: 37
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 37
---
# 重新初始化订阅
  本主题说明如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或复制管理对象 (RMO) 在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中重新初始化订阅。 可以将各个订阅标记为重新初始化，以便在下次同步期间应用新快照。  
  
 **本主题内容**  
  
-   **重新初始化订阅，使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [复制管理对象 (RMO)](#RMOProcedure)  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 重新初始化订阅的过程由两个部分组成：  
  
1.  将对发布的单个或所有订阅“标记”  为重新初始化。 将订阅标记为重新初始化在 **重新初始化订阅** 对话框中，可从 **本地发布** 文件夹和 **本地订阅** 文件夹中的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。 也可以从 **“所有订阅”** 选项卡和复制监视器中的发布节点中对订阅进行标记。 有关启动复制监视器的信息，请参阅 [启动复制监视器](../../relational-databases/replication/monitor/start-the-replication-monitor.md)。 将订阅标记为要重新初始化时，可以选择下列选项之一：  
  
     **使用当前快照**  
     选择此项可以在分发代理或合并代理下一次运行时将当前快照应用于订阅服务器。 如果无法获得有效快照，将无法选定此选项。  
  
     **使用新快照**  
     选择此项可以用新的快照来重新初始化订阅。 只有在快照代理已经生成新快照之后，才能将其应用于订阅服务器。 如果快照代理设置为按计划运行，则直到下一个计划的快照代理运行后才能重新初始化订阅。 选择 **“立即生成新快照”** 可以立即启动快照代理。  
  
     **在重新初始化之前上载未同步的更改**  
     仅限合并复制。 选择此项可以在用快照覆盖订阅服务器上的数据之前，从订阅数据库上载任何挂起的更改。  
  
     如果添加、删除或更改参数化筛选器，则订阅服务器上挂起的更改在重新初始化期间将无法上载到发布服务器。 若要上载挂起的更改，请在更改筛选器前同步所有订阅。  
  
2.  在下次同步订阅时将重新初始化订阅：分发代理（用于事务复制）或合并代理（用于合并复制）将最近的快照应用于每个包含有标记为要重新初始化的订阅的订阅服务器。 有关同步订阅的详细信息，请参阅 [同步推送订阅](../../relational-databases/replication/synchronize-a-push-subscription.md) 和 [同步请求订阅](../../relational-databases/replication/synchronize-a-pull-subscription.md)。  
  
#### 在 Management Studio 中将单个推送订阅或单个请求订阅（位于发布服务器上）标记为要重新初始化  
  
1.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中连接到发布服务器，然后展开服务器节点。  
  
2.  展开 **“复制”** 文件夹，再展开 **“本地发布”** 文件夹。  
  
3.  展开包含要重新初始化的订阅的发布。  
  
4.  右键单击该订阅，然后单击 **重新初始化**。  
  
5.  在 **重新初始化订阅** 对话框中，选择选项，然后单击 **将标记为重新初始化**。  
  
#### 在 Management Studio 中将单个请求订阅（位于订阅服务器）标记为要重新初始化  
  
1.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中连接到订阅服务器，然后展开服务器节点。  
  
2.  展开 **“复制”** 文件夹，再展开 **“本地订阅”** 文件夹。  
  
3.  右键单击该订阅，然后单击 **重新初始化**。  
  
4.  在显示的确认对话框中，单击 **“是”**。  
  
#### 在 Management Studio 中将所有订阅标记为要重新初始化  
  
1.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中连接到发布服务器，然后展开服务器节点。  
  
2.  展开 **“复制”** 文件夹，再展开 **“本地发布”** 文件夹。  
  
3.  右键单击与想要重新初始化，然后单击的订阅的发布 **重新初始化所有订阅**。  
  
4.  在 **重新初始化订阅** 对话框中，选择选项，然后单击 **将标记为重新初始化**。  
  
#### 在复制监视器中将单个推送订阅或单个请求订阅标记为要重新初始化  
  
1.  在复制监视器的左窗格中依次展开发布服务器组、发布服务器，再单击一个发布。  
  
2.  单击 **“所有订阅”** 选项卡。  
  
3.  右键单击你想要重新初始化，然后单击的订阅 **重新初始化订阅**。  
  
4.  在 **重新初始化订阅** 对话框中，选择选项，然后单击 **将标记为重新初始化**。  
  
#### 在复制监视器中将所有订阅标记为要重新初始化  
  
1.  在复制监视器的左窗格中依次展开发布服务器组、发布服务器。  
  
2.  右键单击与想要重新初始化，然后单击的订阅的发布 **重新初始化所有订阅**。  
  
3.  在 **重新初始化订阅** 对话框中，选择选项，然后单击 **将标记为重新初始化**。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 可以使用复制存储过程以编程方式重新初始化订阅。 使用的存储过程取决于订阅的类型（推送或请求）以及订阅所属的发布的类型。  
  
#### 重新初始化对事务发布的请求订阅  
  
1.  在订阅服务器上的订阅数据库上，执行 [sp_reinitpullsubscription & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-reinitpullsubscription-transact-sql.md)。 指定 **@publisher**, ，**@publisher_db**, ，和 **@publication**。 这会将订阅标记为在下一次运行分发代理时将要重新初始化。  
  
2.  （可选）在订阅服务器上启动分发代理，以使订阅同步。 有关详细信息，请参阅 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md)。  
  
#### 重新初始化对事务发布的推送订阅  
  
1.  在发布服务器上，执行 [sp_reinitsubscription & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-reinitsubscription-transact-sql.md)。 指定 **@publication**, ，**@subscriber**, ，和 **@destination_db**。 这会将订阅标记为在下一次运行分发代理时将要重新初始化。  
  
2.  （可选）在分发服务器上启动分发代理，以使订阅同步。 有关详细信息，请参阅 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md)。  
  
#### 重新初始化对合并发布的请求订阅  
  
1.  在订阅服务器上的订阅数据库上，执行 [sp_reinitmergepullsubscription & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-reinitmergepullsubscription-transact-sql.md)。 指定 **@publisher**, ，**@publisher_db**, ，和 **@publication**。 若要重新初始化之前上载订阅服务器的更改，将值指定为 **true** 为 **@upload_first**。 这会将订阅标记为在下一次运行合并代理时将要重新初始化。  
  
    > [!IMPORTANT]  
    >  如果添加、删除或更改参数化筛选器，则订阅服务器上挂起的更改在重新初始化期间将无法上载到发布服务器。 若要上载挂起的更改，请在更改筛选器前同步所有订阅。  
  
2.  （可选）在订阅服务器上启动合并代理，以使订阅同步。 有关详细信息，请参阅 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md)。  
  
#### 重新初始化对合并发布的推送订阅  
  
1.  在发布服务器上，执行 [sp_reinitmergesubscription & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-reinitmergesubscription-transact-sql.md)。 指定 **@publication**, ，**@subscriber**, ，和 **@subscriber_db**。 若要重新初始化之前上载订阅服务器的更改，将值指定为 **true** 为 **@upload_first**。 这会将订阅标记为在下一次运行分发代理时将要重新初始化。  
  
    > [!IMPORTANT]  
    >  如果添加、删除或更改参数化筛选器，则订阅服务器上挂起的更改在重新初始化期间将无法上载到发布服务器。 若要上载挂起的更改，请在更改筛选器前同步所有订阅。  
  
2.  （可选）在分发服务器上启动合并代理，以使订阅同步。 有关详细信息，请参阅 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md)。  
  
#### 创建新的合并发布时设置重新初始化策略  
  
1.  在发布服务器上对发布数据库中，执行 [sp_addmergepublication](../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md), ，指定以下值之一的 **@automatic_reinitialization_policy**:  
  
    -   **1** -自动重新初始化订阅之前从订阅服务器上载更改对该发布的更改所需的方式。  
  
    -   **0** -时自动重新初始化订阅，订阅服务器上的更改将被放弃对发布的更改所需的方式。  
  
    > [!IMPORTANT]  
    >  如果添加、删除或更改参数化筛选器，则订阅服务器上挂起的更改在重新初始化期间将无法上载到发布服务器。 若要上载挂起的更改，请在更改筛选器前同步所有订阅。  
  
     有关详细信息，请参阅 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)。  
  
#### 更改现有合并发布的重新初始化策略  
  
1.  在发布服务器上对发布数据库中，执行 [sp_changemergepublication](../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md), ，并指定 **automatic_reinitialization_policy** 为 **@property** 以及下列其中一项值为 **@value**:  
  
    -   **1** -自动重新初始化订阅之前从订阅服务器上载更改对该发布的更改所需的方式。  
  
    -   **0** -时自动重新初始化订阅，订阅服务器上的更改将被放弃对发布的更改所需的方式。  
  
    > [!IMPORTANT]  
    >  如果添加、删除或更改参数化筛选器，则订阅服务器上挂起的更改在重新初始化期间将无法上载到发布服务器。 若要上载挂起的更改，请在更改筛选器前同步所有订阅。  
  
     有关详细信息，请参阅 [View and Modify Publication Properties](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)。  
  
##  <a name="RMOProcedure"></a> 使用复制管理对象 (RMO)  
 可以将各个订阅标记为重新初始化，以便在下次同步期间应用新的快照。 可以使用复制管理对象 (RMO) 以编程的方式重新初始化订阅。 所用的类取决于订阅所属的发布类型以及订阅类型（即推送订阅或请求订阅）。  
  
#### 重新初始化对事务发布的请求订阅  
  
1.  通过使用创建连接到订阅服务器 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 类。  
  
2.  创建的实例 <xref:Microsoft.SqlServer.Replication.TransPullSubscription> 类，并将设置 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>, ，<xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>, ，<xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>, ，<xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A>, ，以及步骤 1 中的连接 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>。  
  
3.  调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法以获取该对象的属性。  
  
    > [!NOTE]  
    >  如果此方法返回 **false**, ，在步骤 2 中的订阅属性中定义不正确或请求订阅不存在。  
  
4.  调用 <xref:Microsoft.SqlServer.Replication.TransPullSubscription.Reinitialize%2A> 方法。 此方法将订阅标记为要重新初始化。  
  
5.  同步请求订阅。 有关详细信息，请参阅 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md)。  
  
#### 重新初始化对事务发布的推送订阅  
  
1.  通过使用创建连接到发布服务器 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 类。  
  
2.  创建的实例 <xref:Microsoft.SqlServer.Replication.TransSubscription> 类，并将设置 <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>, ，<xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>, ，<xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>, ，<xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A>, ，以及步骤 1 中的连接 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>。  
  
3.  调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法以获取该对象的属性。  
  
    > [!NOTE]  
    >  如果此方法返回 **false**, ，在步骤 2 中的订阅属性中定义不正确或推送订阅不存在。  
  
4.  调用 <xref:Microsoft.SqlServer.Replication.TransSubscription.Reinitialize%2A> 方法。 此方法将订阅标记为要重新初始化。  
  
5.  同步推送订阅。 有关详细信息，请参阅 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md)。  
  
#### 重新初始化对合并发布的请求订阅  
  
1.  通过使用创建连接到订阅服务器 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 类。  
  
2.  创建的实例 <xref:Microsoft.SqlServer.Replication.MergePullSubscription> 类，并将设置 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>, ，<xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>, ，<xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>, ，<xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A>, ，以及步骤 1 中的连接 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>。  
  
3.  调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法以获取该对象的属性。  
  
    > [!NOTE]  
    >  如果此方法返回 **false**, ，在步骤 2 中的订阅属性中定义不正确或请求订阅不存在。  
  
4.  调用 <xref:Microsoft.SqlServer.Replication.MergePullSubscription.Reinitialize%2A> 方法。 传递 **true** 值以在重新初始化之前上载订阅服务器上的更改，或者传递 **false** 值以重新初始化并丢失订阅服务器上任何挂起的更改。 此方法将订阅标记为要重新初始化。  
  
    > [!NOTE]  
    >  如果订阅过期，则无法上载更改。 有关详细信息，请参阅 [Set the Expiration Period for Subscriptions](../../relational-databases/replication/publish/set-the-expiration-period-for-subscriptions.md)。  
  
5.  同步请求订阅。 有关详细信息，请参阅 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md)。  
  
#### 重新初始化对合并发布的推送订阅  
  
1.  通过使用创建连接到发布服务器 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 类。  
  
2.  创建的实例 <xref:Microsoft.SqlServer.Replication.MergeSubscription> 类，并将设置 <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>, ，<xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>, ，<xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>, ，<xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A>, ，以及步骤 1 中的连接 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>。  
  
3.  调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法以获取该对象的属性。  
  
    > [!NOTE]  
    >  如果此方法返回 **false**, ，在步骤 2 中的订阅属性中定义不正确或推送订阅不存在。  
  
4.  调用 <xref:Microsoft.SqlServer.Replication.MergeSubscription.Reinitialize%2A> 方法。 传递 **true** 值以在重新初始化之前上载订阅服务器上的更改，或者传递 **false** 值以重新初始化并丢失订阅服务器上任何挂起的更改。 此方法将订阅标记为要重新初始化。  
  
    > [!NOTE]  
    >  如果订阅过期，则无法上载更改。 有关详细信息，请参阅 [Set the Expiration Period for Subscriptions](../../relational-databases/replication/publish/set-the-expiration-period-for-subscriptions.md)。  
  
5.  同步推送订阅。 有关详细信息，请参阅 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md)。  
  
###  <a name="PShellExample"></a> 示例 (RMO)  
 此示例将重新初始化事务发布的请求订阅。  
  
 [!code-csharp[HowTo#rmo_ReinitTranPullSub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_reinittranpullsub)]  
  
 [!code-vb[HowTo#rmo_vb_ReinitTranPullSub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_reinittranpullsub)]  
  
 此示例将在第一次上载订阅服务器上挂起的更改后，重新初始化合并发布的请求订阅。  
  
 [!code-csharp[HowTo#rmo_ReinitMergePullSub_WithUpload](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_reinitmergepullsub_withupload)]  
  
 [!code-vb[HowTo#rmo_vb_ReinitMergePullSub_WithUpload](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_reinitmergepullsub_withupload)]  
  
## 另请参阅  
 [重新初始化订阅](../../relational-databases/replication/reinitialize-subscriptions.md)   
 [复制管理对象概念](../../relational-databases/replication/concepts/replication-management-objects-concepts.md)   
 [复制安全最佳实践](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  