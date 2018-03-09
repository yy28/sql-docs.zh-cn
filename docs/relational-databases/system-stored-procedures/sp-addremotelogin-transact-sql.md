---
title: "sp_addremotelogin (TRANSACT-SQL) |Microsoft 文档"
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
- sp_addremotelogin_TSQL
- sp_addremotelogin
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addremotelogin
ms.assetid: 71b7cd36-a17d-4b12-b102-10aeb0f9268b
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5024781fdcfb26420432e3eae914dc1ae6c1f958
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2017
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
 [ @remoteserver  **=**  ] *远程服务器*  
 远程登录名所适用的远程服务器的名称。 *远程服务器*是**sysname**，无默认值。 如果仅*远程服务器*指定，则上的所有用户*远程服务器*映射到本地服务器上具有相同名称的现有登录名。 对于本地服务器而言，远程服务器必须是已知的。 这是通过使用 sp_addserver 添加。 当上的用户*远程服务器*连接到正在运行的本地服务器[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]若要执行远程存储的过程，这些连接与本地登录名相匹配他们自己的登录*远程服务器*. *远程服务器*是启动远程过程调用的服务器。  
  
 [ @loginame  **=**  ] *登录*  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 本地实例上的用户的登录 ID。 *登录名*是**sysname**，默认值为 NULL。 *登录名*必须已经存在的本地实例上[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如果*登录*指定，则上的所有用户*远程服务器*映射到该特定的本地登录名。 当上的用户*远程服务器*连接到的本地实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]若要执行远程存储的过程，它们连接作为*登录*。  
  
 [ @remotename  **=**  ] *remote_name*  
 远程服务器上的用户的登录 ID。 *remote_name*是**sysname**，默认值为 NULL。 *remote_name*上必须存在*远程服务器*。 如果*remote_name*指定，则特定用户*remote_name*映射到*登录*本地服务器上。 当*remote_name*上*远程服务器*连接到的本地实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]若要执行远程存储的过程，它将作为连接*登录*。 登录 ID 的*remote_name*可以不同于在远程服务器上，登录 ID*登录*。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="remarks"></a>注释  
 若要执行分布式的查询，使用 sp_addlinkedsrvlogin。  
  
 sp_addremotelogin 不能在用户定义的事务。  
  
## <a name="permissions"></a>Permissions  
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
  
## <a name="see-also"></a>另请参阅  
 [sp_addlinkedsrvlogin &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql.md)   
 [sp_addlogin (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addlogin-transact-sql.md)   
 [sp_addserver &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-addserver-transact-sql.md)   
 [sp_dropremotelogin &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-dropremotelogin-transact-sql.md)   
 [sp_grantlogin (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)   
 [sp_helpremotelogin &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-helpremotelogin-transact-sql.md)   
 [sp_helpserver (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [sp_remoteoption &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/sp-remoteoption-transact-sql.md)   
 [sp_revokelogin (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
