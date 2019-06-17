---
title: 删除推送订阅 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- removing subscriptions
- push subscriptions [SQL Server replication], deleting
- deleting subscriptions
- subscriptions [SQL Server replication], push
ms.assetid: 3c4847e2-aed9-4488-b45d-8164422bdb10
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 75e5953d8f7ef9af1134db56f7061261eee2c0fd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62721430"
---
# <a name="delete-a-push-subscription"></a>删除推送订阅
  本主题说明如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]或复制管理对象 (RMO) 在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中删除推送订阅。  
  
 **本主题内容**  
  
-   **删除推送订阅，使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [复制管理对象 (RMO)](#RMOProcedure)  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 删除发布服务器（从 **的** “本地发布” [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]文件夹）或订阅服务器（从 **“本地订阅”** 文件夹）上的推送订阅。 删除订阅不会从订阅中删除对象或数据，必须对其手动删除。  
  
#### <a name="to-delete-a-push-subscription-at-the-publisher"></a>删除发布服务器上的推送订阅  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中连接到发布服务器，然后展开服务器节点。  
  
2.  展开 **“复制”** 文件夹，再展开 **“本地发布”** 文件夹。  
  
3.  展开与要删除的订阅关联的发布。  
  
4.  右键单击该订阅，再单击 **“删除”** 。  
  
5.  在确认对话框中，选择是否连接到订阅服务器以删除订阅信息。 如果清除了 **“连接到订阅服务器”** 复选框，则应以后连接到订阅服务器删除信息。  
  
#### <a name="to-delete-a-push-subscription-at-the-subscriber"></a>删除订阅服务器上的推送订阅  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中连接到订阅服务器，然后展开服务器节点。  
  
2.  展开 **“复制”** 文件夹，再展开 **“本地订阅”** 文件夹。  
  
3.  右键单击要删除的订阅，再单击 **“删除”** 。  
  
4.  在确认对话框中，选择是否连接到发布服务器以删除订阅信息。 如果清除 **“连接到发布服务器”** 复选框，则应在以后连接到发布服务器以删除订阅信息。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 可以使用复制存储过程以编程方式删除推送订阅。 所用的存储过程取决于订阅所属的发布的类型。  
  
#### <a name="to-delete-a-push-subscription-to-a-snapshot-or-transactional-publication"></a>删除快照发布或事务发布的推送订阅  
  
1.  在发布服务器上，对发布数据库执行 [sp_dropsubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropsubscription-transact-sql)。 指定 **@publication** 和 **@subscriber** 中通过 FTP 传递快照。 将 **@article** 的值指定为 **@article** 。 （可选）如果无法访问分发服务器，将 **@ignore_distributor** 的值指定为 **@ignore_distributor** ，以便在不删除分发服务器上相关对象的情况下删除订阅。  
  
2.  在订阅服务器上，对订阅数据库执行 [sp_subscription_cleanup &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-subscription-cleanup-transact-sql) 以删除订阅数据库中的复制元数据。  
  
#### <a name="to-delete-a-push-subscription-to-a-merge-publication"></a>删除合并发布的推送订阅  
  
1.  在发布服务器上，执行 [sp_dropmergesubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dropmergesubscription-transact-sql)，并指定 **@publication** 、 **@subscriber** 和 **@subscriber_db** 。 （可选）如果无法访问分发服务器，将 **@ignore_distributor** 的值指定为 **@ignore_distributor** ，以便在不删除分发服务器上相关对象的情况下删除订阅。  
  
2.  在订阅服务器上，对订阅数据库执行 [sp_mergesubscription_cleanup &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-mergesubscription-cleanup-transact-sql)。 指定 **@publisher** 或复制管理对象 (RMO) 在 **@publisher_db** 和 **@publication** 文件夹中打开。 这将会删除订阅数据库中的合并元数据。  
  
###  <a name="TsqlExample"></a> 示例 (Transact-SQL)  
 该示例删除对事务发布的推送订阅。  
  
 [!code-sql[HowTo#sp_droptransubscription](../../snippets/tsql/SQL15/replication/howto/tsql/droptranpullsub.sql#sp_droptransubscription)]  
  
 该示例删除对合并发布的推送订阅。  
  
 [!code-sql[HowTo#sp_dropmergesubscription](../../snippets/tsql/SQL15/replication/howto/tsql/dropmergepullsub.sql#sp_dropmergesubscription)]  
  
##  <a name="RMOProcedure"></a> 使用复制管理对象 (RMO)  
 用于删除推送订阅的 RMO 类取决于订阅推送订阅的发布的类型。  
  
#### <a name="to-delete-a-push-subscription-to-a-snapshot-or-transactional-publication"></a>删除快照发布或事务发布的推送订阅  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 类创建与订阅服务器的连接。  
  
2.  创建 <xref:Microsoft.SqlServer.Replication.TransSubscription> 类的实例。  
  
3.  设置 <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>、 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A>、 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>和 <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A> 属性。  
  
4.  将 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 属性设置为步骤 1 中的 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 。  
  
5.  检查 <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> 属性以确保该订阅存在。 如果此属性的值为 `false`，则步骤 2 中所定义的订阅属性不正确或者该订阅不存在。  
  
6.  调用 <xref:Microsoft.SqlServer.Replication.Subscription.Remove%2A> 方法。  
  
#### <a name="to-delete-a-push-subscription-to-a-merge-publication"></a>删除合并发布的推送订阅  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 类创建与订阅服务器的连接。  
  
2.  创建 <xref:Microsoft.SqlServer.Replication.MergeSubscription> 类的实例。  
  
3.  设置 <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>、 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A>、 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>和 <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A> 属性。  
  
4.  将 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 属性设置为步骤 1 中的 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 。  
  
5.  检查 <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> 属性以确保该订阅存在。 如果此属性的值为 `false`，则步骤 2 中所定义的订阅属性不正确或者该订阅不存在。  
  
6.  调用 <xref:Microsoft.SqlServer.Replication.Subscription.Remove%2A> 方法。  
  
###  <a name="PShellExample"></a> 示例 (RMO)  
 可通过使用复制管理对象 (RMO) 以编程方式删除推送订阅。  
  
 [!code-csharp[HowTo#rmo_DropTranPushSub](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_droptranpushsub)]  
  
 [!code-vb[HowTo#rmo_vb_DropTranPushSub](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_droptranpushsub)]  
  
## <a name="see-also"></a>请参阅  
 [订阅发布](subscribe-to-publications.md)   
 [复制安全最佳做法](security/replication-security-best-practices.md)  
  
  
