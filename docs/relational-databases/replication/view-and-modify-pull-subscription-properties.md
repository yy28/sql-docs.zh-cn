---
title: "查看和修改请求订阅属性 | Microsoft Docs"
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
  - "修改订阅"
  - "查看复制属性"
  - "修改复制属性, 请求订阅"
  - "请求订阅 [SQL Server 复制], 修改"
  - "订阅 [SQL Server 复制], 请求"
  - "请求订阅 [SQL Server 复制], 属性"
  - "修改订阅, SQL Server Management Studio"
ms.assetid: 1601e54f-86f0-49e8-b023-87a5d1def033
caps.latest.revision: 37
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 37
---
# 查看和修改请求订阅属性
  本主题说明如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或复制管理对象 (RMO) 在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中查看和修改请求订阅属性。  
  
 **本主题内容**  
  
-   **查看和修改请求订阅属性，使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [复制管理对象 (RMO)](#RMOProcedure)  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 查看从发布服务器上或在订阅服务器上的请求订阅属性 **订阅属性-\< 发布服务器>: \< 发布数据库>** 对话框中，可从 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。 可以从订阅服务器中查看更多属性，并且可以在订阅服务器上修改属性。 也可以从发布服务器的 **“所有订阅”** 选项卡上查看属性信息，此选项卡可以通过复制监视器访问。 有关启动复制监视器的信息，请参阅 [启动复制监视器](../../relational-databases/replication/monitor/start-the-replication-monitor.md)。  
  
#### 从 Management Studio 中的发布服务器查看请求订阅属性  
  
1.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中连接到发布服务器，然后展开服务器节点。  
  
2.  展开 **“复制”** 文件夹，再展开 **“本地发布”** 文件夹。  
  
3.  展开相应的发布，请右键单击订阅，然后单击 **属性**。  
  
4.  查看属性，然后单击 **“确定”**。  
  
#### 从 Management Studio 中的订阅服务器查看和修改请求订阅属性  
  
1.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中连接到订阅服务器，然后展开服务器节点。  
  
2.  展开 **“复制”** 文件夹，再展开 **“本地订阅”** 文件夹。  
  
3.  右键单击订阅，然后单击 **属性**。  
  
4.  根据需要修改属性，然后单击 **“确定”**。  
  
#### 从复制监视器的发布服务器查看请求订阅属性  
  
1.  在复制监视器的左窗格中依次展开发布服务器组、发布服务器，然后单击某个发布。  
  
2.  单击 **“所有订阅”** 选项卡。  
  
3.  右键单击订阅，然后单击 **属性**。  
  
4.  查看属性，然后单击 **“确定”**。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 可以使用复制存储过程以编程方式修改请求订阅以及访问其属性。 所用的存储过程取决于订阅所属的发布的类型。  
  
#### 查看对快照发布或事务发布的请求订阅的属性  
  
1.  在订阅服务器上，执行 [sp_helppullsubscription](../../relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql.md)。 指定 **@publisher**, ，**@publisher_db**, ，和 **@publication**。 此操作将返回关于存储在订阅服务器上系统表中的订阅的信息。  
  
2.  在订阅服务器上，执行 [sp_helpsubscription_properties](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)。 指定 **@publisher**, ，**@publisher_db**, ，**@publication**, ，以及下列其中一项值为 **@publication_type**:  
  
    -   **0** -订阅属于事务发布。  
  
    -   **1** -订阅属于快照发布。  
  
3.  在发布服务器上，执行 [sp_helpsubscription](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)。 指定 **@publication** 和 **@subscriber**。  
  
4.  在发布服务器上，执行 [sp_helpsubscriberinfo](../../relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql.md), ，并指定 **@subscriber**。 此操作将显示关于订阅服务器的信息。  
  
#### 更改对快照发布或事务发布的请求订阅的属性  
  
1.  在订阅服务器上，执行 [sp_change_subscription_properties](../../relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql.md), ，并指定 **@publisher**, ，**@publisher_db**, ，**@publication**, ，其中任何一个值 **0** （事务） 或 **1** （快照） 的 **@publication_type**, 为要更改的订阅属性 **@property**, ，并将新值作为 **@value**。  
  
2.  （可选）在订阅服务器上的订阅数据库上，执行 [sp_changesubscriptiondtsinfo](../../relational-databases/system-stored-procedures/sp-changesubscriptiondtsinfo-transact-sql.md)。 指定的分发代理程序作业的 ID **@jobid**, ，和以下数据转换服务 (DTS) 包属性︰  
  
    -   **@dts_package_name**  
  
    -   **@dts_package_password**  
  
    -   **@dts_package_location**  
  
     此操作将更改订阅的 DTS 包属性。  
  
    > [!NOTE]  
    >  可以通过执行获得 ID 的作业 [sp_helpsubscription](../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md)。  
  
#### 查看对合并发布的请求订阅的属性  
  
1.  在订阅服务器上，执行 [sp_helpmergepullsubscription](../../relational-databases/system-stored-procedures/sp-helpmergepullsubscription-transact-sql.md)。 指定 **@publisher**, ，**@publisher_db**, ，和 **@publication**。  
  
2.  在订阅服务器上，执行 [sp_helpsubscription_properties](../../relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql.md)。 指定 **@publisher**, ，**@publisher_db**, ，**@publication**, ，并且值为 2， **@publication_type**。  
  
3.  在发布服务器上，执行 [sp_helpmergesubscription](../../relational-databases/system-stored-procedures/sp-helpmergesubscription-transact-sql.md) 以显示订阅信息。 若要对某一特定的订阅返回的信息，必须指定 **@publication**, ，**@subscriber**, ，且值为 **请求** 为 **@subscription_type**。  
  
4.  在发布服务器上，执行 [sp_helpsubscriberinfo](../../relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql.md), ，并指定 **@subscriber**。 此操作将显示关于订阅服务器的信息。  
  
#### 更改对合并发布的请求订阅的属性  
  
1.  在订阅服务器上，执行 [sp_changemergepullsubscription](../../relational-databases/system-stored-procedures/sp-changemergepullsubscription-transact-sql.md)。 指定 **@publication**, ，**@publisher**, ，**@publisher_db**, 为要更改的订阅属性 **@property**, ，并将新值作为 **@value**。  
  
##  <a name="RMOProcedure"></a> 使用复制管理对象 (RMO)  
 用于查看或修改请求订阅属性的 RMO 类取决于订阅请求订阅的发布类型。  
  
#### 查看或修改对快照发布或事务发布的请求订阅的属性  
  
1.  通过使用创建连接到订阅服务器 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 类。  
  
2.  创建的实例 <xref:Microsoft.SqlServer.Replication.TransPullSubscription> 类。  
  
3.  设置 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>, ，<xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>, ，<xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>, ，和 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A> 属性。  
  
4.  设置步骤 1 中的连接 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 属性。  
  
5.  调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法以获取该对象的属性。 如果此方法返回 **false**，则说明步骤 3 中的订阅属性定义不正确或服务器上不存在此订阅。  
  
6.  （可选）若要更改属性，设置新的值之一的 <xref:Microsoft.SqlServer.Replication.TransPullSubscription> 属性可以设置，然后调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 方法。  
  
7.  （可选）若要查看新设置，请调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.Refresh%2A> 方法来重新加载项目的属性。  
  
8.  关闭所有连接。  
  
#### 查看或修改对合并发布的请求订阅的属性  
  
1.  通过使用创建连接到订阅服务器 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 类。  
  
2.  创建的实例 <xref:Microsoft.SqlServer.Replication.MergePullSubscription> 类。  
  
3.  设置 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>, ，<xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>, ，<xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>, ，和 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A> 属性。  
  
4.  设置步骤 1 中的连接 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 属性。  
  
5.  调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法以获取该对象的属性。 如果此方法返回 **false**，则说明步骤 3 中的订阅属性定义不正确或服务器上不存在此订阅。  
  
6.  （可选）若要更改属性，设置新的值之一的 <xref:Microsoft.SqlServer.Replication.MergePullSubscription> 属性可以设置，然后调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 方法。  
  
7.  （可选）若要查看新设置，请调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.Refresh%2A> 方法来重新加载项目的属性。  
  
8.  关闭所有连接。  
  
## 另请参阅  
 [查看信息并为订阅 & #40; 执行任务复制监视器 & #41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-subscription-replication-monitor.md)   
 [复制安全最佳实践](../../relational-databases/replication/security/replication-security-best-practices.md)   
 [订阅发布](../../relational-databases/replication/subscribe-to-publications.md)  
  
  