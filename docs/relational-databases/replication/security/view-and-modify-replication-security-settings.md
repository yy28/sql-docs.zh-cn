---
title: "查看和修改复制安全设置 | Microsoft Docs"
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
  - "修改复制安全设置"
  - "复制 [SQL Server], 安全性"
  - "安全性 [SQL Server 复制], 查看设置"
  - "查看复制安全设置"
  - "安全性 [SQL Server 复制], 修改设置"
ms.assetid: 67d79532-1482-4de1-ac9f-4a23d162c85e
caps.latest.revision: 47
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 47
---
# 查看和修改复制安全设置
  本主题说明如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]、[!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 或复制管理对象 (RMO) 在 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 中查看和修改复制安全设置。 例如，您可能需要将日志读取器代理到发布服务器的连接从 SQL Server 身份验证更改为 Windows 集成身份验证，或者您可能需要在 Window 帐户密码更改后更改用于运行代理作业的凭据。 有关每个代理所需的权限的信息，请参阅 [复制代理安全模式](../../../relational-databases/replication/security/replication-agent-security-model.md)。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [限制和局限](#Restrictions)  
  
     [安全性](#Security)  
  
-   **查看和修改复制安全设置，使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [复制管理对象 (RMO)](#RMOProcedure)  
  
-   **跟进︰**  [修改复制安全设置后](#FollowUp)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Restrictions"></a> 限制和局限  
  
-   所使用的存储过程将取决于代理的类型和服务器连接的类型。  
  
-   使用的 RMO 类和属性取决于代理的类型和服务器连接的类型。  
  
###  <a name="Security"></a> 安全性  
 出于安全考虑，在复制存储过程返回的结果集中掩盖密码的实际值。  
  
####  <a name="Permissions"></a> 权限  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 在下列对话框中查看和修改安全设置：  
  
1.  **“更新复制密码”** 对话框，可以通过 **的** “复制” [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]文件夹访问。 如果更改复制拓扑中某服务器上 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 帐户或 Windows 帐户的密码，请使用此对话框，而不用更新使用此帐户的每个代理的密码。 如果多台服务器上的代理使用相同的帐户，则必须连接到每台服务器并更改密码。 在复制使用该密码的所有地方的密码将被更新， 而其他地方（如链接服务器）的密码将不更新。  
  
2.   **代理安全性** 页 **发布属性-\< 发布>** 对话框。 有关访问此对话框的详细信息，请参阅 [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)。  
  
3.   **订阅属性-\< 订阅>** 对话框。 有关访问此对话框的详细信息，请参阅 [View and Modify Push Subscription Properties](../../../relational-databases/replication/view-and-modify-push-subscription-properties.md) 和 [View and Modify Pull Subscription Properties](../../../relational-databases/replication/view-and-modify-pull-subscription-properties.md)。  
  
4.   **分发服务器属性-\< 分发服务器>** 和 **分发数据库属性-\< 数据库>** 对话框。 有关访问这些对话框的详细信息，请参阅 [View and Modify Distributor and Publisher Properties](../../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)。  
  
5.   **发布服务器属性-\< 发布服务器>** 对话框。 有关访问此对话框的详细信息，请参阅 [View and Modify Distributor and Publisher Properties](../../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)。  
  
#### 更改一个或多个代理所用帐户的密码  
  
1.  如果该帐户是 SQL Server 帐户，此对话框还将更改 SQL Server 帐户的密码。 如果该帐户是 Windows 帐户，请首先在 Windows 中更改密码。 有关详细信息，请参阅 Windows 文档。  
  
    > [!NOTE]  
    >  更改复制密码后，必须停止并重新启动使用该密码的每个代理，这样代理的更改才能生效。  
  
2.  连接到 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]中的服务器，然后展开该服务器节点。  
  
3.  用鼠标右键单击 **复制** 文件夹，，然后单击 **更新复制密码**。  
  
4.  在 **“更新复制密码”** 对话框中指定帐户和新密码。  
  
5.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### 更改快照代理的安全设置  
  
1.  在 **代理安全性** 页 **发布属性-\< 发布>** 对话框中，单击 **安全设置** 旁边的按钮 **快照代理程序** 文本框。  
  
2.  在 **“快照代理安全性”** 对话框中指定运行该代理的帐户：  
  
    -   在 **“代理帐户”** 文本框中，输入一个新的 Windows 帐户。  
  
    -   在 **“密码”** 和 **“确认密码”** 文本框中，输入一个新的强密码。  
  
3.  指定将该代理从分发服务器连接到发布服务器的上下文。 如果选中 **“使用以下 SQL Server 登录名”**，还必须指定登录名：  
  
    -   在 **“登录名”** 文本框中，输入登录名  
  
    -   在 **“密码”** 和 **“确认密码”** 文本框中，输入一个新的强密码。  
  
    > [!NOTE]  
    >  如果发布服务器，Oracle 发布服务器中指定的连接上下文 **分发服务器属性-\< 分发服务器>**对话框。 有关更改上下文的过程，请参阅下面的内容。  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### 更改日志读取器代理的安全设置  
  
1.  在 **代理安全性** 页 **发布属性-\< 发布>** 对话框中，单击 **安全设置** 旁边的按钮 **日志读取器代理** 文本框。  
  
2.  在 **“日志读取器代理安全性”** 对话框中指定运行该代理的帐户：  
  
    -   在 **“代理帐户”** 文本框中，输入新的 Windows 帐户  
  
    -   在 **“密码”** 和 **“确认密码”** 文本框中，输入一个新的强密码。  
  
3.  指定将该代理从分发服务器连接到发布服务器的上下文。 如果选中 **“使用以下 SQL Server 登录名”**，还必须指定登录名：  
  
    -   在 **“登录名”** 文本框中，输入登录名  
  
    -   在 **“密码”** 和 **“确认密码”** 文本框中，输入一个新的强密码。  
  
    > [!NOTE]  
    >  如果发布服务器，Oracle 发布服务器中指定的连接上下文 **分发服务器属性-\< 分发服务器>**对话框。 通过下面的过程更改上下文。  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
    > [!NOTE]  
    >  每个已发布数据库都有一个日志读取器代理。 在一个发布上更改代理的安全设置会影响发布数据库中所有发布的设置。  
  
#### 更改将 Oracle 发布的快照代理和日志读取器代理连接到发布服务器的上下文  
  
1.  在 **出版商** 页 **分发服务器属性-\< 分发服务器>** 对话框框中，单击属性按钮 (**...**) 发布服务器旁边。  
  
2.  在 **“到发布服务器的代理连接”** 部分指定已配置的复制管理用户架构所使用的登录名和密码。 有关详细信息，请参阅 [配置 Oracle 发布服务器](../../../relational-databases/replication/non-sql/configure-an-oracle-publisher.md)。  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### 更改推送订阅的分发代理的安全设置  
  
1.  在 **订阅属性-\< 订阅>** 对话框中，您可以在发布服务器上，进行以下更改︰  
  
    -   若要更改分发代理程序在其下运行并将其连接到分发服务器上的帐户，请单击 **代理进程帐户** 行，并单击属性 (**...**) 行中的按钮。 在 **“分发代理安全性”** 对话框中指定帐户和密码。  
  
    -   若要更改分发代理连接到订阅服务器的上下文，请单击 **订阅服务器连接** 行，并单击属性 (**...**) 行中的按钮。 在 **“输入连接信息”** 对话框中指定上下文。  
  
         如果使用排队更新订阅，队列读取器代理还将使用为订阅服务器的连接指定的上下文。  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### 更改请求订阅的分发代理的安全设置  
  
1.  在 **订阅属性-\< 订阅>** 对话框中，您可以在订阅服务器上，进行以下更改︰  
  
    -   若要更改分发代理程序在其下运行并将其连接到订阅服务器上的帐户，请单击 **代理进程帐户** 行，并单击属性 (**...**) 行中的按钮。 在 **“分发代理安全性”** 对话框中指定帐户和密码。  
  
         如果使用排队更新订阅，队列读取器代理还将使用为订阅服务器的连接指定的上下文。  
  
    -   若要更改分发代理连接到分发服务器的上下文，请单击 **分发服务器连接** 行，并单击属性 (**...**) 行中的按钮。 在 **“输入连接信息”** 对话框中指定上下文。  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### 更改推送订阅的合并代理的安全设置  
  
1.  在 **订阅属性-\< 订阅>** 对话框中，您可以在发布服务器上，进行以下更改︰  
  
    -   若要更改在其下运行合并代理并将其连接到发布服务器和分发服务器的帐户，请单击 **代理进程帐户** 行，并单击属性 (**...**) 行中的按钮。 在 **“合并代理安全性”** 对话框中指定帐户和密码。  
  
    -   若要更改合并代理连接到订阅服务器的上下文，请单击 **订阅服务器连接** 行，并单击属性 (**...**) 行中的按钮。 在 **“输入连接信息”** 对话框中指定上下文。  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### 更改请求订阅的合并代理的安全设置  
  
1.  在 **订阅属性-\< 订阅>** 对话框中，您可以在订阅服务器上，进行以下更改︰  
  
    -   若要更改在其下运行合并代理并将其连接到订阅服务器上的帐户，请单击 **代理进程帐户** 行，并单击属性 (**...**) 行中的按钮。 在 **“合并代理安全性”** 对话框中指定帐户和密码。  
  
    -   若要更改合并代理连接到发布服务器和分发服务器的上下文，请单击 **发布服务器连接** 行，并单击属性 (**...**) 行中的按钮。 在 **“输入连接信息”** 对话框中指定上下文。  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
#### 更改运行队列读取器代理的帐户  
  
1.  在 **常规** 页 **分发服务器属性-\< 分发服务器>** 对话框框中，单击属性 (**...**) 的分发数据库旁边的按钮。  
  
2.  在 **分发数据库属性-\< 数据库>** 对话框中，单击 **安全设置** 旁边的按钮 **代理进程帐户** 文本框。  
  
3.  在 **“队列读取器代理安全性”** 对话框中，指定运行代理并将其连接到分发服务器的帐户：  
  
    -   在 **“进程帐户”** 文本框中，输入一个新的 Windows 帐户  
  
    -   在 **“密码”** 和 **“确认密码”** 文本框中，输入一个新的强密码。  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
    > [!NOTE]  
    >  每个分发数据库都有一个队列读取器代理。 更改代理的安全设置会影响使用此分发数据库的所有发布服务器上所有发布的设置。  
  
#### 更改将队列读取器代理连接到发布服务器的上下文  
  
1.  在 **出版商** 页 **分发服务器属性-\< 分发服务器>** 对话框框中，单击属性按钮 (**...**) 发布服务器旁边。  
  
2.  在 **“到发布服务器的代理连接”** 部分，将 **“代理连接模式”** 选项指定为 **“模拟代理进程帐户”** 或 **“SQL Server 身份验证”** 。 如果指定 **“SQL Server 身份验证”**，还需输入 **“登录名”** 和 **“密码”**的值。  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
    > [!NOTE]  
    >  每个分发数据库都有一个队列读取器代理。 更改代理的安全设置会影响使用此分发数据库的所有发布服务器上所有发布的设置。  
  
#### 更改将队列读取器代理连接到订阅服务器的上下文  
  
-   对于订阅，队列读取器代理与分发代理使用相同的连接上下文。 有关详细信息，请参阅上述分发代理的过程。  
  
#### 更改立即更新请求订阅的安全设置  
  
1.  在 **订阅属性-\< 订阅>** 对话框在订阅服务器上，单击 **发布服务器连接** 行，并单击属性 (**...**) 行中的按钮。  
  
2.  在 **“输入连接信息”** 对话框中，请选择下列选项之一：  
  
    -   **“使用来自链接服务器或远程服务器的登录名”**。 如果您定义了远程服务器或订阅服务器与发布服务器使用之间的链接的服务器，请选择此选项 [sp_addserver & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md), ，[sp_addlinkedserver & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md), ，[!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], ，或另一种方法。  
  
    -   **“使用以下登录名和密码进行 SQL Server 身份验证”**。 如果尚未在订阅服务器和发布服务器之间定义远程服务器或链接服务器，则选择此选项。 复制将为您创建链接服务器。 所指定的帐户在发布服务器上必须已经存在。  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
> [!NOTE]  
>  此过程更改复制触发器用于在订阅服务器上发生更改时从订阅服务器连接到发布服务器的方法。 还可以为立即更新订阅更改与分发代理关联的设置。 有关详细信息，请参阅本主题前面介绍的过程。  
>   
>  此过程只适用于请求订阅。 对于推送订阅，使用存储的过程 [sp_link_publication & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md)。  
  
#### 更改从发布服务器到分发服务器的管理连接的密码  
  
1.  在 **出版商** 页 **分发服务器属性-\< 分发服务器>** 对话框框中，输入中的强密码 **密码** 和 **确认密码** 文本框。  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
3.  在 **常规** 页 **发布服务器属性-\< 发布服务器>** 对话框框中，输入中的强密码 **密码** 和 **确认密码** 文本框。  
  
4.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
> [!IMPORTANT]  
>  在以下所有过程中，如果可能，请在运行时提示用户输入安全凭据。 如果将凭据存储在脚本文件中，则必须确保文件的安全以防受到未经授权的访问。  
  
#### 在复制服务器上更改存储密码的所有实例  
  
1.  在主数据库上的复制拓扑中的服务器，执行 [sp_changereplicationserverpasswords](../../../relational-databases/system-stored-procedures/sp-changereplicationserverpasswords-transact-sql.md)。 为 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] @login [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Windows 帐户或 **@login** 登录名，并为 **@password**。 连接到该拓扑中的其他服务器时，此操作会更改该服务器上所有代理使用的密码的每个实例。  
  
    > [!NOTE]  
    >  只更改登录名和密码连接到特定服务器 （如分发服务器或订阅服务器上），该拓扑中指定此服务器的名称 **@server**。  
  
2.  在复制拓扑中必须更新密码的每台服务器上重复执行步骤 1。  
  
    > [!NOTE]  
    >  更改复制密码后，必须停止并重新启动使用该密码的每个代理，这样代理的更改才能生效。  
  
#### 更改快照代理的安全设置  
  
1.  在发布服务器上，执行 [sp_helppublication_snapshot](../../../relational-databases/system-stored-procedures/sp-helppublication-snapshot-transact-sql.md), ，并指定 **@publication**。 此操作将返回快照代理的当前安全设置。  
  
2.  在发布服务器上，执行 [sp_changepublication_snapshot](../../../relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql.md), ，并指定 **@publication** 和一个或多个以下的安全设置，以更改︰  
  
    -   若要更改的 Windows 帐户运行的代理或只是为此帐户的密码指定 **@job_login** 和 **@job_password**。  
  
    -   若要更改连接到发布服务器时使用的安全模式，将值指定为 **1** 或 **0** 为 **@publisher_security_mode**。  
  
    -   当连接到从发布服务器时使用的安全模式更改 **1** 到 **0** 或者更改 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登录名用于此连接中，指定 **@publisher_login** 和 **@publisher_password**。  
  
    > [!IMPORTANT]  
    >  使用远程分发服务器，为所有参数提供的值配置发布服务器时包括 *job_login* 和 *job_password*, ，发送到分发服务器上以纯文本格式。 在执行此存储过程之前，应该对发布服务器及其远程分发服务器之间的连接进行加密。 有关详细信息，请参阅 [启用加密的连接添加到数据库引擎 & #40;SQL Server 配置管理器和 #41;](../../../database-engine/configure-windows/enable encrypted connections to the database engine.md)。  
  
#### 更改日志读取器代理的安全设置  
  
1.  在发布服务器上，执行 [sp_helplogreader_agent](../../../relational-databases/system-stored-procedures/sp-helplogreader-agent-transact-sql.md), ，并指定 **@publisher**。 此操作将返回日志读取器代理的当前安全设置。  
  
2.  在发布服务器上，执行 [sp_changelogreader_agent](../../../relational-databases/system-stored-procedures/sp-changelogreader-agent-transact-sql.md), ，并指定 **@publication** 和一个或多个以下的安全设置，以更改︰  
  
    -   若要更改的 Windows 帐户运行的代理或只是为此帐户的密码指定 **@job_login** 和 **@job_password**。  
  
    -   若要更改连接到发布服务器时使用的安全模式，将值指定为 **1** 或 **0** 为 **@publisher_security_mode**。  
  
    -   当连接到从发布服务器时使用的安全模式更改 **1** 到 **0** 或者更改 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 登录名用于此连接中，指定 **@publisher_login** 和 **@publisher_password**。  
  
    > [!NOTE]  
    >  更改代理登录名或密码之后，必须先停止并重新启动代理，然后更改才能生效。  
  
    > [!IMPORTANT]  
    >  使用远程分发服务器，为所有参数提供的值配置发布服务器时包括 *job_login* 和 *job_password*, ，发送到分发服务器上以纯文本格式。 在执行此存储过程之前，应该对发布服务器及其远程分发服务器之间的连接进行加密。 有关详细信息，请参阅 [启用加密的连接添加到数据库引擎 & #40;SQL Server 配置管理器和 #41;](../../../database-engine/configure-windows/enable encrypted connections to the database engine.md)。  
  
#### 更改推送订阅的分发代理的安全设置  
  
1.  在发布服务器上对发布数据库中，执行 [sp_helpsubscription](../../../relational-databases/system-stored-procedures/sp-helpsubscription-transact-sql.md), ，并指定 **@publication** 和 **@subscriber**。 此操作将返回订阅属性，包括运行在分发服务器上的分发代理的安全设置。  
  
2.  在发布服务器上对发布数据库中，执行 [sp_changesubscription](../../../relational-databases/system-stored-procedures/sp-changesubscription-transact-sql.md), ，并指定 **@publication**, ，**@subscriber**, ，**@subscriber_db**, ，值为 **所有** 为 **@article**, 的安全属性的名称 **@property**, ，和新值的属性的 **@value**。  
  
3.  对下列每个要更改的安全属性重复步骤 2：  
  
    -   若要更改的 Windows 帐户下运行的代理或只为此帐户的密码的值指定 **distrib_job_password** 为 **@property** 和的新密码 **@value**。 在更改帐户本身时，重复步骤 2 的值指定 **distrib_job_login** 为 **@property** 和新的 Windows 帐户，以 **@value**。  
  
    -   若要更改连接到订阅服务器时使用的安全模式，将值指定为 **subscriber_security_mode** 为 **@property** ，值为 **1** （Windows 集成身份验证） 或 **0** （SQL Server 身份验证） 的 **@value**。  
  
    -   当订阅服务器上的安全模式更改为 SQL Server 身份验证，或更改 SQL Server 身份验证的登录信息，将值指定为 **subscriber_password** 为 **@property** 和新密码 **@value**。 重复步骤 2，将值指定为 **subscriber_login** 为 **@property** 和的新登录名 **@value**。  
  
    > [!NOTE]  
    >  更改代理登录名或密码之后，必须先停止并重新启动代理，然后更改才能生效。  
  
    > [!IMPORTANT]  
    >  使用远程分发服务器，提供的所有属性的值配置发布服务器时包括 **distrib_job_login** 和 **distrib_job_password**, ，发送到分发服务器上以纯文本格式。 在执行此存储过程之前，应该对发布服务器及其远程分发服务器之间的连接进行加密。 有关详细信息，请参阅 [启用加密的连接添加到数据库引擎 & #40;SQL Server 配置管理器和 #41;](../../../database-engine/configure-windows/enable encrypted connections to the database engine.md)。  
  
#### 更改请求订阅的分发代理的安全设置  
  
1.  在订阅服务器上，执行 [sp_helppullsubscription](../../../relational-databases/system-stored-procedures/sp-helppullsubscription-transact-sql.md), ，并指定 **@publication**。 此操作将返回订阅属性，包括运行在订阅服务器上的分发代理的安全设置。  
  
2.  在订阅服务器上的订阅数据库上，执行 [sp_change_subscription_properties](../../../relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql.md), ，并指定 **@publisher**, ，**@publisher_db**, ，**@publication**, 的安全属性的名称 **@property**, ，和新值的属性的 **@value**。  
  
3.  对下列每个要更改的安全属性重复步骤 2：  
  
    -   若要更改的 Windows 帐户下运行的代理或只为此帐户的密码的值指定 **distrib_job_password** 为 **@property** 和的新密码 **@value**。 在更改帐户本身时，重复步骤 2 的值指定 **distrib_job_login** 为 **@property** 和新的 Windows 帐户，以 **@value**。  
  
    -   若要更改连接到分发服务器时使用的安全模式，将值指定为 **distributor_security_mode** 为 **@property** ，值为 **1** （Windows 集成身份验证） 或 **0** （SQL Server 身份验证） 的 **@value**。  
  
    -   当分发服务器的安全模式更改为 SQL Server 身份验证或更改 SQL Server 身份验证的登录信息，将值指定为 **distributor_password** 为 **@property** 和新密码 **@value**。 重复步骤 2，将值指定为 **distributor_login** 为 **@property** 和的新登录名 **@value**。  
  
    > [!NOTE]  
    >  更改代理登录名或密码之后，必须先停止并重新启动代理，然后更改才能生效。  
  
#### 更改推送订阅的合并代理的安全设置  
  
1.  在发布服务器上对发布数据库中，执行 [sp_helpmergesubscription](../../../relational-databases/system-stored-procedures/sp-helpmergesubscription-transact-sql.md), ，并指定 **@publication**, ，**@subscriber**, ，和 **@subscriber_db**。 此操作将返回订阅属性，包括运行在分发服务器上的合并代理的安全设置。  
  
2.  在发布服务器上对发布数据库中，执行 [sp_changemergesubscription](../../../relational-databases/system-stored-procedures/sp-changemergesubscription-transact-sql.md), ，并指定 **@publication**, ，**@subscriber**, ，**@subscriber_db**, 的安全属性的名称 **@property**, ，和新值的属性的 **@value**。  
  
3.  对下列每个要更改的安全属性重复步骤 2：  
  
    -   若要更改的 Windows 帐户下运行代理，或只是为此帐户的密码的值指定 **merge_job_password** 为 **@property** 和的新密码 **@value**。 在更改帐户本身时，重复步骤 2 的值指定 **merge_job_login** 为 **@property** 和新的 Windows 帐户，以 **@value**。  
  
    -   若要更改连接到订阅服务器时使用的安全模式，将值指定为 **subscriber_security_mode** 为 **@property** ，值为 **1** （Windows 集成身份验证） 或 **0** （SQL Server 身份验证） 的 **@value**。  
  
    -   当订阅服务器上的安全模式更改为 SQL Server 身份验证，或更改 SQL Server 身份验证的登录信息，将值指定为 **subscriber_password** 为 **@property** 和新密码 **@value**。 重复步骤 2，将值指定为 **subscriber_login** 为 **@property** 和的新登录名 **@value**。  
  
    -   若要更改连接到发布服务器时使用的安全模式，将值指定为 **publisher_security_mode** 为 **@property** ，值为 **1** （Windows 集成身份验证） 或 **0** （SQL Server 身份验证） 的 **@value**。  
  
    -   当发布服务器的安全模式更改为 SQL Server 身份验证，或更改 SQL Server 身份验证的登录信息，将值指定为 **publisher_password** 为 **@property** 和新密码 **@value**。 重复步骤 2，将值指定为 **publisher_login** 为 **@property** 和的新登录名 **@value**。  
  
    > [!NOTE]  
    >  更改代理登录名或密码之后，必须先停止并重新启动代理，然后更改才能生效。  
  
    > [!IMPORTANT]  
    >  使用远程分发服务器，提供的所有属性的值配置发布服务器时包括 **merge_job_login** 和 **merge_job_password**, ，发送到分发服务器上以纯文本格式。 在执行此存储过程之前，应该对发布服务器及其远程分发服务器之间的连接进行加密。 有关详细信息，请参阅 [启用加密的连接添加到数据库引擎 & #40;SQL Server 配置管理器和 #41;](../../../database-engine/configure-windows/enable encrypted connections to the database engine.md)。  
  
#### 更改请求订阅的合并代理的安全设置  
  
1.  在订阅服务器上，执行 [sp_helpmergepullsubscription](../../../relational-databases/system-stored-procedures/sp-helpmergepullsubscription-transact-sql.md), ，并指定 **@publication**。 此操作将返回订阅属性，包括运行在订阅服务器上的合并代理的安全设置。  
  
2.  在订阅服务器上的订阅数据库上，执行 [sp_change_subscription_properties](../../../relational-databases/system-stored-procedures/sp-change-subscription-properties-transact-sql.md), ，并指定 **@publisher**, ，**@publisher_db**, ，**@publication**, 的安全属性的名称 **@property**, ，和新值的属性的 **@value**。  
  
3.  对下列每个要更改的安全属性重复步骤 2：  
  
    -   若要更改的 Windows 帐户下运行的代理或只为此帐户的密码的值指定 **merge_job_password** 为 **@property** 和新密码 **@value**。 在更改帐户本身时，重复步骤 2 的值指定 **merge_job_login** 为 **@property** 和新的 Windows 帐户，以 **@value**。  
  
    -   若要更改连接到分发服务器时使用的安全模式，将值指定为 **distributor_security_mode** 为 **@property** ，值为 **1** （Windows 集成身份验证） 或 **0** （SQL Server 身份验证） 的 **@value**。  
  
    -   当分发服务器的安全模式更改为 SQL Server 身份验证或更改 SQL Server 身份验证的登录信息，将值指定为 **distributor_password** 为 **@property** 和新密码 **@value**。 重复步骤 2，将值指定为 **distributor_login** 为 **@property** 和的新登录名 **@value**。  
  
    -   若要更改连接到发布服务器时使用的安全模式，将值指定为 **publisher_security_mode** 为 **@property** ，值为 **1** （Windows 集成身份验证） 或 **0** （SQL Server 身份验证） 的 **@value**。  
  
    -   当发布服务器的安全模式更改为 SQL Server 身份验证或更改 SQL Server 身份验证的登录信息，将值指定为 **publisher_password** 为 **@property** 和新密码 **@value**。 重复步骤 2，将值指定为 **publisher_login** 为 **@property** 和的新登录名 **@value**。  
  
    > [!NOTE]  
    >  更改代理登录名或密码之后，必须先停止并重新启动代理，然后更改才能生效。  
  
#### 更改快照代理的安全设置以为订阅服务器生成筛选快照  
  
1.  在发布服务器上，执行 [sp_helpdynamicsnapshot_job](../../../relational-databases/system-stored-procedures/sp-helpdynamicsnapshot-job-transact-sql.md), ，并指定 **@publication**。 在结果集中，记下的值 **job_name** 要更改的订阅服务器的分区。  
  
2.  在发布服务器上，执行 [sp_changedynamicsnapshot_job](../../../relational-databases/system-stored-procedures/sp-changedynamicsnapshot-job-transact-sql.md), ，并指定 **@publication**, ，步骤 1 中获取的值 **@dynamic_snapshot_jobname**, ，和的新密码 **@job_password** 或登录名和在其下的代理运行的 Windows 帐户的密码 **@job_login** 和 **@job_password**。  
  
    > [!IMPORTANT]  
    >  使用远程分发服务器，为所有参数提供的值配置发布服务器时包括 *job_login* 和 *job_password*, ，发送到分发服务器上以纯文本格式。 在执行此存储过程之前，应该对发布服务器及其远程分发服务器之间的连接进行加密。 有关详细信息，请参阅 [启用加密的连接添加到数据库引擎 & #40;SQL Server 配置管理器和 #41;](../../../database-engine/configure-windows/enable encrypted connections to the database engine.md)。  
  
#### 更改队列读取器代理的安全设置  
  
1.  在分发服务器上，执行 [sp_helpqreader_agent](../../../relational-databases/system-stored-procedures/sp-helpqreader-agent-transact-sql.md)。 此操作将返回队列读取器代理运行时所用的当前 Windows 帐户。  
  
    -   在分发服务器上，执行 [sp_changeqreader_agent](../../../relational-databases/system-stored-procedures/sp-changeqreader-agent-transact-sql.md), ，指定的 Windows 帐户设置 **@job_login** 和 **@job_passwsord**。  
  
    > [!NOTE]  
    >  更改代理登录名或密码之后，必须先停止并重新启动代理，然后更改才能生效。 每个分发数据库都有一个队列读取器代理。 更改代理的安全设置会影响使用此分发数据库的所有发布服务器上所有发布的设置。  
  
2.  对于订阅，队列读取器代理使用与分发代理相同的连接上下文与订阅服务器建立连接。  
  
#### 更改立即更新订阅服务器连接到发布服务器时所用的安全模式  
  
1.  在订阅服务器上的订阅数据库上，执行 [sp_link_publication](../../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md)。 指定 **@publisher**, ，**@publication**, ，为发布数据库的名称 **@publisher_db**, ，以及下列其中一项值为 **@security_mode**:  
  
    -   **0** ，表示在发布服务器上执行更新时使用 SQL Server 身份验证。 此选项需要为 **@login** 和 **@password**指定发布服务器上的一个有效登录名。  
  
    -   **1** ，表示连接到发布服务器时使用在订阅服务器上执行更改的用户的安全上下文。 请参阅 [sp_link_publication](../../../relational-databases/system-stored-procedures/sp-link-publication-transact-sql.md) 有关与此安全模式相关的限制。  
  
    -   **2** 若要使用的现有，用户定义的链接服务器登录名创建使用 [sp_addlinkedserver & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql.md)。  
  
#### 更改远程分发服务器的密码  
  
1.  在分发数据库上分发服务器上，执行 [sp_changedistributor_password](../../../relational-databases/system-stored-procedures/sp-changedistributor-password-transact-sql.md), ，指定此登录名的新密码 **@password**。  
  
    > [!IMPORTANT]  
    >  未更改的密码 **distributor_admin** 直接。  
  
2.  使用此远程分发服务器的每个发布，在执行 [sp_changedistributor_password](../../../relational-databases/system-stored-procedures/sp-changedistributor-password-transact-sql.md), ，指定步骤 1 中的密码 **@password**。  
  
##  <a name="RMOProcedure"></a> 使用复制管理对象 (RMO)  
  
> [!IMPORTANT]  
>  如果可能，请在运行时提示用户输入安全凭据。 如果必须存储凭据，请使用 [Windows .NET Framework 提供的](http://go.microsoft.com/fwlink/?LinkId=34733) Cryptographic Services [!INCLUDE[msCoName](../../../includes/msconame-md.md)] （加密服务）。  
  
#### 更改存储在复制服务器上的某个密码的所有实例  
  
1.  使用创建连接到复制服务器 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 类。  
  
2.  创建的实例 <xref:Microsoft.SqlServer.Replication.ReplicationServer> 类通过使用步骤 1 中的连接。  
  
3.  调用 <xref:Microsoft.SqlServer.Replication.ReplicationServer.ChangeReplicationServerPasswords%2A> 方法。 指定下列参数：  
  
    -   *security_mode* - <xref:Microsoft.SqlServer.Replication.ReplicationSecurityMode> 值，该值指定正在更改密码的所有实例的身份验证的类型。  
  
    -   *登录名* -正在更改密码的所有实例的登录名。  
  
    -   *密码* 的新密码值。  
  
        > [!IMPORTANT]  
        >  如果可能，请在运行时提示用户输入安全凭据。 如果必须存储凭据，请使用 Windows .NET Framework 提供的 [Cryptographic Services](http://go.microsoft.com/fwlink/?LinkId=34733) （加密服务）。  
  
        > [!NOTE]  
        >  只有一个的成员 **sysadmin** 固定的服务器角色可以调用此方法。  
  
4.  对复制拓扑中需要更新密码的每个服务器重复步骤 1-3。  
  
#### 为事务发布的推送订阅的分发代理更改安全设置  
  
1.  通过使用创建连接到发布服务器 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 类。  
  
2.  创建的实例 <xref:Microsoft.SqlServer.Replication.TransSubscription> 类。  
  
3.  设置 <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>, ，<xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>, ，<xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>, ，和 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A> 属性的订阅，并设置从连接步骤 1 的 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 属性。  
  
4.  调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法以获取该对象的属性。 如果此方法返回 **false**，则说明步骤 3 中的订阅属性没有正确定义或该订阅不存在。  
  
5.  实例上设置一个或多个以下的安全属性 <xref:Microsoft.SqlServer.Replication.TransSubscription>:  
  
    -   若要更改代理运行的 Windows 帐户的凭据，将设置 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> 和 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> 字段 <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A>。  
  
    -   若要指定 Windows 集成身份验证作为代理连接到订阅服务器时使用的身份验证的类型，设置 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> 字段 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberSecurity%2A> 属性设置为 **true**。  
  
    -   若要指定 SQL Server 身份验证作为代理连接到订阅服务器时使用的身份验证的类型，设置 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> 字段 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberSecurity%2A> 属性设置为 **false**, ，并指定的订阅服务器登录凭据 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> 和 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> 字段。  
  
        > [!NOTE]  
        >  始终使用由指定的 Windows 凭据建立代理与分发服务器的连接 <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A>。 此帐户还用于建立使用 Windows 身份验证的远程连接。  
  
6.  （可选）如果指定的值为 **true** 为 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>, ，调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 方法在服务器上提交更改。 如果指定的值为 **false** 为 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> （默认值），更改将立即发送到服务器。  
  
#### 为事务发布的请求订阅的分发代理更改安全设置  
  
1.  通过使用创建连接到订阅服务器 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 类。  
  
2.  创建的实例 <xref:Microsoft.SqlServer.Replication.TransPullSubscription> 类。  
  
3.  设置 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>, ，<xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>, ，<xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>, ，和 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A> 属性的订阅，并设置从连接步骤 1 的 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 属性。  
  
4.  调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法以获取该对象的属性。 如果此方法返回 **false**，则说明步骤 3 中的订阅属性没有正确定义或该订阅不存在。  
  
5.  实例上设置一个或多个以下的安全属性 <xref:Microsoft.SqlServer.Replication.TransPullSubscription>:  
  
    -   若要更改代理运行的 Windows 帐户的凭据，将设置 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> 和 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> 字段 <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A>。  
  
    -   若要指定 Windows 集成身份验证作为代理连接到分发服务器时使用的身份验证的类型，设置 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> 字段 <xref:Microsoft.SqlServer.Replication.PullSubscription.DistributorSecurity%2A> 属性设置为 **true**。  
  
    -   若要指定 SQL Server 身份验证作为代理连接到分发服务器时使用的身份验证的类型，设置 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> 字段 <xref:Microsoft.SqlServer.Replication.PullSubscription.DistributorSecurity%2A> 属性设置为 **false**, ，并指定的分发服务器登录凭据 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> 和 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> 字段。  
  
        > [!NOTE]  
        >  始终使用由指定的 Windows 凭据建立与订阅服务器上的代理连接 <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A>。 此帐户还用于建立使用 Windows 身份验证的远程连接。  
  
6.  （可选）如果指定的值为 **true** 为 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>, ，调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 方法在服务器上提交更改。 如果指定的值为 **false** 为 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> （默认值），更改将立即发送到服务器。  
  
#### 为合并发布的请求订阅的合并代理更改安全设置  
  
1.  通过使用创建连接到订阅服务器 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 类。  
  
2.  创建的实例 <xref:Microsoft.SqlServer.Replication.MergePullSubscription> 类。  
  
3.  设置 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationName%2A>, ，<xref:Microsoft.SqlServer.Replication.PullSubscription.DatabaseName%2A>, ，<xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherName%2A>, ，和 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublicationDBName%2A> 属性的订阅，并设置从连接步骤 1 的 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 属性。  
  
4.  调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法以获取该对象的属性。 如果此方法返回 **false**，则说明步骤 3 中的订阅属性没有正确定义或该订阅不存在。  
  
5.  实例上设置一个或多个以下的安全属性 <xref:Microsoft.SqlServer.Replication.MergePullSubscription>:  
  
    -   若要更改代理运行的 Windows 帐户的凭据，将设置 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> 和 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> 字段 <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A>。  
  
    -   若要指定 Windows 集成身份验证作为代理连接到分发服务器时使用的身份验证的类型，设置 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> 字段 <xref:Microsoft.SqlServer.Replication.PullSubscription.DistributorSecurity%2A> 属性设置为 **true**。  
  
    -   若要指定 SQL Server 身份验证作为代理连接到分发服务器时使用的身份验证的类型，设置 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> 字段 <xref:Microsoft.SqlServer.Replication.PullSubscription.DistributorSecurity%2A> 属性设置为 **false**, ，并指定的分发服务器登录凭据 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> 和 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> 字段。  
  
    -   若要指定 Windows 集成身份验证作为代理连接到发布服务器时使用的身份验证的类型，设置 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> 字段 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherSecurity%2A> 属性设置为 **true**。  
  
    -   若要指定 SQL Server 身份验证作为代理连接到发布服务器时使用的身份验证的类型，设置 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> 字段 <xref:Microsoft.SqlServer.Replication.PullSubscription.PublisherSecurity%2A> 属性设置为 **false**, ，并指定的发布服务器登录凭据 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> 和 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> 字段。  
  
        > [!NOTE]  
        >  始终使用由指定的 Windows 凭据建立与订阅服务器上的代理连接 <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A>。 此帐户还用于建立使用 Windows 身份验证的远程连接。  
  
6.  （可选）如果指定的值为 **true** 为 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>, ，调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 方法在服务器上提交更改。 如果指定的值为 **false** 为 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> （默认值），更改将立即发送到服务器。  
  
#### 为合并发布的推送订阅的合并代理更改安全设置  
  
1.  通过使用创建连接到发布服务器 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 类。  
  
2.  创建的实例 <xref:Microsoft.SqlServer.Replication.MergeSubscription> 类。  
  
3.  设置 <xref:Microsoft.SqlServer.Replication.Subscription.PublicationName%2A>, ，<xref:Microsoft.SqlServer.Replication.Subscription.DatabaseName%2A>, ，<xref:Microsoft.SqlServer.Replication.Subscription.SubscriberName%2A>, ，和 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriptionDBName%2A> 属性的订阅，并设置从连接步骤 1 的 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 属性。  
  
4.  调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法以获取该对象的属性。 如果此方法返回 **false**，则说明步骤 3 中的订阅属性没有正确定义或该订阅不存在。  
  
5.  实例上设置一个或多个以下的安全属性 <xref:Microsoft.SqlServer.Replication.MergeSubscription>:  
  
    -   若要更改代理运行的 Windows 帐户的凭据，将设置 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Login%2A> 和 <xref:Microsoft.SqlServer.Replication.IProcessSecurityContext.Password%2A> 字段 <xref:Microsoft.SqlServer.Replication.PullSubscription.SynchronizationAgentProcessSecurity%2A>。  
  
    -   若要指定 Windows 集成身份验证作为代理连接到订阅服务器时使用的身份验证的类型，设置 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> 字段 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberSecurity%2A> 属性设置为 **true**。  
  
    -   若要指定 SQL Server 身份验证作为代理连接到订阅服务器时使用的身份验证的类型，设置 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> 字段 <xref:Microsoft.SqlServer.Replication.Subscription.SubscriberSecurity%2A> 属性设置为 **false**, ，并指定的订阅服务器登录凭据 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardLogin%2A> 和 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.SqlStandardPassword%2A> 字段。  
  
    -   若要指定 Windows 集成身份验证作为代理连接到发布服务器时使用的身份验证的类型，设置 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> 字段 <xref:Microsoft.SqlServer.Replication.MergeSubscription.PublisherSecurity%2A> 属性设置为 **true**。  
  
    -   若要指定 SQL Server 身份验证作为代理连接到发布服务器时使用的身份验证的类型，设置 <xref:Microsoft.SqlServer.Replication.ConnectionSecurityContext.WindowsAuthentication%2A> 字段 <xref:Microsoft.SqlServer.Replication.MergeSubscription.PublisherSecurity%2A> 属性设置为 **false**, ，并指定的发布服务器登录凭据 <xref:Microsoft.SqlServer.Replication.PublisherConnectionSecurityContext.SqlStandardLogin%2A> 和 <xref:Microsoft.SqlServer.Replication.PublisherConnectionSecurityContext.SqlStandardPassword%2A> 字段。  
  
        > [!NOTE]  
        >  始终使用由指定的 Windows 凭据建立代理与分发服务器的连接 <xref:Microsoft.SqlServer.Replication.Subscription.SynchronizationAgentProcessSecurity%2A>。 此帐户还用于建立使用 Windows 身份验证的远程连接。  
  
6.  （可选）如果指定的值为 **true** 为 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>, ，调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 方法在服务器上提交更改。 如果指定的值为 **false** 为 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> （默认值），更改将立即发送到服务器。  
  
#### 更改即时更新订阅服务器连接到事务发布服务器时使用的登录信息  
  
1.  通过使用创建连接到订阅服务器 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 类。  
  
2.  创建的实例 <xref:Microsoft.SqlServer.Replication.ReplicationDatabase> 对订阅数据库的类。 指定 <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.Name%2A> 和 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 步骤 1 中的 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A>。  
  
3.  调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法以获取该对象的属性。 如果此方法返回 **false**，则说明步骤 2 中的数据库属性定义不正确或此订阅数据库不存在。  
  
4.  调用 <xref:Microsoft.SqlServer.Replication.ReplicationDatabase.LinkPublicationForUpdateableSubscription%2A> 方法，并传递以下参数︰  
  
    -   *发布服务器* -发布服务器的名称。  
  
    -   *PublisherDB* -发布数据库的名称。  
  
    -   *发布* -即时更新订阅服务器订阅的发布的名称。  
  
    -   *分发服务器* -分发服务器的名称。  
  
    -   *PublisherSecurity* - <xref:Microsoft.SqlServer.Replication.PublisherConnectionSecurityContext> 指定连接到发布服务器和登录凭据的连接时使用的即时更新订阅服务器的安全模式的类型的对象。  
  
###  <a name="PShellExample"></a> 示例 (RMO)  
 本示例将检查提供的登录值并为所提供的 Windows 登录名或 SQL Server 登录名（由服务器上的复制存储）更改所有密码。  
  
 [!code-csharp[HowTo#rmo_ChangeServerPasswords](../../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_changeserverpasswords)]  
  
 [!code-vb[HowTo#rmo_vb_ChangeServerPasswords](../../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_changeserverpasswords)]  
  
##  <a name="FollowUp"></a> 跟进：修改复制安全设置后  
 更改代理登录名或密码之后，必须先停止并重新启动代理，然后更改才能生效。  
  
## 另请参阅  
 [复制管理对象概念](../../../relational-databases/replication/concepts/replication-management-objects-concepts.md)   
 [升级复制脚本 & #40;复制 TRANSACT-SQL 编程 & #41;](../../../relational-databases/replication/administration/upgrade-replication-scripts-replication-transact-sql-programming.md)   
 [管理复制中的登录名和密码](../../../relational-databases/replication/security/manage-logins-and-passwords-in-replication.md)   
 [复制代理安全性模式](../../../relational-databases/replication/security/replication-agent-security-model.md)   
 [复制安全最佳实践](../../../relational-databases/replication/security/replication-security-best-practices.md)   
 [安全和保护与 #40;复制和 #41;](../../../relational-databases/replication/security/security-and-protection-replication.md)   
 [复制系统存储过程概念](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)  
  
  