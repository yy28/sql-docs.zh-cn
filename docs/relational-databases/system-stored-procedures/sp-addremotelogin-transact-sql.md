---
title: sp_addremotelogin (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_addremotelogin_TSQL
- sp_addremotelogin
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addremotelogin
ms.assetid: 71b7cd36-a17d-4b12-b102-10aeb0f9268b
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: e23684e04d8e49d1a6456185f94ad74b71b1604c
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52537933"
---
# <a name="spaddremotelogin-transact-sql"></a>sp_addremotelogin (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  在本地服务器上添加新的远程登录 ID。 这样，远程服务器就能够连接并执行远程过程调用。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)] 请改用链接服务器和链接服务器存储过程。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_addremotelogin [ @remoteserver = ] 'remoteserver'   
     [ , [ @loginame = ] 'login' ]   
     [ , [ @remotename = ] 'remote_name' ]  
```  
  
## <a name="arguments"></a>参数  
 [ @remoteserver **=** ] **'**_remoteserver_  
 远程登录名所适用的远程服务器的名称。 *remoteserver*是**sysname**，无默认值。 如果只有*remoteserver*指定，则上的所有用户*remoteserver*映射到本地服务器上具有相同名称的现有登录名。 对于本地服务器而言，远程服务器必须是已知的。 这是通过使用 sp_addserver 添加。 当上的用户*remoteserver*连接到正在运行的本地服务器[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]若要执行远程存储的过程，它们连接的匹配其自己的登录名的本地登录名作为*remoteserver*. *remoteserver*是用于启动远程过程调用的服务器。  
  
 [ @loginame **=** ] **'**_登录_  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 本地实例上的用户的登录 ID。 login 的数据类型为 sysname，默认值为 NULL。 *登录名*的本地实例上必须已存在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如果*登录名*指定，则上的所有用户*remoteserver*映射到该特定本地登录。 当上的用户*remoteserver*连接到的本地实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]若要执行远程存储的过程，这些连接作为*登录*。  
  
 [ @remotename **=** ] **'**_remote_name_  
 远程服务器上的用户的登录 ID。 *remote_name*是**sysname**，默认值为 NULL。 *remote_name*必须存在于*remoteserver*。 如果*remote_name*指定，则特定用户*remote_name*映射到*登录*本地服务器上。 当*remote_name*上*remoteserver*连接到的本地实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]以执行远程存储的过程，它将连接作为*登录*。 登录 ID *remote_name*可以不同于远程服务器上的登录 ID*登录名*。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="remarks"></a>备注  
 若要执行分布式的查询，请使用 sp_addlinkedsrvlogin。  
  
 不能在用户定义的事务内使用 sp_addremotelogin。  
  
## <a name="permissions"></a>权限  
 只有 sysadmin 和 securityadmin 固定服务器角色的成员可以执行 sp_addremotelogin。  
  
## <a name="examples"></a>示例  
  
### <a name="a-mapping-one-to-one"></a>A. 一对一映射  
 以下示例在远程服务器 `ACCOUNTS` 和本地服务器具有相同的用户登录名时将远程名称映射到本地名称。  
  
```  
EXEC sp_addremotelogin 'ACCOUNTS';  
```  
  
### <a name="b-mapping-many-to-one"></a>B. 多对一映射  
 以下示例创建一个条目，该条目将来自远程服务器 `ACCOUNTS` 的所有用户都映射到本地登录 ID `Albert`。  
  
```  
EXEC sp_addremotelogin 'ACCOUNTS', 'Albert';  
```  
  
### <a name="c-using-explicit-one-to-one-mapping"></a>C. 使用显式一对一映射  
 以下示例将来自远程服务器 `Chris` 上的远程用户 `ACCOUNTS` 的远程登录映射到本地用户 `salesmgr`。  
  
```  
EXEC sp_addremotelogin 'ACCOUNTS', 'salesmgr', 'Chris';  
```  
  
## <a name="see-also"></a>请参阅  
 [sp_addlinkedsrvlogin &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql.md)   
 [sp_addlogin (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addlogin-transact-sql.md)   
 [sp_addserver &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)   
 [sp_dropremotelogin &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropremotelogin-transact-sql.md)   
 [sp_grantlogin (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [sp_helpremotelogin &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpremotelogin-transact-sql.md)   
 [sp_helpserver (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [sp_remoteoption &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-remoteoption-transact-sql.md)   
 [sp_revokelogin (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
