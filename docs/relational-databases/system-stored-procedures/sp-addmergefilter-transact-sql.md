---
title: "sp_addmergefilter (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
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
- sp_addmergefilter
- sp_addmergefilter_TSQL
helpviewer_keywords: sp_addmergefilter
ms.assetid: 4c118cb1-2008-44e2-a797-34b7dc34d6b1
caps.latest.revision: "49"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bae5cbac50c347247bba5b0488a7fb70ad8e71a3
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="spaddmergefilter-transact-sql"></a>sp_addmergefilter (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  添加新合并筛选以创建基于与另一个表的联接的分区。 在发布服务器的发布数据库上执行此存储的过程。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_addmergefilter [ @publication = ] 'publication'   
        , [ @article = ] 'article'   
        , [ @filtername = ] 'filtername'   
        , [ @join_articlename = ] 'join_articlename'   
        , [ @join_filterclause = ] join_filterclause  
    [ , [ @join_unique_key = ] join_unique_key ]  
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]  
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]  
    [ , [ @filter_type = ] filter_type ]  
```  
  
## <a name="arguments"></a>参数  
 [  **@publication=** ] *发布*  
 添加合并筛选的发布的名称。 *发布*是**sysname**，无默认值。  
  
 [  **@article=** ] *文章*  
 添加合并筛选的项目的名称。 *文章*是**sysname**，无默认值。  
  
 [  **@filtername=** ] *filtername*  
 筛选的名称。 *filtername*参数是必需的。 *filtername*是**sysname**，无默认值。  
  
 [  **@join_articlename=** ] *join_articlename*  
 是指子项目中，指定父项目*文章*，必须使用指定的联接子句联接*join_filterclause*，以便确定满足在子项目中的行合并筛选器的筛选器条件。 *join_articlename*是**sysname**，无默认值。 给定的发布中必须是文章*发布*。  
  
 [  **@join_filterclause=** ] *join_filterclause*  
 为加入指定的子项目必须使用的联接子句*文章*和指定的父项目*join_article*，以便确定符合条件的合并筛选器的行。 *join_filterclause*是**nvarchar(1000)**。  
  
 [  **@join_unique_key=** ] *join_unique_key*  
 指定如果子项目之间的联接*文章*和父项目*join_article*是一个对多、 一对一、 多对一或多对多。 *join_unique_key*是**int**，默认值为 0。 **0**指示多对一或多对多联接。 **1**指示一对一或一对多的联接。 此值是**1**联接列时窗体中的唯一键*join_article*，或者如果*join_filterclause*之间的外键*文章*和中的主键*join_article*。  
  
> [!CAUTION]  
>  仅将此参数设置为**1**如果你有保证唯一性父项目的基础表中的联接列上的约束。 如果*join_unique_key*设置为**1**不正确，可能会出现数据无法收敛。  
  
 [  **@force_invalidate_snapshot=** ] *force_invalidate_snapshot*  
 确认此存储过程所执行的操作是否会使现有快照失效。 *force_invalidate_snapshot*是**位**，默认值**0**。  
  
 **0**指定合并项目的更改不会导致快照无效。 如果存储的过程检测到更改确实需要新的快照，将会出错，将进行任何更改。  
  
 **1**指定合并项目的更改可能导致快照无效，将需要一次新快照的现有订阅是否可以为现有的快照将被标记为过时和新的快照授予的权限生成。  
  
 [  **@force_reinit_subscription=** ] *force_reinit_subscription*  
 确认此存储过程执行的操作可能需要重新初始化现有订阅。 *force_reinit_subscription*是**位**，默认值为 0。  
  
 **0**指定合并项目的更改不会导致要重新初始化的订阅。 如果该存储过程检测到更改需要重新初始化订阅，则会发生错误，并且不进行任何更改。  
  
 **1**指定合并项目的更改将导致现有订阅重新初始化订阅，可以授予权限，重新初始化订阅发生。  
  
 [  **@filter_type=** ] *filter_type*  
 指定要添加的筛选类型。 *filter_type*是**tinyint**，和可以是以下值之一。  
  
|值|说明|  
|-----------|-----------------|  
|**1**|仅为联接筛选器。 需要它来支持 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 订阅服务器。|  
|**2**|仅为逻辑记录关系。|  
|**3**|同时为联接筛选器和逻辑记录关系。|  
  
 有关详细信息，请参阅[通过逻辑记录对相关行的更改进行分组](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 **sp_addmergefilter**合并复制中使用。  
  
 **sp_addmergefilter**只能用于表项目。 不支持视图项目和索引视图项目。  
  
 此过程也可用于在两个可能或不可能具有联接筛选器的项目之间添加逻辑关系。 *filter_type*用于指定要添加的合并筛选器是否联接筛选器、 逻辑关系，或两者。  
  
 若要使用逻辑记录，发布和项目必须满足许多要求。 有关详细信息，请参阅[通过逻辑记录对相关行的更改进行分组](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)。  
  
 通常，该选项用于具有对已发布的主键表的外键引用的项目，而且该主键表含有在其项目中定义的筛选。 主键行的子集用于确定复制到订阅服务器的外键行。  
  
 当两个已发布项目的源表共享相同的表对象名称时，不能在这两个项目之间添加联接筛选器。 在这种情况下，即使两个表属于不同的架构并具有唯一的项目名，也无法创建联接筛选器。  
  
 当在一个表项目上同时使用参数化行筛选器和联接筛选器时，复制会确定行是否属于某个订阅服务器的分区。 它会通过计算筛选函数或联接筛选器 (使用[OR](../../t-sql/language-elements/or-transact-sql.md)运算符)，而不是评估的交集的两个条件 (使用[AND](../../t-sql/language-elements/and-transact-sql.md)运算符)。  
  
## <a name="example"></a>示例  
 [!code-sql[HowTo#sp_addmergefilter](../../relational-databases/replication/codesnippet/tsql/sp-addmergefilter-transa_1.sql)]  
  
## <a name="permissions"></a>Permissions  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_addmergefilter**。  
  
## <a name="see-also"></a>另请参阅  
 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)   
 [Define and Modify a Join Filter Between Merge Articles](../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)   
 [Join Filters](../../relational-databases/replication/merge/join-filters.md)   
 [sp_changemergefilter (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-changemergefilter-transact-sql.md)   
 [sp_dropmergefilter (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-dropmergefilter-transact-sql.md)   
 [sp_helpmergefilter &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpmergefilter-transact-sql.md)   
 [复制存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
