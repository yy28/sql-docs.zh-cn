---
title: sp_update_proxy (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_update_proxy
- sp_update_proxy_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER PROXY statement
- sp_update_proxy
ms.assetid: 864fd0e6-9d61-4f07-92ef-145318d2f881
caps.latest.revision: 30
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 31154f48d9d13e6ebb67b25919a45ff7a1f7db8b
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "40394844"
---
# <a name="spupdateproxy-transact-sql"></a>sp_update_proxy (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  更改现有代理的属性。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_update_proxy   
    [ @proxy_id = ] id,  
    [ @proxy_name = ] 'proxy_name',  
    [ @credential_name = ] 'credential_name' ,  
    [ @credential_id = ] credential_id ,  
    [ @new_name = ] 'new_name' ,  
    [ @enabled = ] is_enabled ,  
    [ @description = ] 'description'  
```  
  
## <a name="arguments"></a>参数  
 [ **@proxy_id**= ] *id*  
 要更改的代理的代理标识号。 *Proxy_id*是**int**，默认值为 NULL。  
  
 [ **@proxy_name**= ] **'***proxy_name***'**  
 要更改的代理的名称。 *Proxy_name*是**sysname**，默认值为 NULL。  
  
 [ **@credential_name** =] **'***credential_name*****  
 代理的新凭据的名称。 *Credential_name*是**sysname**，默认值为 NULL。 任一*credential_name*或*credential_id*可能指定。  
  
 [ **@credential_id** = ] *credential_id*  
 代理的新凭据的标识号。 *Credential_id*是**int**，默认值为 NULL。 任一*credential_name*或*credential_id*可能指定。  
  
 [ **@new_name**=] **'***new_name*****  
 代理的新名称。 *New_name*是**sysname**，默认值为 NULL。 如果提供，则过程将更改为代理的名称*new_name*。 当此参数为 NULL 时，代理名称保持不变。  
  
 [ **@enabled** = ] *is_enabled*  
 是否启用代理。 *Is_enabled*标志**tinyint**，默认值为 NULL。 当*is_enabled*是**0**，代理未启用，并不能由作业步骤。 当此参数为 NULL 时，代理的状态保持不变。  
  
 [ **@description**=] **'***说明*****  
 代理的新说明。 *描述*是**nvarchar(512)**，默认值为 NULL。 当此参数为 NULL 时，代理的说明保持不变。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>Remarks  
 任一**@proxy_name**或**@proxy_id**必须指定。 如果同时指定这两个参数，这两个参数必须引用相同的代理，否则存储过程会失败。  
  
 任一**@credential_name**或**@credential_id**必须指定要更改代理的凭据。 如果两个参数均被指定，则它们必须引用相同的凭据，否则存储过程将失败。  
  
 此过程将更改代理，但不更改对代理的访问权限。 若要更改对代理服务器访问权限，请使用**sp_grant_login_to_proxy**并**sp_revoke_login_from_proxy**。  
  
## <a name="permissions"></a>Permissions  
 只有的成员**sysadmin**固定的安全角色才能执行此过程。  
  
## <a name="examples"></a>示例  
 以下示例将代理 `Catalog application proxy` 的 enabled 值设置为 `0`。  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_update_proxy  
    @proxy_name = 'Catalog application proxy',  
    @enabled = 0;  
GO  
```  
  
## <a name="see-also"></a>请参阅  
 [SQL Server 代理存储过程&#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sql-server-agent-stored-procedures-transact-sql.md)   
 [实现 SQL Server 代理安全性](../../ssms/agent/implement-sql-server-agent-security.md)   
 [sp_add_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-proxy-transact-sql.md)   
 [sp_delete_proxy &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-delete-proxy-transact-sql.md)   
 [sp_grant_login_to_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-grant-login-to-proxy-transact-sql.md)   
 [sp_revoke_login_from_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-revoke-login-from-proxy-transact-sql.md)  
  
  
