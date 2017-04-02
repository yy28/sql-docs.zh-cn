---
title: "创建发布 | Microsoft Docs"
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
  - "发布 [SQL Server 复制], 创建"
  - "项目 [SQL Server 复制], 定义"
  - "添加项目"
  - "项目 [SQL Server 复制], 添加"
ms.assetid: 52ee6de9-1d58-4cb9-8711-372bddbe7154
caps.latest.revision: 44
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 44
---
# 创建发布
  本主题说明如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]、[!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 或复制管理对象 (RMO) 在 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 中创建发布。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [限制和局限](#Restrictions)  
  
     [安全性](#Security)  
  
-   **创建发布和定义项目，使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [复制管理对象 (RMO)](#RMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Restrictions"></a> 限制和局限  
  
-   发布和项目名称不能包含任何以下字符: %、 \* , ，[、]、 |、:、"、？ , ' , \ , / , \< , >. 如果在数据库中的对象包括以下任何字符，并且想要将其复制，则必须指定不同于中的对象名称的项目名称 **项目属性-\< 项目>** 对话框中，可从 **文章** 向导中的页。  
  
###  <a name="Security"></a> 安全性  
 如果可能，请在运行时提示用户输入安全凭据。 如果必须存储凭据，请使用 [Windows .NET Framework 提供的](http://go.microsoft.com/fwlink/?LinkId=34733) Cryptographic Services [!INCLUDE[msCoName](../../../includes/msconame-md.md)] （加密服务）。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 可以使用新建发布向导创建发布和定义项目。 创建发布后，查看和修改发布属性 **发布属性-\< 发布>** 对话框。 有关从 Oracle 数据库创建发布的信息，请参阅 [从 Oracle 数据库创建发布](../../../relational-databases/replication/publish/create-a-publication-from-an-oracle-database.md)。  
  
#### 创建发布和定义项目  
  
1.  在 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]中连接到发布服务器，然后展开服务器节点。  
  
2.  展开 **复制** 文件夹，然后再右键单击 **本地发布** 文件夹。  
  
3.  单击 **“新建发布”**。  
  
4.  按照新建发布向导中的页完成以下任务：  
  
    -   如果尚未在服务器上配置分发，请指定分发服务器。 有关配置分发的详细信息，请参阅 [配置发布和分发](../../../relational-databases/replication/configure-publishing-and-distribution.md)。  
  
         如果在指定 **分销商** 页面，发布服务器将充当自己的分发服务器 （本地分发服务器），并在服务器未配置为分发服务器、 新建发布向导将配置服务器。 在 **“快照文件夹”** 页中指定分发服务器的快照文件夹。 快照文件夹只是指定共享的目录。向此文件夹中执行读写操作的代理必须对其具有足够的访问权限。 有关正确保护文件夹的详细信息，请参阅 [保护快照文件夹的安全](../../../relational-databases/replication/security/secure-the-snapshot-folder.md)。  
  
         如果指定另一台服务器作为分发服务器，则必须在 **“管理密码”** 页上输入密码来连接发布服务器和分发服务器。 此密码必须与在远程分发服务器上启用发布服务器时所指定的密码相匹配。  
  
         有关详细信息，请参阅 [配置分发](../../../relational-databases/replication/configure-distribution.md)。  
  
    -   选择发布数据库。  
  
    -   选择发布类型。 有关详细信息，请参阅 [复制类型](../../../relational-databases/replication/types-of-replication.md)。  
  
    -   指定要发布的数据和数据库对象；（可选）筛选来自表项目的列，并设置项目属性。  
  
    -   可选择筛选来自表项目的行。 有关详细信息，请参阅 [筛选已发布数据](../../../relational-databases/replication/publish/filter-published-data.md)。  
  
    -   设置快照代理调度。  
  
    -   指定运行下列复制代理和进行连接的凭证：  
  
         \- 所有发布的快照代理。  
  
         \- 日志读取器代理程序，以了解所有事务发布。  
  
         \- 允许更新订阅的事务发布的队列读取器代理。  
  
         有关详细信息，请参阅 [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md) 和 [Replication Security Best Practices](../../../relational-databases/replication/security/replication-security-best-practices.md)。  
  
    -   （可选）编写发布脚本。 有关详细信息，请参阅 [Scripting Replication](../../../relational-databases/replication/scripting-replication.md)。  
  
    -   指定发布的名称。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 可以使用复制存储过程以编程方式创建发布。 使用的存储过程将取决于要创建的发布的类型。  
  
#### 创建快照发布或事务发布  
  
1.  在发布服务器上对发布数据库中，执行 [sp_replicationdboption & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md) 若要启用使用快照复制或事务复制的当前数据库的发布。  
  
2.  对于事务发布，确定发布数据库中是否存在日志读取器代理作业。 （对于快照发布，不需要此步骤）。  
  
    -   如果发布数据库中存在日志读取器代理作业，则继续执行步骤 3。  
  
    -   如果您不确定日志读取器代理作业是否存在某个已发布数据库，执行 [sp_helplogreader_agent & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-helplogreader-agent-transact-sql.md) 在发布数据库上的发布服务器。  
  
    -   如果结果集为空，则创建日志读取器代理作业。 在发布服务器上，执行 [sp_addlogreader_agent & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addlogreader-agent-transact-sql.md)。 指定 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] 的代理运行的 Windows 凭据 **@job_name** 和 **@password**。 如果连接到发布服务器时，代理将使用 SQL Server 身份验证，则必须指定的值为 **0** 为 **@publisher_security_mode** 和 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登录信息 **@publisher_login** 和 **@publisher_password**。 继续执行步骤 3。  
  
3.  在发布服务器上，执行 [sp_addpublication & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md)。 指定的发布名称 **@publication**, ，而且，对于 **@repl_freq** 参数，将值指定为 **快照** 为快照发布或值为 **连续** 事务发布的。 指定任何其他发布选项。 这便定义了发布。  
  
    > [!NOTE]  
    >  发布名称不能包括下列字符：  
    >   
    >  % * [ ] | : " ? \ / \< >  
  
4.  在发布服务器上，执行 [sp_addpublication_snapshot & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)。 指定使用步骤 3 中的发布名称 **@publication** 和在其下的快照代理运行的 Windows 凭据 **@snapshot_job_name** 和 **@password**。 如果连接到发布服务器时，代理将使用 SQL Server 身份验证，则必须指定的值为 **0** 为 **@publisher_security_mode** 和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登录信息 **@publisher_login** 和 **@publisher_password**。 此操作将为发布创建一个快照代理作业。  
  
    > [!IMPORTANT]  
    >  使用远程分发服务器，为所有参数提供的值配置发布服务器时包括 *job_login* 和 *job_password*, ，发送到分发服务器上以纯文本格式。 在执行此存储过程之前，应该对发布服务器及其远程分发服务器之间的连接进行加密。 有关详细信息，请参阅 [启用加密的连接添加到数据库引擎 & #40;SQL Server 配置管理器和 #41;](../../../database-engine/configure-windows/enable encrypted connections to the database engine.md)。  
  
5.  向发布添加项目。 有关详细信息，请参阅 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)。  
  
6.  启动快照代理作业以为此发布生成初始快照。 有关详细信息，请参阅 [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)。  
  
#### 创建合并发布  
  
1.  在发布服务器上，执行 [sp_replicationdboption & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md) 若要启用使用合并复制的当前数据库的发布。  
  
2.  在发布服务器上对发布数据库中，执行 [sp_addmergepublication & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md)。 为 **@publication** 指定发布的名称，并指定任何其他发布选项。 这便定义了发布。  
  
    > [!NOTE]  
    >  发布名称不能包括下列字符：  
    >   
    >  % * [ ] | : " ? \ / \< >  
  
3.  在发布服务器上，执行 [sp_addpublication_snapshot & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addpublication-snapshot-transact-sql.md)。 指定使用步骤 2 中的发布名称 **@publication** 和在其下的快照代理运行的 Windows 凭据 **@snapshot_job_name** 和 **@password**。 如果连接到发布服务器时，代理将使用 SQL Server 身份验证，则必须指定的值为 **0** 为 **@publisher_security_mode** 和 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登录信息 **@publisher_login** 和 **@publisher_password**。 此操作将为发布创建一个快照代理作业。  
  
    > [!IMPORTANT]  
    >  使用远程分发服务器，为所有参数提供的值配置发布服务器时包括 *job_login* 和 *job_password*, ，发送到分发服务器上以纯文本格式。 在执行此存储过程之前，应该对发布服务器及其远程分发服务器之间的连接进行加密。 有关详细信息，请参阅 [启用加密的连接添加到数据库引擎 & #40;SQL Server 配置管理器和 #41;](../../../database-engine/configure-windows/enable encrypted connections to the database engine.md)。  
  
4.  向发布添加项目。 有关详细信息，请参阅 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)。  
  
5.  启动快照代理作业以为此发布生成初始快照。 有关详细信息，请参阅 [Create and Apply the Initial Snapshot](../../../relational-databases/replication/create-and-apply-the-initial-snapshot.md)。  
  
###  <a name="TsqlExample"></a> 示例 (Transact-SQL)  
 此示例创建事务发布。 脚本变量用于传递创建快照代理和日志读取器代理作业时所需的 Windows 凭据。  
  
 [!code-sql[HowTo#sp_AddTranPub](../../../relational-databases/replication/codesnippet/tsql/create-a-publication_1.sql)]  
  
 此示例创建合并发布。 脚本变量用于传递创建快照代理作业时所需的 Windows 凭据。  
  
 [!code-sql[HowTo#sp_AddMergePub](../../../relational-databases/replication/codesnippet/tsql/create-a-publication_2.sql)]  
  
##  <a name="RMOProcedure"></a> 使用复制管理对象 (RMO)  
 可以使用复制管理对象 (RMO) 以编程方式创建发布。 用于创建发布的 RMO 类取决于所创建发布的类型。  
  
#### 创建快照发布或事务发布  
  
1.  通过使用创建连接到发布服务器 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 类。  
  
2.  创建的实例 <xref:Microsoft.SqlServer.Replication.ReplicationDatabase> 类为发布数据库中，设置 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 属性设置为实例 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 从步骤 1，并调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法。 如果 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 返回 **false**, ，验证数据库是否存在。  
  
3.  如果 <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.EnabledTransPublishing%2A> 属性是 **false**, ，将其设置为 **true**。  
  
4.  对于事务发布中，检查的值 <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.LogReaderAgentExists%2A> 属性。 如果该属性为 **true**，说明已经存在一个针对此数据库的日志读取器代理作业。 如果该属性为 **false**，请执行如下操作：  
  
    -   设置 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> 和 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> 或 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.SecurePassword%2A> 字段 <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.LogReaderAgentProcessSecurity%2A> 提供的凭据 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows 帐户下运行日志读取器代理。  
  
        > [!NOTE]  
        >  设置 <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.LogReaderAgentProcessSecurity%2A> 的成员创建发布时不需要 **sysadmin** 固定的服务器角色。 在这种情况下，代理会模拟 SQL Server Agent 帐户。 有关详细信息，请参阅 [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md)。  
  
    -   （可选）设置 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> 和 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> 或 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SecureSqlStandardPassword%2A> 字段 <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.LogReaderAgentPublisherSecurity%2A> 在使用 SQL Server 身份验证连接到发布服务器。  
  
    -   调用 <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.CreateLogReaderAgent%2A> 方法来创建数据库的日志读取器代理作业。  
  
5.  创建的实例 <xref:Microsoft.SqlServer.Replication.TransPublication> 类，并将设置此对象的下列属性︰  
  
    -    <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 步骤 1 中的 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>。  
  
    -   已发布的数据库的名称 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A>。  
  
    -   有关发布的名称 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>。  
  
    -   一个 <xref:Microsoft.SqlServer.Replication.PublicationType> 任一 <xref:Microsoft.SqlServer.Replication.PublicationType.Transactional> 或 <xref:Microsoft.SqlServer.Replication.PublicationType.Snapshot>。  
  
    -    <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> 和 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> 字段 <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A> 运行快照代理所用的 Windows 帐户提供的凭据。 如果使用 Windows 身份验证，在快照代理连接到本地分发服务器或建立远程连接时，也会使用此帐户。  
  
        > [!NOTE]  
        >  设置 <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A> 的成员创建发布时不需要 **sysadmin** 固定的服务器角色。 在这种情况下，代理会模拟 SQL Server Agent 帐户。 有关详细信息，请参阅 [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md)。  
  
    -   （可选） <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> 和 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> 或 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SecureSqlStandardPassword%2A> 字段 <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentPublisherSecurity%2A> 在使用 SQL Server 身份验证连接到发布服务器。  
  
    -   （可选）使用逻辑 OR 运算符 (**|** 在 Visual C# 和 **或者** 在 Visual Basic 中) 以及排除性逻辑 OR 运算符 (**^** 在 Visual C# 和 **异或** 在 Visual Basic 中) 来设置 <xref:Microsoft.SqlServer.Replication.PublicationAttributes> 值 <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> 属性。  
  
    -   （可选）为发布服务器的名称 <xref:Microsoft.SqlServer.Replication.TransPublication.PublisherName%2A> 发布服务器时非 SQL Server 发布服务器。  
  
6.  调用 <xref:Microsoft.SqlServer.Replication.Publication.Create%2A> 方法以创建发布。  
  
    > [!IMPORTANT]  
    >  使用远程分发服务器，提供的所有属性的值配置发布服务器时包括 <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A>, ，发送到分发服务器上以纯文本格式。 您还应该加密在发布服务器和它之前调用的远程分发服务器之间的连接 <xref:Microsoft.SqlServer.Replication.Publication.Create%2A> 方法。 有关详细信息，请参阅 [启用加密的连接添加到数据库引擎 & #40;SQL Server 配置管理器和 #41;](../../../database-engine/configure-windows/enable encrypted connections to the database engine.md)。  
  
7.  调用 <xref:Microsoft.SqlServer.Replication.Publication.CreateSnapshotAgent%2A> 方法来创建发布的快照代理作业。  
  
#### 创建合并发布  
  
1.  通过使用创建连接到发布服务器 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 类。  
  
2.  创建的实例 <xref:Microsoft.SqlServer.Replication.ReplicationDatabase> 类为发布数据库中，设置 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 属性设置为实例 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 从步骤 1，并调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法。 如果 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 返回 **false**, ，验证数据库是否存在。  
  
3.  如果 <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.EnabledMergePublishing%2A> 属性是 **false**, ，将其设置为 **true**, ，并调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A>。  
  
4.  创建的实例 <xref:Microsoft.SqlServer.Replication.MergePublication> 类，并将设置此对象的下列属性︰  
  
    -    <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 步骤 1 中的 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>。  
  
    -   已发布的数据库的名称 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A>。  
  
    -   有关发布的名称 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A>。  
  
    -    <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> 和 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> 字段 <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A> 运行快照代理所用的 Windows 帐户提供的凭据。 如果使用 Windows 身份验证，在快照代理连接到本地分发服务器或建立远程连接时，也会使用此帐户。  
  
        > [!NOTE]  
        >  设置 <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A> 的成员创建发布时不需要 **sysadmin** 固定的服务器角色。 有关详细信息，请参阅 [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md)。  
  
    -   （可选）使用逻辑 OR 运算符 (**|** 在 Visual C# 和 **或者** 在 Visual Basic 中) 以及排除性逻辑 OR 运算符 (**^** 在 Visual C# 和 **异或** 在 Visual Basic 中) 来设置 <xref:Microsoft.SqlServer.Replication.PublicationAttributes> 值 <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> 属性。  
  
5.  调用 <xref:Microsoft.SqlServer.Replication.Publication.Create%2A> 方法以创建发布。  
  
    > [!IMPORTANT]  
    >  使用远程分发服务器，提供的所有属性的值配置发布服务器时包括 <xref:Microsoft.SqlServer.Replication.Publication.SnapshotGenerationAgentProcessSecurity%2A>, ，发送到分发服务器上以纯文本格式。 您还应该加密在发布服务器和它之前调用的远程分发服务器之间的连接 <xref:Microsoft.SqlServer.Replication.Publication.Create%2A> 方法。 有关详细信息，请参阅 [启用加密的连接添加到数据库引擎 & #40;SQL Server 配置管理器和 #41;](../../../database-engine/configure-windows/enable encrypted connections to the database engine.md)。  
  
6.  调用 <xref:Microsoft.SqlServer.Replication.Publication.CreateSnapshotAgent%2A> 方法来创建发布的快照代理作业。  
  
###  <a name="PShellExample"></a> 示例 (RMO)  
 本例将 AdventureWorks 数据库设置为支持事务发布，定义了一个日志读取器代理作业，并且创建了 AdvWorksProductTran 发布。 必须为此发布定义一个项目。 创建日志读取器代理作业和快照代理作业所需的 Windows 帐户凭据在运行时进行传递。 若要了解如何使用 RMO 定义快照项目和事务项目，请参阅 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)。  
  
 [!code-csharp[HowTo#rmo_CreateTranPub](../../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_createtranpub)]  
  
 [!code-vb[HowTo#rmo_vb_CreateTranPub](../../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_createtranpub)]  
  
 本例将 AdventureWorks 数据库设置为支持合并发布，并且创建了 AdvWorksSalesOrdersMerge 发布。 仍然必须为此发布定义项目。 创建快照代理作业所需的 Windows 帐户凭据在运行时进行传递。 若要了解如何使用 RMO 定义合并项目，请参阅 [Define an Article](../../../relational-databases/replication/publish/define-an-article.md)。  
  
 [!code-csharp[HowTo#rmo_CreateMergePub](../../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_createmergepub)]  
  
 [!code-vb[HowTo#rmo_vb_CreateMergePub](../../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_createmergepub)]  
  
## 另请参阅  
 [将 sqlcmd 与脚本变量结合使用](../../../relational-databases/scripting/use-sqlcmd-with-scripting-variables.md)   
 [发布数据和数据库对象](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [复制管理对象概念](../../../relational-databases/replication/concepts/replication-management-objects-concepts.md)   
 [定义项目](../../../relational-databases/replication/publish/define-an-article.md)   
 [查看和修改发布属性](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)   
 [配置分发](../../../relational-databases/replication/configure-distribution.md)   
 [保护分发服务器的安全](../../../relational-databases/replication/security/secure-the-distributor.md)   
 [保护发布服务器的安全](../../../relational-databases/replication/security/secure-the-publisher.md)  
  
  