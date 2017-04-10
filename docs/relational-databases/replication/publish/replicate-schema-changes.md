---
title: "复制架构更改 | Microsoft Docs"
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
  - "复制 [SQL Server], 架构更改"
  - "架构 [SQL Server 复制], 复制更改"
ms.assetid: c09007f0-9374-4f60-956b-8a87670cd043
caps.latest.revision: 43
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 43
---
# 复制架构更改
  本主题说明如何使用 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] 或 [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] 在 [!INCLUDE[tsql](../../../includes/tsql-md.md)]中复制架构更改。  
  
 如果对发布的项目进行以下架构更改，则会默认将其传播到 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 订阅服务器：  
  
-   ALTER TABLE  
  
-   ALTER VIEW  
  
-   ALTER PROCEDURE  
  
-   ALTER FUNCTION  
  
-   ALTER TRIGGER  
  
 **本主题内容**  
  
-   **开始之前：**  
  
     [限制和局限](#Restrictions)  
  
-   **复制架构更改，使用：**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Restrictions"></a> 限制和局限  
  
-   ALTER TABLE … DROP COLUMN 语句将始终复制到所有其订阅包含要被删除的列的订阅服务器，即使禁用对架构更改的复制也是如此。  
  
##  <a name="SSMSProcedure"></a> 使用 SQL Server Management Studio  
 如果您不想要复制的发布的架构更改，请禁用中的架构更改复制 **发布属性-\< 发布>** 对话框。 有关访问此对话框的详细信息，请参阅 [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)。  
  
#### 禁用对架构更改的复制  
  
1.  在 **订阅选项** 页 **发布属性-\< 发布>** 对话框框中，设置的值 **复制架构更改** 属性设置为 **False**。  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
     若要仅传播特定的架构更改，请在架构更改前将此属性设置为 **True** ，然后在更改后将其设置为 **False** 。 相反，若要传播大多数架构更改，而不是一个给定更改，请在架构更改前将此属性设置为 **“False”** ，然后在更改后将其设置为 **“True”** 。  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 可以使用复制存储过程来指定是否复制这些架构更改。 您使用的存储过程取决于发布的类型。  
  
#### 创建不复制架构更改的快照发布或事务发布  
  
1.  在发布服务器上对发布数据库中，执行 [sp_addpublication & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addpublication-transact-sql.md), ，将值指定为 **0** 为 **@replicate_ddl**。 有关详细信息，请参阅 [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)。  
  
#### 创建不复制架构更改的合并发布  
  
1.  在发布服务器上对发布数据库中，执行 [sp_addmergepublication & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-addmergepublication-transact-sql.md), ，将值指定为 **0** 为 **@replicate_ddl**。 有关详细信息，请参阅 [Create a Publication](../../../relational-databases/replication/publish/create-a-publication.md)。  
  
#### 为快照发布或事务发布暂时禁用复制架构更改  
  
1.  复制架构更改的发布，仅为执行 [sp_changepublication & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md), ，将值指定为 **replicate_ddl** 为 **@property** ，值为 **0** 为 **@value**。  
  
2.  对已发布对象执行 DDL 命令。  
  
3.  （可选）重新启用复制架构更改，通过执行 [sp_changepublication & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-changepublication-transact-sql.md), ，将值指定为 **replicate_ddl** 为 **@property** ，值为 **1** 为 **@value**。  
  
#### 为合并发布暂时禁用复制架构更改  
  
1.  复制架构更改的发布，仅为执行 [sp_changemergepublication & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md), ，将值指定为 **replicate_ddl** 为 **@property** ，值为 **0** 为 **@value**。  
  
2.  对已发布对象执行 DDL 命令。  
  
3.  （可选）重新启用复制架构更改，通过执行 [sp_changemergepublication & #40;Transact SQL & #41;](../../../relational-databases/system-stored-procedures/sp-changemergepublication-transact-sql.md), ，将值指定为 **replicate_ddl** 为 **@property** ，值为 **1** 为 **@value**。  
  
## 另请参阅  
 [对发布数据库进行架构更改](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)   
 [对发布数据库进行架构更改](../../../relational-databases/replication/publish/make-schema-changes-on-publication-databases.md)  
  
  