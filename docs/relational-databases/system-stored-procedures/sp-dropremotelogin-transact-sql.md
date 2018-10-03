---
title: sp_dropremotelogin (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_dropremotelogin
- sp_dropremotelogin_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dropremotelogin
ms.assetid: 9f097652-a286-40b2-be73-568d77ada698
ms.author: vanto
manager: craigg
ms.openlocfilehash: a834dbb26bfc8c712531084e528f82bba50cd05e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47800695"
---
# <a name="spdropremotelogin-transact-sql"></a>sp_dropremotelogin (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  删除映射到本地登录名的远程登录名，该登录名用于针对运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的本地服务器执行远程存储过程。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)] 请改用链接的服务器和链接服务器存储的过程。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_dropremotelogin [ @remoteserver = ] 'remoteserver'   
     [ , [ @loginame = ] 'login' ]   
     [ , [ @remotename = ] 'remote_name' ]  
```  
  
## <a name="arguments"></a>参数  
 [  **@remoteserver =** ] **'***remoteserver*****  
 映射到要删除的远程登录名的远程服务器的名称。 *remoteserver*是**sysname**，无默认值。 *remoteserver*必须已经存在。  
  
 [ **@loginame =** ] **'***login***'**  
 与远程服务器相关联的本地服务器上的可选登录名。 login 的数据类型为 sysname，默认值为 NULL。 *登录名*必须已经存在，如果指定。  
  
 [  **@remotename =** ] **'***remote_name*****  
 是映射到的远程登录名的可选名称*登录名*时从远程服务器登录。 *remote_name*是**sysname**，默认值为 NULL。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="remarks"></a>备注  
 如果只有*remoteserver*指定，则从本地服务器中删除该远程服务器的所有远程登录。 如果*登录名*也是从指定的所有远程登录名*remoteserver*从本地服务器中删除映射到该特定本地登录名。 如果*remote_name*同时指定，则仅从该远程用户的远程登录名*remoteserver*从本地服务器中删除。  
  
 若要添加本地服务器用户，请使用**sp_addlogin**。 若要删除本地服务器用户，请使用**sp_droplogin**。  
  
 仅当使用早期版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 时才需要远程登录。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 及更高版本改用链接服务器登录。 使用**sp_addlinkedsrvlogin**并**sp_droplinkedsrvlogin**添加和删除链接的服务器登录名。  
  
 **sp_dropremotelogin**不能在用户定义的事务内执行。  
  
## <a name="permissions"></a>Permissions  
 要求的成员身份**sysadmin**或**securityadmin**固定服务器角色的成员。  
  
## <a name="examples"></a>示例  
  
### <a name="a-dropping-all-remote-logins-for-a-remote-server"></a>A. 删除远程服务器的所有远程登录  
 以下示例删除远程服务器 `ACCOUNTS` 的条目，因此将删除本地服务器中的登录和远程服务器中远程登录之间的所有映射。  
  
```  
EXEC sp_dropremotelogin 'ACCOUNTS';  
```  
  
### <a name="b-dropping-a-login-mapping"></a>B. 删除登录映射  
 以下示例删除一个映射的条目，该条目将来自远程服务器 `ACCOUNTS` 的远程登录映射到本地登录 `Albert`。  
  
```  
EXEC sp_dropremotelogin 'ACCOUNTS', 'Albert';  
```  
  
### <a name="c-dropping-a-remote-user"></a>C. 删除远程用户  
 以下示例删除远程服务器 `Chris` 上的远程登录 `ACCOUNTS`。该远程服务器被映射到本地登录 `salesmgr`。  
  
```  
EXEC sp_dropremotelogin 'ACCOUNTS', 'salesmgr', 'Chris';  
```  
  
## <a name="see-also"></a>请参阅  
 [安全存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addlinkedsrvlogin &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql.md)   
 [sp_addlogin (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addlogin-transact-sql.md)   
 [sp_addremotelogin &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addremotelogin-transact-sql.md)   
 [sp_addserver &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)   
 [sp_droplinkedsrvlogin &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-droplinkedsrvlogin-transact-sql.md)   
 [sp_droplogin (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-droplogin-transact-sql.md)   
 [sp_helpremotelogin &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpremotelogin-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
