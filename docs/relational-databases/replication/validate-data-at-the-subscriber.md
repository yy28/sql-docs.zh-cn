---
title: "在订阅服务器上验证数据 | Microsoft Docs"
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
  - "订阅服务器 [SQL Server 复制], 数据验证"
  - "复制 [SQL Server], 验证数据"
  - "事务复制, 验证数据"
  - "验证数据"
  - "合并复制数据验证 [SQL Server 复制], SQL Server Management Studio"
ms.assetid: 215b4c9a-0ce9-4c00-ac0b-43b54151dfa3
caps.latest.revision: 39
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 39
---
# 在订阅服务器上验证数据
  本主题说明如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 或复制管理对象 (RMO) 在 [!INCLUDE[tsql](../../includes/tsql-md.md)] 中验证订阅服务器上的数据。  
  
 验证数据分为三个部分：  
  
1.  将对发布的单个或所有订阅“标记”  为要验证。 可以在“验证单个订阅” 、“验证多个订阅” 和“验证所有订阅”  对话框中，将订阅标记为要验证，这些对话框可以通过 **中的“本地发布”****文件夹和“本地订阅”**[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]文件夹访问。 也可以从 **“所有订阅”** 选项卡、 **“订阅监视列表”** 选项卡和复制监视器中的发布节点中对订阅进行标记。 有关启动复制监视器的信息，请参阅 [启动复制监视器](../../relational-databases/replication/monitor/start-the-replication-monitor.md)。  
  
2.  下次分发代理（对于事务复制）或合并代理（对于合并复制）同步订阅时，将对订阅进行验证。 分发代理通常是连续运行的，在这种情况下验证会立即进行；合并代理通常是按需运行的，在这种情况下验证在运行代理后进行。  
  
3.  查看验证结果：  
  
    -   在复制监视器的详细信息窗口中查看：对于事务复制，在 **“分发服务器到订阅服务器的历史记录”** 选项卡中；对于合并复制，在 **“同步历史记录”** 选项卡中。  
  
    -   在 **的** “查看同步状态” [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]对话框中查看。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [限制和局限](#Restrictions)  
  
-   **验证订阅服务器上的数据，使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [复制管理对象 (RMO)](#RMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Restrictions"></a> 限制和局限  
  
-   复制监视器的过程仅适用于推送订阅，因为请求订阅不能在复制监视器中同步。 但是，可以在复制监视器中将订阅标记为要验证并查看请求订阅的验证结果。  
  
-   验证结果指示验证是成功还是失败，但如果失败，并不指定哪些行验证失败。 若要比较发布服务器和订阅服务器中的数据，请使用 [tablediff Utility](../../tools/tablediff-utility.md)。 有关使用此实用工具处理复制的数据的详细信息，请参阅 [比较复制的表之间的差异和 #40;复制编程 & #41;](../../relational-databases/replication/administration/compare-replicated-tables-for-differences-replication-programming.md)。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### 验证事务发布的订阅的数据 (Management Studio)  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中连接到发布服务器，然后展开服务器节点。  
  
2.  展开 **“复制”** 文件夹，再展开 **“本地发布”** 文件夹。  
  
3.  右键单击想要验证的订阅，然后单击的发布 **验证多个订阅**。  
  
4.  在 **“验证多个订阅”** 对话框中，选择要验证的订阅：  
  
    -   选择 **“验证所有 SQL Server 订阅”**。  
  
    -   选择 **“验证下列订阅”**，再选择一个或多个订阅。  
  
5.  若要指定要执行 （行计数或行计数和校验和） 的验证类型，请单击 **验证选项**, ，然后指定选项中的 **订阅验证选项** 对话框。  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
7.  在复制监视器或 **“查看同步状态”** 对话框中查看验证结果。 对于每个订阅：  
  
    1.  展开的发布，右键单击该订阅，然后单击 **查看同步状态**。  
  
    2.  如果代理未运行，请单击 **“查看同步状态”** 对话框中的 **“启动”** 。 该对话框将显示有关验证的信息性消息。  
  
     如果未显示有关验证的任何消息，则说明该代理已记录了后续消息。 在这种情况下，请在复制监视器中查看验证结果。 有关详细信息，请参阅本主题中有关复制监视器相关操作的过程。  
  
#### 验证合并发布的单个订阅的数据 (Management Studio)  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中连接到发布服务器，然后展开服务器节点。  
  
2.  展开 **“复制”** 文件夹，再展开 **“本地发布”** 文件夹。  
  
3.  展开要验证的订阅，右键单击该订阅，然后单击的发布 **验证单个订阅**。  
  
4.  在 **“验证单个订阅”** 对话框中，选择 **“验证此订阅”**。  
  
5.  若要指定要执行 （行计数或行计数和校验和） 的验证类型，请单击 **选项**, ，然后指定选项中的 **订阅验证选项** 对话框。  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
7.  在复制监视器或 **“查看同步状态”** 对话框中查看验证结果：  
  
    1.  展开的发布，右键单击该订阅，然后单击 **查看同步状态**。  
  
    2.  如果代理未运行，请单击 **“查看同步状态”** 对话框中的 **“启动”** 。 该对话框将显示有关验证的信息性消息。  
  
     如果未显示有关验证的任何消息，则说明该代理已记录了后续消息。 在这种情况下，请在复制监视器中查看验证结果。 有关详细信息，请参阅本主题中有关复制监视器相关操作的过程。  
  
#### 验证合并发布的所有订阅的数据 (Management Studio)  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中连接到发布服务器，然后展开服务器节点。  
  
2.  展开 **“复制”** 文件夹，再展开 **“本地发布”** 文件夹。  
  
3.  右键单击想要验证的订阅，然后单击的发布 **验证所有订阅**。  
  
4.  在 **验证所有订阅** 对话框框中，指定要执行 （行计数或行计数和校验和） 的验证类型。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
6.  在复制监视器或 **“查看同步状态”** 对话框中查看验证结果。 对于每个订阅：  
  
    1.  展开的发布，右键单击该订阅，然后单击 **查看同步状态**。  
  
    2.  如果代理未运行，请单击 **“查看同步状态”** 对话框中的 **“启动”** 。 该对话框将显示有关验证的信息性消息。  
  
     如果未显示有关验证的任何消息，则说明该代理已记录了后续消息。 在这种情况下，请在复制监视器中查看验证结果。 有关详细信息，请参阅本主题中有关复制监视器相关操作的过程。  
  
#### 验证事务发布的所有推送订阅的数据（复制监视器）  
  
1.  在复制监视器的左窗格中依次展开发布服务器组、发布服务器。  
  
2.  右键单击想要验证的订阅，然后单击的发布 **验证多个订阅**。  
  
3.  在 **“验证多个订阅”** 对话框中，选择要验证的订阅：  
  
    -   选择 **“验证所有 SQL Server 订阅”**。  
  
    -   选择 **“验证下列订阅”**，再选择一个或多个订阅。  
  
4.  若要指定要执行 （行计数或行计数和校验和） 的验证类型，请单击 **验证选项**, ，然后指定选项中的 **订阅验证选项** 对话框。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
6.  单击 **“所有订阅”** 选项卡。  
  
7.  查看验证结果。 对于每个推送订阅：  
  
    1.  如果代理未运行，右键单击该订阅，然后单击 **开始同步**。  
  
    2.  右键单击该订阅，然后单击 **查看详细信息**。  
  
    3.  在 **“所选会话中的操作”** 文本区域中的 **“分发服务器到订阅服务器的历史记录”** 选项卡中，查看信息。  
  
#### 验证合并发布的单个推送订阅的数据（复制监视器）  
  
1.  在复制监视器的左窗格中依次展开发布服务器组、发布服务器，再单击一个发布。  
  
2.  单击 **“所有订阅”** 选项卡。  
  
3.  右键单击你想要验证，然后单击的订阅 **验证单个订阅**。  
  
4.  在 **“验证单个订阅”** 对话框中，选择 **“验证此订阅”**。  
  
5.  若要指定要执行 （行计数或行计数和校验和） 的验证类型，请单击 **选项**, ，然后指定选项中的 **订阅验证选项** 对话框。  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
7.  单击 **“所有订阅”** 选项卡。  
  
8.  查看验证结果：  
  
    1.  如果代理未运行，右键单击该订阅，然后单击 **开始同步**。  
  
    2.  右键单击该订阅，然后单击 **查看详细信息**。  
  
    3.  查看 **“同步历史记录”** 选项卡 **“所选会话的最后消息”** 文本区域中的信息。  
  
#### 验证合并发布的所有推送订阅的数据（复制监视器）  
  
1.  在复制监视器的左窗格中依次展开发布服务器组、发布服务器。  
  
2.  右键单击想要验证的订阅，然后单击的发布 **验证所有订阅**。  
  
3.  在 **验证所有订阅** 对话框框中，指定要执行 （行计数或行计数和校验和） 的验证类型。  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
5.  单击 **“所有订阅”** 选项卡。  
  
6.  查看验证结果。 对于每个推送订阅：  
  
    1.  如果代理未运行，右键单击该订阅，然后单击 **开始同步**。  
  
    2.  右键单击该订阅，然后单击 **查看详细信息**。  
  
    3.  查看 **“同步历史记录”** 选项卡 **“所选会话的最后消息”** 文本区域中的信息。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### 验证事务发布中所有项目的数据  
  
1.  在发布服务器上对发布数据库中，执行 [sp_publication_validation & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-publication-validation-transact-sql.md)。 指定 **@publication** 以及下列其中一项值为 **@rowcount_only**:  
  
    -   **1** -只检查行计数 （默认值）  
  
    -   **2** -行计数和二进制校验和。  
  
    > [!NOTE]  
    >  当您执行 [sp_publication_validation & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-publication-validation-transact-sql.md), ，[sp_article_validation & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md) 为每篇文章中发布器执行。 若要成功执行 [sp_publication_validation & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-publication-validation-transact-sql.md), ，必须已发布的基表中的所有列拥有 SELECT 权限。  
  
2.  （可选）如果分发代理尚未运行，请为每个订阅都启动分发代理。 有关详细信息，请参阅 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) 和 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md)。  
  
3.  检查代理输出以获取验证结果。 有关详细信息，请参阅 [验证已复制数据](../../relational-databases/replication/validate-replicated-data.md)。  
  
#### 验证事务发布中单个项目的数据  
  
1.  在发布服务器上对发布数据库中，执行 [sp_article_validation & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md)。 指定 **@publication**, ，项目的名称 **@article**, ，以及下列其中一项值为 **@rowcount_only**:  
  
    -   **1** -只检查行计数 （默认值）  
  
    -   **2** -行计数和二进制校验和。  
  
    > [!NOTE]  
    >  若要成功执行 [sp_article_validation & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md), ，必须已发布的基表中的所有列拥有 SELECT 权限。  
  
2.  （可选）如果分发代理尚未运行，请为每个订阅都启动分发代理。 有关详细信息，请参阅 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) 和 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md)。  
  
3.  检查代理输出以获取验证结果。 有关详细信息，请参阅 [验证已复制数据](../../relational-databases/replication/validate-replicated-data.md)。  
  
#### 验证订阅事务发布的单个订阅服务器的数据  
  
1.  在发布服务器上对发布数据库中，打开显式事务使用 [BEGIN TRANSACTION & #40;Transact SQL & #41;](../../t-sql/language-elements/begin-transaction-transact-sql.md)。  
  
2.  在发布服务器上对发布数据库中，执行 [sp_marksubscriptionvalidation & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-marksubscriptionvalidation-transact-sql.md)。 指定的发布 **@publication**, ，为订阅服务器的名称 **@subscriber**, ，以及订阅数据库的名称 **@destination_db**。  
  
3.  （可选）对每个要验证的订阅都重复步骤 2。  
  
4.  在发布服务器上对发布数据库中，执行 [sp_article_validation & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md)。 指定 **@publication**, ，项目的名称 **@article**, ，以及下列其中一项值为 **@rowcount_only**:  
  
    -   **1** -只检查行计数 （默认值）  
  
    -   **2** -行计数和二进制校验和。  
  
    > [!NOTE]  
    >  若要成功执行 [sp_article_validation & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-article-validation-transact-sql.md), ，必须已发布的基表中的所有列拥有 SELECT 权限。  
  
5.  在发布服务器上对发布数据库中，将提交事务使用 [COMMIT TRANSACTION & #40;Transact SQL & #41;](../../t-sql/language-elements/commit-transaction-transact-sql.md)。  
  
6.  （可选）为每个要验证的项目都重复步骤 1 到步骤 5。  
  
7.  （可选）如果分发代理尚未运行，请启动分发代理。 有关详细信息，请参阅 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) 和 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md)。  
  
8.  检查代理输出以获取验证结果。 有关详细信息，请参阅 [Validate Data at the Subscriber](../../relational-databases/replication/validate-data-at-the-subscriber.md)。  
  
#### 验证合并发布的所有订阅中的数据  
  
1.  在发布服务器上对发布数据库中，执行 [sp_validatemergepublication & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-validatemergepublication-transact-sql.md)。 指定 **@publication** 并为 **@level**指定以下值之一：  
  
    -   **1** -仅限行计数验证。  
  
    -   **3** -行计数二进制校验和验证。  
  
     这样会标记所有订阅以便验证。  
  
2.  启动每个订阅的合并代理。 有关详细信息，请参阅 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) 和 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md)。  
  
3.  检查代理输出以获取验证结果。 有关详细信息，请参阅 [Validate Data at the Subscriber](../../relational-databases/replication/validate-data-at-the-subscriber.md)。  
  
#### 验证订阅合并发布的所选订阅中的数据  
  
1.  在发布服务器上对发布数据库中，执行 [sp_validatemergesubscription & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-validatemergesubscription-transact-sql.md)。 指定 **@publication**, ，为订阅服务器的名称 **@subscriber**, ，订阅数据库的名称 **@subscriber_db**, ，以及下列其中一项值为 **@level**:  
  
    -   **1** -仅限行计数验证。  
  
    -   **3** -行计数二进制校验和验证。  
  
     这样会标记所选订阅以便验证。  
  
2.  启动每个订阅的合并代理。 有关详细信息，请参阅 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) 和 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md)。  
  
3.  检查代理输出以获取验证结果。  
  
4.  为每个要验证的订阅重复步骤 1 到步骤 3。  
  
> [!NOTE]  
>  对合并发布的订阅也在同步结束通过指定验证 **-验证** 参数在运行时 [复制合并代理](../../relational-databases/replication/agents/replication-merge-agent.md)。  
  
#### 使用合并代理参数验证订阅中的数据  
  
1.  通过以下方式之一从命令提示符下启动订阅服务器（请求订阅）或分发服务器（推送订阅）上的合并代理。  
  
    -   将值指定为 **1** （限行计数） 或 **3** （行计数和二进制校验和） 为 **-验证** 参数。  
  
    -   指定 **行计数验证** 或 **行计数和校验和验证** 为 **-ProfileName** 参数。  
  
     有关详细信息，请参阅 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) 或 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md)。  
  
##  <a name="RMOProcedure"></a> 使用复制管理对象 (RMO)  
 通过使用复制，您可以使用复制管理对象 (RMO) 以编程方式验证订阅服务器上的数据是否与发布服务器上的数据匹配。 使用的对象取决于复制拓扑的类型。 事务复制要求验证发布的所有订阅。  
  
> [!NOTE]  
>  有关示例，请参阅 [示例 (RMO)](#RMOExample), ，本部分中更高版本。  
  
#### 验证事务发布中所有项目的数据  
  
1.  通过使用创建连接到发布服务器 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 类。  
  
2.  创建的实例 <xref:Microsoft.SqlServer.Replication.TransPublication> 类。 设置 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> 和 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> 发布的属性。 设置 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 属性设置为在步骤 1 中创建的连接。  
  
3.  调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法以获取该对象的其余属性。 如果此方法返回 **false**，则说明步骤 2 中的发布属性定义不正确，或者此发布不存在。  
  
4.  调用 <xref:Microsoft.SqlServer.Replication.TransPublication.ValidatePublication%2A> 方法。 传递以下参数：  
  
    -   <xref:Microsoft.SqlServer.Replication.ValidationOption>  
  
    -   <xref:Microsoft.SqlServer.Replication.ValidationMethod>  
  
    -   一个布尔值，指示是否在验证完成后停止分发代理。  
  
     这将把项目标记为等待验证。  
  
5.  如果尚未运行，则启动分发代理以同步每个订阅。 有关详细信息，请参阅 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md) 或 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md)。 验证操作的结果将写入代理历史记录。 有关详细信息，请参阅 [Monitoring Replication](../../relational-databases/replication/monitor/monitoring-replication-overview.md)。  
  
#### 验证合并发布的所有订阅中的数据  
  
1.  通过使用创建连接到发布服务器 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 类。  
  
2.  创建的实例 <xref:Microsoft.SqlServer.Replication.MergePublication> 类。 设置 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> 和 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> 发布的属性。 设置 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 属性设置为在步骤 1 中创建的连接。  
  
3.  调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法以获取该对象的其余属性。 如果此方法返回 **false**，则说明步骤 2 中的发布属性定义不正确，或者此发布不存在。  
  
4.  调用 <xref:Microsoft.SqlServer.Replication.MergePublication.ValidatePublication%2A> 方法。 传递所需 <xref:Microsoft.SqlServer.Replication.ValidationOption>。  
  
5.  对每个订阅运行合并代理以开始验证，或者等待下一个计划的代理运行。 有关详细信息，请参阅 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) 和 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md)。 验证操作的结果将写入代理的历史记录，您可以使用复制监视器查看。 有关详细信息，请参阅 [Monitoring Replication](../../relational-databases/replication/monitor/monitoring-replication-overview.md)。  
  
#### 验证合并发布的单个订阅中的数据  
  
1.  通过使用创建连接到发布服务器 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 类。  
  
2.  创建的实例 <xref:Microsoft.SqlServer.Replication.MergePublication> 类。 设置 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> 和 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> 发布的属性。 设置 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 属性设置为在步骤 1 中创建的连接。  
  
3.  调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法以获取该对象的其余属性。 如果此方法返回 **false**，则说明步骤 2 中的发布属性定义不正确，或者此发布不存在。  
  
4.  调用 <xref:Microsoft.SqlServer.Replication.MergePublication.ValidateSubscription%2A> 方法。 正在验证的订阅者和订阅数据库的名称和所需传递 <xref:Microsoft.SqlServer.Replication.ValidationOption>。  
  
5.  对订阅运行合并代理以开始验证，或者等待下一个计划的代理运行。 有关详细信息，请参阅 [Synchronize a Pull Subscription](../../relational-databases/replication/synchronize-a-pull-subscription.md) 和 [Synchronize a Push Subscription](../../relational-databases/replication/synchronize-a-push-subscription.md)。 验证操作的结果将写入代理的历史记录，您可以使用复制监视器查看。 有关详细信息，请参阅 [Monitoring Replication](../../relational-databases/replication/monitor/monitoring-replication-overview.md)。  
  
###  <a name="RMOExample"></a> 示例 (RMO)  
 此示例将对事务发布的所有订阅标记为行计数验证。  
  
 [!code-csharp[HowTo#rmo_ValidateTranPub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_validatetranpub)]  
  
 [!code-vb[HowTo#rmo_vb_ValidateTranPub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_validatetranpub)]  
  
 此示例将对合并发布的特定订阅标记为行计数验证。  
  
 [!code-csharp[HowTo#rmo_ValidateMergeSub](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_validatemergesub)]  
  
 [!code-vb[HowTo#rmo_vb_ValidateMergeSub](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_validatemergesub)]  
  
  