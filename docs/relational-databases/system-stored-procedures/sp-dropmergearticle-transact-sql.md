---
title: sp_dropmergearticle (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 05/02/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_dropmergearticle
- sp_dropmergearticle_TSQL
helpviewer_keywords:
- sp_dropmergearticle
ms.assetid: 5ef1fbf7-c03d-4488-9ab2-64aae296fa4f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4d96dd15857847e739600f087fa63b2c34453d27
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/03/2018
ms.locfileid: "52816039"
---
# <a name="spdropmergearticle-transact-sql"></a>sp_dropmergearticle (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  删除合并发布中的项目。 在发布服务器上对发布数据库执行此存储的过程。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_dropmergearticle [ @publication= ] 'publication'  
        , [ @article= ] 'article'   
    [ , [ @ignore_distributor= ] ignore_distributor   
    [ , [ @reserved= ] reserved   
    [ , [ @force_invalidate_snapshot= ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
    [ , [ @ignore_merge_metadata = ] ignore_merge_metadata ]  
```  
  
## <a name="arguments"></a>参数  
 [ **@publication=**] **'***publication***'**  
 要从中删除项目的发布的名称。 *发布*是**sysname**，无默认值。  
  
 [ **@article=**] **'***文章*****  
 要从给定发布中删除的项目的名称。 *文章*是**sysname**，无默认值。 如果**所有**，将删除指定的合并发布中的所有现有项目。 即使*一文*是**所有**，发布仍必须分开删除文章。  
  
 [ **@ignore_distributor=**] *ignore_distributor*  
 指示是否在未连接到分发服务器的情况下执行此存储过程。 *ignore_distributor*是**位**，默认值为**0**。  
  
 [  **@reserved=**]*保留*  
 供将来使用的保留参数。 *保留*是**nvarchar(20)**，默认值为 NULL。  
  
 [  **@force_invalidate_snapshot=**] *force_invalidate_snapshot*  
 启用或禁用使快照失效的功能。 *force_invalidate_snapshot*是**位**，默认值**0**。  
  
 **0**指定对合并项目的更改不会导致快照无效。  
  
 **1**表示对合并项目的更改可能导致快照无效，如果是这种情况的值**1**提供了新快照的权限。  
  
 [  **@force_reinit_subscription =** ] *force_reinit_subscription*  
 确认删除项目是否要求重新初始化现有订阅。 *force_reinit_subscription*是**位**，默认值为**0**。  
  
 **0**指定删除项目不会导致重新初始化订阅。  
  
 **1**意味着的删除文章导致现有订阅重新初始化，并使订阅重新初始化发生的权限。  
  
 [  **@ignore_merge_metadata=** ] *ignore_merge_metadata*  
 仅限内部使用。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_dropmergearticle**合并复制中使用。 有关删除项目的详细信息，请参阅[添加项目和从现有发布删除项目](../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)。  
  
 执行**sp_dropmergearticle**从发布中删除项目不会删除该对象从发布数据库或订阅数据库中的相应对象。 如果需要，可以使用 `DROP <object>` 手动删除这些对象。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_dropmergearticle**。  
  
## <a name="example"></a>示例  
  
```sql  
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
  
```sql  
DECLARE @publication AS sysname;  
DECLARE @table1 AS sysname;  
DECLARE @table2 AS sysname;  
DECLARE @table3 AS sysname;  
DECLARE @salesschema AS sysname;  
DECLARE @hrschema AS sysname;  
DECLARE @filterclause AS nvarchar(1000);  
SET @publication = N'AdvWorksSalesOrdersMerge';   
SET @table1 = N'Employee';   
SET @table2 = N'SalesOrderHeader';   
SET @table3 = N'SalesOrderDetail';   
SET @salesschema = N'Sales';  
SET @hrschema = N'HumanResources';  
SET @filterclause = N'Employee.LoginID = HOST_NAME()';  
  
-- Drop the merge join filter between SalesOrderHeader and SalesOrderDetail.  
EXEC sp_dropmergefilter   
  @publication = @publication,   
  @article = @table3,   
  @filtername = N'SalesOrderDetail_SalesOrderHeader',   
  @force_invalidate_snapshot = 1,   
  @force_reinit_subscription = 1;  
  
-- Drops the merge join filter between Employee and SalesOrderHeader.  
EXEC sp_dropmergefilter   
  @publication = @publication,   
  @article = @table2,   
  @filtername = N'SalesOrderHeader_Employee',   
  @force_invalidate_snapshot = 1,   
  @force_reinit_subscription = 1;  
  
-- Drops the article for the SalesOrderDetail table.  
EXEC sp_dropmergearticle   
  @publication = @publication,   
  @article = @table3,  
  @force_invalidate_snapshot = 1,   
  @force_reinit_subscription = 1;  
  
-- Drops the article for the SalesOrderHeader table.  
EXEC sp_dropmergearticle   
  @publication = @publication,   
  @article = @table2,   
  @force_invalidate_snapshot = 1,   
  @force_reinit_subscription = 1;  
  
-- Drops the article for the Employee table.  
EXEC sp_dropmergearticle   
  @publication = @publication,   
  @article = @table1,  
  @force_invalidate_snapshot = 1,   
  @force_reinit_subscription = 1;  
GO  
```  
  
## <a name="see-also"></a>请参阅  
 [删除项目](../../relational-databases/replication/publish/delete-an-article.md)   
 [向现有发布添加项目和从中删除项目](../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)   
 [sp_addmergearticle &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)   
 [sp_changemergearticle (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)   
 [sp_helpmergearticle (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-helpmergearticle-transact-sql.md)   
 [复制存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
