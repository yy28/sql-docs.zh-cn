---
title: sp_addlogin （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_addlogin
- sp_addlogin_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addlogin
ms.assetid: 030f19c3-a5e3-4b53-bfc4-de4bfca0fddc
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 5868120af1e98c4b2f3be78f2cf7927df53b42d1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68072666"
---
# <a name="sp_addlogin-transact-sql"></a>sp_addlogin (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  创建新的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名，该登录名允许用户使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]请改用[CREATE LOGIN](../../t-sql/statements/create-login-transact-sql.md) 。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_addlogin [ @loginame = ] 'login'   
    [ , [ @passwd = ] 'password' ]   
    [ , [ @defdb = ] 'database' ]   
    [ , [ @deflanguage = ] 'language' ]   
    [ , [ @sid = ] sid ]   
    [ , [ @encryptopt = ] 'encryption_option' ]   
[;]  
```  
  
## <a name="arguments"></a>参数  
 [ @loginame= ]"*login*"  
 登录的名称。 *login*的**sysname**为，无默认值。  
  
 [ @passwd= ]'*password*'  
 登录的密码。 *password*的值为**sysname**，默认值为 NULL。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]  
  
 [ @defdb= ]"*数据库*"  
 登录的默认数据库（在登录后登录首先连接到该数据库）。 *数据库*为**sysname**，默认值为**master**。  
  
 [ @deflanguage= ]"*language*"  
 登录的默认语言。 *language*的值为**sysname**，默认值为 NULL。 如果未指定*语言*，则新登录名的默认*语言*将设置为服务器的当前默认语言。  
  
 [ @sid= ]"*sid*"  
 安全标识号 (SID)。 *sid*为**varbinary （16）**，默认值为 NULL。 如果*sid*为 NULL，则系统将为新登录生成 sid。 尽管使用**varbinary**数据类型，但 NULL 以外的值的长度必须正好是16个字节，并且不能已经存在。 指定*sid*很有用，例如，在编写脚本或将登录名[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]从一台服务器移动到另一台服务器，并希望登录名在不同服务器上具有相同的 sid。  
  
 [ @encryptopt= ]"*encryption_option*"  
 指定是以明文形式，还是以明文密码的哈希运算结果来传递密码。 注意，不进行加密。 在本讨论中使用“加密”一词是为了向后兼容。 如果传入明文密码，将对它进行哈希运算。 哈希值将存储起来。 *encryption_option*为**varchar （20）**，可以是下列值之一。  
  
|值|说明|  
|-----------|-----------------|  
|Null|以明文形式传递密码。 这是默认值。|  
|**skip_encryption**|密码已经过哈希运算。 
  [!INCLUDE[ssDE](../../includes/ssde-md.md)]应存储值，且不对其重新进行哈希运算。|  
|**skip_encryption_old**|所提供的密码由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的早期版本进行哈希运算。 
  [!INCLUDE[ssDE](../../includes/ssde-md.md)]应存储值，且不对其重新进行哈希运算。 提供该选项只是为了升级。|  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="remarks"></a>备注  
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名可以包含 1 到 128 个字符，其中包括字母、符号和数字。 登录名不能包含反\\斜杠（）;保留登录名，例如 sa 或 public，或已经存在;或为 NULL 或空字符串（`''`）。  
  
 如果提供默认数据库的名称，则不用执行 USE 语句就可以连接到指定的数据库。 但是，您不能使用默认数据库，除非数据库所有者（通过使用[sp_adduser](../../relational-databases/system-stored-procedures/sp-adduser-transact-sql.md)或[sp_addrolemember](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)）或[sp_addrole](../../relational-databases/system-stored-procedures/sp-addrole-transact-sql.md)向您授予对该数据库的访问权限。  
  
 SID 号是一个 GUID，用于唯一地标识服务器中的登录名。  
  
 更改服务器的默认语言将不会更改现有登录的默认语言。 若要更改服务器的默认语言，请使用[sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)。  
  
 如果**** 在将登录名添加到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]时已对密码进行哈希处理，则使用 skip_encryption 取消密码哈希会很有用。 如果密码是由早期版本的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]进行哈希处理的，请使用**skip_encryption_old**。  
  
 不能在用户定义事务内执行 sp_addlogin。  
  
 下表显示了数个与 sp_addlogin 一起使用的存储过程。  
  
|存储过程|说明|  
|----------------------|-----------------|  
|[sp_grantlogin](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)|添加 Windows 用户或组。|  
|[sp_password](../../relational-databases/system-stored-procedures/sp-password-transact-sql.md)|更改用户密码。|  
|[sp_defaultdb](../../relational-databases/system-stored-procedures/sp-defaultdb-transact-sql.md)|更改用户的默认数据库。|  
|[sp_defaultlanguage](../../relational-databases/system-stored-procedures/sp-defaultlanguage-transact-sql.md)|更改用户的默认语言。|  
  
## <a name="permissions"></a>权限  
 需要 ALTER ANY LOGIN 权限。  
  
## <a name="examples"></a>示例  
  
### <a name="a-creating-a-sql-server-login"></a>A. 创建 SQL Server 登录  
 以下示例为用户 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 创建 `Victoria` 登录，密码为 `B1r12-36`，并且不指定默认数据库。  
  
```  
EXEC sp_addlogin 'Victoria', 'B1r12-36';  
GO  
```  
  
### <a name="b-creating-a-sql-server-login-that-has-a-default-database"></a>B. 创建具有默认数据库的 SQL Server 登录  
 以下示例为用户 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 创建 `Albert` 登录，密码为 `B5432-3M6`，默认数据库为 `corporate`。  
  
```  
EXEC sp_addlogin 'Albert', 'B5432-3M6', 'corporate';  
GO  
```  
  
### <a name="c-creating-a-sql-server-login-that-has-a-different-default-language"></a>C. 创建具有不同默认语言的 SQL Server 登录  
 以下示例为用户 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 创建 `TzTodorov` 登录，密码为 `709hLKH7chjfwv`，默认数据库为 `AdventureWorks2012`，默认语言为 `Bulgarian`。  
  
```  
EXEC sp_addlogin 'TzTodorov', '709hLKH7chjfwv', 'AdventureWorks2012', N'български'  
```  
  
### <a name="d-creating-a-sql-server-login-that-has-a-specific-sid"></a>D. 创建具有特定 SID 的 SQL Server 登录  
 以下示例为用户 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 创建 `Michael` 登录名，密码为 `B548bmM%f6`，默认数据库为 `AdventureWorks2012`，默认语言为 `us_english`，SID 为 `0x0123456789ABCDEF0123456789ABCDEF`。  
  
```  
EXEC sp_addlogin 'Michael', 'B548bmM%f6', 'AdventureWorks2012', 'us_english', 0x0123456789ABCDEF0123456789ABCDEF  
```  
  
## <a name="see-also"></a>另请参阅  
 [CREATE LOGIN &#40;Transact-sql&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [sp_droplogin &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-droplogin-transact-sql.md)   
 [sp_helpuser &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md)   
 [sp_revokelogin &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)   
 [xp_logininfo &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/xp-logininfo-transact-sql.md)  
  
  
