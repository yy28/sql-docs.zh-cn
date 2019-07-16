---
title: sp_registercustomresolver (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_registercustomresolver
- sp_registercustomresolver_TSQL
helpviewer_keywords:
- sp_registercustomresolver
ms.assetid: 6d2b0472-0e1f-4005-833c-735d1940fe93
author: stevestein
ms.author: sstein
ms.openlocfilehash: 0d003cccfa6fdedd0610ea34f15acb6ee1833e5a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68075727"
---
# <a name="spregistercustomresolver-transact-sql"></a>sp_registercustomresolver (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  注册可在合并复制同步过程中调用的业务逻辑处理程序或基于 COM 的自定义冲突解决程序。 此存储过程在分发服务器上执行。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_registercustomresolver [ @article_resolver = ] 'article_resolver'   
    [ , [ @resolver_clsid = ] 'resolver_clsid' ]  
    [ , [ @is_dotnet_assembly = ] 'is_dotnet_assembly' ]  
    [ , [ @dotnet_assembly_name = ] 'dotnet_assembly_name' ]  
    [ , [ @dotnet_class_name = ] 'dotnet_class_name' ]  
```  
  
## <a name="arguments"></a>参数  
`[ @article_resolver = ] 'article_resolver'` 指定正在注册的自定义业务逻辑的友好名称。 *article_resolver*是**nvarchar(255)** ，无默认值。  
  
`[ @resolver_clsid = ] 'resolver_clsid'` 指定正在注册 COM 对象的 CLSID 值。 自定义业务逻辑*resolver_clsid*是**nvarchar （50)** ，默认值为 NULL。 在注册业务逻辑处理程序程序集时，必须将该参数设置为有效的 CLSID，或将其设置为 NULL。  
  
`[ @is_dotnet_assembly = ] 'is_dotnet_assembly'` 指定要注册的自定义业务逻辑的类型。 *is_dotnet_assembly*是**nvarchar （50)** ，默认值为 FALSE。 **true**指示正在注册的自定义业务逻辑是业务逻辑处理程序程序集;**false**指示它是一个 COM 组件。  
  
`[ @dotnet_assembly_name = ] 'dotnet_assembly_name'` 是实现业务逻辑处理程序的程序集的名称。 *dotnet_assembly_name*是**nvarchar(255)** ，默认值为 NULL。 如果该程序集未部署到与合并代理可执行文件相同的目录中、与同步启动合并代理的应用程序相同的目录中或全局程序集缓存 (GAC) 中，则必须指定该程序集的完整路径。  
  
`[ @dotnet_class_name = ] 'dotnet_class_name'` 是替代的类名称<xref:Microsoft.SqlServer.Replication.BusinessLogicSupport.BusinessLogicModule>实现业务逻辑处理程序。 名称应在窗体中指定**Namespace.Classname**。 *dotnet_class_name*是**nvarchar(255)** ，默认值为 NULL。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>备注  
 **sp_registercustomresolver**合并复制中使用。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的服务器角色或**db_owner**固定的数据库角色可以执行**sp_registercustomresolver**。  
  
## <a name="see-also"></a>请参阅  
 [为合并项目实现业务逻辑处理程序](../../relational-databases/replication/implement-a-business-logic-handler-for-a-merge-article.md)   
 [为合并项目实现自定义冲突解决程序](../../relational-databases/replication/implement-a-custom-conflict-resolver-for-a-merge-article.md)   
 [sp_lookupcustomresolver &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-lookupcustomresolver-transact-sql.md)   
 [sp_unregistercustomresolver &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-unregistercustomresolver-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
