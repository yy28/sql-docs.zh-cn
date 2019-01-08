---
title: 删除发布 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- removing publications
- publications [SQL Server replication], deleting
- articles [SQL Server replication], deleting
- deleting publications
ms.assetid: 408a1360-12ee-4896-ac94-482ae839593b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 08623cc2f9bf5d57141644a9f24c01d29d04cbe3
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52771649"
---
# <a name="delete-a-publication"></a>删除发布
  本主题说明如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 、 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]或复制管理对象 (RMO) 在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中删除发布。  
  
 **本主题内容**  
  
-   **删除发布，使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [复制管理对象 (RMO)](#RMOProcedure)  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 从 **中的** “本地发布” [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]文件夹中删除发布。  
  
#### <a name="to-delete-a-publication"></a>删除发布  
  
1.  在 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]中连接到发布服务器，然后展开服务器节点。  
  
2.  展开 **“复制”** 文件夹，再展开 **“本地发布”** 文件夹。  
  
3.  右键单击要删除的发布，然后单击 **“删除”**。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 可以使用复制存储过程以编程方式删除发布。 使用的存储过程取决于要删除的发布的类型。  
  
> [!NOTE]  
>  删除发布并不会删除发布数据库中的已发布对象，也不会删除订阅数据库中的相应对象。 如有必要，使用 `DROP <object>` 命令手动删除这些对象。  
  
#### <a name="to-delete-a-snapshot-or-transactional-publication"></a>删除快照发布或事务发布  
  
1.  执行以下操作之一：  
  
    -   若要删除单个发布，请在发布服务器上，对发布数据库执行 [sp_droppublication](/sql/relational-databases/system-stored-procedures/sp-droppublication-transact-sql) 。  
  
    -   若要删除发布数据库中的所有发布并删除其中的所有复制对象，请在发布服务器上执行 [sp_removedbreplication](/sql/relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql) 。 指定的值`tran`有关**@type**。 （可选）如果无法访问分发服务器，或者数据库的状态为可疑或脱机，则将 **@force** @type **@force**文件夹中删除发布。 （可选）如果未对发布数据库执行 **@dbname** ，则为 [sp_removedbreplication](/sql/relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql) 指定数据库的名称。  
  
        > [!NOTE]  
        >  将 **@force** @type **@force** 可能会使与复制相关的发布对象保留在数据库中。  
  
2.  如果此数据库中没有任何其他发布，则执行 [sp_replicationdboption &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql) 以禁止当前数据库使用快照复制或事务复制进行发布。  
  
3.  （可选）在订阅服务器上，对订阅数据库执行 [sp_subscription_cleanup](/sql/relational-databases/system-stored-procedures/sp-subscription-cleanup-transact-sql) 以删除订阅数据库中的任何剩余复制元数据。  
  
#### <a name="to-delete-a-merge-publication"></a>删除合并发布  
  
1.  执行以下操作之一：  
  
    -   若要删除单个发布，请在发布服务器上对发布数据库执行 [sp_dropmergepublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropmergepublication-transact-sql)。  
  
    -   若要删除发布数据库中的所有发布并删除其中的所有复制对象，请在发布服务器上执行 [sp_removedbreplication](/sql/relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql) 。 指定的值`merge`有关**@type**。 （可选）如果无法访问分发服务器，或者数据库的状态为可疑或脱机，则将 **@force** @type **@force**文件夹中删除发布。 （可选）如果未对发布数据库执行 **@dbname** ，则为 [sp_removedbreplication](/sql/relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql) 指定数据库的名称。  
  
        > [!NOTE]  
        >  将 **@force** @type **@force** 可能会使与复制相关的发布对象保留在数据库中。  
  
2.  如果此数据库中没有任何其他发布，则执行 [sp_replicationdboption &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql) 以禁止当前数据库使用合并复制进行发布。  
  
3.  在订阅服务器上，对订阅数据库执行 [sp_mergesubscription_cleanup &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-mergesubscription-cleanup-transact-sql) 以删除订阅数据库中的任何剩余复制元数据。  
  
###  <a name="TsqlExample"></a> 示例 (Transact-SQL)  
 该示例演示如何删除事务发布并禁用数据库的事务发布。 该示例假定以前删除了所有订阅。 有关详细信息，请参阅 [Delete a Pull Subscription](../delete-a-pull-subscription.md) 或 [Delete a Push Subscription](../delete-a-push-subscription.md)。  
  
 [!code-sql[HowTo#sp_droppublication](../../../snippets/tsql/SQL15/replication/howto/tsql/droptranpub.sql#sp_droppublication)]  
  
 该示例演示如何删除合并发布并禁用数据库的合并发布。 该示例假定以前删除了所有订阅。 有关详细信息，请参阅 [Delete a Pull Subscription](../delete-a-pull-subscription.md) 或 [Delete a Push Subscription](../delete-a-push-subscription.md)。  
  
 [!code-sql[HowTo#sp_dropmergepublication](../../../snippets/tsql/SQL15/replication/howto/tsql/dropmergepub.sql#sp_dropmergepublication)]  
  
##  <a name="RMOProcedure"></a> 使用复制管理对象 (RMO)  
 可以使用复制管理对象 (RMO) 以编程方式删除发布。 用于删除发布的 RMO 类取决于要删除的发布的类型。  
  
#### <a name="to-remove-a-snapshot-or-transactional-publication"></a>删除快照发布或事务发布  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 类创建与发布服务器的连接。  
  
2.  创建 <xref:Microsoft.SqlServer.Replication.TransPublication> 类的实例。  
  
3.  设置发布的 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> 和 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> 属性，并将 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 属性设置为步骤 1 中创建的连接。  
  
4.  请检查 <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> 属性以验证发布是否存在。 如果此属性的值为 `false`，则步骤 3 中的发布属性定义不正确，或者发布不存在。  
  
5.  调用 <xref:Microsoft.SqlServer.Replication.Publication.Remove%2A> 方法。  
  
6.  （可选）如果此数据库中不存在其他事务发布，则可按照下面的步骤为事务发布禁用此数据库：  
  
    1.  创建 <xref:Microsoft.SqlServer.Replication.ReplicationDatabase> 类的实例。 将 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 属性设置为步骤 1 中的 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 实例。  
  
    2.  调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法。 如果该方法返回 `false`，请确认数据库是否存在。  
  
    3.  将 <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.EnabledTransPublishing%2A> 属性设置为 `false`。  
  
    4.  调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 方法。  
  
7.  关闭连接。  
  
#### <a name="to-remove-a-merge-publication"></a>删除合并发布  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 类创建与发布服务器的连接。  
  
2.  创建 <xref:Microsoft.SqlServer.Replication.MergePublication> 类的实例。  
  
3.  设置发布的 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> 和 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> 属性，并将 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 属性设置为步骤 1 中创建的连接。  
  
4.  请检查 <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> 属性以验证发布是否存在。 如果此属性的值为 `false`，则步骤 3 中的发布属性定义不正确，或者发布不存在。  
  
5.  调用 <xref:Microsoft.SqlServer.Replication.Publication.Remove%2A> 方法。  
  
6.  （可选）如果此数据库中不存在其他合并发布，则可按照下面的步骤为合并发布禁用此数据库：  
  
    1.  创建 <xref:Microsoft.SqlServer.Replication.ReplicationDatabase> 类的实例。 将 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 属性设置为步骤 1 中的 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 实例。  
  
    2.  调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法。 如果该方法返回 `false`，请验证数据库是否存在。  
  
    3.  将 <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.EnabledMergePublishing%2A> 属性设置为 `false`。  
  
    4.  调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 方法。  
  
7.  关闭连接。  
  
###  <a name="PShellExample"></a> 示例 (RMO)  
 下面的示例删除事务发布。 如果此数据库不存在其他事务发布，则事务发布也被禁用。  
  
 [!code-csharp[HowTo#rmo_DropTranPub](../../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_droptranpub)]  
  
 [!code-vb[HowTo#rmo_vb_DropTranPub](../../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_droptranpub)]  
  
 下面的示例删除合并发布。 如果此数据库不存在其他合并发布，则合并发布也被禁用。  
  
 [!code-csharp[HowTo#rmo_DropMergePub](../../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_dropmergepub)]  
  
 [!code-vb[HowTo#rmo_vb_DropMergePub](../../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_dropmergepub)]  
  
## <a name="see-also"></a>请参阅  
 [Replication System Stored Procedures Concepts](../concepts/replication-system-stored-procedures-concepts.md)   
 [发布数据和数据库对象](publish-data-and-database-objects.md)  
  
  
