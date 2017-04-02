---
title: "查看和修改发布属性 | Microsoft Docs"
ms.custom: ""
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "查看复制属性"
  - "修改复制属性, 项目"
  - "项目 [SQL Server 复制], 修改"
  - "发布 [SQL Server 复制], 属性"
  - "项目 [SQL Server 复制], 属性"
  - "修改复制属性, 发布"
  - "发布 [SQL Server 复制], 修改"
ms.assetid: 27d72ea4-bcb6-48f2-b4aa-eb1410da7efc
caps.latest.revision: 44
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 44
---
# 查看和修改发布属性
  本主题说明如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]、[!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 或复制管理对象 (RMO) 在 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 中查看和修改发布属性。  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [限制和局限](#Restrictions)  
  
     [建议](#Recommendations)  
  
-   **查看和修改发布属性，使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [复制管理对象 (RMO)](#RMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Restrictions"></a> 限制和局限  
  
-   创建复制后，有些属性便不可以再进行修改，如果该发布存在订阅，则其他属性也无法再进行修改。 不能进行修改的属性将显示为只读。  
  
###  <a name="Recommendations"></a> 建议  
  
-   创建发布之后，某些属性更改要求新的快照。 如果发布具有多个订阅，某些更改还会要求重新初始化所有订阅。 有关详细信息，请参阅 [更改发布和项目属性](../../../relational-databases/replication/publish/change-publication-and-article-properties.md) 和 [添加项目和删除现有发布的文章](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 查看和修改发布属性 **发布属性-\< 发布>** 对话框中，位于 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 和复制监视器。 有关启动复制监视器的信息，请参阅 [启动复制监视器](../../../relational-databases/replication/monitor/start-the-replication-monitor.md)。  
  
  **发布属性-\< 发布>** 对话框包含下列页︰  
  
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
  
#### 在 Management Studio 中查看和修改发布属性  
  
1.  在 [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)]中连接到发布服务器，然后展开服务器节点。  
  
2.  展开 **“复制”** 文件夹，再展开 **“本地发布”** 文件夹。  
  
3.  右键单击发布，然后单击 **属性**。  
  
4.  根据需要修改属性，然后单击 **“确定”**。  
  
#### 在复制监视器中查看和修改发布属性  
  
1.  在复制监视器的左侧窗格中展开发布服务器组，然后展开一个发布服务器。  
  
2.  右键单击发布，然后单击 **属性**。  
  
3.  根据需要修改属性，然后单击 **“确定”**。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 可以使用复制存储过程以编程方式修改发布以及返回其属性。 您使用的存储过程取决于发布的类型。  
  
#### 查看快照发布或事务发布的属性  
  
1.  执行 [sp_helppublication](../../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md), ，指定的发布名称 **@publication** 参数。 如果未指定此参数，则会返回发布服务器上所有发布的相关信息。  
  
#### 更改快照发布或事务发布的属性  
  
1.  执行 [sp_changepublication](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md), ，指定要在中更改的发布属性 **@property** 参数，并在此属性的新值 **@value** 参数。  
  
    > [!NOTE]  
    >  如果该更改将要求生成新快照，您还必须指定的值为 **1** 为 **@force_invalidate_snapshot**, ，而且，如果该更改将要求重新初始化订阅服务器，必须指定的值为 **1** 为 **@force_reinit_subscription**。 有关详细信息属性，更改时需要新的快照或重新初始化，请参阅 [更改发布和项目属性](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)。  
  
#### 查看合并发布的属性  
  
1.  执行 [sp_helpmergepublication](../../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md), ，指定的发布名称 **@publication** 参数。 如果未指定此参数，则会返回发布服务器上所有发布的相关信息。  
  
#### 更改合并发布的属性  
  
1.  执行 [sp_changemergepublication](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md), ，指定要更改中的发布属性 **@property** 参数，并在此属性的新值 **@value** 参数。  
  
    > [!NOTE]  
    >  如果该更改将要求生成新快照，您还必须指定的值为 **1** 为 **@force_invalidate_snapshot**, ，而且，如果该更改将要求重新初始化订阅服务器，必须指定的值为 **1** 为 **@force_reinit_subscription** 有关属性的详细信息，更改时需要新的快照或重新初始化，请参阅 [更改发布和项目属性](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)。  
  
#### 查看快照的属性  
  
1.  执行 [sp_helppublication_snapshot](../../../relational-databases/system-stored-procedures/sp-helppublication-snapshot-transact-sql.md), ，指定的发布名称 **@publication** 参数。  
  
#### 更改快照的属性  
  
1.  执行 [sp_changepublication_snapshot](../../../relational-databases/system-stored-procedures/sp-changepublication-snapshot-transact-sql.md), ，指定一个或多个相应的快照参数的新快照属性。  
  
###  <a name="TsqlExample"></a> 示例 (Transact-SQL)  
 此事务复制示例将返回该发布的属性。  
  
 [!code-sql[HowTo#sp_helppublication](../../../relational-databases/replication/codesnippet/tsql/view-and-modify-publicat_1.sql)]  
  
 此事务复制示例将为发布禁用架构复制。  
  
 [!code-sql[HowTo#sp_changepublication](../../../relational-databases/replication/codesnippet/tsql/view-and-modify-publicat_2.sql)]  
  
 此合并复制示例将返回该发布的属性。  
  
 [!code-sql[HowTo#sp_helpmergepublication](../../../relational-databases/replication/codesnippet/tsql/view-and-modify-publicat_3.sql)]  
  
 此合并复制示例将为发布禁用架构复制。  
  
 [!code-sql[HowTo#sp_changemergepublication](../../../relational-databases/replication/codesnippet/tsql/view-and-modify-publicat_4.sql)]  
  
##  <a name="RMOProcedure"></a> 使用复制管理对象 (RMO)  
 可以使用复制管理对象 (RMO) 以编程方式修改发布以及访问其属性。 查看或修改发布属性所使用的 RMO 类取决于发布的类型。  
  
#### 查看或修改快照发布或事务发布的属性  
  
1.  通过使用创建连接到发布服务器 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 类。  
  
2.  创建的实例 <xref:Microsoft.SqlServer.Replication.TransPublication> 类中，设置 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> 和 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> 属性的发布，并设置 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 属性设置为在步骤 1 中创建的连接。  
  
3.  调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法以获取该对象的属性。 如果此方法返回 **false**，则说明步骤 2 中的发布属性定义不正确，或者此发布不存在。  
  
4.  （可选）若要更改属性，为一个或多个可设置的属性设置新值。 使用逻辑 AND 运算符 (**&** 在 Microsoft Visual C# 和 **和** Microsoft Visual Basic 中) 以确定给定 <xref:Microsoft.SqlServer.Replication.PublicationAttributes> 值设置为 <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> 属性。 使用逻辑 OR 运算符 (**|** 在 Visual C# 和 **或者** 在 Visual Basic 中) 以及排除性逻辑 OR 运算符 (**^** 在 Visual C# 和 **异或** 在 Visual Basic 中) 更改 <xref:Microsoft.SqlServer.Replication.PublicationAttributes> 值 <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> 属性。  
  
5.  （可选）如果指定的值为 **true** 为 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>, ，调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 方法在服务器上提交更改。 如果指定的值为 **false** 为 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> （默认值），更改将立即发送到服务器。  
  
#### 查看或修改合并发布的属性  
  
1.  通过使用创建连接到发布服务器 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 类。  
  
2.  创建的实例 <xref:Microsoft.SqlServer.Replication.MergePublication> 类中，设置 <xref:Microsoft.SqlServer.Replication.Publication.Name%2A> 和 <xref:Microsoft.SqlServer.Replication.Publication.DatabaseName%2A> 属性的发布，并设置 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 属性设置为在步骤 1 中创建的连接。  
  
3.  调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法以获取该对象的属性。 如果此方法返回 **false**，则说明步骤 2 中的发布属性定义不正确，或者此发布不存在。  
  
4.  （可选）若要更改属性，为一个或多个可设置的属性设置新值。 使用逻辑 AND 运算符 (**&** 在 Visual C# 和 **和** 在 Visual Basic 中) 以确定给定 <xref:Microsoft.SqlServer.Replication.PublicationAttributes> 值设置为 <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> 属性。 使用逻辑 OR 运算符 (**|** 在 Visual C# 和 **或者** 在 Visual Basic 中) 以及排除性逻辑 OR 运算符 (**^** 在 Visual C# 和 **异或** 在 Visual Basic 中) 更改 <xref:Microsoft.SqlServer.Replication.PublicationAttributes> 值 <xref:Microsoft.SqlServer.Replication.Publication.Attributes%2A> 属性。  
  
5.  （可选）如果指定的值为 **true** 为 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A>, ，调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CommitPropertyChanges%2A> 方法在服务器上提交更改。 如果指定的值为 **false** 为 <xref:Microsoft.SqlServer.Replication.ReplicationObject.CachePropertyChanges%2A> （默认值），更改将立即发送到服务器。  
  
###  <a name="PShellExample"></a> 示例 (RMO)  
 该示例设置事务发布的发布属性。 这些更改将被缓存，直至将其显式发送到服务器。  
  
 [!code-csharp[HowTo#rmo_ChangeTranPub_cached](../../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_changetranpub_cached)]  
  
 [!code-vb[HowTo#rmo_vb_ChangeTranPub_cached](../../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_changetranpub_cached)]  
  
 该示例禁用合并发布的 DDL 复制。  
  
 [!code-csharp[HowTo#rmo_ChangeMergePub_ddl](../../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_changemergepub_ddl)]  
  
 [!code-vb[HowTo#rmo_vb_ChangeMergePub_ddl](../../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_changemergepub_ddl)]  
  
## 另请参阅  
 [发布数据和数据库对象](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [更改发布和项目属性](../../../relational-databases/replication/publish/change-publication-and-article-properties.md)   
 [对发布数据库进行架构更改](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)   
 [复制系统存储过程概念](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [从发布 & #40; 添加项目和删除项目SQL Server Management Studio & #41;](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-a-publication.md)   
 [查看信息并执行任务发布 & #40;复制监视器 & #41;](../../../relational-databases/replication/monitor/view-information-and-perform-tasks-for-a-publication-replication-monitor.md)   
 [查看和修改项目属性](../../../relational-databases/replication/publish/view-and-modify-article-properties.md)  
  
  