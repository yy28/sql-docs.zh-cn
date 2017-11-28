---
title: "sp_revoke_login_from_proxy (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_revoke_login_from_proxy_TSQL
- sp_revoke_login_from_proxy
dev_langs: TSQL
helpviewer_keywords: sp_revoke_login_from_proxy
ms.assetid: e4546c13-9fba-4bab-8b42-d6f18b33ec25
caps.latest.revision: "20"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: efb329d4bdbdaef250e9843ed1f4641d0a679181
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="sprevokeloginfromproxy-transact-sql"></a>sp_revoke_login_from_proxy (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  删除对安全主体服务器的代理的访问权。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_revoke_login_from_proxy   
    [ @name = ] 'name' ,  
    [ @proxy_id = ] id ,  
    [ @proxy_name = ] 'proxy_name'  
```  
  
## <a name="arguments"></a>参数  
 [  **@name=** ] *名称*  
 名称[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登录名、 服务器角色或**msdb**数据库角色，若要删除的访问权限。 *名称*是**nvarchar(256)**无默认值。  
  
 [  **@proxy_id=** ] *id*  
 要删除其访问权的代理的 ID。 任一*id*或*proxy_name*必须指定，但不能同时指定。 *Id*是**int**，默认值为 NULL。  
  
 [  **@proxy_name=** ] *proxy_name*  
 要删除其访问权的代理的名称。 任一*id*或*proxy_name*必须指定，但不能同时指定。 *Proxy_name*是**sysname**，默认值为 NULL。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 引用此代理的登录名所拥有的作业将无法运行。  
  
## <a name="permissions"></a>Permissions  
 若要执行此存储过程，用户必须为 **sysadmin** 固定服务器角色的成员。  
  
## <a name="examples"></a>示例  
 以下示例将撤消登录名 `terrid` 访问代理 `Catalog application proxy` 的访问权。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_revoke_login_from_proxy  
    @name = N'terrid',  
    @proxy_name = N'Catalog application proxy' ;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server 代理存储过程 &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [sp_grant_login_to_proxy &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-grant-login-to-proxy-transact-sql.md)   
 [sp_help_proxy &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-help-proxy-transact-sql.md)  
  
  
