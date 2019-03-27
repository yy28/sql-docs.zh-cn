---
title: sp_add_proxy (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_add_proxy
- sp_add_proxy_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE PROXY statement
- sp_add_proxy
ms.assetid: cb59df37-f103-439b-bec1-2871fb669a8b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 247c834abfbc47485628702bf4cd87c7662c44a8
ms.sourcegitcommit: 2db83830514d23691b914466a314dfeb49094b3c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58494269"
---
# <a name="spaddproxy-transact-sql"></a>sp_add_proxy (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  添加指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理的代理。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_add_proxy  
    [ @proxy_name = ] 'proxy_name' ,  
    [ @enabled = ] is_enabled ,  
    [ @description = ] 'description' ,  
    [ @credential_name = ] 'credential_name' ,  
    [ @credential_id = ] credential_id ,  
    [ @proxy_id = ] id OUTPUT   
```  
  
## <a name="arguments"></a>参数  
`[ @proxy_name = ] 'proxy_name'` 要创建的代理的名称。 *Proxy_name*是**sysname**，默认值为 NULL。 当*proxy_name*为 NULL 或空字符串，该代理默认名称*user_name*提供。  
  
`[ @enabled = ] is_enabled` 指定是否启用代理。 *Is_enabled*标志**tinyint**，默认值为 1。 当*is_enabled*是**0**，代理未启用，并不能由作业步骤。  
  
`[ @description = ] 'description'` 代理服务器的说明。 该说明仅**nvarchar(512)**，默认值为 NULL。 该说明便于您记录代理，而 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代理不会在其他地方使用该说明。 因此，该参数是可选的。  
  
`[ @credential_name = ] 'credential_name'` 代理的凭据的名称。 *Credential_name*是**sysname**，默认值为 NULL。 任一*credential_name*或*credential_id*必须指定。  
  
`[ @credential_id = ] credential_id` 代理凭据的标识号。 *Credential_id*是**int**，默认值为 NULL。 任一*credential_name*或*credential_id*必须指定。  
  
`[ @proxy_id = ] id OUTPUT` 如果成功创建分配到代理的代理标识号。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="result-sets"></a>结果集  
 None  
  
## <a name="remarks"></a>备注  
 必须运行此存储的过程**msdb**数据库。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent 代理的代理帐户用于管理作业步骤的安全性，这些作业步骤涉及除 [!INCLUDE[tsql](../../includes/tsql-md.md)] 子系统以外的其他子系统。 每个代理对应于一个安全凭据。 代理可以访问任何数量的子系统。  
  
## <a name="permissions"></a>权限  
 只有的成员**sysadmin**固定的安全角色才能执行此过程。  
  
 成员**sysadmin**固定的安全角色可以创建使用任何代理的作业步骤。 使用存储的过程[sp_grant_login_to_proxy &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-grant-login-to-proxy-transact-sql.md)向代理授予其他登录访问权限。  
  
## <a name="examples"></a>示例  
 该示例为 `CatalogApplicationCredential` 凭据创建一个代理。 代码假定凭据已经存在。 有关凭据的详细信息，请参阅[CREATE CREDENTIAL &#40;TRANSACT-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_add_proxy  
    @proxy_name = 'Catalog application proxy',  
    @enabled = 1,  
    @description = 'Maintenance tasks on catalog application.',  
    @credential_name = 'CatalogApplicationCredential' ;  
GO  
```  
  
## <a name="see-also"></a>请参阅  
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [sp_grant_login_to_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grant-login-to-proxy-transact-sql.md)   
 [sp_revoke_login_from_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revoke-login-from-proxy-transact-sql.md)  
  
  
