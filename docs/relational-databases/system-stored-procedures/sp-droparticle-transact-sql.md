---
title: "sp_droparticle (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- sp_droparticle_TSQL
- sp_droparticle
helpviewer_keywords: sp_droparticle
ms.assetid: 09fec594-53f4-48a5-8edb-c50731c7adb2
caps.latest.revision: "25"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5c2d3ec47a41e2783bc5bab5a5eaaf1a4cedd3de
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="spdroparticle-transact-sql"></a>sp_droparticle (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  从快照发布或事务发布中删除一个项目。 如果项目存在一个或多个订阅，则不能删除该项目。 在发布服务器的发布数据库上执行此存储的过程。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_droparticle [ @publication= ] 'publication'  
        , [ @article= ] 'article'  
    [ , [ @ignore_distributor = ] ignore_distributor ]  
    [ , [ @force_invalidate_snapshot= ] force_invalidate_snapshot ]  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @from_drop_publication = ] from_drop_publication ]  
```  
  
## <a name="arguments"></a>参数  
 [  **@publication=**] *发布*  
 包含要删除的项目的发布名称。 *发布*是**sysname**，无默认值。  
  
 [  **@article=**] *文章*  
 是要除去项目的名称。 *文章*是**sysname**，无默认值。  
  
 [  **@ignore_distributor =**] *ignore_distributor*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 [  **@force_invalidate_snapshot =** ] *force_invalidate_snapshot*  
 确认此存储过程所执行的操作是否会使现有快照失效。 *force_invalidate_snapshot*是**位**，默认值为**0**。  
  
 **0**指定文章的更改不会导致快照无效。 如果该存储过程检测到更改确实需要新的快照，则会发生错误，并且不进行任何更改。  
  
 **1**指定文章的更改可能导致快照无效，将需要一次新快照的现有订阅是否可以为现有的快照将被标记为过时和新的快照生成授予的权限。  
  
 [  **@publisher** =] *发布服务器*  
 指定一个非[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器。 *发布服务器*是**sysname**，默认值为 NULL。  
  
> [!NOTE]  
>  *发布服务器*上更改项目属性时不应使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器。  
  
 [  **@from_drop_publication** =] *from_drop_publication*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 **sp_droparticle**快照和事务复制中使用。  
  
 为水平筛选的项目， **sp_droparticle**检查**类型**中项目的列[sysarticles &#40;Transact SQL &#41;](../../relational-databases/system-tables/sysarticles-transact-sql.md)表来确定是否一个视图或筛选器应还删除。 如果视图或筛选是自动生成的，则将其与项目一起删除。 如果是手动创建的，则不将其删除。  
  
 执行**sp_droparticle**以从发布删除项目不会删除该对象从发布数据库或从订阅数据库的相应对象。 如果需要，请使用 `DROP <object>` 手动删除这些对象。  
  
## <a name="example"></a>示例  
 [!code-sql[HowTo#sp_droparticle](../../relational-databases/replication/codesnippet/tsql/sp-droparticle-transact-_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_droparticle**。  
  
## <a name="see-also"></a>另请参阅  
 [删除项目](../../relational-databases/replication/publish/delete-an-article.md)   
 [向现有发布添加项目和从中删除项目](../../relational-databases/replication/publish/add-articles-to-and-drop-articles-from-existing-publications.md)   
 [sp_addarticle &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_changearticle (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [sp_helparticle (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)   
 [sp_helparticlecolumns &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-helparticlecolumns-transact-sql.md)   
 [复制存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
