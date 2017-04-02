---
title: "查看和修改分发服务器和发布服务器属性 | Microsoft Docs"
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
  - "查看复制属性"
  - "分发服务器 [SQL Server 复制], 修改"
  - "修改复制属性, 分发服务器"
  - "分发服务器 [SQL Server 复制], 属性"
ms.assetid: 5dae1d59-c377-4c6e-adc9-b68c5b328f79
caps.latest.revision: 43
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 43
---
# 查看和修改分发服务器和发布服务器属性
  本主题说明如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或复制管理对象 (RMO) 在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中查看和修改分发服务器和发布服务器属性。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [建议](#Recommendations)  
  
     [安全性](#Security)  
  
-   **查看和修改分发服务器和发布服务器属性，使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [复制管理对象 (RMO)](#RMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Recommendations"></a> 建议  
  
-   对于运行低于 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]版本的发布服务器， **sysadmin** 固定服务器角色中的用户可以在 **“订阅服务器”** 页上注册订阅服务器。 从 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]开始，不再需要为复制显式注册订阅服务器。  
  
###  <a name="Security"></a> 安全性  
 如果可能，请在运行时提示用户输入安全凭据。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### 查看和修改分发服务器属性  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中连接到分发服务器，然后展开服务器节点。  
  
2.  用鼠标右键单击 **复制** 文件夹，，然后单击 **分发服务器属性**。  
  
3.  查看和修改属性在 **分发服务器属性-\< 分发服务器>** 对话框。  
  
    -   若要查看和修改分发数据库的属性，请单击属性按钮 (**...**) 上的数据库 **常规** 对话框左侧的页。  
  
    -   若要查看和修改发布服务器与分发服务器相关联的属性，请单击属性按钮 (**...**) 发布服务器上，为 **出版商** 对话框中的页。  
  
    -   若要访问复制代理的配置文件，请单击此对话框的 **“常规”** 页上的 **“默认配置文件”** 按钮。 有关详细信息，请参阅 [Replication Agent Profiles](../../relational-databases/replication/agents/replication-agent-profiles.md)。  
  
    -   若要更改管理存储过程在发布服务器上执行以及在分发服务器上更新信息时所用帐户的密码，请在该对话框的 **“发布服务器”** 页面上的 **“密码”** 和 **“确认密码”** 框中输入新密码。 有关详细信息，请参阅 [安全分发服务器](../../relational-databases/replication/security/secure-the-distributor.md)。  
  
4.  根据需要修改属性，然后单击 **“确定”**。  
  
#### 查看和修改发布服务器属性  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中连接到发布服务器，然后展开服务器节点。  
  
2.  用鼠标右键单击 **复制** 文件夹，，然后单击 **发布服务器属性**。  
  
3.  查看和修改属性在 **发布服务器属性-\< 发布服务器 >** 对话框。  
  
    -   **sysadmin** 固定服务器角色中的用户可以在 **“发布数据库”** 页上为复制启用数据库。 启用数据库不会将发布该数据库;相反，它允许任何用户 **db_owner** 该数据库在数据库中创建一个或多个发布的固定的数据库角色。  
  
4.  根据需要修改属性，然后单击 **“确定”**。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 可以使用复制存储过程以编程方式查看发布服务器和分发服务器属性。  
  
#### 查看分发服务器和分发数据库属性  
  
1.  执行 [sp_helpdistributor](../../relational-databases/system-stored-procedures/sp-helpdistributor-transact-sql.md) 来返回有关分发服务器、 分发数据库和工作目录的信息。  
  
2.  执行 [sp_helpdistributiondb](../../relational-databases/system-stored-procedures/sp-helpdistributiondb-transact-sql.md) 来返回指定的分发数据库的属性。  
  
#### 更改分发服务器和分发数据库属性  
  
1.  在分发服务器上，执行 [sp_changedistributor_property](../../relational-databases/system-stored-procedures/sp-changedistributor-property-transact-sql.md) 修改分发服务器属性。  
  
2.  在分发服务器上，执行 [sp_changedistributiondb](../../relational-databases/system-stored-procedures/sp-changedistributiondb-transact-sql.md) 修改分发数据库属性。  
  
3.  在分发服务器上，执行 [sp_changedistributor_password](../../relational-databases/system-stored-procedures/sp-changedistributor-password-transact-sql.md) 若要更改分发服务器密码。  
  
    > [!IMPORTANT]  
    >  如果可能，请在运行时提示用户输入安全凭据。 如果必须将凭据存储在脚本文件中，请确保该文件的安全以防受到未经授权的访问。  
  
4.  在分发服务器上，执行 [sp_changedistpublisher](../../relational-databases/system-stored-procedures/sp-changedistpublisher-transact-sql.md) 更改发布服务器使用分发服务器的属性。  
  
###  <a name="TsqlExample"></a> 示例 (Transact-SQL)  
 下面的示例 [!INCLUDE[tsql](../../includes/tsql-md.md)] 脚本返回有关分发服务器和分发数据库的信息。  
  
 [!code-sql[HowTo#sp_helpdistributor](../../relational-databases/replication/codesnippet/tsql/view-and-modify-distribu_1.sql)]  
  
 [!code-sql[HowTo#sp_helpdistributiondb](../../relational-databases/replication/codesnippet/tsql/view-and-modify-distribu_2.sql)]  
  
 该示例更改分发服务器的保持期、连接到分发服务器时使用的密码以及分发服务器检查各种复制代理的状态时采用的时间间隔（也称为检测信号时间间隔）。  
  
> [!IMPORTANT]  
>  如果可能，请在运行时提示用户输入安全凭据。 如果必须将凭据存储在脚本文件中，请确保该文件的安全以防受到未经授权的访问。  
  
 [!code-sql[HowTo#sp_changedistributor_property](../../relational-databases/replication/codesnippet/tsql/view-and-modify-distribu_3.sql)]  
  
 [!code-sql[HowTo#sp_changedistributiondb](../../relational-databases/replication/codesnippet/tsql/view-and-modify-distribu_4.sql)]  
  
 [!code-sql[HowTo#sp_changedistributor_password](../../relational-databases/replication/codesnippet/tsql/view-and-modify-distribu_5.sql)]  
  
##  <a name="RMOProcedure"></a> 使用复制管理对象 (RMO)  
  
#### 查看和修改分发服务器属性  
  
1.  通过使用创建连接到分发服务器 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 类。  
  
2.  创建的实例 <xref:Microsoft.SqlServer.Replication.ReplicationServer> 类。 传递 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 步骤 1 中的对象。  
  
3.  （可选）检查 <xref:Microsoft.SqlServer.Replication.ReplicationServer.IsDistributor%2A> 属性以验证当前连接的服务器为分发服务器。  
  
4.  调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.Load%2A> 方法，以从服务器获取的属性。  
  
5.  （可选）若要更改属性，请将设置一个或多个可以设置的分发服务器属性的新值 <xref:Microsoft.SqlServer.Replication.ReplicationServer> 对象。  
  
6.  （可选）如果 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> 属性 <xref:Microsoft.SqlServer.Replication.ReplicationServer> 对象设置为 **true**, ，调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 方法，以将所做的更改提交到服务器。  
  
#### 查看和修改分发数据库属性  
  
1.  通过使用创建连接到分发服务器 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 类。  
  
2.  创建的实例 <xref:Microsoft.SqlServer.Replication.DistributionDatabase> 类。 指定名称属性并传递 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 步骤 1 中的对象。  
  
3.  调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法，以从服务器获取的属性。 如果此方法返回 **false**，则该服务器上不存在指定名称的数据库。  
  
4.  （可选）若要更改属性，设置新的值之一的 <xref:Microsoft.SqlServer.Replication.DistributionDatabase> 可以设置的属性。  
  
5.  （可选）如果 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> 属性 <xref:Microsoft.SqlServer.Replication.DistributionDatabase> 对象设置为 **true**, ，调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 方法，以将所做的更改提交到服务器。  
  
#### 查看和修改发布服务器属性  
  
1.  通过使用创建连接到发布服务器 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 类。  
  
2.  创建的实例 <xref:Microsoft.SqlServer.Replication.DistributionPublisher> 类。 指定 <xref:Microsoft.SqlServer.Replication.DistributionPublisher.Name%2A> 属性并传递 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 步骤 1 中的对象。  
  
3.  （可选）若要更改属性，设置新的值之一的 <xref:Microsoft.SqlServer.Replication.DistributionPublisher> 可以设置的属性。  
  
4.  （可选）如果 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> 属性 <xref:Microsoft.SqlServer.Replication.DistributionPublisher> 对象设置为 **true**, ，调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 方法，以将所做的更改提交到服务器。  
  
#### 更改从发布服务器到分发服务器的管理连接的密码  
  
1.  通过使用创建连接到分发服务器 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 类。  
  
2.  创建的实例 <xref:Microsoft.SqlServer.Replication.ReplicationServer> 类。  
  
3.  设置 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 属性设置为在步骤 1 中创建的连接。  
  
4.  调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.Load%2A> 方法以获取该对象的属性。  
  
5.  调用 <xref:Microsoft.SqlServer.Replication.ReplicationServer.ChangeDistributorPassword%2A> 方法。 为 *password* 参数传递新的密码值。  
  
    > [!IMPORTANT]  
    >  如果可能，请在运行时提示用户输入安全凭据。 如果必须存储凭据，请使用 [Windows .NET Framework 提供的](http://go.microsoft.com/fwlink/?LinkId=34733) Cryptographic Services [!INCLUDE[msCoName](../../includes/msconame-md.md)] （加密服务）。  
  
6.  （可选）执行下列步骤以更改每个使用该分发服务器的远程发布服务器上的密码：  
  
    1.  通过使用创建连接到发布服务器 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 类。  
  
    2.  创建的实例 <xref:Microsoft.SqlServer.Replication.ReplicationServer> 类。  
  
    3.  设置 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 属性设置为步骤 6a 中创建的连接。  
  
    4.  调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.Load%2A> 方法以获取该对象的属性。  
  
    5.  调用 <xref:Microsoft.SqlServer.Replication.ReplicationServer.ChangeDistributorPassword%2A> 方法。 为 *password* 参数传递步骤 5 中的新密码值。  
  
###  <a name="PShellExample"></a> 示例 (RMO)  
 此示例显示如何更改分发和分发数据库属性。  
  
> [!IMPORTANT]  
>  若要避免将凭据存储在代码中，应当在运行时提供新分发服务器密码。  
  
 [!code-csharp[HowTo#rmo_ChangeDistPub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_changedistpub)]  
  
 [!code-vb[HowTo#rmo_vb_ChangeDistPub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_changedistpub)]  
  
## 另请参阅  
 [复制管理对象概念](../../relational-databases/replication/concepts/replication-management-objects-concepts.md)   
 [禁用发布和分发](../../relational-databases/replication/disable-publishing-and-distribution.md)   
 [配置分发](../../relational-databases/replication/configure-distribution.md)   
 [复制管理对象概念](../../relational-databases/replication/concepts/replication-management-objects-concepts.md)   
 [分发服务器和发布服务器信息脚本](../../relational-databases/replication/administration/distributor-and-publisher-information-script.md)   
 [复制系统存储过程概念](../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [查看信息并为发布服务器和 #40; 执行任务复制监视器 & #41;](../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-publisher-replication-monitor.md)  
  
  