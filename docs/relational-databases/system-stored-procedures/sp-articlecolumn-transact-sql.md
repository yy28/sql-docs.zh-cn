---
title: sp_articlecolumn (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_articlecolumn
- sp_articlecolumn_TSQL
helpviewer_keywords:
- sp_articlecolumn
ms.assetid: 8abaa8c1-d99e-4788-970f-c4752246c577
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 636a0a23c70170ce625b9e462e2715c1c884bda7
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2018
ms.locfileid: "53210116"
---
# <a name="sparticlecolumn-transact-sql"></a>sp_articlecolumn (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  用于指定项目中包含的列以垂直筛选已发布表中的数据。 在发布服务器上对发布数据库执行此存储的过程。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_articlecolumn [ @publication = ] 'publication'  
        , [ @article = ] 'article'  
    [ , [ @column = ] 'column' ]  
    [ , [ @operation = ] 'operation' ]  
    [ , [ @refresh_synctran_procs = ] refresh_synctran_procs ]  
    [ , [ @ignore_distributor = ] ignore_distributor ]  
    [ , [ @change_active = ] change_actve ]  
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @internal = ] 'internal' ]  
```  
  
## <a name="arguments"></a>参数  
 [  **@publication=**] **'**_发布_  
 包含此项目的发布的名称。 *发布*是**sysname**，无默认值。  
  
 [  **@article=**] **'**_文章_  
 项目的名称。 *文章*是**sysname**，无默认值。  
  
 [  **@column=**] **'**_列_  
 要添加或删除的列的名称。 *列*是**sysname**，默认值为 NULL。 如果为 NULL，则发布所有列。  
  
 [  **@operation=**] **'**_操作_  
 指定在项目中添加还是删除列。 *操作*是**nvarchar(5)**，使用默认值为 add。 **添加**会标记列以进行复制。 **删除**会取消列的标记。  
  
 [  **@refresh_synctran_procs=**] *refresh_synctran_procs*  
 指定是否重新生成支持立即更新订阅的存储过程以匹配复制的列数。 *refresh_synctran_procs*是**位**，默认值为**1**。 如果**1**，重新生成存储的过程。  
  
 [  **@ignore_distributor =**] *ignore_distributor*  
 指示是否无需连接到分发服务器上执行此存储的过程。 *ignore_distributor*是**位**，默认值为**0**。 如果**0**，必须启用数据库进行发布，并应刷新项目缓存以反映该项目复制的新列。 如果**1**，允许的项目驻留在未发布数据库中; 应仅在恢复情况下使用要删除的项目列。  
  
 [  **@change_active =** ] *change_active*  
 允许修改具有订阅的发布中的列。 *change_active*是**int**默认值为**0**。 如果**0**，则不修改列。 如果**1**，可以添加或从具有订阅的活动项目中删除列。  
  
 [ **@force_invalidate_snapshot =** ] *force_invalidate_snapshot*  
 确认此存储过程所执行的操作是否会使现有快照失效。 *force_invalidate_snapshot*是**位**，默认值为**0**。  
  
 **0**指定对项目的更改不会导致快照无效。 如果该存储过程检测到更改确实需要新的快照，则会发生错误，并且不进行任何更改。  
  
 **1**指定更改项目可能导致快照无效，如果有现有订阅需要新快照，向其授予权限将现有快照标记为过时并生成新快照。  
  
 [ **@force_reinit_subscription =** ] *force_reinit_subscription*  
 确认此存储过程所执行的操作可能需要重新初始化现有订阅。 *force_reinit_subscription*是**位**，默认值为**0**。  
  
 **0**指定对项目的更改不会导致重新初始化订阅。 如果该存储过程检测到更改将需要重新初始化订阅，则会发生错误，并且不进行任何更改。 **1**指定对项目的更改会导致现有订阅重新初始化，并授予重新初始化订阅发生的权限。  
  
 [  **@publisher=** ] **'**_发布服务器上_  
 指定一个非[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器。 *发布服务器*是**sysname**，默认值为 NULL。  
  
> [!NOTE]  
>  *发布服务器*不能与[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器。  
  
 [  **@internal=** ] **'**_内部_  
 仅限内部使用。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_articlecolumn**快照复制和事务复制中使用。  
  
 可以使用筛选仅一个未订阅的项目**sp_articlecolumn**。  
  
## <a name="example"></a>示例  
 [!code-sql[HowTo#sp_AddTranArticle](../../relational-databases/replication/codesnippet/tsql/sp-articlecolumn-transac_1.sql)]  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_articlecolumn**。  
  
## <a name="see-also"></a>请参阅  
 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)   
 [定义和修改列筛选器](../../relational-databases/replication/publish/define-and-modify-a-column-filter.md)   
 [筛选已发布数据](../../relational-databases/replication/publish/filter-published-data.md)   
 [sp_addarticle &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_articleview &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)   
 [sp_changearticle (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [sp_droparticle (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md)   
 [sp_helparticle (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)   
 [sp_helparticlecolumns &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helparticlecolumns-transact-sql.md)   
 [复制存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
