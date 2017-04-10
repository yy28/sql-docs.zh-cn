---
title: "删除推送订阅 | Microsoft Docs"
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
  - "删除订阅"
  - "推送订阅 [SQL Server 复制], 删除"
  - "删除订阅"
  - "订阅 [SQL Server 复制], 推送"
ms.assetid: 3c4847e2-aed9-4488-b45d-8164422bdb10
caps.latest.revision: 35
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 35
---
# 删除推送订阅
  本主题说明如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或复制管理对象 (RMO) 在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中删除推送订阅。  
  
 **本主题内容**  
  
-   **删除推送订阅，使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [复制管理对象 (RMO)](#RMOProcedure)  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 删除发布服务器上的推送订阅 (从 **本地发布** 文件夹中的 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]) 还是订阅服务器 (从 **本地订阅** 文件夹)。 删除订阅不会从订阅中删除对象或数据，必须对其手动删除。  
  
#### 删除发布服务器上的推送订阅  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中连接到发布服务器，然后展开服务器节点。  
  
2.  展开 **“复制”** 文件夹，再展开 **“本地发布”** 文件夹。  
  
3.  展开与要删除的订阅关联的发布。  
  
4.  右键单击该订阅，然后单击 **删除**。  
  
5.  在确认对话框中，选择是否连接到订阅服务器以删除订阅信息。 如果清除了 **“连接到订阅服务器”** 复选框，则应以后连接到订阅服务器删除信息。  
  
#### 删除订阅服务器上的推送订阅  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中连接到订阅服务器，然后展开服务器节点。  
  
2.  展开 **“复制”** 文件夹，再展开 **“本地订阅”** 文件夹。  
  
3.  右键单击要删除，然后单击的订阅 **删除**。  
  
4.  在确认对话框中，选择是否连接到发布服务器以删除订阅信息。 如果清除 **“连接到发布服务器”** 复选框，则应在以后连接到发布服务器以删除订阅信息。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 可以使用复制存储过程以编程方式删除推送订阅。 所用的存储过程取决于订阅所属的发布的类型。  
  
#### 删除快照发布或事务发布的推送订阅  
  
1.  在发布服务器上对发布数据库中，执行 [sp_dropsubscription & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql.md)。 指定 **@publication** 和 **@subscriber**。 将 **@article** 的值指定为 **all**。 （可选）如果无法访问分发服务器上，指定的值 **1** 为 **@ignore_distributor** 以删除订阅而不删除分发服务器上的相关的对象。  
  
2.  在订阅服务器上的订阅数据库上，执行 [sp_subscription_cleanup & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-subscription-cleanup-transact-sql.md) 若要在订阅数据库中删除复制元数据。  
  
#### 删除合并发布的推送订阅  
  
1.  在发布服务器上，执行 [sp_dropmergesubscription & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-dropmergesubscription-transact-sql.md), ，并指定 **@publication**, ，**@subscriber** 和 **@subscriber_db**。 （可选）如果无法访问分发服务器上，指定的值 **1** 为 **@ignore_distributor** 以删除订阅而不删除分发服务器上的相关的对象。  
  
2.  在订阅服务器上的订阅数据库上，执行 [sp_mergesubscription_cleanup & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-mergesubscription-cleanup-transact-sql.md)。 指定 **@publisher**, ，**@publisher_db**, ，和 **@publication**。 这将会删除订阅数据库中的合并元数据。  
  
###  <a name="TsqlExample"></a> 示例 (Transact-SQL)  
 该示例删除对事务发布的推送订阅。  
  
 [!code-sql[HowTo#sp_droptransubscription](../../relational-databases/replication/codesnippet/tsql/delete-a-push-subscription_1.sql)]  
  
 该示例删除对合并发布的推送订阅。  
  
 [!code-sql[HowTo#sp_dropmergesubscription](../../relational-databases/replication/codesnippet/tsql/delete-a-push-subscription_2.sql)]  
  
##  <a name="RMOProcedure"></a> 使用复制管理对象 (RMO)  
 用于删除推送订阅的 RMO 类取决于订阅推送订阅的发布的类型。  
  
#### 删除快照发布或事务发布的推送订阅  
  
1.  通过使用创建连接到订阅服务器 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 类。  
  
2.  创建的实例 <xref:Microsoft.SqlServer.Replication.TransSubscription> 类。  
  
3.  设置 <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>, ，<xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A>, ，<xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>, ，和 <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A> 属性。  
  
4.  设置 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 步骤 1 中的 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 属性。  
  
5.  检查 <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> 属性以验证订阅是否存在。 如果此属性的值为 **false**，则步骤 2 中所定义的订阅属性不正确或者该订阅不存在。  
  
6.  调用 <xref:Microsoft.SqlServer.Replication.Subscription.Remove%2A> 方法。  
  
#### 删除合并发布的推送订阅  
  
1.  通过使用创建连接到订阅服务器 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 类。  
  
2.  创建的实例 <xref:Microsoft.SqlServer.Replication.MergeSubscription> 类。  
  
3.  设置 <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>, ，<xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A>, ，<xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>, ，和 <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A> 属性。  
  
4.  设置 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 步骤 1 中的 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 属性。  
  
5.  检查 <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> 属性以验证订阅是否存在。 如果此属性的值为 **false**，则步骤 2 中所定义的订阅属性不正确或者该订阅不存在。  
  
6.  调用 <xref:Microsoft.SqlServer.Replication.Subscription.Remove%2A> 方法。  
  
###  <a name="PShellExample"></a> 示例 (RMO)  
 可通过使用复制管理对象 (RMO) 以编程方式删除推送订阅。  
  
 [!code-csharp[HowTo#rmo_DropTranPushSub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_droptranpushsub)]  
  
 [!code-vb[HowTo#rmo_vb_DropTranPushSub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_droptranpushsub)]  
  
## 另请参阅  
 [订阅发布](../../relational-databases/replication/subscribe-to-publications.md)   
 [复制安全最佳实践](../../relational-databases/replication/security/replication-security-best-practices.md)  
  
  