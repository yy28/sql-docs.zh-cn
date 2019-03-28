---
title: sp_lookupcustomresolver (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_lookupcustomresolver_TSQL
- sp_lookupcustomresolver
helpviewer_keywords:
- sp_lookupcustomresolver
ms.assetid: 356a7b8a-ae53-4fb5-86ee-fcfddbf23ddd
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b7f1bfc868b34ac16e1c38aedc9193002d35d5b8
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58532724"
---
# <a name="splookupcustomresolver-transact-sql"></a>sp_lookupcustomresolver (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回在分发服务器上注册的基于 COM 的自定义冲突解决程序组件的业务逻辑处理程序或类标识符 (CLSID) 值的相关信息。 在发布服务器上对发布数据库执行此存储的过程。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_lookupcustomresolver [ @article_resolver = ] 'article_resolver'   
    [, [ @resolver_clsid = ] 'resolver_clsid' OUTPUT ]  
    [ , [ @is_dotnet_assembly = ] is_dotnet_assembly OUTPUT ]  
    [ , [ @dotnet_assembly_name = ] 'dotnet_assembly_name' OUTPUT ]  
    [ , [ @dotnet_class_name = ] 'dotnet_class_name' OUTPUT ]  
    [ , [ @publisher = ] 'publisher' ]  
```  
  
## <a name="arguments"></a>参数  
`[ @article_resolver = ] 'article_resolver'` 指定要注销的自定义业务逻辑的名称。 *article_resolver*是**nvarchar(255)**，无默认值。 如果被删除的业务逻辑是 COM 组件，则此参数是该组件的友好名称。 如果业务逻辑是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 程序集，则此参数是该程序集的名称。  
  
`[ @resolver_clsid = ] 'resolver_clsid' OUTPUT` 中指定的自定义业务逻辑的名称与关联的 COM 对象的 CLSID 值*article_resolver*参数。 *resolver_clsid*是**nvarchar （50)**，默认值为 NULL。  
  
`[ @is_dotnet_assembly = ] 'is_dotnet_assembly' OUTPUT` 指定要注册的自定义业务逻辑的类型。 *is_dotnet_assembly*是**位**，默认值为 0。 **1**指示正在注册的自定义业务逻辑是业务逻辑处理程序程序集;**0**指示它是一个 COM 组件。  
  
`[ @dotnet_assembly_name = ] 'dotnet_assembly_name' OUTPUT` 是实现业务逻辑处理程序的程序集的名称。 *dotnet_assembly_name*是**nvarchar(255)**，默认值为 NULL。  
  
`[ @dotnet_class_name = ] 'dotnet_class_name' OUTPUT` 是替代的类名称<xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule>实现业务逻辑处理程序。 *dotnet_class_name*是**nvarchar(255)**，默认值为 NULL。  
  
`[ @publisher = ] 'publisher'` 是发布服务器的名称。 *发布服务器*是**sysname**，默认值为 NULL。 未从发布服务器调用该存储过程时使用此参数。 如果未指定，则假定本地服务器是发布服务器。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_lookupcustomresolver**合并复制中使用。  
  
 **sp_lookupcustomresolver**返回值为 NULL *resolver_clsid*时该组件不会注册，此时的分布和值为"00000000-0000-0000-0000-000000000000"时注册属于.NET framework 程序集注册为业务逻辑处理程序。  
  
 **sp_lookupcustomresolver**由调用[sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)并[sp_changemergearticle](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)以验证指定*article_resolver*。  
  
## <a name="permissions"></a>权限  
 只有的成员**db_owner**上对发布数据库的固定的数据库角色可以执行**sp_lookupcustomresolver**。  
  
## <a name="see-also"></a>请参阅  
 [Advanced Merge Replication Conflict Detection and Resolution](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [在合并同步期间执行业务逻辑](../../relational-databases/replication/merge/execute-business-logic-during-merge-synchronization.md)   
 [为合并项目实现业务逻辑处理程序](../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)   
 [指定合并项目冲突解决程序](../../relational-databases/replication/publish/specify-a-merge-article-resolver.md)   
 [sp_registercustomresolver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-registercustomresolver-transact-sql.md)   
 [sp_unregistercustomresolver &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-unregistercustomresolver-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
