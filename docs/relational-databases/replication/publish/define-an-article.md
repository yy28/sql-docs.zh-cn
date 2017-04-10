---
title: "定义项目 | Microsoft Docs"
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
  - "项目 [SQL Server 复制], 定义"
  - "sp_addmergearticle"
  - "添加项目"
  - "sp_addarticle"
  - "项目 [SQL Server 复制], 添加"
ms.assetid: 220584d8-b291-43ae-b036-fbba3cc07a2e
caps.latest.revision: 45
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 45
---
# 定义项目
  本主题说明如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]、[!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 或复制管理对象 (RMO) 在 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 中定义项目。   
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [限制和局限](#Restrictions)  
  
     [安全性](#Security)  
  
-   **定义项目，使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [复制管理对象 (RMO)](#RMOProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Restrictions"></a> 限制和局限  
  
-   项目名称不能包含以下任何字符：%、*、[、]、|、:、"、? , ' , \ , / , \< , >. 如果数据库中的对象包括任意上述字符，并且您希望复制它们，那么必须指定一个不同于相应对象名称的项目名称。  
  
##  <a name="Security"></a> 安全性  
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
 在创建发布后，可以使用复制存储过程以编程方式创建项目。 用于创建项目的存储过程取决于要为其定义项目的发布的类型。 有关详细信息，请参阅 [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)。  
  
#### 为快照发布或事务发布定义项目  
  
1.  在发布服务器上对发布数据库中，执行 [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)。 指定项目所属的发布名称 **@publication**, ，项目的名称，为 **@article**, 要发布的数据库对象 **@source_object**, ，以及任何其他可选参数。 使用 **@source_owner** 如果不指定该对象的架构所有权 **dbo**。 如果该项目不是基于日志的表项目，指定该项目类型 **@type**; 有关详细信息，请参阅 [指定项目类型和 #40;复制 TRANSACT-SQL 编程 & #41;](../../../relational-databases/replication/publish/specify-article-types-replication-transact-sql-programming.md)。  
  
2.  若要水平筛选表中的行或查看项目，请使用 [sp_articlefilter](../../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md) 来定义筛选器子句。 有关详细信息，请参阅 [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md)。  
  
3.  若要垂直筛选表中的列，或查看项目，请使用 [sp_articlecolumn](../../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)。 有关详细信息，请参阅 [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md)。  
  
4.  执行 [sp_articleview](../../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md) 如果对项目进行筛选。  
  
5.  如果发布拥有现有订阅和 [sp_helppublication](../../../relational-databases/system-stored-procedures/sp-helppublication-transact-sql.md) 返回的值为 **0** 中 **immediate_sync** 列中，您必须调用 [sp_addsubscription](../../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md) 将项目添加到每个现有订阅。  
  
6.  如果发布具有现有请求订阅，则执行 [sp_refreshsubscriptions](../../../relational-databases/system-stored-procedures/sp-refreshsubscriptions-transact-sql.md) 在发布服务器上创建新的快照为现有请求订阅，其中包含新的项目。  
  
    > [!NOTE]  
    >  对于不使用快照初始化订阅，您不需要执行 [sp_refreshsubscriptions](../../../relational-databases/system-stored-procedures/sp-refreshsubscriptions-transact-sql.md) 通过执行此过程如 [sp_addarticle](../../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)。  
  
#### 为合并发布定义项目  
  
1.  在发布服务器上对发布数据库中，执行 [sp_addmergearticle](../../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)。 指定的发布名称 **@publication**, ，项目的名称的名称 **@article**, ，以及要发布的对象 **@source_object**。 若要水平筛选表行，为指定值 **@subset_filterclause**。 有关详细信息，请参阅 [Define and Modify a Parameterized Row Filter for a Merge Article](../../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md) 和 [Define and Modify a Static Row Filter](../../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md)。 如果相应项目不是表项目，请将 **@type**指定为该项目类型。 有关详细信息，请参阅 [指定项目类型和 #40;复制 TRANSACT-SQL 编程 & #41;](../../../relational-databases/replication/publish/specify-article-types-replication-transact-sql-programming.md)。  
  
2.  （可选）在发布服务器上对发布数据库中，执行 [sp_addmergefilter](../../../relational-databases/system-stored-procedures/sp-addmergefilter-transact-sql.md) 来定义两个项目之间的联接筛选器。 有关详细信息，请参阅 [Define and Modify a Join Filter Between Merge Articles](../../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)。  
  
3.  （可选）在发布服务器上对发布数据库中，执行 [sp_mergearticlecolumn](../../../relational-databases/system-stored-procedures/sp-mergearticlecolumn-transact-sql.md) 到筛选器表的列。 有关详细信息，请参阅 [Define and Modify a Column Filter](../../../relational-databases/replication/publish/define-and-modify-a-column-filter.md)。  
  
###  <a name="TsqlExample"></a> 示例 (Transact-SQL)  
 本例为某个事务发布定义了一个基于 `Product` 表的项目，其中项目在水平和垂直两个方向上进行了筛选。  
  
 [!code-sql[HowTo#sp_AddTranArticle](../../../relational-databases/replication/codesnippet/tsql/define-an-article_1.sql)]  
  
 本例为某个合并发布定义项目，其中 `SalesOrderHeader` 项目基于 **SalesPersonID**进行静态筛选，而 `SalesOrderDetail` 项目则基于 `SalesOrderHeader`进行联接筛选。  
  
 [!code-sql[HowTo#sp_AddMergeArticle](../../../relational-databases/replication/codesnippet/tsql/define-an-article_2.sql)]  
  
##  <a name="RMOProcedure"></a> 使用复制管理对象 (RMO)  
 可以使用复制管理对象 (RMO) 以编程方式定义项目。 用来定义项目的 RMO 类取决于要为其定义项目的发布的类型。  
  
###  <a name="PShellExample"></a> 示例 (RMO)  
 下例向一个事务发布添加一个带有行和列筛选器的项目。  
  
 [!code-csharp[HowTo#rmo_CreateTranArticles](../../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_createtranarticles)]  
  
 [!code-vb[HowTo#rmo_vb_CreateTranArticles](../../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_createtranarticles)]  
  
 下例将三个项目添加到一个合并发布。 这些项目具有列筛选器，而且使用两个联接筛选器来将一个参数化行筛选器传播给其他项目。  
  
 [!code-csharp[HowTo#rmo_CreateMergeArticles](../../../relational-databases/replication/codesnippet/csharp/rmohowto/rmotestevelope.cs#rmo_createmergearticles)]  
  
 [!code-vb[HowTo#rmo_vb_CreateMergeArticles](../../../relational-databases/replication/codesnippet/visualbasic/rmohowtovb/rmotestenv.vb#rmo_vb_createmergearticles)]  
  
## 另请参阅  
 [创建发布](../../../relational-databases/replication/publish/create-a-publication.md)   
 [复制系统存储过程概念](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)   
 [向现有发布添加项目和从中删除项目](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)   
 [筛选已发布数据](../../../relational-databases/replication/publish/filter-published-data.md)   
 [发布数据和数据库对象](../../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [复制系统存储过程概念](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)  
  
  