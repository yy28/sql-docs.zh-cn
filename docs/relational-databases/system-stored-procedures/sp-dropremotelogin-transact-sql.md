---
title: sp_dropremotelogin (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_dropremotelogin
- sp_dropremotelogin_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dropremotelogin
ms.assetid: 9f097652-a286-40b2-be73-568d77ada698
caps.latest.revision: 30
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 7f1262ade6b92cdcac57df0397e9f6c57ee47c23
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
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
 [  **@remoteserver =** ] *****远程服务器*****  
 映射到要删除的远程登录名的远程服务器的名称。 *远程服务器*是**sysname**，无默认值。 *远程服务器*必须已存在。  
  
 [ **@loginame =** ] **'***login***'**  
 与远程服务器相关联的本地服务器上的可选登录名。 login 的数据类型为 sysname，默认值为 NULL。 *登录名*必须已存在，如果指定。  
  
 [  **@remotename =** ] *****remote_name*****  
 是映射到的远程登录名的可选名称*登录*从远程服务器在登录时。 *remote_name*是**sysname**，默认值为 NULL。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="remarks"></a>注释  
 如果仅*远程服务器*指定，则从本地服务器中删除该远程服务器的所有远程登录名。 如果*登录*也是从指定的所有远程登录名*远程服务器*从本地服务器中删除映射到该特定的本地登录名。 如果*remote_name*同时指定，则仅从该远程用户的远程登录*远程服务器*从本地服务器中删除。  
  
 若要添加本地服务器用户，请使用**sp_addlogin**。 若要删除本地服务器的用户，使用**sp_droplogin**。  
  
 仅当使用早期版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 时才需要远程登录。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0 及更高版本改用链接服务器登录。 使用**sp_addlinkedsrvlogin**和**sp_droplinkedsrvlogin**添加和删除链接的服务器登录名。  
  
 **sp_dropremotelogin**不能在用户定义的事务内执行。  
  
## <a name="permissions"></a>权限  
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
  
## <a name="see-also"></a>另请参阅  
 [安全存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addlinkedsrvlogin &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql.md)   
 [sp_addlogin (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addlogin-transact-sql.md)   
 [sp_addremotelogin &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-addremotelogin-transact-sql.md)   
 [sp_addserver &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)   
 [sp_droplinkedsrvlogin &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-droplinkedsrvlogin-transact-sql.md)   
 [sp_droplogin (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-droplogin-transact-sql.md)   
 [sp_helpremotelogin &#40;Transact SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpremotelogin-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
