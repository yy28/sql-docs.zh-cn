---
title: sp_addmergefilter (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_addmergefilter
- sp_addmergefilter_TSQL
helpviewer_keywords:
- sp_addmergefilter
ms.assetid: 4c118cb1-2008-44e2-a797-34b7dc34d6b1
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 6f2843456f4f95d1019b51f82082d59977ce14d5
ms.sourcegitcommit: 2db83830514d23691b914466a314dfeb49094b3c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58493692"
---
# <a name="spaddmergefilter-transact-sql"></a>sp_addmergefilter (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  添加新合并筛选以创建基于与另一个表的联接的分区。 在发布服务器上对发布数据库执行此存储的过程。  
  
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
`[ @publication = ] 'publication'` 是在其中添加合并筛选器的名称。 *发布*是**sysname**，无默认值。  
  
`[ @article = ] 'article'` 是在其添加合并筛选的名称。 *文章*是**sysname**，无默认值。  
  
`[ @filtername = ] 'filtername'` 是筛选器的名称。 *filtername*是一个必需的参数。 *filtername*是**sysname**，无默认值。  
  
`[ @join_articlename = ] 'join_articlename'` 是到子项目中，指定的父项目*一文*，必须使用指定的联接子句联接*join_filterclause*，从而确定满足子项目中的行合并筛选器的筛选器条件。 *join_articlename*是**sysname**，无默认值。 该项目必须位于由给定的发布中*发布*。  
  
`[ @join_filterclause = ] join_filterclause` 必须用于联接指定的子项目的联接子句*一文*和指定的父项目*join_article*，从而确定符合条件的合并筛选器的行。 *join_filterclause*是**nvarchar(1000)**。  
  
`[ @join_unique_key = ] join_unique_key` 指定如果子项目之间的联接*一文*父项目*join_article*是-一对多、 一对一、 多对一或多对多。 *join_unique_key*是**int**，默认值为 0。 **0**表示多对一或多对多联接。 **1**表示一对一或一对多联接。 此值是**1**当联接的列形成中的唯一键*join_article*，或者，如果*join_filterclause*之间的外键*文章*和中的主键*join_article*。  
  
> [!CAUTION]  
>  仅将此参数设置为**1**如果可保证唯一性的父项目的基础表中具有的联接列上的约束。 如果*join_unique_key*设置为**1**非收敛性的数据不正确，可能会发生。  
  
`[ @force_invalidate_snapshot = ] force_invalidate_snapshot` 确认此存储过程所执行的操作会使现有快照失效。 *force_invalidate_snapshot*是**位**，默认值**0**。  
  
 **0**指定对合并项目的更改不会导致快照无效。 如果存储的过程检测到更改确实需要新快照，将发生错误，并且将进行任何更改。  
  
 **1**指定对合并项目的更改可能导致快照无效，如果有现有订阅需要新快照，向其授予权限将现有快照标记为过时和新的快照生成。  
  
`[ @force_reinit_subscription = ] force_reinit_subscription` 确认此存储过程所执行的操作可能需要重新初始化现有订阅。 *force_reinit_subscription*是**位**，默认值为 0。  
  
 **0**指定对合并项目的更改不会导致重新初始化订阅。 如果该存储过程检测到更改需要重新初始化订阅，则会发生错误，并且不进行任何更改。  
  
 **1**指定对合并项目的更改将导致现有订阅重新初始化，并授予重新初始化订阅发生的权限。  
  
`[ @filter_type = ] filter_type` 指定要添加的筛选类型。 *filter_type*是**tinyint**，可以是下列值之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**1**|仅为联接筛选器。 需要它来支持 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 订阅服务器。|  
|**2**|仅为逻辑记录关系。|  
|**3**|同时为联接筛选器和逻辑记录关系。|  
  
 有关详细信息，请参阅[通过逻辑记录对相关行的更改进行分组](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_addmergefilter**合并复制中使用。  
  
 **sp_addmergefilter**只能用于表项目。 不支持视图项目和索引视图项目。  
  
 此过程也可用于在两个可能或不可能具有联接筛选器的项目之间添加逻辑关系。 *filter_type*用于指定所添加的合并筛选是否为联接筛选器、 逻辑关系，或两者。  
  
 若要使用逻辑记录，发布和项目必须满足许多要求。 有关详细信息，请参阅[通过逻辑记录对相关行的更改进行分组](../../relational-databases/replication/merge/group-changes-to-related-rows-with-logical-records.md)。  
  
 通常，该选项用于具有对已发布的主键表的外键引用的项目，而且该主键表含有在其项目中定义的筛选。 主键行的子集用于确定复制到订阅服务器的外键行。  
  
 当两个已发布项目的源表共享相同的表对象名称时，不能在这两个项目之间添加联接筛选器。 在这种情况下，即使两个表属于不同的架构并具有唯一的项目名，也无法创建联接筛选器。  
  
 当在一个表项目上同时使用参数化行筛选器和联接筛选器时，复制会确定行是否属于某个订阅服务器的分区。 它是通过计算筛选函数或联接筛选器 (使用[OR](../../t-sql/language-elements/or-transact-sql.md)运算符)，而不是评估两个条件的交集 (使用[AND](../../t-sql/language-elements/and-transact-sql.md)运算符)。  
  
## <a name="example"></a>示例  
 [!code-sql[HowTo#sp_addmergefilter](../../relational-databases/replication/codesnippet/tsql/sp-addmergefilter-transa_1.sql)]  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_addmergefilter**。  
  
## <a name="see-also"></a>请参阅  
 [Define an Article](../../relational-databases/replication/publish/define-an-article.md)   
 [定义和修改合并项目间的联接筛选器](../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)   
 [Join Filters](../../relational-databases/replication/merge/join-filters.md)   
 [sp_changemergefilter (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-changemergefilter-transact-sql.md)   
 [sp_dropmergefilter (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-dropmergefilter-transact-sql.md)   
 [sp_helpmergefilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpmergefilter-transact-sql.md)   
 [复制存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
