---
title: sp_mergearticlecolumn (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_mergearticlecolumn
- sp_mergearticlecolumn_TSQL
helpviewer_keywords:
- sp_mergearticlecolumn
ms.assetid: b4f2b888-e094-4759-a472-d893638995eb
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d2cb929ffc3506d6dcb4a0745c53b47a45fdb469
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62627800"
---
# <a name="spmergearticlecolumn-transact-sql"></a>sp_mergearticlecolumn (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  对合并发布进行垂直分区。 在发布服务器上对发布数据库执行此存储的过程。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_mergearticlecolumn [ @publication = ] 'publication'  
        , [ @article = ] 'article'  
    [ , [ @column = ] 'column'  
    [ , [ @operation = ] 'operation'   
    [ , [ @schema_replication = ] 'schema_replication' ]  
    [ , [ @force_invalidate_snapshot = ] force_invalidate_snapshot ]   
    [ , [ @force_reinit_subscription = ] force_reinit_subscription ]   
```  
  
## <a name="arguments"></a>参数  
`[ @publication = ] 'publication'` 是发布的名称。 *发布*是**sysname**，无默认值。  
  
`[ @article = ] 'article'` 是在发布中项目的名称。 *文章*是**sysname**，无默认值。  
  
`[ @column = ] 'column'` 标识要在其中创建垂直分区的列。 *列*是**sysname**，默认值为 NULL。 如果为 NULL 和 `@operation = N'add'`，默认情况下，源表中的所有列将添加到项目。 *列*不能为 NULL 时*操作*设置为**删除**。 若要从项目中排除列，请执行**sp_mergearticlecolumn**并指定*列*并`@operation = N'drop'`为每个要删除的列从指定*文章*.  
  
`[ @operation = ] 'operation'` 是复制状态。 *操作*是**nvarchar(4)** ，使用默认值为 ADD。 **添加**会标记列以进行复制。 **删除**清除该列。  
  
`[ @schema_replication = ] 'schema_replication'` 指定合并代理运行时将传播架构更改。 *schema_replication*是**nvarchar(5)** ，默认值为 FALSE。  
  
> [!NOTE]  
>  仅**FALSE**支持*schema_replication*。  
  
`[ @force_invalidate_snapshot = ] force_invalidate_snapshot` 启用或禁用使快照失效的功能。 *force_invalidate_snapshot*是**位**，默认值为**0**。  
  
 **0**指定对合并项目的更改不会导致快照无效。  
  
 **1**指定对合并项目的更改可能导致快照无效，如果是这种情况的值**1**提供了新快照的权限。  
  
`[ @force_reinit_subscription = ]force_reinit_subscription_` 启用或禁用使订阅重新初始化的功能。 *force_reinit_subscription*为 bit，默认值为**0**。  
  
 **0**指定对合并项目的更改不会导致重新初始化订阅。  
  
 **1**指定对合并项目的更改可能导致订阅重新初始化，如果是这种情况的值**1**使订阅重新初始化发生的权限。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_mergearticlecolumn**合并复制中使用。  
  
 如果正在使用自动标识范围管理，则不能从项目删除标识列。 有关详细信息，请参阅[复制标识列](../../relational-databases/replication/publish/replicate-identity-columns.md)。  
  
 如果创建初始快照后，应用程序设置了新的垂直分区，则一定会生成新的快照且重新应用于每个订阅。 当下一个已计划的快照和分发或合并代理运行时应用快照。  
  
 如果行跟踪用于冲突检测（默认值），则基表最多可包含 1,024 列，但是必须从项目中筛选列，以便最多发布 246 列。 如果使用列跟踪，则基表最多可包含 246 列。  
  
## <a name="example"></a>示例  
 [!code-sql[HowTo#sp_AddMergeArticle](../../relational-databases/replication/codesnippet/tsql/sp-mergearticlecolumn-tr_1.sql)]  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_mergearticlecolumn**。  
  
## <a name="see-also"></a>请参阅  
 [定义和修改合并项目间的联接筛选器](../../relational-databases/replication/publish/define-and-modify-a-join-filter-between-merge-articles.md)   
 [定义和修改合并项目的参数化行筛选器](../../relational-databases/replication/publish/define-and-modify-a-parameterized-row-filter-for-a-merge-article.md)   
 [筛选已发布数据](../../relational-databases/replication/publish/filter-published-data.md)   
 [复制存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/replication-stored-procedures-transact-sql.md)  
  
  
