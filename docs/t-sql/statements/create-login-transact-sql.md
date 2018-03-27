---
title: CREATE LOGIN (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- CREATE_LOGIN_TSQL
- CREATE LOGIN
- LOGIN_TSQL
- LOGIN
dev_langs:
- TSQL
helpviewer_keywords:
- passwords [SQL Server], logins
- mapping logins [SQL Server]
- logins [SQL Server], creating
- CREATE LOGIN statement
- permissions [SQL Server], logins
- Windows domain accounts [SQL Server]
- re-hashing passwords
- certificates [SQL Server], logins
ms.assetid: eb737149-7c92-4552-946b-91085d8b1b01
caps.latest.revision: ''
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 87b7859980292cd8c6bf50f72c59b3cd3125800e
ms.sourcegitcommit: 3ed9be04cc7fb9ab1a9ec230c298ad2932acc71b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/17/2018
---
# <a name="create-login-transact-sql"></a>CREATE LOGIN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  为 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 创建[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]登录名。  

[!INCLUDE[ssMIlimitation](../../includes/sql-db-mi-limitation.md)]

 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
-- Syntax for SQL Server  
  
CREATE LOGIN login_name { WITH <option_list1> | FROM <sources> }  
  
<option_list1> ::=   
    PASSWORD = { 'password' | hashed_password HASHED } [ MUST_CHANGE ]  
    [ , <option_list2> [ ,... ] ]  
  
<option_list2> ::=    
    SID = sid  
    | DEFAULT_DATABASE = database      
    | DEFAULT_LANGUAGE = language  
    | CHECK_EXPIRATION = { ON | OFF}  
    | CHECK_POLICY = { ON | OFF}  
    | CREDENTIAL = credential_name   
  
<sources> ::=  
    WINDOWS [ WITH <windows_options>[ ,... ] ]  
    | CERTIFICATE certname  
    | ASYMMETRIC KEY asym_key_name  
  
<windows_options> ::=        
    DEFAULT_DATABASE = database  
    | DEFAULT_LANGUAGE = language  
```  
  
```  
-- Syntax for Azure SQL Database and Azure SQL Data Warehouse  
  
CREATE LOGIN login_name  
 { WITH <option_list3> }  
  
<option_list3> ::=   
    PASSWORD = { 'password' }  
    [ SID = sid ]  
```  
  
```  
-- Syntax for Parallel Data Warehouse  
  
CREATE LOGIN loginName { WITH <option_list1> | FROM WINDOWS }  
  
<option_list1> ::=   
    PASSWORD = { 'password' } [ MUST_CHANGE ]  
    [ , <option_list2> [ ,... ] ]  
  
<option_list2> ::=    
      CHECK_EXPIRATION = { ON | OFF}  
    | CHECK_POLICY = { ON | OFF}  
```  
  
## <a name="arguments"></a>参数  
 login_name  
 指定创建的登录名。 有四种类型的登录名：[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名、Windows 登录名、证书映射登录名和非对称密钥映射登录名。 在创建从 Windows 域帐户映射的登录名时，必须以 [\<domainName>\\<login_name>] 格式使用 Windows 2000 之前的用户登录名。 不能使用 login_name@DomainName 格式的 UPN。 有关示例，请参阅本主题后面的示例 D。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证登录名的类型为 sysname，它必须符合[标识符](http://msdn.microsoft.com/library/ms175874.aspx)规则，且不能包含“\\”。 Windows 登录名可以包含“\\”。 Active Directory 用户的登录名需少于 21 个字符。  
  
 PASSWORD ='password'****  
 仅适用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名。 指定正在创建的登录名的密码。 应使用强密码。 有关详细信息，请参阅[强密码](../../relational-databases/security/strong-passwords.md)和[密码策略](../../relational-databases/security/password-policy.md)。 从 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 开始，存储的密码信息使用 SHA-512 加盐密码进行计算。  
  
 密码是区分大小写的。 密码应始终至少包含 8 个字符，并且不能超过 128 个字符。  密码可以包含 a-z、A-Z、0-9 和大多数非字母数字字符。 密码不能包含单引号或 login_name。  
  
 PASSWORD =hashed_password  
 **适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 仅适用于 HASHED 关键字。 指定要创建的登录名的密码的哈希值。  
  
 HASHED  
 **适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 仅适用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名。 指定在 PASSWORD 参数后输入的密码已经过哈希运算。 如果未选择此选项，则在将作为密码输入的字符串存储到数据库中之前，对其进行哈希运算。 此选项应仅用于在服务器之间迁移数据库。 切勿使用 HASHED 选项创建新的登录名。 HASHED 选项不能用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7 或更早版本创建的哈希。  
  
 MUST_CHANGE  
 **适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 仅适用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名。 如果包括此选项，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将在首次使用新登录名时提示用户输入新密码。  
  
 CREDENTIAL =credential_name  
 **适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 将映射到新 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名的凭据的名称。 该凭据必须已存在于服务器中。 当前此选项只将凭据链接到登录名。 凭据不能映射到系统管理员 (sa) 登录名。  
  
 SID = sid  
 用于重新创建登录名。 仅适用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证登录名，不适用于 Windows 身份验证登录名。 指定新的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证登录名的 SID。 如果未使用此选项，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将自动分配 SID。 SID 结构取决于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 版本。  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名 SID：基于 GUID 的 16 字节 (binary(16)) 文本值。 例如 `SID = 0x14585E90117152449347750164BA00A7`。  
  
-   [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 登录名 SID：对 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 有效的 SID 结构。 通常，这是包含 `0x01060000000000640000000000000000` 的 32 字节 (binary(32)) 文本以及表示 GUID 的 16 个字节。 例如 `SID = 0x0106000000000064000000000000000014585E90117152449347750164BA00A7`。  
  
DEFAULT_DATABASE =database  
 **适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 指定将指派给登录名的默认数据库。 如果未包括此选项，则默认数据库将设置为 master。  
  
DEFAULT_LANGUAGE =language  
 **适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 指定将指派给登录名的默认语言。 如果未包括此选项，则默认语言将设置为服务器的当前默认语言。 即使将来服务器的默认语言发生更改，登录名的默认语言也仍保持不变。  
  
CHECK_EXPIRATION = { ON | OFF }  
 **适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 仅适用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名。 指定是否应对此登录帐户强制实施密码过期策略。 默认值为 OFF。  
  
CHECK_POLICY = { ON | OFF }  
 **适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 仅适用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名。 指定应对此登录名强制实施运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的计算机的 Windows 密码策略。 默认值为 ON。  
  
 如果 Windows 策略要求强密码，密码必须至少包含以下四个特点中的三个：  
  
-   大写字符 (A-Z)。  
-   小写字符 (a-z)。  
-   数字 (0-9)。  
-   一个非字母数字字符，如空格、_、@、*、^、%、!、$、# 或 &。  
  
WINDOWS  
 **适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 指定将登录名映射到 Windows 登录名。  
  
CERTIFICATE certname  
 **适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 指定将与此登录名关联的证书名称。 此证书必须已存在于 master 数据库中。  
  
ASYMMETRIC KEY asym_key_name  
 **适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 指定将与此登录名关联的非对称密钥的名称。 此密钥必须已存在于 master 数据库中。  
  
## <a name="remarks"></a>Remarks  
 密码是区分大小写的。  
  
 只有创建 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名时，才支持对密码预先进行哈希运算。  
  
 如果指定 MUST_CHANGE，则 CHECK_EXPIRATION 和 CHECK_POLICY 必须设置为 ON。 否则，该语句将失败。  
  
 不支持 CHECK_POLICY = OFF 和 CHECK_EXPIRATION = ON 的组合。  
  
 如果 CHECK_POLICY 设置为 OFF，将对 lockout_time 进行重置，并将 CHECK_EXPIRATION 设置为 OFF。  
  
> [!IMPORTANT]  
>  只有在 [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] 及更高版本上才会强制执行 CHECK_EXPIRATION 和 CHECK_POLICY。 有关详细信息，请参阅 [Password Policy](../../relational-databases/security/password-policy.md)。  
  
 从证书或非对称密钥创建的登录名仅用于代码签名。 不能用于连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 仅当 master 中已存在证书或非对称密钥时，才能从证书或非对称密钥创建登录名。  
  
 有关用于传输登录名的脚本，请参阅[如何在 SQL Server 2005 和 SQL Server 2008 的实例之间传输登录名和密码](http://support.microsoft.com/kb/918992)。  
  
 自动创建登录名将启用新的登录名，并授予它服务器级 CONNECT SQL 权限。  
 
 服务器的[身份验证模式](../../relational-databases/security/choose-an-authentication-mode.md)必须匹配登录名类型才能允许访问。
  
 有关设计权限系统的信息，请参阅 [Getting Started with Database Engine Permissions](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)。  
  
## <a name="includesssdsfullincludessssdsfull-mdmd-and-includesssdwincludessssdw-mdmd-logins"></a>[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 和 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 登录名  
 在 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]中，CREATE LOGIN 语句必须是批处理中的唯一语句。  
  
 在连接到 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]的一些方法（如 sqlcmd）中，必须使用 \<login>@\<server> 符号将 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 服务器名称追加到连接字符串中的登录名之后。 例如，如果登录名是 `login1`，[!INCLUDE[ssSDS](../../includes/sssds-md.md)] 服务器的完全限定名称是 `servername.database.windows.net`，则连接字符串的 username 参数应是 `login1@servername`。 由于 username 参数的总长度为 128 个字符，因此，login_name 被限定为 127 个字符减去服务器名称的长度。 在示例中，`login_name` 只能包含 117 个字符，因为 `servername` 包含 10 个字符。  
  
 在 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]和 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]中，必须连接到 master 数据库才能创建登录名。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 规则允许你创建 \<loginname>@\<servername> 格式的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证登录名。 如果你的 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]服务器是 myazureserver 并且登录名是 myemail@live.com，则必须提供 myemail@live.com@myazureserver 格式的登录名。  
  
 在 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]中，对连接和服务器级别的防火墙规则进行身份验证时所需的登录数据会暂时缓存在每个数据库中。 此缓存定期刷新。 若要强制刷新身份验证缓存并确保数据库具有最新版本的登录名表，请执行 [DBCC FLUSHAUTHCACHE (Transact-SQL)](../../t-sql/database-console-commands/dbcc-flushauthcache-transact-sql.md)。  
  
 有关 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]登录名的详细信息，请参阅[管理 Microsoft Azure SQL 数据库中的数据库和登录名](http://msdn.microsoft.com/library/ee336235.aspx)。  
  
## <a name="permissions"></a>权限  
 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，需要对服务器的 ALTER ANY LOGIN 权限或 securityadmin 固定服务器角色的成员身份。  
  
 在 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] 中，只有服务器级主体（由设置过程创建）或 master 数据库中的 `loginmanager` 数据库角色成员可以创建新登录名。  
  
 如果使用 CREDENTIAL 选项，则还需要对此服务器的 ALTER ANY CREDENTIAL 权限。  
  
## <a name="next-steps"></a>Next Steps  
 创建登录名后，登录名可以连接到[!INCLUDE[ssDE](../../includes/ssde-md.md)]或 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]，但是只具有授予 public 角色的权限。 考虑执行以下一些活动。  
  
-   要连接到数据库，请创建登录名对应的数据库用户。 有关详细信息，请参阅 [CREATE USER (Transact-SQL)](../../t-sql/statements/create-user-transact-sql.md)。  
  
-   使用 [CREATE SERVER ROLE (Transact-SQL)](../../t-sql/statements/create-server-role-transact-sql.md) 创建用户定义的服务器角色。 使用 ALTER SERVER ROLE ... ADD MEMBER 将新登录名添加到用户定义的服务器角色。 有关详细信息，请参阅 [CREATE SERVER ROLE (Transact-SQL)](../../t-sql/statements/create-server-role-transact-sql.md) 和 [ALTER SERVER ROLE (Transact-SQL)](../../t-sql/statements/alter-server-role-transact-sql.md)。  
  
-   使用 sp_addsrvrolemember 将登录名添加到固定服务器角色。 有关详细信息，请参阅[服务器级别角色](../../relational-databases/security/authentication-access/server-level-roles.md)和 [sp_addsrvrolemember (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addsrvrolemember-transact-sql.md)。  
  
-   使用 GRANT 语句将服务器级别权限授予新的登录名或包含该登录名的角色。 有关详细信息，请参阅 [GRANT (Transact-SQL)](../../t-sql/statements/grant-transact-sql.md)的信息。  
  
## <a name="examples"></a>示例  
  
### <a name="a-creating-a-login-with-a-password"></a>A. 创建带密码的登录名  
 以下示例为特定用户创建登录名并分配密码。  
  
```  
CREATE LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>';  
GO  
```  
  
### <a name="b-creating-a-login-with-a-password-that-must-be-changed"></a>B. 创建带必须更改的密码的登录名
 以下示例为特定用户创建登录名并分配密码。 `MUST_CHANGE` 选项要求用户在首次连接服务器时更改此密码。  
  
**适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
```  
CREATE LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>' 
    MUST_CHANGE,  CHECK_EXPIRATION = ON;
GO  
```  
[!NOTE] 当 CHECK_EXPIRATION 设为 OFF (关)时，不能使用 MUST_CHANGE 选项。
  
### <a name="c-creating-a-login-mapped-to-a-credential"></a>C. 创建映射到凭据的登录名  
 以下示例使用该用户为特定用户创建登录名。 此登录名映射到凭据。  
  
**适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
```  
CREATE LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>',   
    CREDENTIAL = <credentialName>;  
GO  
```  
  
### <a name="d-creating-a-login-from-a-certificate"></a>D. 从证书创建登录名  
 下例用 master 中的证书为特定用户创建登录名。  
  
**适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
```  
USE MASTER;  
CREATE CERTIFICATE <certificateName>  
    WITH SUBJECT = '<login_name> certificate in master database',  
    EXPIRY_DATE = '12/05/2025';  
GO  
CREATE LOGIN <login_name> FROM CERTIFICATE <certificateName>;  
GO  
```  
  
### <a name="e-creating-a-login-from-a-windows-domain-account"></a>E. 从 Windows 域帐户创建登录名  
 以下示例使用 Windows 域帐户创建一个登录名。  
  
**适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
```  
CREATE LOGIN [<domainName>\<login_name>] FROM WINDOWS;  
GO  
```  
  
### <a name="f-creating-a-login-from-a-sid"></a>F. 从 SID 创建登录名  
 下面的示例首先创建 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证登录名，并确定该登录名的 SID。  
  
```  
CREATE LOGIN TestLogin WITH PASSWORD = 'SuperSecret52&&';  
  
SELECT name, sid FROM sys.sql_logins WHERE name = 'TestLogin';  
GO  
```  
  
 我的查询返回 0x241C11948AEEB749B0D22646DB1A19F2 作为 SID。 你的查询将返回不同的值。 以下语句将删除登录名，然后重新创建登录名。 使用前面的查询中的 SID。  
  
```  
DROP LOGIN TestLogin;  
GO  
  
CREATE LOGIN TestLogin   
WITH PASSWORD = 'SuperSecret52&&', SID = 0x241C11948AEEB749B0D22646DB1A19F2;  
  
SELECT * FROM sys.sql_logins WHERE name = 'TestLogin';  
GO  
```  
  
## <a name="examples-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="g-creating-a-sql-server-authentication-login-with-a-password"></a>G. 创建具有密码的 SQL Server 身份验证登录名  
 下面的示例创建密码为 `A2c3456` 的登录名 `Mary7`。  
  
```sql  
CREATE LOGIN Mary7 WITH PASSWORD = 'A2c3456$#' ;  
```  
  
### <a name="h-using-options"></a>H. 使用选项  
 下面的示例创建具有密码和一些可选参数的登录名 `Mary8`。  
  
```  
CREATE LOGIN Mary8 WITH PASSWORD = 'A2c3456$#' MUST_CHANGE,  
CHECK_EXPIRATION = ON,  
CHECK_POLICY = ON;  
```  
  
### <a name="i-creating-a-login-from-a-windows-domain-account"></a>I. 从 Windows 域帐户创建登录名  
 下面的示例在 `Contoso` 域中使用 Windows 域帐户创建名为 `Mary` 的登录名。  
  
```  
CREATE LOGIN [Contoso\Mary] FROM WINDOWS;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [数据库引擎权限入门](../../relational-databases/security/authentication-access/getting-started-with-database-engine-permissions.md)   
 [主体（数据库引擎）](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [密码策略](../../relational-databases/security/password-policy.md)   
 [ALTER LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/alter-login-transact-sql.md)   
 [DROP LOGIN (Transact-SQL)](../../t-sql/statements/drop-login-transact-sql.md)   
 [EVENTDATA (Transact-SQL)](../../t-sql/functions/eventdata-transact-sql.md)   
 [创建登录名](../../relational-databases/security/authentication-access/create-a-login.md)  
  
  
