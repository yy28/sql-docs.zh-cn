---
title: 查看和修改推送订阅属性 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- viewing replication properties
- push subscriptions [SQL Server replication], properties
- subscriptions [SQL Server replication], push
- push subscriptions [SQL Server replication], modifying
- modifying replication properties, push subscriptions
- modifying subscriptions, SQL Server Management Studio
ms.assetid: 801d2995-7aa5-4626-906e-c8190758ec71
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 5dc55cc688f4e40d188492636c3653556f88b1c6
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/09/2019
ms.locfileid: "54127257"
---
# <a name="view-and-modify-push-subscription-properties"></a>查看和修改推送订阅属性
  本主题说明如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]或复制管理对象 (RMO) 在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中查看和修改推送订阅属性。  
  
 **本主题内容**  
  
-   **查看和修改推送订阅属性，使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [复制管理对象 (RMO)](#RMOProcedure)  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 可以从下列位置查看和修改发布服务器的推送订阅属性：  
  
-   **订阅属性-\<发布服务器 >:\<发布数据库 >** 对话框中，可从[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]。  
  
-   **“所有订阅”** 选项卡，该选项卡可以从复制监视器中找到。 有关启动复制监视器的信息，请参阅[启动复制监视器](monitor/start-the-replication-monitor.md)。  
  
#### <a name="to-view-and-modify-push-subscription-properties-in-management-studio"></a>在 Management Studio 中查看和修改推送订阅属性  
  
1.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中连接到发布服务器，然后展开服务器节点。  
  
2.  展开 **“复制”** 文件夹，再展开 **“本地发布”** 文件夹。  
  
3.  展开相应的发布，右键单击订阅，然后单击 **“属性”**。  
  
4.  根据需要修改属性，然后单击 **“确定”**。  
  
#### <a name="to-view-and-modify-push-subscription-properties-in-replication-monitor"></a>在复制监视器中查看和修改推送订阅属性  
  
1.  在复制监视器的左窗格中依次展开发布服务器组、发布服务器，然后单击某个发布。  
  
2.  单击 **“所有订阅”** 选项卡。  
  
3.  右键单击订阅，然后单击 **“属性”**。  
  
4.  根据需要修改属性，然后单击 **“确定”**。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 可以使用复制存储过程以编程方式修改推送订阅和访问其属性。 所用的存储过程取决于订阅所属的发布的类型。  
  
#### <a name="to-view-the-properties-of-a-push-subscription-to-a-snapshot-or-transactional-publication"></a>查看快照或事务发布的推送订阅的属性  
  
1.  在发布服务器上，对发布数据库执行 [sp_helpsubscription](/sql/relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql)。 指定 **@publication**或复制管理对象 (RMO) 在 **@subscriber**，并为 **@article** 指定值 **@article**中获取。  
  
2.  在发布服务器上，对发布数据库执行 [sp_helpsubscriberinfo](/sql/relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql)，同时指定 **@subscriber**中获取。  
  
#### <a name="to-change-the-properties-of-a-push-subscription-to-a-snapshot-or-transactional-publication"></a>更改快照或事务发布的推送订阅的属性  
  
1.  在发布服务器上，对发布数据库执行 [sp_changesubscriber](/sql/relational-databases/system-stored-procedures/sp-changesubscriber-transact-sql)，同时指定 **@subscriber** 及任何参数。  
  
2.  在发布服务器上，对发布数据库执行 [sp_changesubscription](/sql/relational-databases/system-stored-procedures/sp-changesubscription-transact-sql)。 指定 **@publication**或复制管理对象 (RMO) 在 **@subscriber**或复制管理对象 (RMO) 在 **@destination_db**，为 **@article** 指定值 **@article**，将 **@property**指定为要更改的订阅属性，并将 **@value**中获取。 这将更改推送订阅的安全设置。  
  
3.  （可选）若要更改订阅的 Data Transformation Services (DTS) 包属性，请在订阅服务器上，对订阅数据库执行 [sp_changesubscriptiondtsinfo](/sql/relational-databases/system-stored-procedures/sp-changesubscriptiondtsinfo-transact-sql) 。 为 **@jobid** 指定分发代理作业的 ID，并指定以下 DTS 包属性：  
  
    -   **@dts_package_name**  
  
    -   **@dts_package_password**  
  
    -   **@dts_package_location**  
  
     此操作将更改订阅的 DTS 包属性。  
  
    > [!NOTE]  
    >  可以通过执行 [sp_helpsubscription](/sql/relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql)来获得作业 ID。  
  
#### <a name="to-view-the-properties-of-a-push-subscription-to-a-merge-publication"></a>查看合并发布的推送订阅的属性  
  
1.  在发布服务器上，对发布数据库执行 [sp_helpmergesubscription](/sql/relational-databases/system-stored-procedures/sp-helpmergesubscription-transact-sql)。 指定 **@publication** 和 **@subscriber**中获取。  
  
2.  在发布服务器上，执行 [sp_helpsubscriberinfo](/sql/relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql)，同时指定 **@subscriber**中获取。  
  
#### <a name="to-change-the-properties-of-a-push-subscription-to-a-merge-publication"></a>更改合并发布的推送订阅的属性  
  
1.  在发布服务器上，对发布数据库执行 [sp_changemergesubscription](/sql/relational-databases/system-stored-procedures/sp-changemergesubscription-transact-sql)。 指定 **@publication**或复制管理对象 (RMO) 在 **@subscriber**或复制管理对象 (RMO) 在 **@subscriber_db**，将 **@property**指定为要更改的订阅属性，并将 **@value**中获取。  
  
###  <a name="TsqlExample"></a> 示例 (Transact-SQL)  
  
##  <a name="RMOProcedure"></a> 使用复制管理对象 (RMO)  
 用于查看或修改推送订阅属性的 RMO 类取决于订阅推送订阅的发布的类型。  
  
#### <a name="to-view-or-modify-properties-of-a-push-subscription-to-a-snapshot-or-transactional-publication"></a>查看或修改快照发布或事务发布的推送订阅的属性  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 类创建与发布服务器的连接。  
  
2.  创建 <xref:Microsoft.SqlServer.Replication.TransSubscription> 类的实例。  
  
3.  设置 <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>、 <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>、 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>和 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A> 属性。  
  
4.  将 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 属性设置为步骤 1 中的 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 。  
  
5.  调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法获取该对象的属性。 如果此方法返回 `false`，则说明步骤 3 中的订阅属性没有正确定义或该订阅不存在。  
  
6.  （可选）若要更改属性，请为可以设置的 <xref:Microsoft.SqlServer.Replication.TransSubscription> 属性中的一个设置新值，然后再调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 方法。  
  
7.  （可选）若要查看新设置，请调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.Refresh%2A> 方法重新加载此订阅的属性。  
  
#### <a name="to-view-or-modify-properties-of-a-push-subscription-to-a-merge-publication"></a>查看或修改合并发布的推送订阅的属性  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 类创建与订阅服务器的连接。  
  
2.  创建 <xref:Microsoft.SqlServer.Replication.MergeSubscription> 类的实例。  
  
3.  设置 <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>、 <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>、 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>和 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A> 属性。  
  
4.  将 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 属性设置为步骤 1 中的 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 。  
  
5.  调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法获取该对象的属性。 如果此方法返回 `false`，则说明步骤 3 中的订阅属性没有正确定义或该订阅不存在。  
  
6.  （可选）若要更改属性，请为可以设置的 <xref:Microsoft.SqlServer.Replication.MergeSubscription> 属性中的一个设置新值，然后再调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 方法。  
  
7.  （可选）若要查看新设置，请调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.Refresh%2A> 方法重新加载此订阅的属性。  
  
## <a name="see-also"></a>请参阅  
 [查看信息和执行其任务使用复制监视器](monitor/view-information-and-perform-tasks-replication-monitor.md)   
 [Replication Security Best Practices](security/replication-security-best-practices.md)   
 [订阅发布](subscribe-to-publications.md)  
  
  
