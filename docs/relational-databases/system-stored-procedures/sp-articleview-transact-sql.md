---
title: sp_articleview (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- sp_articleview
- sp_articleview_TSQL
helpviewer_keywords:
- sp_articleview
ms.assetid: a3d63fd6-f360-4a2f-8a82-a0dc15f650b3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 369c7218e5d4d2c18d14d07b97d336cbe31ed4b3
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47727935"
---
# <a name="sparticleview-transact-sql"></a>sp_articleview (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  在垂直或水平筛选表时创建用于定义已发布项目的视图。 该视图用作目标表的架构和数据的筛选源。 只有未订阅的项目才能由此存储过程修改。 在发布服务器上对发布数据库执行此存储的过程。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_articleview [ @publication = ] 'publication'  
        , [ @article = ] 'article'  
    [ , [ @view_name = ] 'view_name']  
    [ , [ @filter_clause = ] 'filter_clause']  
    [ , [ @change_active = ] change_active ]  
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
    [ , [ @publisher = ] 'publisher' ]  
    [ , [ @refreshsynctranprocs = ] refreshsynctranprocs ]  
    [ , [ @internal = ] internal ]  
```  
  
## <a name="arguments"></a>参数  
 [ **@publication=**] **'***publication***'**  
 包含项目的发布的名称。 *发布*是**sysname**，无默认值。  
  
 [ **@article=**] **'***文章*****  
 项目的名称。 *文章*是**sysname**，无默认值。  
  
 [ **@view_name=**] **'***view_name*****  
 定义已发布项目的视图的名称。 *view_name*是**nvarchar(386)**，默认值为 NULL。  
  
 [  **@filter_clause=**] **'***filter_clause*****  
 是定义水平筛选器的限制 (WHERE) 子句。 当输入限制子句时，将省略 WHERE 关键字。 *filter_clause*是**ntext**，默认值为 NULL。  
  
 [  **@change_active =** ] *change_active*  
 允许修改具有订阅的发布中的列。 *change_active*是**int**，默认值为**0**。 如果**0**，则不更改列。 如果**1**，可以创建或在具有订阅的活动项目上重新创建视图。  
  
 [  **@force_invalidate_snapshot =** ] *force_invalidate_snapshot*  
 确认此存储过程所执行的操作是否会使现有快照失效。 *force_invalidate_snapshot*是**位**，默认值为**0**。  
  
 **0**指定对项目的更改不会导致快照无效。 如果该存储过程检测到更改确实需要新的快照，则会发生错误，并且不进行任何更改。  
  
 **1**指定更改项目可能导致快照无效，如果有现有订阅需要新快照，向其授予权限将现有快照标记为过时并生成新快照。  
  
 [  **@force_reinit_subscription =]** *force_reinit_subscription*  
 确认此存储过程所执行的操作可能需要重新初始化现有订阅。 *force_reinit_subscription*是**位**默认值为**0**。  
  
 **0**指定对项目的更改不会导致重新初始化订阅。 如果该存储过程检测到更改将需要重新初始化订阅，则会发生错误，并且不进行任何更改。  
  
 **1**指定更改项目会导致现有订阅重新初始化，并授予重新初始化订阅发生的权限。  
  
 [ **@publisher** =] **'***发布服务器*****  
 指定一个非[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器。 *发布服务器*是**sysname**，默认值为 NULL。  
  
> [!NOTE]  
>  *发布服务器*从发布时不应使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器。  
  
 [ **@refreshsynctranprocs** =] *refreshsynctranprocs*  
 指示是否自动重新创建用于同步复制的存储过程。 *refreshsynctranprocs*是**位**，默认值为 1。  
  
 **1**意味着，将重新创建存储的过程。  
  
 **0**意味着，存储的过程不是重新创建。  
  
 [ **@internal**=]*内部*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_articleview**创建用于定义已发布的项目，并将插入在该视图的 ID 的视图**sync_objid**的列[sysarticles &#40;-&#41; ](../../relational-databases/system-tables/sysarticles-transact-sql.md)表，并将其插入限制子句中的文本**filter_clause**列。 如果所有列被都复制，并且没有无**filter_clause**，则**sync_objid**中[sysarticles &#40;-&#41; ](../../relational-databases/system-tables/sysarticles-transact-sql.md)表设置的 ID基础表，以及如何使用**sp_articleview**不是必需的。  
  
 若要发布垂直筛选的表 (即，到筛选器的列) 首次运行**sp_addarticle**没有*sync_object*参数，运行[sp_articlecolumn &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)为每个列来复制 （定义垂直筛选器），并运行一次**sp_articleview**创建用于定义已发布的项目的视图。  
  
 若要发布水平筛选的表 （即筛选行），运行[sp_addarticle &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)没有*筛选器*参数。 运行[sp_articlefilter &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md)，提供所有参数，包括*filter_clause*。 然后运行**sp_articleview**，并提供包括相同的所有参数*filter_clause*。  
  
 若要发布垂直和水平筛选的表，请运行[sp_addarticle &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)没有*sync_object*或*筛选器*参数。 运行[sp_articlecolumn &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)一次的复制，每一列，然后运行[sp_articlefilter &#40;-&#41; ](../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md)并**sp_articleview**。  
  
 如果项目已具有用于定义已发布的项目的视图**sp_articleview**删除现有视图并自动创建一个新。 如果手动创建视图 (**类型**中[sysarticles &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-tables/sysarticles-transact-sql.md)是**5**)，将不删除现有视图。  
  
 如果创建自定义筛选存储过程和用于手动定义已发布的项目的视图时，不能运行**sp_articleview**。 相反，提供它们作为*筛选器*并*sync_object*参数[sp_addarticle &#40;-&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)，以及相应的*类型*值。  
  
## <a name="example"></a>示例  
 [!code-sql[HowTo#sp_AddTranArticle](../../relational-databases/replication/codesnippet/tsql/sp-articleview-transact-_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_articleview**。  
  
## <a name="see-also"></a>请参阅  
 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)   
 [定义和修改静态行筛选器](../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md)   
 [sp_addarticle &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_articlefilter (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-articlefilter-transact-sql.md)   
 [sp_changearticle (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [sp_droparticle (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md)   
 [sp_helparticle (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)   
 [复制存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
