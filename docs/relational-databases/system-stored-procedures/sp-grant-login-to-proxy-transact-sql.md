---
title: "sp_grant_login_to_proxy (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 08/09/2016
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
- sp_grant_login_to_proxy
- sp_grant_login_to_proxy_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_grant_login_to_proxy
ms.assetid: 90e1a6d5-a692-4462-a163-4b0709d83150
caps.latest.revision: "32"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a1d3fb0ea64fc6e6545c5eb5754853d667ff4110
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="spgrantlogintoproxy-transact-sql"></a>sp_grant_login_to_proxy (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  授予安全主体数据库访问代理的权限。  

  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_grant_login_to_proxy   
     { [ @login_name = ] 'login_name'   
     | [ @fixed_server_role = ] 'fixed_server_role'   
     | [ @msdb_role = ] 'msdb_role' } ,   
     { [ @proxy_id = ] id | [ @proxy_name = ] 'proxy_name' }  
```  
  
## <a name="arguments"></a>参数  
 [  **@login_name**  =] *login_name*  
 被授予访问权限的登录名。 *Login_name*是**nvarchar(256)**，默认值为 NULL。 之一 **@login_name** ，  **@fixed_server_role** ，或 **@msdb_role** 必须指定，或存储的过程将失败。  
  
 [  **@fixed_server_role** =] *fixed_server_role*  
 被授予访问权限的固定服务器角色。 *Fixed_server_role*是**nvarchar(256)**，默认值为 NULL。 之一 **@login_name** ，  **@fixed_server_role** ，或 **@msdb_role** 必须指定，或存储的过程将失败。  
  
 [  **@msdb_role** =] '*msdb_role*  
 中的数据库角色**msdb**数据库授予访问权限。 *Msdb_role*是**nvarchar(256)**，默认值为 NULL。 之一 **@login_name** ，  **@fixed_server_role** ，或 **@msdb_role** 必须指定，或存储的过程将失败。  
  
 [  **@proxy_id** =] *id*  
 访问权限被授予的代理的标识符。 *Id*是**int**，默认值为 NULL。 之一 **@proxy_id** 或 **@proxy_name** 必须指定，或存储的过程将失败。  
  
 [  **@proxy_name** =] *proxy_name*  
 要授予访问权限的代理的名称。 *Proxy_name*是**nvarchar(256)**，默认值为 NULL。 之一 **@proxy_id** 或 **@proxy_name** 必须指定，或存储的过程将失败。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 **sp_grant_login_to_proxy**必须从运行**msdb**数据库。  
  
## <a name="permissions"></a>Permissions  
 只有的成员**sysadmin**固定的服务器角色可能会执行**sp_grant_login_to_proxy**。  
  
## <a name="examples"></a>示例  
 下面的示例允许登录名`adventure-works\terrid`使用的代理`Catalog application proxy`。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_grant_login_to_proxy  
    @login_name = N'adventure-works\terrid',  
    @proxy_name = N'Catalog application proxy' ;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [sp_add_proxy &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-add-proxy-transact-sql.md)   
 [sp_revoke_login_from_proxy &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-revoke-login-from-proxy-transact-sql.md)  
  
  
