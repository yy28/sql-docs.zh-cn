---
title: "设置合并发布的兼容级别 | Microsoft Docs"
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
  - "兼容性 [SQL Server], 复制"
  - "向后兼容性 [SQL Server], 复制"
  - "发布 [SQL Server 复制], 向后兼容性"
ms.assetid: db47ac73-948b-4d77-b272-bb3565135ea5
caps.latest.revision: 33
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 33
---
# 设置合并发布的兼容级别
  本主题说明如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中设置合并发布的兼容级别。 合并复制使用发布兼容级别来确定给定数据库中的发布可以使用哪些功能。  
  
 **本主题内容**  
  
-   **设置合并发布的兼容级别，使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 在新建发布向导的 **“订阅服务器类型”** 页上设置兼容级别。 有关访问此向导的详细信息，请参阅 [创建发布](../../../relational-databases/replication/publish/create-a-publication.md)。 创建了发布快照后，可以提高兼容级别但不能降低兼容级别。 将兼容级别增加上 **常规** 页 **发布属性-\< 发布>** 对话框。 有关访问此对话框的详细信息，请参阅 [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)。 如果要提高发布兼容级别，则运行该兼容级别的早期版本的服务器上的所有现有订阅都将不能同步。  
  
> [!NOTE]  
>  由于兼容级别具有其他发布属性的含义，并且项目属性对这些含义有效。因此，请不要使用同一个对话框更改兼容级别和其他属性。 应该在更改属性后重新生成发布的快照。  
  
#### 设置发布兼容级别  
  
-   在新建发布向导的 **“订阅服务器类型”** 页上，选择发布应支持的订阅服务器类型。  
  
#### 提高发布兼容级别  
  
-   在 **常规** 页 **发布属性-\< 发布>** 对话框中，选择为 **兼容性级别**。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 可以在创建发布时以编程方式设置合并发布的兼容级别，或者以后以编程方式进行修改。 可使用复制存储过程来设置或更改此发布属性。  
  
#### 设置合并发布的发布兼容级别  
  
1.  在发布服务器上，执行 [sp_addmergepublication & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md), ，为指定值 **@publication_compatibility_level** 以使该发布的早期版本兼容 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。 有关详细信息，请参阅 [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)。  
  
#### 更改合并发布的发布兼容级别  
  
1.  执行 [sp_changemergepublication & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md), ，并指定 **publication_compatibility_level** 为 **@property** 和相应的发布兼容级别为 **@value**。  
  
#### 确定合并发布的发布兼容级别  
  
1.  执行 [sp_helpmergepublication & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-helpmergepublication-transact-sql.md), ，指定所需的发布。  
  
2.  找到发布兼容级别中的 **backward_comp_level** 结果集中的列。  
  
###  <a name="TsqlExample"></a> 示例 (Transact-SQL)  
 该示例创建合并发布并设置发布兼容级别。  
  
```  
-- To avoid storing the login and password in the script file, the values   
-- are passed into SQLCMD as scripting variables. For information about   
-- how to use scripting variables on the command line and in SQL Server  
-- Management Studio, see the "Executing Replication Scripts" section in  
-- the topic "Programming Replication Using System Stored Procedures".  
  
--Add a new merge publication.  
DECLARE @publicationDB AS sysname;  
DECLARE @publication AS sysname;  
DECLARE @login AS sysname;  
DECLARE @password AS sysname;  
SET @publicationDB = N'AdventureWorks2012';   
SET @publication = N'AdvWorksSalesOrdersMerge'   
SET @login = $(Login);  
SET @password = $(Password);  
  
-- Create a new merge publication.   
USE [AdventureWorks2012]  
EXEC sp_addmergepublication   
@publication = @publication,   
-- Set the compatibility level to SQL Server 2014.  
@publication_compatibility_level = '120RTM';   
  
-- Create the snapshot job for the publication.  
EXEC sp_addpublication_snapshot   
@publication = @publication,  
@job_login = @login,  
@job_password = @password;  
GO  
```  
  
 该示例更改合并发布的发布兼容级别。  
  
> [!NOTE]  
>  如果发布使用任何要求采用特定兼容级别的功能，则可能不允许更改发布兼容级别。 有关详细信息，请参阅 [复制向后兼容性](../../../relational-databases/replication/replication-backward-compatibility.md)。  
  
```  
DECLARE @publication AS sysname;  
SET @publication = N'AdvWorksSalesOrdersMerge' ;  
  
-- Change the publication compatibility level to   
-- SQL Server 2012.  
EXEC sp_changemergepublication   
@publication = @publication,   
@property = N'publication_compatibility_level',   
@value = N'110RTM';  
GO  
  
```  
  
 该示例返回合并发布的当前发布兼容级别。  
  
```  
DECLARE @publication AS sysname;  
SET @publication = N'AdvWorksSalesOrdersMerge' ;  
EXEC sp_helpmergepublication   
@publication = @publication;  
GO  
  
```  
  
## 另请参阅  
 [创建发布](../../../relational-databases/replication/publish/create-a-publication.md)  
  
  