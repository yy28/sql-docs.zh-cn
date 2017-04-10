---
title: "删除发布 | Microsoft Docs"
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
  - "删除发布"
  - "发布 [SQL Server 复制], 删除"
  - "项目 [SQL Server 复制], 删除"
  - "删除发布"
ms.assetid: 408a1360-12ee-4896-ac94-482ae839593b
caps.latest.revision: 35
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 35
---
# 删除发布
  本主题说明如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]、[!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 或复制管理对象 (RMO) 在 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 中删除发布。  
  
 **本主题内容**  
  
-   **删除发布，使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [复制管理对象 (RMO)](#RMOProcedure)  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 从 **中的** “本地发布” [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]文件夹中删除发布。  
  
#### 删除发布  
  
1.  在 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]中连接到发布服务器，然后展开服务器节点。  
  
2.  展开 **“复制”** 文件夹，再展开 **“本地发布”** 文件夹。  
  
3.  右键单击要删除，然后单击的发布 **删除**。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 可以使用复制存储过程以编程方式删除发布。 使用的存储过程取决于要删除的发布的类型。  
  
> [!NOTE]  
>  删除发布并不会删除发布数据库中的已发布对象，也不会删除订阅数据库中的相应对象。 如有必要，使用 `DROP <object>` 命令手动删除这些对象。  
  
#### 删除快照发布或事务发布  
  
1.  执行以下操作之一：  
  
    -   若要删除单个发布，执行 [sp_droppublication](../../../relational-databases/system-stored-procedures/sp-droppublication-transact-sql.md) 发布服务器上对发布数据库。  
  
    -   若要删除中的所有发布并从已发布数据库中删除所有复制对象，执行 [sp_removedbreplication](../../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md) 在发布服务器。 为 **@type** 指定 **tran**值。 （可选）如果无法访问分发服务器或数据库的状态为可疑或脱机，指定的值 **1** 为 **@force**。 （可选）指定的数据库的名称 **@dbname** 如果 [sp_removedbreplication](../../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md) 不发布数据库上执行。  
  
        > [!NOTE]  
        >  将值指定为 **1** 为 **@force** 可能在数据库中保留与复制相关的发布对象。  
  
2.  （可选）如果此数据库不有任何其他发布，则执行 [sp_replicationdboption & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md) 若要禁用使用快照复制或事务复制的当前数据库的发布。  
  
3.  （可选）在订阅服务器上的订阅数据库上，执行 [sp_subscription_cleanup](../../../relational-databases/system-stored-procedures/sp-subscription-cleanup-transact-sql.md) 订阅数据库中删除任何剩余复制元数据。  
  
#### 删除合并发布  
  
1.  执行以下操作之一：  
  
    -   若要删除单个发布，执行 [sp_dropmergepublication & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-dropmergepublication-transact-sql.md) 在发布数据库上的发布服务器。  
  
    -   若要删除中的所有发布并从已发布数据库中删除所有复制对象，执行 [sp_removedbreplication](../../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md) 在发布服务器。 为 **@type** 指定 **merge**值。 （可选）如果无法访问分发服务器或数据库的状态为可疑或脱机，指定的值 **1** 为 **@force**。 （可选）指定的数据库的名称 **@dbname** 如果 [sp_removedbreplication](../../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md) 不发布数据库上执行。  
  
        > [!NOTE]  
        >  将值指定为 **1** 为 **@force** 可能在数据库中保留与复制相关的发布对象。  
  
2.  （可选）如果此数据库不有任何其他发布，则执行 [sp_replicationdboption & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md) 若要禁用使用合并复制的当前数据库的发布。  
  
3.  （可选）在订阅服务器上的订阅数据库上，执行 [sp_mergesubscription_cleanup & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-mergesubscription-cleanup-transact-sql.md) 若要在订阅数据库中删除任何剩余复制元数据。  
  
###  <a name="TsqlExample"></a> 示例 (Transact-SQL)  
 该示例演示如何删除事务发布并禁用数据库的事务发布。 该示例假定以前删除了所有订阅。 有关详细信息，请参阅 [Delete a Pull Subscription](../../../relational-databases/replication/delete-a-pull-subscription.md) 或 [Delete a Push Subscription](../../../relational-databases/replication/delete-a-push-subscription.md)。  
  
 [!code-sql[HowTo#sp_droppublication](../../../relational-databases/replication/codesnippet/tsql/delete-a-publication_1.sql)]  
  
 该示例演示如何删除合并发布并禁用数据库的合并发布。 该示例假定以前删除了所有订阅。 有关详细信息，请参阅 [Delete a Pull Subscription](../../../relational-databases/replication/delete-a-pull-subscription.md) 或 [Delete a Push Subscription](../../../relational-databases/replication/delete-a-push-subscription.md)。  
  
 [!code-sql[HowTo#sp_dropmergepublication](../../../relational-databases/replication/codesnippet/tsql/delete-a-publication_2.sql)]  
  
##  <a name="RMOProcedure"></a> 使用复制管理对象 (RMO)  
 可以使用复制管理对象 (RMO) 以编程方式删除发布。 用于删除发布的 RMO 类取决于要删除的发布的类型。  
  
#### 删除快照发布或事务发布  
  
1.  通过使用创建连接到发布服务器 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 类。  
  
2.  创建的实例 <xref:Microsoft.SqlServer.Replication.TransPublication> 类。  
  
3.  设置 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> 和 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> 属性的发布，并设置 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 属性设置为在步骤 1 中创建的连接。  
  
4.  检查 <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> 属性以验证发布是否存在。 如果此属性的值为 **false**，则步骤 3 中的发布属性定义不正确，或者发布不存在。  
  
5.  调用 <xref:Microsoft.SqlServer.Replication.Publication.Remove%2A> 方法。  
  
6.  （可选）如果此数据库中不存在其他事务发布，则可按照下面的步骤为事务发布禁用此数据库：  
  
    1.  创建的实例 <xref:Microsoft.SqlServer.Replication.ReplicationDatabase> 类。 设置 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 属性设置为实例 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 步骤 1 中。  
  
    2.  调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法。 如果该方法返回 **false**，请确认数据库是否存在。  
  
    3.  设置 <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.EnabledTransPublishing%2A> 属性设置为 **false**。  
  
    4.  调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 方法。  
  
7.  关闭连接。  
  
#### 删除合并发布  
  
1.  通过使用创建连接到发布服务器 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 类。  
  
2.  创建的实例 <xref:Microsoft.SqlServer.Replication.MergePublication> 类。  
  
3.  设置 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> 和 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> 属性的发布，并设置 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 属性设置为在步骤 1 中创建的连接。  
  
4.  检查 <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> 属性以验证发布是否存在。 如果此属性的值为 **false**，则步骤 3 中的发布属性定义不正确，或者发布不存在。  
  
5.  调用 <xref:Microsoft.SqlServer.Replication.Publication.Remove%2A> 方法。  
  
6.  （可选）如果此数据库中不存在其他合并发布，则可按照下面的步骤为合并发布禁用此数据库：  
  
    1.  创建的实例 <xref:Microsoft.SqlServer.Replication.ReplicationDatabase> 类。 设置 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 属性设置为实例 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 步骤 1 中。  
  
    2.  调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法。 如果该方法返回 **false**，请验证数据库是否存在。  
  
    3.  设置 <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.EnabledMergePublishing%2A> 属性设置为 **false**。  
  
    4.  调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 方法。  
  
7.  关闭连接。  
  
###  <a name="PShellExample"></a> 示例 (RMO)  
 下面的示例删除事务发布。 如果此数据库不存在其他事务发布，则事务发布也被禁用。  
  
 [!code-csharp[HowTo#rmo_DropTranPub](../../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_droptranpub)]  
  
 [!code-vb[HowTo#rmo_vb_DropTranPub](../../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_droptranpub)]  
  
 下面的示例删除合并发布。 如果此数据库不存在其他合并发布，则合并发布也被禁用。  
  
 [!code-csharp[HowTo#rmo_DropMergePub](../../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_dropmergepub)]  
  
 [!code-vb[HowTo#rmo_vb_DropMergePub](../../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_dropmergepub)]  
  
## 另请参阅  
 [复制系统存储过程概念](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [发布数据和数据库对象](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)  
  
  