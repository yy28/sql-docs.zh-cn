---
title: "查看和修改推送订阅属性 | Microsoft Docs"
ms.custom: ""
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "查看复制属性"
  - "推送订阅 [SQL Server 复制], 属性"
  - "订阅 [SQL Server 复制], 推送"
  - "推送订阅 [SQL Server 复制], 修改"
  - "修改复制属性, 推送订阅"
  - "修改订阅, SQL Server Management Studio"
ms.assetid: 801d2995-7aa5-4626-906e-c8190758ec71
caps.latest.revision: 37
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 37
---
# 查看和修改推送订阅属性
  本主题说明如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或复制管理对象 (RMO) 在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中查看和修改推送订阅属性。  
  
 **本主题内容**  
  
-   **查看和修改推送订阅属性，使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [复制管理对象 (RMO)](#RMOProcedure)  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 可以从下列位置查看和修改发布服务器的推送订阅属性：  
  
-    **订阅属性-\< 发布服务器>: \< 发布数据库>** 对话框中，可从 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。  
  
-   **“所有订阅”** 选项卡，该选项卡可以从复制监视器中找到。 有关启动复制监视器的信息，请参阅 [启动复制监视器](../../relational-databases/replication/monitor/start-the-replication-monitor.md)。  
  
#### 在 Management Studio 中查看和修改推送订阅属性  
  
1.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中连接到发布服务器，然后展开服务器节点。  
  
2.  展开 **“复制”** 文件夹，再展开 **“本地发布”** 文件夹。  
  
3.  展开相应的发布，请右键单击订阅，然后单击 **属性**。  
  
4.  根据需要修改属性，然后单击 **“确定”**。  
  
#### 在复制监视器中查看和修改推送订阅属性  
  
1.  在复制监视器的左窗格中依次展开发布服务器组、发布服务器，然后单击某个发布。  
  
2.  单击 **“所有订阅”** 选项卡。  
  
3.  右键单击订阅，然后单击 **属性**。  
  
4.  根据需要修改属性，然后单击 **“确定”**。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 可以使用复制存储过程以编程方式修改推送订阅和访问其属性。 所用的存储过程取决于订阅所属的发布的类型。  
  
#### 查看快照或事务发布的推送订阅的属性  
  
1.  在发布服务器上对发布数据库中，执行 [sp_helpsubscription](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)。 指定 **@publication**、 **@subscriber**，并为 **@article** 指定值 **all**。  
  
2.  在发布服务器上对发布数据库中，执行 [sp_helpsubscriberinfo](../../relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql.md), ，并指定 **@subscriber**。  
  
#### 更改快照或事务发布的推送订阅的属性  
  
1.  在发布服务器上对发布数据库中，执行 [sp_changesubscriber](../../relational-databases/system-stored-procedures/sp-changesubscriber-transact-sql.md), ，并指定 **@subscriber** 和要更改的订阅服务器属性的任何参数。  
  
2.  在发布服务器上对发布数据库中，执行 [sp_changesubscription](../../relational-databases/system-stored-procedures/sp-changesubscription-transact-sql.md)。 指定 **@publication**, ，**@subscriber**, ，**@destination_db**, ，值为 **所有** 为 **@article**, 为要更改的订阅属性 **@property**, ，和为新值 **@value**。 这将更改推送订阅的安全设置。  
  
3.  （可选）若要更改订阅的数据转换服务 (DTS) 包属性，请执行 [sp_changesubscriptiondtsinfo](../../relational-databases/system-stored-procedures/sp-changesubscriptiondtsinfo-transact-sql.md) 在订阅服务器上的订阅数据库。 为 **@jobid** 指定分发代理作业的 ID，并指定以下 DTS 包属性：  
  
    -   **@dts_package_name**  
  
    -   **@dts_package_password**  
  
    -   **@dts_package_location**  
  
     此操作将更改订阅的 DTS 包属性。  
  
    > [!NOTE]  
    >  可以通过执行获得 ID 的作业 [sp_helpsubscription](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)。  
  
#### 查看合并发布的推送订阅的属性  
  
1.  在发布服务器上对发布数据库中，执行 [sp_helpmergesubscription](../../relational-databases/system-stored-procedures/sp-helpmergesubscription-transact-sql.md)。 指定 **@publication** 和 **@subscriber**。  
  
2.  在发布服务器上，执行 [sp_helpsubscriberinfo](../../relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql.md), ，并指定 **@subscriber**。  
  
#### 更改合并发布的推送订阅的属性  
  
1.  在发布服务器上对发布数据库中，执行 [sp_changemergesubscription](../../relational-databases/system-stored-procedures/sp-changemergesubscription-transact-sql.md)。 指定 **@publication**, ，**@subscriber**, ，**@subscriber_db**, 为要更改的订阅属性 **@property**, ，并将新值作为 **@value**。  
  
###  <a name="TsqlExample"></a> 示例 (Transact-SQL)  
  
##  <a name="RMOProcedure"></a> 使用复制管理对象 (RMO)  
 用于查看或修改推送订阅属性的 RMO 类取决于订阅推送订阅的发布的类型。  
  
#### 查看或修改快照发布或事务发布的推送订阅的属性  
  
1.  通过使用创建连接到发布服务器 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 类。  
  
2.  创建的实例 <xref:Microsoft.SqlServer.Replication.TransSubscription> 类。  
  
3.  设置 <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>, ，<xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>, ，<xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>, ，和 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A> 属性。  
  
4.  设置 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 步骤 1 中的 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 属性设置。  
  
5.  调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法以获取该对象的属性。 如果此方法返回 **false**，则说明步骤 3 中的订阅属性没有正确定义或该订阅不存在。  
  
6.  （可选）若要更改属性，设置新的值之一的 <xref:Microsoft.SqlServer.Replication.TransSubscription> 属性可以设置，然后调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 方法。  
  
7.  （可选）若要查看新设置，请调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.Refresh%2A> 方法来重新加载该订阅的属性。  
  
#### 查看或修改合并发布的推送订阅的属性  
  
1.  通过使用创建连接到订阅服务器 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 类。  
  
2.  创建的实例 <xref:Microsoft.SqlServer.Replication.MergeSubscription> 类。  
  
3.  设置 <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>, ，<xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>, ，<xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>, ，和 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A> 属性。  
  
4.  设置 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 步骤 1 中的 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 属性设置。  
  
5.  调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法以获取该对象的属性。 如果此方法返回 **false**，则说明步骤 3 中的订阅属性没有正确定义或该订阅不存在。  
  
6.  （可选）若要更改属性，设置新的值之一的 <xref:Microsoft.SqlServer.Replication.MergeSubscription> 属性可以设置，然后调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 方法。  
  
7.  （可选）若要查看新设置，请调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.Refresh%2A> 方法来重新加载该订阅的属性。  
  
## 另请参阅  
 [查看信息并为订阅 & #40; 执行任务复制监视器 & #41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-subscription-replication-monitor.md)   
 [复制安全最佳实践](../../relational-databases/replication/security/replication-security-best-practices.md)   
 [订阅发布](../../relational-databases/replication/subscribe-to-publications.md)  
  
  