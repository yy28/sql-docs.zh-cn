---
title: 创建推送订阅 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- push subscriptions [SQL Server replication], creating
- merge replication subscribing [SQL Server replication], push subscriptions
- subscriptions [SQL Server replication], push
- snapshot replication [SQL Server], subscribing
- transactional replication, subscribing
ms.assetid: adfbbc61-58d1-4330-9ad6-b14ab1142e2b
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b571bec94c873b830654126e39d75d554599e5fa
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/09/2019
ms.locfileid: "54135537"
---
# <a name="create-a-push-subscription"></a>创建推送订阅
  本主题说明如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]或复制管理对象 (RMO) 在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中创建推送订阅。 有关为非 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 订阅服务器创建推送订阅的信息，请参阅[为非 SQL Server 订阅服务器创建订阅](create-a-subscription-for-a-non-sql-server-subscriber.md)。  
  
  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 使用新建订阅向导，在发布服务器或订阅服务器上创建推送订阅。 按照向导中的页的指示执行下列操作：  
  
-   指定发布服务器和发布。  
  
-   选择运行复制代理的位置。 对于推送订阅，根据发布类型的不同，在 **“分发代理位置”** 页或 **“合并代理位置”** 页上选择 **“在分发服务器上运行所有代理(推送订阅)”** 。  
  
-   指定订阅服务器和订阅数据库。  
  
-   指定复制代理建立连接所用的登录名和密码：  
  
    -   对于快照发布和事务发布的订阅，在 **“分发代理安全性”** 页上指定凭据。  
  
    -   对于合并发布的订阅，在 **“合并代理安全性”** 页上指定凭据。  
  
     有关每个代理所需权限的信息，请参阅 [R复制代理安全模式](security/replication-agent-security-model.md)。  
  
-   指定同步计划和初始化订阅服务器的时间。  
  
-   指定合并发布的其他选项：订阅类型以及用于参数化筛选的值。  
  
-   指定允许更新订阅的事务发布的其他选项：订阅服务器是立即在发布服务器上提交更改还是将它们写入队列、用于从订阅服务器连接到发布服务器的凭据。  
  
-   还可以编写订阅的脚本（可选）。  
  
#### <a name="to-create-a-push-subscription-from-the-publisher"></a>从发布服务器创建推送订阅  
  
1.  在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中连接到发布服务器，然后展开服务器节点。  
  
2.  展开 **“复制”** 文件夹，再展开 **“本地发布”** 文件夹。  
  
3.  右键单击要为其创建一个或多个订阅的发布，然后单击 **“新建订阅”**。  
  
4.  完成新建订阅向导中的页。  
  
#### <a name="to-create-a-push-subscription-from-the-subscriber"></a>从订阅服务器创建推送订阅  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中连接到订阅服务器，然后展开服务器节点。  
  
2.  展开 **“复制”** 文件夹。  
  
3.  右键单击 **“本地订阅”** 文件夹，再单击 **“新建订阅”**。  
  
4.  在新建订阅向导的“发布”页上，从“发布服务器”下拉列表中选择“\<查找 SQL Server 发布服务器>”或“\<查找 Oracle 发布服务器>”。  
  
5.  在 **“连接到服务器”** 对话框中连接到发布服务器。  
  
6.  在 **“发布”** 页上，选择一个发布。  
  
7.  完成新建订阅向导中的页。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 可以使用复制存储过程以编程方式创建推送订阅。 所用的存储过程取决于订阅所属的发布的类型。  
  
> [!IMPORTANT]  
>  如果可能，请在运行时提示用户输入安全凭据。 如果必须在脚本文件中存储凭据，则必须保护文件以防止未经授权的访问。  
  
#### <a name="to-create-a-push-subscription-to-a-snapshot-or-transactional-publication"></a>创建快照或事务发布的推送订阅  
  
1.  在发布服务器的发布数据库中，通过执行 [sp_helppublication](/sql/relational-databases/system-stored-procedures/sp-helppublication-transact-sql)核实发布是否支持推送订阅。  
  
    -   如果 **allow_push** 的值为 **1**，则支持推送订阅。  
  
    -   如果的值**allow_push**是**0**，执行[sp_changepublication](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql)，并指定**allow_push**为 **@property**并`true`有关**@value**。  
  
2.  在发布服务器的发布数据库中，执行 [sp_addsubscription](/sql/relational-databases/system-stored-procedures/sp-addsubscription-transact-sql)。 指定 **@publication**或复制管理对象 (RMO) 在 **@subscriber** ，将 **@destination_db**。 将 **@subscription_type** 指定为 **@subscription_type**。 有关如何更新 subscription 的信息，请参阅[创建事务发布的可更新订阅](publish/create-an-updatable-subscription-to-a-transactional-publication.md)  
  
3.  在发布服务器的发布数据库中，执行 [sp_addpushsubscription_agent](/sql/relational-databases/system-stored-procedures/sp-addpushsubscription-agent-transact-sql)。 指定下列各项：  
  
    -   分发服务器中的分发代理运行时所使用的 **@subscriber**或复制管理对象 (RMO) 在 **@subscriber_db**和 **@publication** 参数。  
  
    -   分发服务器中的分发代理运行时所使用的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] @job_login **@job_login** ，将 **@job_password**。  
  
        > [!NOTE]  
        >  使用 Windows 集成身份验证进行的连接始终使用由 **@job_login** 和 **@job_password**中为非 SQL Server 订阅服务器创建订阅。 分发代理始终使用 Windows 集成身份验证与分发服务器建立本地连接。 默认情况下，该代理将使用 Windows 集成身份验证连接到订阅服务器。  
  
    -   （可选） **0** 指定为 **@subscriber_security_mode** 值以及 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 **@subscriber_login** ，将 **@subscriber_password**。 如果您需要在连接到订阅服务器时使用 SQL Server 身份验证，则指定这些参数。  
  
    -   该订阅的分发代理作业计划。 有关详细信息，请参阅 [Specify Synchronization Schedules](specify-synchronization-schedules.md)。  
  
    > [!IMPORTANT]  
    >  用远程分发服务器在发布服务器上创建推送订阅时，为所有参数（包括 *job_login* 和 *job_password*）提供的值将以纯文本格式发送到分发服务器。 在执行此存储过程之前，应该对发布服务器及其远程分发服务器之间的连接进行加密。 有关详细信息，请参阅[启用数据库引擎的加密连接（SQL Server 配置管理器）](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)。  
  
#### <a name="to-create-a-push-subscription-to-a-merge-publication"></a>创建合并发布的推送订阅  
  
1.  在发布服务器的发布数据库中，通过执行 [sp_helpmergepublication](/sql/relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql)核实发布是否支持推送订阅。  
  
    -   如果 **allow_push** 的值为 **1**，则发布支持推送订阅。  
  
    -   如果的值**allow_push**不是**1**，执行[sp_changemergepublication](/sql/relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql)，并指定**allow_push**为**@property** 并`true`有关**@value**。  
  
2.  在发布服务器的发布数据库中，执行 [sp_addmergesubscription](/sql/relational-databases/system-stored-procedures/sp-addmergesubscription-transact-sql)，并指定以下参数：  
  
    -   **@publication**。 这是发布的名称。  
  
    -   **@subscriber_type**。 对于客户端订阅，请指定 **local** ，对于服务器订阅，请指定 **global**。  
  
    -   **@subscription_priority**。 对于服务器订阅，请指定订阅的优先级（从**0.00** 到 **99.99**）。  
  
         有关详细信息，请参阅 [高级合并复制冲突的检测和解决](merge/advanced-merge-replication-conflict-detection-and-resolution.md)。  
  
3.  在发布服务器的发布数据库中，执行 [sp_addmergepushsubscription_agent](/sql/relational-databases/system-stored-procedures/sp-addmergepushsubscription-agent-transact-sql)。 指定下列各项：  
  
    -   订阅服务器中的分发代理运行时所使用的 **@subscriber**或复制管理对象 (RMO) 在 **@subscriber_db**和 **@publication** 参数。  
  
    -   分发服务器中的合并代理运行时所使用的 **@job_login** ，将 **@job_password**。  
  
        > [!NOTE]  
        >  使用 Windows 集成身份验证进行的连接始终使用由 **@job_login** ，将 **@job_password**。 合并代理始终使用 Windows 集成身份验证与分发服务器进行本地连接。 默认情况下，该代理将使用 Windows 集成身份验证连接到订阅服务器。  
  
    -   （可选） **0** 指定为 **@subscriber_security_mode** 值以及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 **@subscriber_login** ，将 **@subscriber_password**。 如果您需要在连接到订阅服务器时使用 SQL Server 身份验证，则指定这些参数。  
  
    -   （可选） **0** 指定为 **@publisher_security_mode** 值以及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 **@publisher_login** ，将 **@publisher_password**。 如果您需要在连接到发布服务器时使用 SQL Server 身份验证，则指定这些值。  
  
    -   该订阅的合并代理作业计划。 有关详细信息，请参阅 [Specify Synchronization Schedules](specify-synchronization-schedules.md)。  
  
    > [!IMPORTANT]  
    >  用远程分发服务器在发布服务器上创建推送订阅时，为所有参数（包括 *job_login* 和 *job_password*）提供的值将以纯文本格式发送到分发服务器。 在执行此存储过程之前，应该对发布服务器及其远程分发服务器之间的连接进行加密。 有关详细信息，请参阅[启用数据库引擎的加密连接（SQL Server 配置管理器）](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)。  
  
###  <a name="TsqlExample"></a> 示例 (Transact-SQL)  
 以下示例创建事务发布的推送订阅。 登录名和密码值在运行时使用 **sqlcmd** 脚本变量提供。  
  
 [!code-sql[HowTo#sp_addtranpushsubscription_agent](../../snippets/tsql/SQL15/replication/howto/tsql/createtranpushsub.sql#sp_addtranpushsubscription_agent)]  
  
 以下示例创建合并发布的推送订阅。 登录名和密码值在运行时使用 **sqlcmd** 脚本变量提供。  
  
 [!code-sql[HowTo#sp_addmergepushsubscriptionagent](../../snippets/tsql/SQL15/replication/howto/tsql/createmergepushsub.sql#sp_addmergepushsubscriptionagent)]  
  
##  <a name="RMOProcedure"></a> 使用复制管理对象 (RMO)  
 可以使用复制管理对象 (RMO) 以编程方式创建推送订阅。 用于创建推送订阅的 RMO 类取决于对其创建订阅的发布的类型。  
  
> [!IMPORTANT]  
>  如果可能，请在运行时提示用户输入安全凭据。 如果必须存储凭据，请使用 [Windows .NET Framework 提供的](https://go.microsoft.com/fwlink/?LinkId=34733) Cryptographic Services [!INCLUDE[msCoName](../../includes/msconame-md.md)] （加密服务）。  
  
#### <a name="to-create-a-push-subscription-to-a-snapshot-or-transactional-publication"></a>创建快照或事务发布的推送订阅  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 类创建与发布服务器的连接。  
  
2.  使用步骤 1 中的发布服务器连接，创建 <xref:Microsoft.SqlServer.Replication.TransPublication> 类的实例。 指定 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>、 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A>和 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>。  
  
3.  调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法。 如果此方法返回`false`，步骤 2 中指定的属性不正确或服务器上不存在发布。  
  
4.  在 <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> 属性和 <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowPush> 之间执行逻辑位与（在 Visual C# 中为 `&`，在 Visual Basic 中为 `And`）运算。 如果结果为 <xref:Microsoft.SqlServer.Replication.PublicationAttributes.None>，则将 <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> 设置为 <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> 和 <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowPush> 之间的逻辑位或（在 Visual C# 中为 `|`，在 Visual Basic 为 `Or`）的结果。 然后，调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 以启用推送订阅。  
  
5.  如果订阅数据库不存在，则使用 <xref:Microsoft.SqlServer.Management.Smo.Database> 类创建该数据库。 有关详细信息，请参阅[创建、更改和删除数据库](../server-management-objects-smo/tasks/creating-altering-and-removing-databases.md)。  
  
6.  创建 <xref:Microsoft.SqlServer.Replication.TransSubscription> 类的实例。  
  
7.  设置下列订阅属性：  
  
    -   在步骤 1 中为 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 创建的与发布服务器的 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>。  
  
    -   用于 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A>的订阅数据库的名称。  
  
    -   用于 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>的订阅服务器的名称。  
  
    -   用于 <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>的发布数据库的名称。  
  
    -   用于 <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>的发布的名称。  
  
    -   <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> 的 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> 和 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.SecurePassword%2A> 或 <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A> 字段，用于提供分发代理在分发服务器中运行所使用的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 帐户的凭据。 该帐户用于与分发服务器进行本地连接，同时还用于使用 Windows 身份验证进行远程连接。  
  
        > [!NOTE]  
        >  当 `sysadmin` 固定服务器角色的成员创建订阅时，不需要设置 <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A>，尽管建议这样做。 在这种情况下，代理会模拟 SQL Server Agent 帐户。 有关详细信息，请参阅 [复制代理安全模式](security/replication-agent-security-model.md)。  
  
    -   （可选）<xref:Microsoft.SqlServer.Replication.Subscription.CreateSyncAgentByDefault%2A> 的 `true` 值（默认值），用于创建用来同步订阅的代理作业。 如果您指定了 `false`，则只能以编程的方式同步订阅。  
  
    -   （可选）在使用 SQL Server 身份验证连接到订阅服务器时设置 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> 的 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> 和 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SecureSqlStandardPassword%2A> 或 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberSecurity%2A> 字段。  
  
8.  调用 <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A> 方法。  
  
    > [!IMPORTANT]  
    >  在具有远程分发服务器的发布服务器上创建推送订阅时，为所有属性（包括 <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A>）提供的值将作为纯文本发送到分发服务器。 在调用 <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A> 方法之前，应该对发布服务器与其远程分发服务器之间的连接进行加密。 有关详细信息，请参阅[启用数据库引擎的加密连接（SQL Server 配置管理器）](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)。  
  
#### <a name="to-create-a-push-subscription-to-a-merge-publication"></a>创建合并发布的推送订阅  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 类创建与发布服务器的连接。  
  
2.  使用步骤 1 中的发布服务器连接，创建 <xref:Microsoft.SqlServer.Replication.MergePublication> 类的实例。 指定 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>、 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A>和 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>。  
  
3.  调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法。 如果此方法返回`false`，步骤 2 中指定的属性不正确或服务器上不存在发布。  
  
4.  在 <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> 属性和 <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowPush> 之间执行逻辑位与（在 Visual C# 中为 `&`，在 Visual Basic 中为 `And`）运算。 如果结果为 <xref:Microsoft.SqlServer.Replication.PublicationAttributes.None>，则将 <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> 设置为 <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> 和 <xref:Microsoft.SqlServer.Replication.PublicationAttributes.AllowPush> 之间的逻辑位或（在 Visual C# 中为 `|`，在 Visual Basic 为 `Or`）的结果。 然后，调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 以启用推送订阅。  
  
5.  如果订阅数据库不存在，则使用 <xref:Microsoft.SqlServer.Management.Smo.Database> 类创建该数据库。 有关详细信息，请参阅[创建、更改和删除数据库](../server-management-objects-smo/tasks/creating-altering-and-removing-databases.md)。  
  
6.  创建 <xref:Microsoft.SqlServer.Replication.MergeSubscription> 类的实例。  
  
7.  设置下列订阅属性：  
  
    -   在步骤 1 中为 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 创建的与发布服务器的 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>。  
  
    -   用于 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A>的订阅数据库的名称。  
  
    -   用于 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>的订阅服务器的名称。  
  
    -   用于 <xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>的发布数据库的名称。  
  
    -   用于 <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>的发布的名称。  
  
    -   <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> 的 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> 和 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.SecurePassword%2A> 或 <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A> 字段，用于提供合并代理在分发服务器中运行时所使用的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 帐户的凭据。 该帐户用于与分发服务器进行本地连接，同时还用于使用 Windows 身份验证进行远程连接。  
  
        > [!NOTE]  
        >  当 `sysadmin` 固定服务器角色的成员创建订阅时，不需要设置 <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A>，尽管建议这样做。 在这种情况下，代理会模拟 SQL Server Agent 帐户。 有关详细信息，请参阅 [复制代理安全模式](security/replication-agent-security-model.md)。  
  
    -   （可选）<xref:Microsoft.SqlServer.Replication.Subscription.CreateSyncAgentByDefault%2A> 的 `true` 值（默认值），用于创建用来同步订阅的代理作业。 如果您指定了 `false`，则只能以编程的方式同步订阅。  
  
    -   （可选）在使用 SQL Server 身份验证连接到订阅服务器时设置 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> 的 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> 和 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SecureSqlStandardPassword%2A> 或 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberSecurity%2A> 字段。  
  
    -   （可选）在使用 SQL Server 身份验证连接到发布服务器时设置 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> 的 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> 和 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SecureSqlStandardPassword%2A> 或 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherSecurity%2A> 字段。  
  
8.  调用 <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A> 方法。  
  
    > [!IMPORTANT]  
    >  在具有远程分发服务器的发布服务器上创建推送订阅时，为所有属性（包括 <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A>）提供的值将作为纯文本发送到分发服务器。 在调用 <xref:Microsoft.SqlServer.Replication.Subscription.Create%2A> 方法之前，应该对发布服务器与其远程分发服务器之间的连接进行加密。 有关详细信息，请参阅[启用数据库引擎的加密连接（SQL Server 配置管理器）](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)。  
  
###  <a name="PShellExample"></a> 示例 (RMO)  
 该示例创建事务发布的新推送订阅。 用于运行分发代理作业的 Windows 帐户凭据在运行时通过。  
  
 [!code-csharp[HowTo#rmo_CreateTranPushSub](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_createtranpushsub)]  
  
 [!code-vb[HowTo#rmo_vb_CreateTranPushSub](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_createtranpushsub)]  
  
 该示例创建合并发布的新推送订阅。 用于运行合并代理作业的 Windows 帐户凭据在运行时通过。  
  
 [!code-csharp[HowTo#rmo_CreateMergePushSub](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_createmergepushsub)]  
  
 [!code-vb[HowTo#rmo_vb_CreateMergePushSub](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_createmergepushsub)]  
  
## <a name="see-also"></a>请参阅  
 [查看和修改推送订阅属性](view-and-modify-push-subscription-properties.md)   
 [Replication Security Best Practices](security/replication-security-best-practices.md)   
 [Create a Publication](publish/create-a-publication.md)   
 [Replication Management Objects Concepts](concepts/replication-management-objects-concepts.md)   
 [同步推送订阅](synchronize-a-push-subscription.md)   
 [Subscribe to Publications](subscribe-to-publications.md)   
 [将 sqlcmd 与脚本变量结合使用](../scripting/sqlcmd-use-with-scripting-variables.md)  
  
  
