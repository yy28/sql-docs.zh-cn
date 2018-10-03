---
title: sp_addlogin (TRANSACT-SQL) |Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 7d6981879f08b65c334eae9cd81e73223bc353bf
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47724566"
---
# <a name="spaddlogin-transact-sql"></a>sp_addlogin (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  创建新的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名，该登录名允许用户使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 使用[CREATE LOGIN](../../t-sql/statements/create-login-transact-sql.md)相反。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
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
 [ @loginame=] '*登录名*  
 登录的名称。 *登录名*是**sysname**，无默认值。  
  
 [ @passwd= ] '*password*'  
 登录的密码。 *密码*是**sysname**，默认值为 NULL。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]  
  
 [ @defdb=] '*数据库*  
 登录的默认数据库（在登录后登录首先连接到该数据库）。 *数据库*是**sysname**，默认值为**主**。  
  
 [ @deflanguage=] '*语言*  
 登录的默认语言。 *语言*是**sysname**，默认值为 NULL。 如果*语言*未指定，默认*语言*的新登录名设置为服务器的当前默认语言。  
  
 [ @sid=] '*sid*  
 安全标识号 (SID)。 *sid*是**varbinary(16)**，默认值为 NULL。 如果*sid*为 NULL，则系统将生成新的登录名的 SID。 尽管使用**varbinary**数据类型，NULL 以外的值必须是 16 个字节的长度，并且不能已存在。 指定*sid*非常有用，例如，当您要编写脚本或移动[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]从一台服务器的登录名到另一个并且您想要在不同服务器上使用相同的 SID 的登录名。  
  
 [ @encryptopt=] '*encryption_option*  
 指定是以明文形式，还是以明文密码的哈希运算结果来传递密码。 注意，不进行加密。 在本讨论中使用“加密”一词是为了向后兼容。 如果传入明文密码，将对它进行哈希运算。 哈希值将存储起来。 *encryption_option*是**varchar （20)**，可以是下列值之一。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|NULL|以明文形式传递密码。 这是默认设置。|  
|**skip_encryption**|密码已经过哈希运算。 [!INCLUDE[ssDE](../../includes/ssde-md.md)]应存储值，且不对其重新进行哈希运算。|  
|**skip_encryption_old**|所提供的密码由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的早期版本进行哈希运算。 [!INCLUDE[ssDE](../../includes/ssde-md.md)]应存储值，且不对其重新进行哈希运算。 提供该选项只是为了升级。|  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="remarks"></a>备注  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名可以包含 1 到 128 个字符，其中包括字母、符号和数字。 登录名不能包含反斜杠 (\\); 可以是保留的登录名，例如 sa 或 public，或已经存在; 或者为 NULL 或空字符串 (`''`)。  
  
 如果提供默认数据库的名称，则不用执行 USE 语句就可以连接到指定的数据库。 但是，不能使用的默认数据库，直到你被授予访问权限的数据库由数据库所有者 (通过使用[sp_adduser](../../relational-databases/system-stored-procedures/sp-adduser-transact-sql.md)或[sp_addrolemember](../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md)) 或[sp_addrole](../../relational-databases/system-stored-procedures/sp-addrole-transact-sql.md).  
  
 SID 号是一个 GUID，用于唯一地标识服务器中的登录名。  
  
 更改服务器的默认语言将不会更改现有登录的默认语言。 若要更改服务器的默认语言，请使用[sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)。  
  
 使用**skip_encryption**来取消密码哈希非常有用如果时该登录名添加到已对密码[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 如果密码已哈希处理的早期版本的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，使用**skip_encryption_old**。  
  
 不能在用户定义事务内执行 sp_addlogin。  
  
 下表显示了数个与 sp_addlogin 一起使用的存储过程。  
  
|存储过程|Description|  
|----------------------|-----------------|  
|[sp_grantlogin](../../relational-databases/system-stored-procedures/sp-grantlogin-transact-sql.md)|添加 Windows 用户或组。|  
|[sp_password](../../relational-databases/system-stored-procedures/sp-password-transact-sql.md)|更改用户密码。|  
|[sp_defaultdb](../../relational-databases/system-stored-procedures/sp-defaultdb-transact-sql.md)|更改用户的默认数据库。|  
|[sp_defaultlanguage](../../relational-databases/system-stored-procedures/sp-defaultlanguage-transact-sql.md)|更改用户的默认语言。|  
  
## <a name="permissions"></a>Permissions  
 需要 ALTER ANY LOGIN 权限。  
  
## <a name="examples"></a>示例  
  
### <a name="a-creating-a-sql-server-login"></a>A. 创建 SQL Server 登录  
 以下示例为用户 `Victoria` 创建 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录，密码为 `B1r12-36`，并且不指定默认数据库。  
  
```  
EXEC sp_addlogin 'Victoria', 'B1r12-36';  
GO  
```  
  
### <a name="b-creating-a-sql-server-login-that-has-a-default-database"></a>B. 创建具有默认数据库的 SQL Server 登录  
 以下示例为用户 `Albert` 创建 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录，密码为 `B5432-3M6`，默认数据库为 `corporate`。  
  
```  
EXEC sp_addlogin 'Albert', 'B5432-3M6', 'corporate';  
GO  
```  
  
### <a name="c-creating-a-sql-server-login-that-has-a-different-default-language"></a>C. 创建具有不同默认语言的 SQL Server 登录  
 以下示例为用户 `TzTodorov` 创建 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录，密码为 `709hLKH7chjfwv`，默认数据库为 `AdventureWorks2012`，默认语言为 `Bulgarian`。  
  
```  
EXEC sp_addlogin 'TzTodorov', '709hLKH7chjfwv', 'AdventureWorks2012', N'български'  
```  
  
### <a name="d-creating-a-sql-server-login-that-has-a-specific-sid"></a>D. 创建具有特定 SID 的 SQL Server 登录  
 以下示例为用户 `Michael` 创建 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名，密码为 `B548bmM%f6`，默认数据库为 `AdventureWorks2012`，默认语言为 `us_english`，SID 为 `0x0123456789ABCDEF0123456789ABCDEF`。  
  
```  
EXEC sp_addlogin 'Michael', 'B548bmM%f6', 'AdventureWorks2012', 'us_english', 0x0123456789ABCDEF0123456789ABCDEF  
```  
  
## <a name="see-also"></a>请参阅  
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [sp_droplogin (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-droplogin-transact-sql.md)   
 [sp_helpuser &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md)   
 [sp_revokelogin (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-revokelogin-transact-sql.md)   
 [xp_logininfo &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/xp-logininfo-transact-sql.md)  
  
  
