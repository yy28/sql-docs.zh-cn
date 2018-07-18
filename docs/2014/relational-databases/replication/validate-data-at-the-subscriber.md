---
title: 验证订阅服务器上的数据 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Subscribers [SQL Server replication], data validation
- replication [SQL Server], validating data
- transactional replication, validating data
- validating data
- merge replication data validation [SQL Server replication], SQL Server Management Studio
ms.assetid: 215b4c9a-0ce9-4c00-ac0b-43b54151dfa3
caps.latest.revision: 39
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d900cb88e99963fd57c7192d0f2934312434bc37
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37282983"
---
# <a name="validate-data-at-the-subscriber"></a>在订阅服务器上验证数据
  本主题说明如何使用 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 、 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]或复制管理对象 (RMO) 在 [!INCLUDE[tsql](../../includes/tsql-md.md)]中验证订阅服务器上的数据。  
  
 验证数据分为三个部分：  
  
1.  将对发布的单个或所有订阅“标记”  为要验证。 可以在“验证单个订阅”、“验证多个订阅”和“验证所有订阅”对话框中，将订阅标记为要验证，这些对话框可以通过 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 中的“本地发布”**文件夹和“本地订阅”** 文件夹访问。 也可以从 **“所有订阅”** 选项卡、 **“订阅监视列表”** 选项卡和复制监视器中的发布节点中对订阅进行标记。 有关启动复制监视器的信息，请参阅[启动复制监视器](monitor/start-the-replication-monitor.md)。  
  
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
  
-   验证结果指示验证是成功还是失败，但如果失败，并不指定哪些行验证失败。 若要比较发布服务器和订阅服务器中的数据，请使用 [tablediff Utility](../../tools/tablediff-utility.md)。 若要详细了解如何将此实用工具与已复制数据配合使用，请参阅[比较所复制表的差异（复制编程）](administration/compare-replicated-tables-for-differences-replication-programming.md)。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
  
#### <a name="to-validate-data-for-subscriptions-to-a-transactional-publication-management-studio"></a>验证事务发布的订阅的数据 (Management Studio)  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中连接到发布服务器，然后展开服务器节点。  
  
2.  展开 **“复制”** 文件夹，再展开 **“本地发布”** 文件夹。  
  
3.  右键单击要验证其订阅的发布，然后单击 **“验证多个订阅”**。  
  
4.  在 **“验证多个订阅”** 对话框中，选择要验证的订阅：  
  
    -   选择 **“验证所有 SQL Server 订阅”**。  
  
    -   选择 **“验证下列订阅”**，再选择一个或多个订阅。  
  
5.  若要指定要执行的验证类型（行计数，或行计数和校验和），请单击 **“验证选项”**，然后在 **“订阅验证选项”** 对话框中指定选项。  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
7.  在复制监视器或 **“查看同步状态”** 对话框中查看验证结果。 对于每个订阅：  
  
    1.  展开发布，右键单击该订阅，然后单击 **“查看同步状态”**。  
  
    2.  如果代理未运行，请单击 **“查看同步状态”** 对话框中的 **“启动”** 。 该对话框将显示有关验证的信息性消息。  
  
     如果未显示有关验证的任何消息，则说明该代理已记录了后续消息。 在这种情况下，请在复制监视器中查看验证结果。 有关详细信息，请参阅本主题中有关复制监视器相关操作的过程。  
  
#### <a name="to-validate-data-for-a-single-subscription-to-a-merge-publication-management-studio"></a>验证合并发布的单个订阅的数据 (Management Studio)  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中连接到发布服务器，然后展开服务器节点。  
  
2.  展开 **“复制”** 文件夹，再展开 **“本地发布”** 文件夹。  
  
3.  展开要验证其订阅的发布，右键单击该订阅，然后单击 **“验证单个订阅”**。  
  
4.  在 **“验证单个订阅”** 对话框中，选择 **“验证此订阅”**。  
  
5.  若要指定要执行的验证类型（行计数，或行计数和校验和），请单击 **“选项”**，然后在 **“订阅验证选项”** 对话框中指定选项。  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
7.  在复制监视器或 **“查看同步状态”** 对话框中查看验证结果：  
  
    1.  展开发布，右键单击该订阅，然后单击 **“查看同步状态”**。  
  
    2.  如果代理未运行，请单击 **“查看同步状态”** 对话框中的 **“启动”** 。 该对话框将显示有关验证的信息性消息。  
  
     如果未显示有关验证的任何消息，则说明该代理已记录了后续消息。 在这种情况下，请在复制监视器中查看验证结果。 有关详细信息，请参阅本主题中有关复制监视器相关操作的过程。  
  
#### <a name="to-validate-data-for-all-subscriptions-to-a-merge-publication-management-studio"></a>验证合并发布的所有订阅的数据 (Management Studio)  
  
1.  在 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]中连接到发布服务器，然后展开服务器节点。  
  
2.  展开 **“复制”** 文件夹，再展开 **“本地发布”** 文件夹。  
  
3.  右键单击要验证其订阅的发布，然后单击 **“验证所有订阅”**。  
  
4.  在 **“验证所有订阅”** 对话框中，指定要执行的验证类型（行计数，或行计数和校验和）。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
6.  在复制监视器或 **“查看同步状态”** 对话框中查看验证结果。 对于每个订阅：  
  
    1.  展开发布，右键单击该订阅，然后单击 **“查看同步状态”**。  
  
    2.  如果代理未运行，请单击 **“查看同步状态”** 对话框中的 **“启动”** 。 该对话框将显示有关验证的信息性消息。  
  
     如果未显示有关验证的任何消息，则说明该代理已记录了后续消息。 在这种情况下，请在复制监视器中查看验证结果。 有关详细信息，请参阅本主题中有关复制监视器相关操作的过程。  
  
#### <a name="to-validate-data-for-all-push-subscriptions-to-a-transactional-publication-replication-monitor"></a>验证事务发布的所有推送订阅的数据（复制监视器）  
  
1.  在复制监视器的左窗格中依次展开发布服务器组、发布服务器。  
  
2.  右键单击要验证其订阅的发布，然后单击 **“验证多个订阅”**。  
  
3.  在 **“验证多个订阅”** 对话框中，选择要验证的订阅：  
  
    -   选择 **“验证所有 SQL Server 订阅”**。  
  
    -   选择 **“验证下列订阅”**，再选择一个或多个订阅。  
  
4.  若要指定要执行的验证类型（行计数，或行计数和校验和），请单击 **“验证选项”**，然后在 **“订阅验证选项”** 对话框中指定选项。  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
6.  单击 **“所有订阅”** 选项卡。  
  
7.  查看验证结果。 对于每个推送订阅：  
  
    1.  如果代理未运行，请右键单击该订阅，然后单击 **“开始同步”**。  
  
    2.  右键单击该订阅，然后单击 **“查看详细信息”**。  
  
    3.  在 **“所选会话中的操作”** 文本区域中的 **“分发服务器到订阅服务器的历史记录”** 选项卡中，查看信息。  
  
#### <a name="to-validate-data-for-a-single-push-subscription-to-a-merge-publication-replication-monitor"></a>验证合并发布的单个推送订阅的数据（复制监视器）  
  
1.  在复制监视器的左窗格中依次展开发布服务器组、发布服务器，再单击一个发布。  
  
2.  单击 **“所有订阅”** 选项卡。  
  
3.  右键单击要验证的订阅，然后单击 **“验证单个订阅”**。  
  
4.  在 **“验证单个订阅”** 对话框中，选择 **“验证此订阅”**。  
  
5.  若要指定要执行的验证类型（行计数，或行计数和校验和），请单击 **“选项”**，然后在 **“订阅验证选项”** 对话框中指定选项。  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
7.  单击 **“所有订阅”** 选项卡。  
  
8.  查看验证结果：  
  
    1.  如果代理未运行，请右键单击该订阅，然后单击 **“开始同步”**。  
  
    2.  右键单击该订阅，然后单击 **“查看详细信息”**。  
  
    3.  查看 **“同步历史记录”** 选项卡 **“所选会话的最后消息”** 文本区域中的信息。  
  
#### <a name="to-validate-data-for-all-push-subscriptions-to-a-merge-publication-replication-monitor"></a>验证合并发布的所有推送订阅的数据（复制监视器）  
  
1.  在复制监视器的左窗格中依次展开发布服务器组、发布服务器。  
  
2.  右键单击要验证其订阅的发布，然后单击 **“验证所有订阅”**。  
  
3.  在 **“验证所有订阅”** 对话框中，指定要执行的验证类型（行计数，或行计数和校验和）。  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
5.  单击 **“所有订阅”** 选项卡。  
  
6.  查看验证结果。 对于每个推送订阅：  
  
    1.  如果代理未运行，请右键单击该订阅，然后单击 **“开始同步”**。  
  
    2.  右键单击该订阅，然后单击 **“查看详细信息”**。  
  
    3.  查看 **“同步历史记录”** 选项卡 **“所选会话的最后消息”** 文本区域中的信息。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
  
#### <a name="to-validate-data-for-all-articles-in-a-transactional-publication"></a>验证事务发布中所有项目的数据  
  
1.  在发布服务器上，对发布数据库执行 [sp_publication_validation &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-publication-validation-transact-sql)。 指定 **@publication** 并为 **@rowcount_only**指定以下值之一：  
  
    -   **1** - 只检查行计数（默认值）  
  
    -   **2** - 行计数和二进制校验和。  
  
    > [!NOTE]  
    >  执行 [sp_publication_validation &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-publication-validation-transact-sql) 时，将会对发布中的每个项目执行 [sp_article_validation &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-article-validation-transact-sql)。 若要成功地执行 [sp_publication_validation &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-publication-validation-transact-sql)，必须对发布的基表中的所有列拥有 SELECT 权限。  
  
2.  （可选）如果分发代理尚未运行，请为每个订阅都启动分发代理。 有关详细信息，请参阅 [Synchronize a Pull Subscription](synchronize-a-pull-subscription.md) 和 [Synchronize a Push Subscription](synchronize-a-push-subscription.md)。  
  
3.  检查代理输出以获取验证结果。 有关详细信息，请参阅[验证已复制的数据](validate-replicated-data.md)。  
  
#### <a name="to-validate-data-for-a-single-article-in-a-transactional-publication"></a>验证事务发布中单个项目的数据  
  
1.  在发布服务器上，对发布数据库执行 [sp_article_validation &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-article-validation-transact-sql)。 指定 **@publication**、为 **@article**指定项目名称并为 **@rowcount_only**指定以下值之一：  
  
    -   **1** - 只检查行计数（默认值）  
  
    -   **2** - 行计数和二进制校验和。  
  
    > [!NOTE]  
    >  若要成功地执行 [sp_article_validation &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-article-validation-transact-sql)，必须对发布的基表中的所有列拥有 SELECT 权限。  
  
2.  （可选）如果分发代理尚未运行，请为每个订阅都启动分发代理。 有关详细信息，请参阅 [Synchronize a Pull Subscription](synchronize-a-pull-subscription.md) 和 [Synchronize a Push Subscription](synchronize-a-push-subscription.md)。  
  
3.  检查代理输出以获取验证结果。 有关详细信息，请参阅[验证已复制的数据](validate-replicated-data.md)。  
  
#### <a name="to-validate-data-for-a-single-subscriber-to-a-transactional-publication"></a>验证订阅事务发布的单个订阅服务器的数据  
  
1.  在发布服务器的发布数据库中，使用 [BEGIN TRANSACTION &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/begin-transaction-transact-sql) 打开一个显式事务。  
  
2.  在发布服务器上，对发布数据库执行 [sp_marksubscriptionvalidation &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-marksubscriptionvalidation-transact-sql)。 为 **@publication**指定发布，为 **@subscriber**指定订阅服务器的名称，并为 **@destination_db**。  
  
3.  （可选）对每个要验证的订阅都重复步骤 2。  
  
4.  在发布服务器上，对发布数据库执行 [sp_article_validation &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-article-validation-transact-sql)。 指定 **@publication**、为 **@article**指定项目名称并为 **@rowcount_only**指定以下值之一：  
  
    -   **1** - 只检查行计数（默认值）  
  
    -   **2** - 行计数和二进制校验和。  
  
    > [!NOTE]  
    >  若要成功地执行 [sp_article_validation &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-article-validation-transact-sql)，必须对发布的基表中的所有列拥有 SELECT 权限。  
  
5.  在发布服务器的发布数据库中，使用 [COMMIT TRANSACTION &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/commit-transaction-transact-sql) 提交事务。  
  
6.  （可选）为每个要验证的项目都重复步骤 1 到步骤 5。  
  
7.  （可选）如果分发代理尚未运行，请启动分发代理。 有关详细信息，请参阅 [Synchronize a Pull Subscription](synchronize-a-pull-subscription.md) 和 [Synchronize a Push Subscription](synchronize-a-push-subscription.md)。  
  
8.  检查代理输出以获取验证结果。 有关详细信息，请参阅 [Validate Data at the Subscriber](validate-data-at-the-subscriber.md)。  
  
#### <a name="to-validate-data-in-all-subscriptions-to-a-merge-publication"></a>验证合并发布的所有订阅中的数据  
  
1.  在发布服务器上，对发布数据库执行 [sp_validatemergepublication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-validatemergepublication-transact-sql)。 指定 **@publication** 并为 **@level**指定以下值之一：  
  
    -   **1** - 只验证行计数。  
  
    -   **3** - 行计数二进制校验和验证。  
  
     这样会标记所有订阅以便验证。  
  
2.  启动每个订阅的合并代理。 有关详细信息，请参阅 [Synchronize a Pull Subscription](synchronize-a-pull-subscription.md) 和 [Synchronize a Push Subscription](synchronize-a-push-subscription.md)。  
  
3.  检查代理输出以获取验证结果。 有关详细信息，请参阅 [Validate Data at the Subscriber](validate-data-at-the-subscriber.md)。  
  
#### <a name="to-validate-data-in-selected-subscriptions-to-a-merge-publication"></a>验证订阅合并发布的所选订阅中的数据  
  
1.  在发布服务器上，对发布数据库执行 [sp_validatemergesubscription &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-validatemergesubscription-transact-sql)。 指定 **@publication**指定发布，为 **@subscriber**指定订阅服务器的名称，为 **@subscriber_db**指定项目名称并为 **@level**指定以下值之一：  
  
    -   **1** - 只验证行计数。  
  
    -   **3** - 行计数二进制校验和验证。  
  
     这样会标记所选订阅以便验证。  
  
2.  启动每个订阅的合并代理。 有关详细信息，请参阅 [Synchronize a Pull Subscription](synchronize-a-pull-subscription.md) 和 [Synchronize a Push Subscription](synchronize-a-push-subscription.md)。  
  
3.  检查代理输出以获取验证结果。  
  
4.  为每个要验证的订阅重复步骤 1 到步骤 3。  
  
> [!NOTE]  
>  通过在运行 **Replication Merge Agent** 时指定 [-Validate](agents/replication-merge-agent.md)参数还可以在同步结束时验证对合并发布的订阅。  
  
#### <a name="to-validate-data-in-a-subscription-using-merge-agent-parameters"></a>使用合并代理参数验证订阅中的数据  
  
1.  通过以下方式之一从命令提示符下启动订阅服务器（请求订阅）或分发服务器（推送订阅）上的合并代理。  
  
    -   为 **-Validate** 参数指定值 **1** （行计数）或 **3** （行计数和二进制校验和）。  
  
    -   为 **-ProfileName** 参数指定 **rowcount validation** 或 **rowcount and checksum validation** 。  
  
     有关详细信息，请参阅 [Synchronize a Pull Subscription](synchronize-a-pull-subscription.md) 或 [Synchronize a Push Subscription](synchronize-a-push-subscription.md)。  
  
##  <a name="RMOProcedure"></a> 使用复制管理对象 (RMO)  
 通过使用复制，您可以使用复制管理对象 (RMO) 以编程方式验证订阅服务器上的数据是否与发布服务器上的数据匹配。 使用的对象取决于复制拓扑的类型。 事务复制要求验证发布的所有订阅。  
  
> [!NOTE]  
>  有关示例，请参阅本节后面的 [示例 (RMO)](#RMOExample)。  
  
#### <a name="to-validate-data-for-all-articles-in-a-transactional-publication"></a>验证事务发布中所有项目的数据  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 类创建与发布服务器的连接。  
  
2.  创建 <xref:Microsoft.SqlServer.Replication.TransPublication> 类的实例。 设置发布的 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> 和 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> 属性。 将 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 属性设置为步骤 1 中创建的连接。  
  
3.  调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法获取该对象的其余属性。 如果此方法返回`false`，步骤 2 中的发布属性定义不正确或不存在发布。  
  
4.  调用 <xref:Microsoft.SqlServer.Replication.TransPublication.ValidatePublication%2A> 方法。 传递以下参数：  
  
    -   <xref:Microsoft.SqlServer.Replication.ValidationOption>  
  
    -   <xref:Microsoft.SqlServer.Replication.ValidationMethod>  
  
    -   一个布尔值，指示是否在验证完成后停止分发代理。  
  
     这将把项目标记为等待验证。  
  
5.  如果尚未运行，则启动分发代理以同步每个订阅。 有关详细信息，请参阅 [Synchronize a Push Subscription](synchronize-a-push-subscription.md) 或 [Synchronize a Pull Subscription](synchronize-a-pull-subscription.md)。 验证操作的结果将写入代理历史记录。 有关详细信息，请参阅 [Monitoring Replication](monitoring-replication.md)。  
  
#### <a name="to-validate-data-in-all-subscriptions-to-a-merge-publication"></a>验证合并发布的所有订阅中的数据  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 类创建与发布服务器的连接。  
  
2.  创建 <xref:Microsoft.SqlServer.Replication.MergePublication> 类的实例。 设置发布的 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> 和 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> 属性。 将 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 属性设置为步骤 1 中创建的连接。  
  
3.  调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法获取该对象的其余属性。 如果此方法返回`false`，步骤 2 中的发布属性定义不正确或不存在发布。  
  
4.  调用 <xref:Microsoft.SqlServer.Replication.MergePublication.ValidatePublication%2A> 方法。 传递所需的 <xref:Microsoft.SqlServer.Replication.ValidationOption>。  
  
5.  对每个订阅运行合并代理以开始验证，或者等待下一个计划的代理运行。 有关详细信息，请参阅 [Synchronize a Pull Subscription](synchronize-a-pull-subscription.md) 和 [Synchronize a Push Subscription](synchronize-a-push-subscription.md)。 验证操作的结果将写入代理的历史记录，您可以使用复制监视器查看。 有关详细信息，请参阅 [Monitoring Replication](monitoring-replication.md)。  
  
#### <a name="to-validate-data-in-a-single-subscription-to-a-merge-publication"></a>验证合并发布的单个订阅中的数据  
  
1.  使用 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 类创建与发布服务器的连接。  
  
2.  创建 <xref:Microsoft.SqlServer.Replication.MergePublication> 类的实例。 设置发布的 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> 和 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> 属性。 将 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 属性设置为步骤 1 中创建的连接。  
  
3.  调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法获取该对象的其余属性。 如果此方法返回`false`，步骤 2 中的发布属性定义不正确或不存在发布。  
  
4.  调用 <xref:Microsoft.SqlServer.Replication.MergePublication.ValidateSubscription%2A> 方法。 传递要验证的订阅服务器和订阅数据库的名称以及所需的 <xref:Microsoft.SqlServer.Replication.ValidationOption>。  
  
5.  对订阅运行合并代理以开始验证，或者等待下一个计划的代理运行。 有关详细信息，请参阅 [Synchronize a Pull Subscription](synchronize-a-pull-subscription.md) 和 [Synchronize a Push Subscription](synchronize-a-push-subscription.md)。 验证操作的结果将写入代理的历史记录，您可以使用复制监视器查看。 有关详细信息，请参阅 [Monitoring Replication](monitoring-replication.md)。  
  
###  <a name="RMOExample"></a> 示例 (RMO)  
 此示例将对事务发布的所有订阅标记为行计数验证。  
  
 [!code-csharp[HowTo#rmo_ValidateTranPub](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_validatetranpub)]  
  
 [!code-vb[HowTo#rmo_vb_ValidateTranPub](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_validatetranpub)]  
  
 此示例将对合并发布的特定订阅标记为行计数验证。  
  
 [!code-csharp[HowTo#rmo_ValidateMergeSub](../../snippets/csharp/SQL15/replication/howto/cs/rmotestevelope.cs#rmo_validatemergesub)]  
  
 [!code-vb[HowTo#rmo_vb_ValidateMergeSub](../../snippets/visualbasic/SQL15/replication/howto/vb/rmotestenv.vb#rmo_vb_validatemergesub)]  
  
  
