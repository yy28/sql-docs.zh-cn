---
title: 查看和修改请求订阅属性 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- modifying subscriptions
- viewing replication properties
- modifying replication properties, pull subscriptions
- pull subscriptions [SQL Server replication], modifying
- subscriptions [SQL Server replication], pull
- pull subscriptions [SQL Server replication], properties
- modifying subscriptions, SQL Server Management Studio
ms.assetid: 1601e54f-86f0-49e8-b023-87a5d1def033
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 1b847a22d31bbf3ea7540c55339fe27531134125
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85063717"
---
# <a name="view-and-modify-pull-subscription-properties"></a>查看和修改请求订阅属性
  本主题说明如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]或复制管理对象 (RMO) 在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中查看和修改请求订阅属性。  
  
 **本主题内容**  
  
-   **查看和修改请求订阅属性，使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [复制管理对象 (RMO)](#RMOProcedure)  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 在**订阅属性- \<Publisher> ： \<PublicationDatabase> **对话框中查看发布服务器或订阅服务器的请求订阅属性，可从获取该对话框 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 。 可以从订阅服务器中查看更多属性，并且可以在订阅服务器上修改属性。 也可以从发布服务器的 **“所有订阅”** 选项卡上查看属性信息，此选项卡可以通过复制监视器访问。 有关启动复制监视器的信息，请参阅[启动复制监视器](monitor/start-the-replication-monitor.md)。  
  
#### <a name="to-view-pull-subscription-properties-from-the-publisher-in-management-studio"></a>从 Management Studio 中的发布服务器查看请求订阅属性  
  
1.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中连接到发布服务器，然后展开服务器节点。  
  
2.  展开 **“复制”** 文件夹，再展开 **“本地发布”** 文件夹。  
  
3.  展开相应的发布，右键单击订阅，然后单击 **“属性”** 。  
  
4.  查看属性，然后单击 **“确定”** 。  
  
#### <a name="to-view-and-modify-pull-subscription-properties-from-the-subscriber-in-management-studio"></a>从 Management Studio 中的订阅服务器查看和修改请求订阅属性  
  
1.  在 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]中连接到订阅服务器，然后展开服务器节点。  
  
2.  展开 **“复制”** 文件夹，再展开 **“本地订阅”** 文件夹。  
  
3.  右键单击订阅，然后单击 **“属性”** 。  
  
4.  根据需要修改属性，然后单击 **“确定”** 。  
  
#### <a name="to-view-pull-subscription-properties-from-the-publisher-in-replication-monitor"></a>从复制监视器的发布服务器查看请求订阅属性  
  
1.  在复制监视器的左窗格中依次展开发布服务器组、发布服务器，然后单击某个发布。  
  
2.  单击 **“所有订阅”** 选项卡。  
  
3.  右键单击订阅，然后单击 **“属性”** 。  
  
4.  查看属性，然后单击 **“确定”** 。  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> 使用 Transact-SQL  
 可以使用复制存储过程以编程方式修改请求订阅以及访问其属性。 所用的存储过程取决于订阅所属的发布的类型。  
  
#### <a name="to-view-the-properties-of-a-pull-subscription-to-a-snapshot-or-transactional-publication"></a>查看对快照发布或事务发布的请求订阅的属性  
  
1.  在订阅服务器上，执行 [sp_helppullsubscription](/sql/relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql)。 指定 **@publisher** 、 **@publisher_db** 和 **@publication** 。 此操作将返回关于存储在订阅服务器上系统表中的订阅的信息。  
  
2.  在订阅服务器上，执行 [sp_helpsubscription_properties](/sql/relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql)。 **@publisher**为指定、 **@publisher_db** 、 **@publication** 和以下值之一 **@publication_type** ：  
  
    -   **0** - 订阅属于事务发布。  
  
    -   **1** - 订阅属于快照发布。  
  
3.  在发布服务器上，执行 [sp_helpsubscription](/sql/relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql)。 指定 **@publication** 和 **@subscriber** 。  
  
4.  在发布服务器上，执行 [sp_helpsubscriberinfo](/sql/relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql)，同时指定 **@subscriber**访问该对话框）中，可以从发布服务器或订阅服务器查看请求订阅属性。 此操作将显示关于订阅服务器的信息。  
  
#### <a name="to-change-the-properties-of-a-pull-subscription-to-a-snapshot-or-transactional-publication"></a>更改对快照发布或事务发布的请求订阅的属性  
  
1.  在订阅服务器上，执行[sp_change_subscription_properties](/sql/relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql)，同时指定 **@publisher** 、、、值为 **@publisher_db** **@publication** **0** （事务）或**1** （快照） **@publication_type** 、要更改为的订阅属性 **@property** ，以及新值为 **@value** 。  
  
2.  （可选）在订阅服务器上，对订阅数据库执行 [sp_changesubscriptiondtsinfo](/sql/relational-databases/system-stored-procedures/sp-changesubscriptiondtsinfo-transact-sql)。 为指定分发代理作业的 ID **@jobid** ，并指定以下数据转换服务（DTS）包属性：  
  
    -   **@dts_package_name**  
  
    -   **@dts_package_password**  
  
    -   **@dts_package_location**  
  
     此操作将更改订阅的 DTS 包属性。  
  
    > [!NOTE]  
    >  可以通过执行 [sp_helpsubscription](/sql/relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql)来获得作业 ID。  
  
#### <a name="to-view-the-properties-of-a-pull-subscription-to-a-merge-publication"></a>查看对合并发布的请求订阅的属性  
  
1.  在订阅服务器上，执行 [sp_helpmergepullsubscription](/sql/relational-databases/system-stored-procedures/sp-helpmergepullsubscription-transact-sql)。 指定 **@publisher** 、 **@publisher_db** 和 **@publication** 。  
  
2.  在订阅服务器上，执行 [sp_helpsubscription_properties](/sql/relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql)。 **@publisher**将、 **@publisher_db** 、 **@publication** 和的值指定为 2 **@publication_type** 。  
  
3.  在发布服务器上，执行 [sp_helpmergesubscription](/sql/relational-databases/system-stored-procedures/sp-helpmergesubscription-transact-sql) 以显示订阅信息。 若要返回有关特定订阅的信息，您必须 **@publication** **@subscriber** 为、和的值指定**pull** **@subscription_type** 。  
  
4.  在发布服务器上，执行 [sp_helpsubscriberinfo](/sql/relational-databases/system-stored-procedures/sp-helpsubscriberinfo-transact-sql)，同时指定 **@subscriber**访问该对话框）中，可以从发布服务器或订阅服务器查看请求订阅属性。 此操作将显示关于订阅服务器的信息。  
  
#### <a name="to-change-the-properties-of-a-pull-subscription-to-a-merge-publication"></a>更改对合并发布的请求订阅的属性  
  
1.  在订阅服务器上，执行 [sp_changemergepullsubscription](/sql/relational-databases/system-stored-procedures/sp-changemergepullsubscription-transact-sql)。 指定 **@publication** 、 **@publisher** 、 **@publisher_db** 、要更改为的订阅属性 **@property** ，并将新值指定为 **@value** 。  
  
##  <a name="using-replication-management-objects-rmo"></a><a name="RMOProcedure"></a> 使用复制管理对象 (RMO)  
 用于查看或修改请求订阅属性的 RMO 类取决于订阅请求订阅的发布类型。  
  
#### <a name="to-view-or-modify-properties-of-a-pull-subscription-to-a-snapshot-or-transactional-publication"></a>查看或修改对快照发布或事务发布的请求订阅的属性  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 类创建与订阅服务器的连接。  
  
2.  创建的 <xref:Microsoft.SqlServer.Replication.TransPullSubscription> 类的实例。  
  
3.  设置 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>、 <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>、 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>和 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A> 属性。  
  
4.  为 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 属性设置步骤 1 中的连接。  
  
5.  调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法获取该对象的属性。 如果此方法返回 `false`，则说明步骤 3 中的订阅属性定义不正确或服务器上不存在此订阅。  
  
6.  （可选）若要更改属性，请为可以设置的 <xref:Microsoft.SqlServer.Replication.TransPullSubscription> 属性中的一个设置新值，然后再调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 方法。  
  
7.  （可选）若要查看新设置，请调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.Refresh%2A> 方法以重新加载该项目的属性。  
  
8.  关闭所有连接。  
  
#### <a name="to-view-or-modify-properties-of-a-pull-subscription-to-a-merge-publication"></a>查看或修改对合并发布的请求订阅的属性  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 类创建与订阅服务器的连接。  
  
2.  创建的 <xref:Microsoft.SqlServer.Replication.MergePullSubscription> 类的实例。  
  
3.  设置 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>、 <xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>、 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>和 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A> 属性。  
  
4.  为 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 属性设置步骤 1 中的连接。  
  
5.  调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法获取该对象的属性。 如果此方法返回 `false`，则说明步骤 3 中的订阅属性定义不正确或服务器上不存在此订阅。  
  
6.  （可选）若要更改属性，请为可以设置的 <xref:Microsoft.SqlServer.Replication.MergePullSubscription> 属性中的一个设置新值，然后再调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 方法。  
  
7.  （可选）若要查看新设置，请调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.Refresh%2A> 方法以重新加载该项目的属性。  
  
8.  关闭所有连接。  
  
## <a name="see-also"></a>另请参阅  
 [使用复制监视器查看信息和执行任务](monitor/view-information-and-perform-tasks-replication-monitor.md)   
 [Replication Security Best Practices](security/replication-security-best-practices.md)   
 [订阅发布](subscribe-to-publications.md)  
  
  
