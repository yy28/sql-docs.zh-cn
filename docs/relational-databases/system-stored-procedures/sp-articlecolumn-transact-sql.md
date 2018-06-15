---
title: sp_articlecolumn (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_articlecolumn
- sp_articlecolumn_TSQL
helpviewer_keywords:
- sp_articlecolumn
ms.assetid: 8abaa8c1-d99e-4788-970f-c4752246c577
caps.latest.revision: 28
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 407c4470ae7dad6a871736df822cb00a22882122
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32993194"
---
# <a name="sparticlecolumn-transact-sql"></a>sp_articlecolumn (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  用于指定项目中包含的列以垂直筛选已发布表中的数据。 在发布服务器的发布数据库上执行此存储的过程。  
  
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
 [ **@publication=**] **'***publication***'**  
 包含此项目的发布的名称。 *发布*是**sysname**，无默认值。  
  
 [  **@article=**] *****文章*****  
 项目的名称。 *文章*是**sysname**，无默认值。  
  
 [  **@column=**] *****列*****  
 要添加或删除的列的名称。 *列*是**sysname**，默认值为 NULL。 如果为 NULL，则发布所有列。  
  
 [  **@operation=**] *****操作*****  
 指定在项目中添加还是删除列。 *操作*是**nvarchar(5)**，默认值为添加。 **添加**将标记为复制的列。 **删除**取消标记列。  
  
 [  **@refresh_synctran_procs=**] *refresh_synctran_procs*  
 指定是否重新生成支持立即更新订阅的存储过程以匹配复制的列数。 *refresh_synctran_procs*是**位**，默认值为**1**。 如果**1**，重新生成存储的过程。  
  
 [  **@ignore_distributor =**] *ignore_distributor*  
 指示是否没有连接到分发服务器的情况下执行此存储的过程。 *ignore_distributor*是**位**，默认值为**0**。 如果**0**，数据库必须启用了发布，并应刷新文章缓存以反映项目所复制的新列。 如果**1**，允许的驻留在未发布的数据库; 应仅在恢复情况下使用的项目中删除这些项目列。  
  
 [  **@change_active =** ] *change_active*  
 允许修改具有订阅的发布中的列。 *change_active*是**int**默认值为**0**。 如果**0**，列不会修改。 如果**1**，可以添加或从有订阅的活动项目中删除列。  
  
 [  **@force_invalidate_snapshot =** ] *force_invalidate_snapshot*  
 确认此存储过程所执行的操作是否会使现有快照失效。 *force_invalidate_snapshot*是**位**，默认值为**0**。  
  
 **0**指定文章的更改不会导致快照无效。 如果该存储过程检测到更改确实需要新的快照，则会发生错误，并且不进行任何更改。  
  
 **1**指定文章的更改可能导致快照无效，将需要一次新快照的现有订阅是否可以为现有的快照将被标记为过时和新的快照生成授予的权限。  
  
 [ **@force_reinit_subscription =** ] *force_reinit_subscription*  
 确认此存储过程执行的操作可能需要重新初始化现有订阅。 *force_reinit_subscription*是**位**，默认值为**0**。  
  
 **0**指定文章的更改不会导致要重新初始化的订阅。 如果该存储过程检测到更改将需要重新初始化订阅，则会发生错误，并且不进行任何更改。 **1**指定文章更改导致现有订阅重新初始化订阅，可以授予权限，重新初始化订阅发生。  
  
 [  **@publisher=** ] *****发布服务器*****  
 指定一个非[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器。 *发布服务器*是**sysname**，默认值为 NULL。  
  
> [!NOTE]  
>  *发布服务器*不应与使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器。  
  
 [  **@internal=** ] *****内部*****  
 仅限内部使用。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 **sp_articlecolumn**快照复制和事务复制中使用。  
  
 可以使用筛选仅取消订阅的项目**sp_articlecolumn**。  
  
## <a name="example"></a>示例  
 [!code-sql[HowTo#sp_AddTranArticle](../../relational-databases/replication/codesnippet/tsql/sp-articlecolumn-transac_1.sql)]  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_articlecolumn**。  
  
## <a name="see-also"></a>另请参阅  
 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)   
 [定义和修改列筛选器](../../relational-databases/replication/publish/define-and-modify-a-column-filter.md)   
 [筛选已发布数据](../../relational-databases/replication/publish/filter-published-data.md)   
 [sp_addarticle &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_articleview &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)   
 [sp_changearticle (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [sp_droparticle (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md)   
 [sp_helparticle (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)   
 [sp_helparticlecolumns &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-helparticlecolumns-transact-sql.md)   
 [复制存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
