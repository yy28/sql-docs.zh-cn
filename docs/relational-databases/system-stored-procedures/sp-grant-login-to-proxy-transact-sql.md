---
title: sp_grant_login_to_proxy （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_grant_login_to_proxy
- sp_grant_login_to_proxy_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_grant_login_to_proxy
ms.assetid: 90e1a6d5-a692-4462-a163-4b0709d83150
ms.author: vanto
author: VanMSFT
ms.openlocfilehash: bdfeab5754a2397c01ace2bb9f822fa168eeef6b
ms.sourcegitcommit: 454270de64347db917ebe41c081128bd17194d73
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/07/2019
ms.locfileid: "72005855"
---
# <a name="sp_grant_login_to_proxy-transact-sql"></a>sp_grant_login_to_proxy (Transact-SQL)

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
`[ @login_name = ] 'login_name'` 要向其授予访问权限的登录名。 *Login_name*为**nvarchar （256）** ，默认值为 NULL。 必须指定 **\@login_name**、 **\@fixed_server_role**或 **\@** msdb_role 之一，否则存储过程将失败。  
  
`[ @fixed_server_role = ] 'fixed_server_role'` 要向其授予访问权限的固定服务器角色。 *Fixed_server_role*为**nvarchar （256）** ，默认值为 NULL。 必须指定 **\@login_name**、 **\@fixed_server_role**或 **\@** msdb_role 之一，否则存储过程将失败。  
  
`[ @msdb_role = ] 'msdb_role'` **msdb**数据库中的数据库角色，以授予对的访问权限。 *Msdb_role*为**nvarchar （256）** ，默认值为 NULL。 必须指定 **\@login_name**、 **\@fixed_server_role**或 **\@** msdb_role 之一，否则存储过程将失败。  
  
`[ @proxy_id = ] id` 要为其授予访问权限的代理的标识符。 *Id*为**int**，默认值为 NULL。 必须指定 **\@proxy_id**或 **\@proxy_name**中的一个，否则存储过程将失败。  
  
`[ @proxy_name = ] 'proxy_name'` 要为其授予访问权限的代理的名称。 *Proxy_name*为**nvarchar （256）** ，默认值为 NULL。 必须指定 **\@proxy_id**或 **\@proxy_name**中的一个，否则存储过程将失败。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功）或**1** （失败）  
  
## <a name="remarks"></a>Remarks  
 必须从**msdb**数据库运行**sp_grant_login_to_proxy** 。  
  
## <a name="permissions"></a>Permissions  
 只有**sysadmin**固定服务器角色的成员才能**sp_grant_login_to_proxy**执行。  
  
## <a name="examples"></a>示例  
 以下示例允许登录 `adventure-works\terrid` 使用代理 `Catalog application proxy`。  
  
```sql
USE msdb ;  
GO  
  
EXEC dbo.sp_grant_login_to_proxy  
    @login_name = N'adventure-works\terrid',  
    @proxy_name = N'Catalog application proxy' ;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [sp_add_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-proxy-transact-sql.md)   
 [sp_revoke_login_from_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revoke-login-from-proxy-transact-sql.md)  
  
  
