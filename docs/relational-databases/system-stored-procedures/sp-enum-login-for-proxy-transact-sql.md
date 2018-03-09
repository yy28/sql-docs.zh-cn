---
title: sp_enum_login_for_proxy (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_enum_login_for_proxy_TSQL
- sp_enum_login_for_proxy
dev_langs:
- TSQL
helpviewer_keywords:
- sp_enum_login_for_proxy
ms.assetid: 62a75019-248a-44c8-a5cc-c79f55ea3acf
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8235a8c0fa9febcad446f9a6c48eecf6c470d592
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2018
---
# <a name="spenumloginforproxy-transact-sql"></a>sp_enum_login_for_proxy (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  列出安全主体服务器和代理服务器之间的关联。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_enum_login_for_proxy  
    [ @name = ] 'name'  
    [ @proxy_id = ] id,  
    [ @proxy_name = ] 'proxy_name'  
```  
  
## <a name="arguments"></a>参数  
 [ **@name**= ] '*name*'  
 名称[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]主体、 登录名、 服务器角色或**msdb**到列表的代理的数据库角色。 名称是**nvarchar(256)**，默认值为 NULL。  
  
 [ **@proxy_id**= ] *id*  
 要列出信息的代理的代理标识号。 *Proxy_id*是**int**，默认值为 NULL。 任一*id*或*proxy_name*可指定。  
  
 [ **@proxy_name**= ] **'***proxy_name***'**  
 要列出信息的代理的名称。 *Proxy_name*是**sysname**，默认值为 NULL。 任一*id*或*proxy_name*可指定。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="result-sets"></a>结果集  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**proxy_id**|**int**|代理服务器标识号。|  
|**proxy_name**|**sysname**|代理服务器的名称。|  
|**名称**|**sysname**|关联的安全主体服务器的名称。|  
|**flags**|**int**|安全主体服务器的类型。<br /><br /> **0**  =  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登录名<br /><br /> **1** = 固定的系统角色<br /><br /> **2** = 中的数据库角色**msdb**|  
  
## <a name="remarks"></a>注释  
 当未提供参数时， **sp_enum_login_for_proxy**列出有关实例中的所有登录名为每个代理的信息。  
  
 如果代理 id 或代理服务器名称，则**sp_enum_login_for_proxy**列出有权访问代理的登录名。 如果登录名，则**sp_enum_login_for_proxy**的代理的登录帐户具有访问权限的列表。  
  
 当同时提供代理信息和登录名时，如果指定的登录有权访问指定的代理，则结果集将返回一行。  
  
 此存储的过程位于**msdb**。  
  
## <a name="permissions"></a>权限  
 此过程默认值的成员的执行权限**sysadmin**固定的服务器角色。  
  
## <a name="examples"></a>示例  
  
### <a name="a-listing-all-associations"></a>A. 列出所有关联  
 以下示例列出了在当前实例的登录和代理之间建立的所有权限。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_enum_login_for_proxy ;  
GO  
```  
  
### <a name="b-listing-proxies-for-a-specific-login"></a>B. 列出特定登录的代理  
 以下示例列出了登录 `terrid` 有权访问的代理。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_enum_login_for_proxy  
    @name = 'terrid' ;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [sp_help_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-proxy-transact-sql.md)   
 [sp_grant_login_to_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grant-login-to-proxy-transact-sql.md)   
 [sp_revoke_login_from_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revoke-login-from-proxy-transact-sql.md)  
  
  
