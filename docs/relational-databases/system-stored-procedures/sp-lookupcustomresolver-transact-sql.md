---
title: "sp_lookupcustomresolver (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- sp_lookupcustomresolver_TSQL
- sp_lookupcustomresolver
helpviewer_keywords:
- sp_lookupcustomresolver
ms.assetid: 356a7b8a-ae53-4fb5-86ee-fcfddbf23ddd
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: df262bcf0d12d99b2c16b7eeff18cbc80c151ad8
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="splookupcustomresolver-transact-sql"></a>sp_lookupcustomresolver (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回在分发服务器上注册的基于 COM 的自定义冲突解决程序组件的业务逻辑处理程序或类标识符 (CLSID) 值的相关信息。 在发布服务器的发布数据库上执行此存储的过程。  
  
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
 [  **@article_resolver =** ] *article_resolver*  
 指定要注销的自定义业务逻辑的名称。 *article_resolver*是**nvarchar （255)**，无默认值。 如果被删除的业务逻辑是 COM 组件，则此参数是该组件的友好名称。 如果业务逻辑是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] .NET Framework 程序集，则此参数是该程序集的名称。  
  
 [  **@resolver_clsid** =] *resolver_clsid*输出  
 是中指定的自定义业务逻辑的名称与关联的 COM 对象的 CLSID 值*article_resolver*参数。 *resolver_clsid*是**nvarchar(50)**，默认值为 NULL。  
  
 [  **@is_dotnet_assembly=** ] *is_dotnet_assembly*输出  
 指定要注册的自定义业务逻辑的类型。 *is_dotnet_assembly*是**位**，默认值为 0。 **1**指示要注册的自定义业务逻辑是业务逻辑处理程序程序集;**0**指示它是一个 COM 组件。  
  
 [  **@dotnet_assembly_name=** ] *dotnet_assembly_name*输出  
 实现业务逻辑处理程序的程序集的名称。 *dotnet_assembly_name*是**nvarchar （255)**，默认值为 NULL。  
  
 [  **@dotnet_class_name=** ] *dotnet_class_name*输出  
 实现业务逻辑处理程序时优先级高于 <xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule> 的类的名称。 *dotnet_class_name*是**nvarchar （255)**，默认值为 NULL。  
  
 [  **@publisher=** ] *发布服务器*  
 发布服务器的名称。 *发布服务器*是**sysname**，默认值为 NULL。 未从发布服务器调用该存储过程时使用此参数。 如果未指定，则假定本地服务器是发布服务器。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 **sp_lookupcustomresolver**合并复制中使用。  
  
 **sp_lookupcustomresolver**返回的 NULL 值*resolver_clsid*组件未注册时在分发和值为"00000000-0000-0000-0000-000000000000"时注册属于.NET framework 程序集注册为业务逻辑处理程序。  
  
 **sp_lookupcustomresolver**由调用[sp_addmergearticle](../../relational-databases/system-stored-procedures/sp-addmergearticle-transact-sql.md)和[sp_changemergearticle](../../relational-databases/system-stored-procedures/sp-changemergearticle-transact-sql.md)来验证指定*article_resolver*。  
  
## <a name="permissions"></a>Permissions  
 只有的成员**db_owner**发布数据库上的固定的数据库角色可以执行**sp_lookupcustomresolver**。  
  
## <a name="see-also"></a>另请参阅  
 [Advanced Merge Replication Conflict Detection and Resolution](../../relational-databases/replication/merge/advanced-merge-replication-conflict-detection-and-resolution.md)   
 [在合并同步期间执行业务逻辑](../../relational-databases/replication/merge/execute-business-logic-during-merge-synchronization.md)   
 [为合并项目实现业务逻辑处理程序](../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)   
 [指定合并项目冲突解决程序](../../relational-databases/replication/publish/specify-a-merge-article-resolver.md)   
 [sp_registercustomresolver &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-registercustomresolver-transact-sql.md)   
 [sp_unregistercustomresolver &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-unregistercustomresolver-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
