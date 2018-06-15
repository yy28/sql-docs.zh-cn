---
title: 执行 sp_articlefilter (Transact SQL) |Microsoft 文档
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
- sp_articlefilter_TSQL
- sp_articlefilter
helpviewer_keywords:
- sp_articlefilter
ms.assetid: 4c3fee32-a43f-4757-a029-30aef4696afb
caps.latest.revision: 33
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 1ec7582f644a3701ef209c2ad3d4774e1aefdfb5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
ms.locfileid: "32992536"
---
# <a name="sparticlefilter-transact-sql"></a>sp_articlefilter (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  基于表项目筛选发布的数据。 在发布服务器的发布数据库上执行此存储的过程。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_articlefilter [ @publication = ] 'publication'  
        , [ @article = ] 'article'  
    [ , [ @filter_name = ] 'filter_name' ]  
    [ , [ @filter_clause = ] 'filter_clause' ]  
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>参数  
 [ **@publication=**] **'***publication***'**  
 包含项目的发布的名称。 *发布*是**sysname**，无默认值。  
  
 [  **@article=**] *****文章*****  
 项目的名称。 *文章*是**sysname**，无默认值。  
  
 [  **@filter_name=**] *****filter_name*****  
 是从创建的筛选器存储过程的名称*filter_name*。 *filter_name*是**nvarchar(386)**，默认值为 NULL。 您必须为项目筛选指定唯一的名称。  
  
 [  **@filter_clause=**] *****filter_clause*****  
 是定义水平筛选器的限制 (WHERE) 子句。 当输入限制子句时，将省略关键字 WHERE。 *filter_clause*是**ntext**，默认值为 NULL。  
  
 [  **@force_invalidate_snapshot =** ] *force_invalidate_snapshot*  
 确认此存储过程所执行的操作是否会使现有快照失效。 *force_invalidate_snapshot*是**位**，默认值为**0**。  
  
 **0**指定文章的更改不会导致快照无效。 如果该存储过程检测到更改确实需要新的快照，则会发生错误，并且不进行任何更改。  
  
 **1**指定文章的更改可能导致快照无效，将需要一次新快照的现有订阅是否可以为现有的快照将被标记为过时和新的快照生成授予的权限。  
  
 [  **@force_reinit_subscription =** ] *force_reinit_subscription*  
 确认此存储过程执行的操作可能需要重新初始化现有订阅。 *force_reinit_subscription*是**位**，默认值为**0**。  
  
 **0**指定文章的更改不会导致需要重新初始化订阅。 如果该存储过程检测到更改将需要重新初始化订阅，则会发生错误，并且不进行任何更改。  
  
 **1**指定文章的更改会导致现有订阅重新初始化订阅，可以授予权限，重新初始化订阅发生。  
  
 [  **@publisher=** ] *****发布服务器*****  
 指定一个非[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器。 *发布服务器*是**sysname**，默认值为 NULL。  
  
> [!NOTE]  
>  *发布服务器*不应与使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]发布服务器。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 **执行 sp_articlefilter**快照复制和事务复制中使用。  
  
 执行**执行 sp_articlefilter** for 具有现有订阅的项目要求重新初始化这些订阅。  
  
 **执行 sp_articlefilter**创建筛选器，将插入中的筛选器存储过程的 ID**筛选器**列[sysarticles &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-tables/sysarticles-transact-sql.md)表，然后将插入的文本中的限制子句**filter_clause**列。  
  
 若要创建项目具有水平筛选器，执行[sp_addarticle &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)没有*筛选器*参数。 执行**执行 sp_articlefilter**，提供所有参数包括*filter_clause*，然后执行[sp_articleview &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)，提供所有参数包括相同*filter_clause*。 如果筛选器已存在并且**类型**中**sysarticles**是**1** （基于日志的文章） 删除以前的筛选器，并创建一个新的筛选器。  
  
 如果*filter_name*和*filter_clause*不提供，删除以前的筛选器和筛选器 ID 设置为**0**。  
  
## <a name="example"></a>示例  
 [!code-sql[HowTo#sp_AddTranArticle](../../relational-databases/replication/codesnippet/tsql/sp-articlefilter-transac_1.sql)]  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**执行 sp_articlefilter**。  
  
## <a name="see-also"></a>另请参阅  
 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)   
 [定义和修改静态行筛选器](../../relational-databases/replication/publish/define-and-modify-a-static-row-filter.md)   
 [sp_addarticle &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-addarticle-transact-sql.md)   
 [sp_articleview &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-articleview-transact-sql.md)   
 [sp_changearticle (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-changearticle-transact-sql.md)   
 [sp_droparticle (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-droparticle-transact-sql.md)   
 [sp_helparticle (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-helparticle-transact-sql.md)   
 [复制存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
