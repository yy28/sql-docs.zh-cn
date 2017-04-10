---
title: "实现合并项目的业务逻辑处理程序 | Microsoft Docs"
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
  - "合并复制冲突解决 [SQL Server 复制], 业务逻辑处理程序"
  - "合并复制业务逻辑处理程序 [SQL Server 复制]"
  - "冲突解决 [SQL Server 复制], 合并复制"
  - "业务逻辑处理程序 [SQL Server 复制]"
  - "BusinessLogicModule 类"
ms.assetid: ed477595-6d46-4fa2-b0d3-a5358903ec05
caps.latest.revision: 44
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 44
---
# 实现合并项目的业务逻辑处理程序
  本主题说明如何使用复制编程方式或复制管理对象 (RMO) 在 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 中实现合并项目的业务逻辑处理程序。  
  
  <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport> 命名空间实现了一个接口，使您能够编写复杂的业务逻辑以处理在合并复制同步过程中发生的事件。 复制进程可以针对同步期间复制的每个已更改行调用业务逻辑处理程序中的方法。  
  
 实现业务逻辑处理程序的一般过程是：  
  
1.  创建业务逻辑处理程序程序集。  
  
2.  在分发服务器上注册程序集。  
  
3.  在运行合并代理的服务器上部署程序集。 对于请求订阅，代理在订阅服务器上运行，而对于推送订阅，代理在分发服务器上运行。 使用 Web 同步时，代理在 Web 服务器上运行。  
  
4.  创建使用业务逻辑处理程序的项目，或修改现有项目以使用业务逻辑处理程序。  
  
 指定的业务逻辑处理程序是针对每个同步的行来执行的， 因此复杂的逻辑以及对其他应用程序或网络服务的调用都可能会影响性能。 有关业务逻辑处理程序的详细信息，请参阅 [执行合并同步期间业务逻辑](../../relational-databases/replication/merge/execute-business-logic-during-merge-synchronization.md)。  
  
 **本主题内容**  
  
-   **实现合并项目的业务逻辑处理程序，使用：**  
  
     [复制编程方式](#ReplProg)  
  
     [复制管理对象 (RMO)](#RMOProcedure)  
  
##  <a name="ReplProg"></a> 使用复制编程  
  
#### 创建和部署业务逻辑处理程序  
  
1.  在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Studio 中，为包含可实现业务逻辑处理程序的代码的 .NET 程序集创建一个新项目。  
  
2.  将对以下列命名空间的引用添加到该项目。  
  
    |程序集引用|位置|  
    |------------------------|--------------|  
    |<xref:Microsoft.SqlServer.Replication.BusinessLogicSupport>|[!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)]COM （默认安装）|  
    |<xref:System.Data>|GAC（.NET Framework 的组件）|  
    |<xref:System.Data.Common>|GAC（.NET Framework 的组件）|  
  
3.  添加类，并重写 <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> 类。  
  
4.  实现 <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.HandledChangeStates%2A> 属性来指示更改处理的类型。  
  
5.  重写一个或多个下列方法之一 <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> 类︰  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.CommitHandler%2A> -在同步期间提交数据更改时调用。  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.DeleteErrorHandler%2A> -在上载或下载时调用在 DELETE 语句时，将发生错误时。  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.DeleteHandler%2A> -DELETE 语句时调用上载或下载。  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.InsertErrorHandler%2A> -在上载或下载时调用 INSERT 语句出错时。  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.InsertHandler%2A> 的 INSERT 语句时调用上载或下载。  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.UpdateConflictsHandler%2A> -当发布服务器和订阅服务器上出现冲突的 UPDATE 语句时调用。  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.UpdateDeleteConflictHandler%2A> 的 UPDATE 语句与发布服务器和订阅服务器上的 DELETE 语句冲突时调用。  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.UpdateErrorHandler%2A> -在上载或下载时调用 UPDATE 语句出错时。  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.UpdateHandler%2A> 的 UPDATE 语句时调用上载或下载。  
  
6.  生成该项目以创建业务逻辑处理程序程序集。  
  
7.  在包含合并代理可执行文件 (replmerg.exe) 的目录中部署该程序集，对默认安装来说，该目录为 [!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)]COM，或将该程序集安装在 .NET 全局程序集缓存 (GAC) 中。 如果合并代理之外的应用程序需要访问该程序集，您只能将该程序集安装在 GAC 中。 程序集可安装到 gac 中使用全局程序集缓存工具 (**Gacutil.exe)** .NET Framework SDK 中提供。  
  
    > [!NOTE]  
    >  必须在每个运行合并代理的服务器上部署业务逻辑处理程序，包括使用 Web 同步时 replisapi.dll 所驻留的 IIS 服务器。  
  
#### 注册业务逻辑处理程序  
  
1.  在发布服务器上，执行 [sp_enumcustomresolvers & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-enumcustomresolvers-transact-sql.md) 若要验证，该程序集没有已注册为业务逻辑处理程序。  
  
2.  在分发服务器上，执行 [sp_registercustomresolver & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-registercustomresolver-transact-sql.md), ，指定业务逻辑处理程序的友好名称 **@article_resolver**, ，值为 **true** 为 **@is_dotnet_assembly**, ，为程序集的名称 **@dotnet_assembly_name**, ，和类，并重写的完全限定名称 <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> 为 **@dotnet_class_name**。  
  
    > [!NOTE]  
    >  如果该程序集未部署与合并代理可执行文件的相同目录中，与应用程序的相同目录中，同步启动合并代理程序，或者在全局程序集缓存 (GAC) 中，您需要的程序集名称与指定的完整路径 **@dotnet_assembly_name**。 使用 Web 同步时，必须指定程序集在 Web 服务器中的位置。  
  
#### 将业务逻辑处理程序与新的表项目一起使用  
  
1.  执行 [sp_addmergearticle & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md) 若要定义一个项目，指定业务逻辑处理程序的友好名称 **@article_resolver**。 有关详细信息，请参阅 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)。  
  
#### 将业务逻辑处理程序用于现有的表项目  
  
1.  执行 [sp_changemergearticle & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md), ，并指定 **@publication**, ，**@article**, ，值为 **article_resolver** 为 **@property**, ，和业务逻辑处理程序的友好名称 **@value**。  
  
###  <a name="TsqlExample"></a> 示例（复制编程方式）  
 该示例演示了可创建审核日志的业务逻辑处理程序。  
  
 [!code-csharp[HowTo#rmo_BusinessLogicCode](../../relational-databases/replication/codesnippet/csharp/rmohowto/businesslogic.cs#rmo_businesslogiccode)]  
  
 [!code-vb[HowTo#rmo_vb_BusinessLogicCode](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/businesslogic.vb#rmo_vb_businesslogiccode)]  
  
 以下示例在分发服务器中注册了业务逻辑处理程序程序集，并更改了一个现有合并项目以使用此自定义业务逻辑。  
  
 [!code-sql[HowTo#sp_RegisterBLH_10](../../relational-databases/replication/codesnippet/tsql/implement-a-business-log_3.sql)]  
  
##  <a name="RMOProcedure"></a> 使用复制管理对象 (RMO)  
  
#### 创建业务逻辑处理程序  
  
1.  在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Studio 中，为包含可实现业务逻辑处理程序的代码的 .NET 程序集创建一个新项目。  
  
2.  将对以下列命名空间的引用添加到该项目。  
  
    |程序集引用|位置|  
    |------------------------|--------------|  
    |<xref:Microsoft.SqlServer.Replication.BusinessLogicSupport>|[!INCLUDE[ssInstallPath](../../includes/ssinstallpath-md.md)]COM （默认安装）|  
    |<xref:System.Data>|GAC（.NET Framework 的组件）|  
    |<xref:System.Data.Common>|GAC（.NET Framework 的组件）|  
  
3.  添加类，并重写 <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> 类。  
  
4.  实现 <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.HandledChangeStates%2A> 属性来指示更改处理的类型。  
  
5.  重写一个或多个下列方法之一 <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> 类︰  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.CommitHandler%2A> -在同步期间提交数据更改时调用。  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.DeleteErrorHandler%2A> -如果 DELETE 语句时，就会出错调用上载或下载。  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.DeleteHandler%2A> -DELETE 语句时调用上载或下载。  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.InsertErrorHandler%2A> -在上载或下载时调用的 INSERT 语句时出错。  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.InsertHandler%2A> 的 INSERT 语句时调用上载或下载。  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.UpdateConflictsHandler%2A> -当发布服务器和订阅服务器上出现冲突的 UPDATE 语句时调用。  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.UpdateDeleteConflictHandler%2A> 的 UPDATE 语句与发布服务器和订阅服务器上的 DELETE 语句冲突时调用。  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.UpdateErrorHandler%2A> -在上载或下载时调用 UPDATE 语句时出错。  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule.UpdateHandler%2A> 的 UPDATE 语句时调用上载或下载。  
  
    > [!NOTE]  
    >  自定义业务逻辑未显式处理的任何项目冲突都由项目的默认冲突解决程序进行处理。  
  
6.  生成该项目以创建业务逻辑处理程序程序集。  
  
#### 注册业务逻辑处理程序  
  
1.  通过使用创建连接到分发服务器 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 类。  
  
2.  创建的实例 <xref:Microsoft.SqlServer.Replication.ReplicationServer> 类。 传递 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 步骤 1 中。  
  
3.  调用 <xref:Microsoft.SqlServer.Replication.ReplicationServer.EnumBusinessLogicHandlers%2A> 并检查返回 <xref:System.Collections.ArrayList> 对象，以确保该程序集不已注册为业务逻辑处理程序。  
  
4.  创建的实例 <xref:Microsoft.SqlServer.Replication.BusinessLogicHandler> 类。 指定以下属性：  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicHandler.DotNetAssemblyName%2A> -.NET 程序集的名称。 如果该程序集未部署到与合并代理可执行文件相同的目录中、与同步启动合并代理的应用程序相同的目录中或 GAC 中，则必须随程序集名称提供完整的路径。 将业务逻辑处理程序与 Web 同步一起使用时，必须随程序集名称提供完整的路径。  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicHandler.DotNetClassName%2A> 的类，并重写的完全限定名称 <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> 并实现业务逻辑处理程序。  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicHandler.FriendlyName%2A> -访问业务逻辑处理程序时，你使用的友好名称。  
  
    -   <xref:Microsoft.SqlServer.Replication.BusinessLogicHandler.IsDotNetAssembly%2A> -值为 **true**。  
  
#### 部署业务逻辑处理程序  
  
1.  将程序集部署到运行合并代理的服务器上，具体部署位置为在分发服务器上注册业务逻辑处理程序时所指定的文件位置。 对于请求订阅，代理在订阅服务器上运行，而对于推送订阅，代理在分发服务器上运行。 使用 Web 同步时，代理在 Web 服务器上运行。 如果注册业务逻辑处理程序时未对程序集名称提供完整的路径，则将程序集部署到与合并代理可执行文件相同的目录中、与同步启动合并代理的应用程序相同的目录中。 如果有多个应用程序使用相同的程序集，则可以将程序集安装在 GAC 中。  
  
#### 将业务逻辑处理程序与新的表项目一起使用  
  
1.  通过使用创建连接到发布服务器 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 类。  
  
2.  创建的实例 <xref:Microsoft.SqlServer.Replication.MergeArticle> 类。 设置以下属性：  
  
    -   项目的名称 <xref:Microsoft.SqlServer.Replication.Article.Name%2A>。  
  
    -   有关发布的名称 <xref:Microsoft.SqlServer.Replication.Article.PublicationName%2A>。  
  
    -   为发布数据库的名称 <xref:Microsoft.SqlServer.Replication.Article.DatabaseName%2A>。  
  
    -   业务逻辑处理程序的友好名称 (<xref:Microsoft.SqlServer.Replication.BusinessLogicHandler.FriendlyName%2A>) 为 <xref:Microsoft.SqlServer.Replication.MergeArticle.ArticleResolver%2A>。  
  
3.  调用 <xref:Microsoft.SqlServer.Replication.Article.Create%2A> 方法。 有关详细信息，请参阅 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)。  
  
#### 将业务逻辑处理程序用于现有的表项目  
  
1.  通过使用创建连接到发布服务器 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 类。  
  
2.  创建的实例 <xref:Microsoft.SqlServer.Replication.MergeArticle> 类。  
  
3.  设置 <xref:Microsoft.SqlServer.Replication.Article.Name%2A>, ，<xref:Microsoft.SqlServer.Replication.Article.PublicationName%2A>, ，和 <xref:Microsoft.SqlServer.Replication.Article.DatabaseName%2A> 属性。  
  
4.  设置步骤 1 中的连接 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 属性。  
  
5.  调用 <xref:Microsoft.SqlServer.Replication.ReplicationObject.LoadProperties%2A> 方法以获取该对象的属性。 如果此方法返回 **false**，则说明步骤 3 中的项目属性定义不正确或此项目不存在。 有关详细信息，请参阅 [View and Modify Article Properties](../../relational-databases/replication/publish/view-and-modify-article-properties.md)。  
  
6.  设置业务逻辑处理程序的友好名称 <xref:Microsoft.SqlServer.Replication.MergeArticle.ArticleResolver%2A>。 这是值 <xref:Microsoft.SqlServer.Replication.BusinessLogicHandler.FriendlyName%2A> 注册业务逻辑处理程序时所指定属性。  
  
###  <a name="PShellExample"></a> 示例 (RMO)  
 此示例是一个业务逻辑处理程序，它记录有关订阅服务器上的插入、更新和删除操作的信息。  
  
 [!code-csharp[HowTo#rmo_BusinessLogicCode](../../relational-databases/replication/codesnippet/csharp/rmohowto/businesslogic.cs#rmo_businesslogiccode)]  
  
 [!code-vb[HowTo#rmo_vb_BusinessLogicCode](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/businesslogic.vb#rmo_vb_businesslogiccode)]  
  
 此示例在分发服务器上注册业务逻辑处理程序。  
  
 [!code-csharp[HowTo#rmo_RegisterBLH_10](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_registerblh_10)]  
  
 [!code-vb[HowTo#rmo_vb_RegisterBLH_10](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_registerblh_10)]  
  
 此示例更改现有项目以使用业务逻辑处理程序。  
  
 [!code-csharp[HowTo#rmo_ChangeMergeArticle_BLH](../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_changemergearticle_blh)]  
  
 [!code-vb[HowTo#rmo_vb_ChangeMergeArticle_BLH](../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_changemergearticle_blh)]  
  
## 另请参阅  
 [为合并项目实现自定义冲突解决程序](../../relational-databases/replication/implement-a-custom-conflict-resolver-for-a-merge-article.md)   
 [调试业务逻辑处理程序 & #40;复制编程 & #41;](../../relational-databases/replication/debug-a-business-logic-handler-replication-programming.md)   
 [复制安全最佳实践](../../relational-databases/replication/security/replication-security-best-practices.md)   
 [复制管理对象概念](../../relational-databases/replication/concepts/replication-management-objects-concepts.md)  
  
  