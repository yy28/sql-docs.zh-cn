---
title: "删除项目 | Microsoft Docs"
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
  - "项目 [SQL Server 复制], 删除"
  - "sp_droparticle"
  - "sp_dropmergearticle"
  - "删除项目"
  - "删除项目"
  - "删除项目"
ms.assetid: 185b58fc-38c0-4abe-822e-6ec20066c863
caps.latest.revision: 41
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 41
---
# 删除项目
  本主题说明如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或复制管理对象 (RMO) 在 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 中删除项目。  可以删除的项目，以及是否删除项目需要新的快照或重新初始化订阅的条件有关的信息，请参阅 [添加项目和删除现有发布的文章](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)。  
  
 **本主题内容**  
  
-   **删除项目，使用：**  
  
     [Transact-SQL](#TsqlProcedure)  
  
     [复制管理对象 (RMO)](#RMOProcedure)  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 可以使用复制存储过程以编程方式删除项目。 使用的存储过程取决于项目所属的发布的类型。  
  
#### 从快照或事务发布中删除项目  
  
1.  执行 [sp_droparticle & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md) 若要删除的项目，由指定 **@article**, ，从指定的发布 **@publication**。 将值指定为 **1** 为 **@force_invalidate_snapshot**。  
  
2.  （可选）若要从数据库完全删除已发布的对象，请在发布服务器上对发布数据库执行 `DROP <objectname>` 命令。  
  
#### 从合并发布删除项目  
  
1.  执行 [sp_dropmergearticle & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-dropmergearticle-transact-sql.md) 若要删除的项目，由指定 **@article**, ，从指定的发布 **@publication**。 如有必要，将值指定为 **1** 为 **@force_invalidate_snapshot** ，值为 **1** 为 **@force_reinit_subscription**。  
  
2.  （可选）若要从数据库完全删除已发布的对象，请在发布服务器上对发布数据库执行 `DROP <objectname>` 命令。  
  
###  <a name="TsqlExample"></a> 示例 (Transact-SQL)  
 下面的示例将从事务发布中删除项目。 由于此更改使现有快照，值为失效 **1** 为指定 **@force_invalidate_snapshot** 参数。  
  
```  
DECLARE @publication AS sysname;  
DECLARE @article AS sysname;  
SET @publication = N'AdvWorksProductTran';   
SET @article = N'Product';   
  
-- Drop the transactional article.  
USE [AdventureWorks]  
EXEC sp_droparticle   
  @publication = @publication,   
  @article = @article,  
  @force_invalidate_snapshot = 1;  
GO  
```  
  
 下面的示例将从合并发布中删除两个项目。 因为这些更改会使现有快照的值无效 **1** 为指定 **@force_invalidate_snapshot** 参数。  
  
```  
DECLARE @publication AS sysname;  
DECLARE @article1 AS sysname;  
DECLARE @article2 AS sysname;  
SET @publication = N'AdvWorksSalesOrdersMerge';  
SET @article1 = N'SalesOrderDetail';   
SET @article2 = N'SalesOrderHeader';   
  
-- Remove articles from a merge publication.  
USE [AdventureWorks]  
EXEC sp_dropmergearticle   
  @publication = @publication,   
  @article = @article1,  
  @force_invalidate_snapshot = 1;  
EXEC sp_dropmergearticle   
  @publication = @publication,   
  @article = @article2,  
  @force_invalidate_snapshot = 1;  
GO  
```  
  
##  <a name="RMOProcedure"></a> 使用复制管理对象 (RMO)  
 可以使用复制管理对象 (RMO) 以编程方式删除项目。 用于删除项目的 RMO 类取决于该项目所属的发布的类型。  
  
#### 删除属于快照发布或事务发布的项目  
  
1.  通过使用创建连接到发布服务器 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 类。  
  
2.  创建的实例 <xref:Microsoft.SqlServer.Replication.TransArticle> 类。  
  
3.  设置 <xref:Microsoft.SqlServer.Replication.Article.Name%2A>, ，<xref:Microsoft.SqlServer.Replication.Article.PublicationName%2A>, ，和 <xref:Microsoft.SqlServer.Replication.Article.DatabaseName%2A> 属性。  
  
4.  设置步骤 1 中的连接 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 属性。  
  
5.  检查 <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> 属性来验证项目是否存在。 如果此属性的值为 **false**，则步骤 3 中的项目属性定义不正确或此项目不存在。  
  
6.  调用 <xref:Microsoft.SqlServer.Replication.Article.Remove%2A> 方法。  
  
7.  关闭所有连接。  
  
#### 删除属于合并发布的项目  
  
1.  通过使用创建连接到发布服务器 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 类。  
  
2.  创建的实例 <xref:Microsoft.SqlServer.Replication.MergeArticle> 类。  
  
3.  设置 <xref:Microsoft.SqlServer.Replication.Article.Name%2A>, ，<xref:Microsoft.SqlServer.Replication.Article.PublicationName%2A>, ，和 <xref:Microsoft.SqlServer.Replication.Article.DatabaseName%2A> 属性。  
  
4.  设置步骤 1 中的连接 <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> 属性。  
  
5.  检查 <xref:Microsoft.SqlServer.Replication.ReplicationObject.IsExistingObject%2A> 属性来验证项目是否存在。 如果此属性的值为 **false**，则步骤 3 中的项目属性定义不正确或此项目不存在。  
  
6.  调用 <xref:Microsoft.SqlServer.Replication.Article.Remove%2A> 方法。  
  
7.  关闭所有连接。  
  
## 另请参阅  
 [向现有发布添加项目和从中删除项目](../../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)   
 [复制系统存储过程概念](../../../relational-databases/replication/concepts/replication-system-stored-procedures-concepts.md)  
  
  