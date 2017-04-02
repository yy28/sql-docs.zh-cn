---
title: "查看和修改项目属性 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "TSQL"
helpviewer_keywords: 
  - "sp_changearticle"
  - "sp_helparticle"
  - "查看复制属性"
  - "sp_changemergearticle"
  - "sp_helpmergearticle"
  - "修改复制属性, 项目"
  - "项目 [SQL Server 复制], 修改"
  - "项目 [SQL Server 复制], 属性"
ms.assetid: e71831fa-3d39-4e4a-9706-4d3a497082cc
caps.latest.revision: 37
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 37
---
# 查看和修改项目属性
  本主题说明如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]、[!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 或复制管理对象 (RMO) 在 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 中查看和修改项目属性。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [限制和局限](#Restrictions)  
  
     [建议](#Recommendations)  
  
-   **查看和修改项目属性，使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [复制管理对象 (RMO)](#RMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Restrictions"></a> 限制和局限  
  
-   创建复制后，有些属性便不可以再进行修改，如果该发布存在订阅，则其他属性也无法再进行修改。 不能进行修改的属性将显示为只读。  
  
###  <a name="Recommendations"></a> 建议  
  
-   创建发布之后，某些属性更改要求新的快照。 如果发布具有多个订阅，某些更改还会要求重新初始化所有订阅。 有关详细信息，请参阅 [更改发布和项目属性](../../../relational-databases/replication/publish/change-publication-and-article-properties.md) 和 [添加项目和删除现有发布的文章](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 查看和修改项目属性 **发布属性-\< 发布>** 对话框中，位于 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 和复制监视器。 有关启动复制监视器的信息，请参阅 [启动复制监视器](../../../relational-databases/replication/monitor/start-the-replication-monitor.md)。  
  
-   **“常规”** 页，包含发布名称和说明、数据库名称、发布类型以及订阅过期设置。  
  
-   **“项目”** 页，对应于新建发布向导中的 **“项目”** 页。 使用此页可添加和删除项目，以及更改项目的属性和列筛选。  
  
-   **“筛选行”** 页，对应于新建发布向导中的 **“筛选表行”** 页。 使用此页可添加、编辑和删除所有发布类型的静态行筛选器，以及添加、编辑和删除合并发布的参数化行筛选器和联接筛选器。  
  
-   **“快照”** 页，使您可以指定快照的格式和位置、快照是否压缩，以及应用快照前后要运行的脚本。  
  
-    **FTP 快照** （对于快照和事务发布和运行 SQL Server 2005 之前版本的发布服务器的合并发布） 的页面允许您指定的订阅服务器是否可以下载快照文件通过文件传输协议 (FTP)。  
  
-    **FTP 快照和 Internet** （用于从运行 SQL Server 2005 或更高版本的发布服务器的合并发布） 的页面允许您指定的订阅服务器是否能下载快照文件通过 FTP，以及是否订阅服务器才能同步通过 HTTPS 对订阅。  
  
-   **“订阅选项”** 页，使您可以设置多个应用于所有订阅的选项。 这些选项会随着发布类型而有所不同。  
  
-   **“发布访问列表”** 页，使您可以指定可以访问发布的登录名和组。  
  
-   **“代理安全性”** 页，使您可以访问用于运行下列代理并连接复制拓扑中计算机的帐户设置：所有发布的快照代理、所有事务发布的日志读取器代理以及允许排队更新订阅的事务发布的队列读取器代理。  
  
-    **数据分区** （用于从运行 SQL Server 2005 或更高版本的发布服务器的合并发布） 的页面允许您指定是否使用参数化筛选器的发布的订阅服务器可以请求快照，是否不可用。 它还允许一次性或按循环计划生成一个或多个分区的快照。  
  
#### 查看和修改项目属性  
  
1.  在 **文章** 页 **发布属性-\< 发布>** 对话框中，选择一篇文章，然后单击 **项目属性**。  
  
2.  选择要将更改应用于哪些项目属性：  
  
    -   单击 **设置属性的突出显示 \< ObjectType> 文章** 启动 **项目属性-\< 对象名>** 对话框; 属性在此对话框中所做的更改仅应用于突出显示在对象窗格中的对象 **文章** 页。  
  
    -   单击 **设置属性的所有 \< 对象类型> 文章**, ，以启动 **所有属性 \< ObjectType> 文章** 对话框; 属性在此对话框中所做的更改应用于该类型的对象窗格中的所有对象 **文章** 页上，包括尚未选择发布。  
  
        > [!NOTE]  
        >  属性中所做的更改 **所有属性 \< ObjectType> 文章** 对话框重写中的以前所做的任何 **项目属性-\< 对象名>** 对话框。 例如，若要为某对象类型的所有项目设置一些默认值，但还希望为单个对象设置一些属性，请首先设置所有项目的默认值。 然后再设置单个对象的属性。  
  
3.  根据需要修改属性，然后单击 **“确定”**。  
  
4.  单击 **确定** 上 **发布属性-\< 发布>** 对话框。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 可以使用复制存储过程以编程方式修改项目以及返回其属性。 使用的存储过程取决于项目所属的发布的类型。  
  
#### 查看属于快照发布或事务发布的项目的属性  
  
1.  执行 [sp_helparticle](../../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md), ，指定的发布名称 **@publication** 参数和项目的名称 **@article** 参数。 如果未指定 **@article**，将返回该发布中所有项目的信息。  
  
2.  执行 [sp_helparticlecolumns](../../../relational-databases/system-stored-procedures/sp-helparticlecolumns-transact-sql.md) 的表项目，可列出基表中可用的所有列。  
  
#### 修改属于快照发布或事务发布的项目的属性  
  
1.  执行 [sp_changearticle](../../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md), ，指定要更改在项目属性 **@property** 参数，并在此属性的新值 **@value** 参数。  
  
    > [!NOTE]  
    >  如果更改要求生成新快照，您还必须指定的值为 **1** 为 **@force_invalidate_snapshot**, ，如果更改要求重新初始化订阅服务器，您还必须指定的值和 **1** 为 **@force_reinit_subscription**。 有关详细信息属性，更改时需要新的快照或重新初始化，请参阅 [更改发布和项目属性](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)。  
  
#### 查看属于合并发布的项目的属性  
  
1.  执行 [sp_helpmergearticle](../../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md), ，指定的发布名称 **@publication** 参数和项目的名称 **@article** 参数。 如果未指定这些参数，将返回为发布或发布服务器中所有项目的信息。  
  
2.  执行 [sp_helpmergearticlecolumn](../../../relational-databases/system-stored-procedures/sp-helpmergearticlecolumn-transact-sql.md) 的表项目，可列出基表中可用的所有列。  
  
#### 修改属于合并发布的项目的属性  
  
1.  执行 [sp_changemergearticle](../../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md), ，指定要更改在项目属性 **@property** 参数，并在此属性的新值 **@value** 参数。  
  
    > [!NOTE]  
    >  如果更改要求生成新快照，您还必须指定的值为 **1** 为 **@force_invalidate_snapshot**, ，如果更改要求重新初始化订阅服务器，您还必须指定的值和 **1** 为 **@force_reinit_subscription**。 有关详细信息属性，更改时需要新的快照或重新初始化，请参阅 [更改发布和项目属性](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)。  
  
###  <a name="TsqlExample"></a> 示例 (Transact-SQL)  
 此事务复制示例返回了已发布项目的属性。  
  
 [!code-sql[HowTo#sp_helptranarticle](../../../relational-databases/replication/codesnippet/tsql/view-and-modify-article-_1.sql)]  
  
 此事务复制示例更改了已发布项目的架构选项。  
  
 [!code-sql[HowTo#sp_changetranarticle](../../../relational-databases/replication/codesnippet/tsql/view-and-modify-article-_2.sql)]  
  
 此合并复制示例返回了已发布项目的属性。  
  
 [!code-sql[HowTo#sp_helpmergearticle](../../../relational-databases/replication/codesnippet/tsql/view-and-modify-article-_3.sql)]  
  
 此合并复制示例更改了发布项目的冲突检测设置。  
  
 [!code-sql[HowTo#sp_changemergearticle](../../../relational-databases/replication/codesnippet/tsql/view-and-modify-article-_4.sql)]  
  
##  <a name="RMOProcedure"></a> 使用复制管理对象 (RMO)  
 可以使用复制管理对象 (RMO) 以编程方式修改项目以及访问其属性。 用于查看或修改项目属性的 RMO 类取决于项目所属的发布的类型。  
  
#### 查看或修改属于快照发布或事务发布的项目的属性  
  
1.  通过使用创建连接到发布服务器 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 类。  
  
2.  创建的实例 <xref:Microsoft.SqlServer.Replication.TransArticle> 类。  
  
3.  设置 <xref:Microsoft.SqlServer.Replication.Article.Name%2A>, ，<xref:Microsoft.SqlServer.Replication.Article.PublicationName%2A>, ，和 <xref:Microsoft.SqlServer.Replication.Article.DatabaseName%2A> 属性。  
  
4.  设置步骤 1 中的连接 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 属性。  
  
5.  调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法以获取该对象的属性。 如果此方法返回 **false**，则说明步骤 3 中的项目属性定义不正确或此项目不存在。  
  
6.  （可选）若要更改属性，设置新的值之一的 <xref:Microsoft.SqlServer.Replication.TransArticle> 可以设置的属性。  
  
7.  （可选）如果指定的值为 **true** 为 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>, ，调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 方法在服务器上提交更改。 如果指定的值为 **false** 为 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> （默认值），更改将立即发送到服务器。  
  
#### 查看或修改属于合并发布的项目的属性  
  
1.  通过使用创建连接到发布服务器 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 类。  
  
2.  创建的实例 <xref:Microsoft.SqlServer.Replication.MergeArticle> 类。  
  
3.  设置 <xref:Microsoft.SqlServer.Replication.Article.Name%2A>, ，<xref:Microsoft.SqlServer.Replication.Article.PublicationName%2A>, ，和 <xref:Microsoft.SqlServer.Replication.Article.DatabaseName%2A> 属性。  
  
4.  设置步骤 1 中的连接 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 属性。  
  
5.  调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法以获取该对象的属性。 如果此方法返回 **false**，则说明步骤 3 中的项目属性定义不正确或此项目不存在。  
  
6.  （可选）若要更改属性，设置新的值之一的 <xref:Microsoft.SqlServer.Replication.MergeArticle> 可以设置的属性。  
  
7.  （可选）如果指定的值为 **true** 为 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>, ，调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 方法在服务器上提交更改。 如果指定的值为 **false** 为 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> （默认值），更改将立即发送到服务器。  
  
###  <a name="PShellExample"></a> 示例 (RMO)  
 此示例更改一个合并项目来指定该项目所使用的业务逻辑处理程序。  
  
 [!code-csharp[HowTo#rmo_ChangeMergeArticle_BLH](../../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_changemergearticle_blh)]  
  
 [!code-vb[HowTo#rmo_vb_ChangeMergeArticle_BLH](../../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_changemergearticle_blh)]  
  
## 另请参阅  
 [实现合并项目的业务逻辑处理程序](../../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)   
 [发布数据和数据库对象](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [更改发布和项目属性](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [复制系统存储过程概念](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [高级合并复制冲突的检测和解决](../../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)  
  
  