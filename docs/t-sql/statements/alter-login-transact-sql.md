---
title: ALTER LOGIN (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/17/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: t-sql|statements
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ALTER_LOGIN_TSQL
- ALTER LOGIN
dev_langs:
- TSQL
helpviewer_keywords:
- ALTER LOGIN statement
- change password
- mapping logins [SQL Server]
- logins [SQL Server], modifying
- passwords [SQL Server], modifying
- names [SQL Server], logins
- modifying login accounts
ms.assetid: e247b84e-c99e-4af8-8b50-57586e1cb1c5
caps.latest.revision: 68
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: c39118f020f50d3349e15cb5581e52347e74ee70
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="alter-login-transact-sql"></a>ALTER LOGIN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  更改 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录帐户的属性。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
-- Syntax for SQL Server  
  
ALTER LOGIN login_name   
    {   
    <status_option>   
    | WITH <set_option> [ ,... ]  
    | <cryptographic_credential_option>  
    }   
[;]  
  
<status_option> ::=  
        ENABLE | DISABLE  
  
<set_option> ::=              
    PASSWORD = 'password' | hashed_password HASHED  
    [   
      OLD_PASSWORD = 'oldpassword'  
      | <password_option> [<password_option> ]   
    ]  
    | DEFAULT_DATABASE = database  
    | DEFAULT_LANGUAGE = language  
    | NAME = login_name  
    | CHECK_POLICY = { ON | OFF }  
    | CHECK_EXPIRATION = { ON | OFF }  
    | CREDENTIAL = credential_name  
    | NO CREDENTIAL  
  
<password_option> ::=   
    MUST_CHANGE | UNLOCK  
  
<cryptographic_credentials_option> ::=   
    ADD CREDENTIAL credential_name  
  | DROP CREDENTIAL credential_name  
```  
  
```  
-- Syntax for Azure SQL Database and Azure SQL Data Warehouse 
  
ALTER LOGIN login_name   
  {   
      <status_option>   
    | WITH <set_option> [ ,.. .n ]   
  }   
[;]  
  
<status_option> ::=  
    ENABLE | DISABLE  
  
<set_option> ::=   
    PASSWORD ='password'   
    [  
      OLD_PASSWORD ='oldpassword'  
    ]   
    | NAME = login_name  
```  
  
```  
-- Syntax for Parallel Data Warehouse  
  
ALTER LOGIN login_name   
    {   
    <status_option>   
    | WITH <set_option> [ ,... ]  
    }   
  
<status_option> ::=ENABLE | DISABLE  
  
<set_option> ::=              
    PASSWORD ='password'   
    [   
      OLD_PASSWORD ='oldpassword'  
      | <password_option> [<password_option> ]   
    ]  
    | NAME = login_name  
    | CHECK_POLICY = { ON | OFF }  
    | CHECK_EXPIRATION = { ON | OFF }   
      
<password_option> ::=   
    MUST_CHANGE | UNLOCK  
```  
  
## <a name="arguments"></a>参数  
 login_name  
 指定正在更改的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名的名称。 域登录名必须用方括号括起来，其格式为 [domain\user]。  
  
 ENABLE | DISABLE  
 启用或禁用此登录名。 禁用登录名不会影响已连接登录名的行为。 （使用 `KILL` 语句终止现有连接。）禁用的登录名将保留它们的权限，且仍然可以模拟。  
  
 PASSWORD ='password'****  
 仅适用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名。 指定正在更改的登录名的密码。 密码是区分大小写的。  
  
 与 SQL 数据库持续保持活动连接需要至少每隔 10 小时进行重新授权（由数据库引擎执行）。 数据库引擎使用最初提交的密码尝试重新授权，且无需用户输入。 出于性能原因，在 SQL 数据库中重置密码时，连接将不会重新进行身份验证，即使该连接因连接池而重置。 这与本地 SQL Server 的行为不同。 如果自最初授权连接时已更改密码，则必须终止连接，并使用新密码建立新连接。 具有 KILL DATABASE CONNECTION 权限的用户可使用 KILL 命令，显式终止与 SQL 数据库的连接。 有关详细信息，请参阅 [KILL (Transact-SQL)](../../t-sql/language-elements/kill-transact-sql.md)。  
  
 PASSWORD =hashed_password  
 **适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 仅适用于 HASHED 关键字。 指定要创建的登录名的密码的哈希值。  
  
> [!IMPORTANT]  
>  当一个登录名（或包含的数据库用户）进行连接并经过身份验证后，该连接缓存有关该登录名的标识信息。 对于 Windows 身份验证登录，此标识信息包含有关 Windows 组中的成员身份的信息。 只要保持连接，该登录名的标识就保持已经过身份验证的状态。 若要在标识中强制进行更改（例如，重置密码或更改 Windows 组成员身份），则必须从身份验证机构（Windows 或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]）注销，然后再次登录。 **sysadmin** 固定服务器角色的成员或任何使用 **ALTER ANY CONNECTION** 权限的登录名都可以使用 **KILL** 命令结束连接，并强制登录名重新连接。 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 可以在打开与对象资源管理器和查询编辑器窗口之间的多个连接时重用连接信息。 关闭所有连接可强制重新连接。  
  
 HASHED  
   
**适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 仅适用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名。 指定在 PASSWORD 参数后输入的密码已经过哈希运算。 如果未选择此选项，则在将密码存储到数据库之前，对其进行哈希运算。 此选项只能用于在两台服务器之间同步登录名。 切勿使用 HASHED 选项定期更改密码。  
  
 OLD_PASSWORD ='oldpassword'****  
 仅适用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名。 要指派新密码的登录的当前密码。 密码是区分大小写的。  
  
 MUST_CHANGE  
 适用范围：[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、并行数据仓库。  
  
 仅适用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名。 如果包括此选项，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将在首次使用已更改的登录名时提示输入更新的密码。  
  
 DEFAULT_DATABASE =database  
**适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 指定将指派给登录名的默认数据库。  
  
 DEFAULT_LANGUAGE =language  
 
 **适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 指定将指派给登录名的默认语言。 所有 SQL 数据库登录名的默认语言为英语，并且无法更改。 Linux 上 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 `sa` 登录名的默认语言是英语，但可以更改。  
  
 NAME = login_name  
 正在重命名的登录的新名称。 如果是 Windows 登录，则与新名称对应的 Windows 主体的 SID 必须匹配与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中的登录相关联的 SID。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名的新名称不能包含反斜杠字符 (\\)。  
  
 CHECK_EXPIRATION = { ON | OFF }  
 适用范围：[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、并行数据仓库。  
  
 仅适用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名。 指定是否应对此登录帐户强制实施密码过期策略。 默认值为 OFF。  
  
 CHECK_POLICY = { ON | OFF }  
 适用范围：[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、并行数据仓库。  
  
 仅适用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名。 指定应对此登录名强制实施运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的计算机的 Windows 密码策略。 默认值为 ON。  
  
 CREDENTIAL = credential_name  
 **适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 将映射到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录的凭据的名称。 该凭据必须已存在于服务器中。 有关详细信息，请参阅[凭据（数据库引擎）](../../relational-databases/security/authentication-access/credentials-database-engine.md)。 凭据不能映射到 sa 登录名。  
  
 NO CREDENTIAL  
 **适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 删除登录到服务器凭据的当前所有映射。 有关详细信息，请参阅[凭据（数据库引擎）](../../relational-databases/security/authentication-access/credentials-database-engine.md)。  
  
 UNLOCK  
 适用范围：[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、并行数据仓库。  
  
 仅适用于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名。 指定应解锁被锁定的登录名。  
  
 ADD CREDENTIAL  
 **适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 将可扩展的密钥管理 (EKM) 提供程序凭据添加到登录名。 有关详细信息，请参阅[可扩展的密钥管理 (EKM)](../../relational-databases/security/encryption/extensible-key-management-ekm.md)。  
  
 DROP CREDENTIAL  
 **适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
从登录名删除可扩展密钥管理 (EKM) 提供程序凭据。 有关详细信息，请参阅[可扩展的密钥管理 (EKM)](../../relational-databases/security/encryption/extensible-key-management-ekm.md)。  
  
## <a name="remarks"></a>Remarks  
 如果 CHECK_POLICY 设置为 ON，则无法使用 HASHED 参数。  
  
 如果 CHECK_POLICY 更改为 ON，则将出现以下行为：  
  
-   用当前的密码哈希值初始化密码历史记录。  
  
 如果 CHECK_POLICY 更改为 OFF，则将出现以下行为：  
  
-   CHECK_EXPIRATION 也设置为 OFF。  
  
-   清除密码历史记录。  
  
-   重置 lockout_time 的值。  
  
如果指定 MUST_CHANGE，则 CHECK_EXPIRATION 和 CHECK_POLICY 必须设置为 ON。 否则，该语句将失败。  
  
如果 CHECK_POLICY 设置为 OFF，则 CHECK_EXPIRATION 不能设置为 ON。 包含此选项组合的 ALTER LOGIN 语句将失败。  
  
不能使用带 DISABLE 参数的 ALTER_LOGIN 来拒绝对 Windows 组的访问。 例如，ALTER_LOGIN [domain\group] DISABLE 将返回下列错误信息：  
  
 “消息 15151，级别 16，状态 1，第 1 行”  
  
 “无法更改登录名 'Domain\Group'，因为它不存在，或者你没有相应权限。”  
  
 这是设计的结果。  
  
在 [!INCLUDE[ssSDS](../../includes/sssds-md.md)]中，对连接和服务器级别的防火墙规则进行身份验证时所需的登录数据会暂时缓存在每个数据库中。 此缓存定期刷新。 若要强制刷新身份验证缓存并确保数据库具有最新版本的登录名表，请执行 [DBCC FLUSHAUTHCACHE (Transact-SQL)](../../t-sql/database-console-commands/dbcc-flushauthcache-transact-sql.md)。  
  
## <a name="permissions"></a>权限  
 需要 ALTER ANY LOGIN 权限。  
  
 如果使用 CREDENTIAL 选项，则还需要 ALTER ANY CREDENTIAL 权限。  
  
 如果正在更改的登录名是 sysadmin 固定服务器角色的成员或 CONTROL SERVER 权限的被授权者，则进行以下更改时还需要 CONTROL SERVER 权限：  
  
-   在不提供旧密码的情况下重置密码。  
  
-   启用 MUST_CHANGE、CHECK_POLICY 或 CHECK_EXPIRATION。  
  
-   更改登录名。  
  
-   启用或禁用登录名。  
  
-   将登录名映射到其他凭据。  
  
 主体可更改用于自身登录的密码、默认语言以及默认数据库。  
  
## <a name="examples"></a>示例  
  
### <a name="a-enabling-a-disabled-login"></a>A. 启用已禁用的登录名  
 以下示例将启用 `Mary5` 登录名。  
  
```sql  
ALTER LOGIN Mary5 ENABLE;  
```  
  
### <a name="b-changing-the-password-of-a-login"></a>B. 更改登录密码  
 以下示例将登录名 `Mary5` 的密码更改为强密码。  
  
```sql  
ALTER LOGIN Mary5 WITH PASSWORD = '<enterStrongPasswordHere>';  
```  
  
### <a name="c-changing-the-name-of-a-login"></a>C. 更改登录名称  
 以下示例将 `Mary5` 登录名称更改为 `John2`。  
  
```sql  
ALTER LOGIN Mary5 WITH NAME = John2;  
```  
  
### <a name="d-mapping-a-login-to-a-credential"></a>D. 将登录名映射到凭据  
 以下示例将登录名 `John2` 映射到凭据 `Custodian04`。  
  
```sql  
ALTER LOGIN John2 WITH CREDENTIAL = Custodian04;  
```  
  
### <a name="e-mapping-a-login-to-an-extensible-key-management-credential"></a>E. 将登录名映射到可扩展密钥管理凭据  
 以下示例将登录名 `Mary5` 映射到 EKM 凭据 `EKMProvider1`。  
  
 
**适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
```sql  
ALTER LOGIN Mary5  
ADD CREDENTIAL EKMProvider1;  
GO  
```  
  
### <a name="f-unlocking-a-login"></a>F. 解除锁定登录名  
 若要解除锁定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名，请执行以下语句，并将 **** 替换为所需帐户密码。  
  
  
```sql  
ALTER LOGIN [Mary5] WITH PASSWORD = '****' UNLOCK ;  

GO  
```  
  
 若要在不更改密码的情况下解除锁定登录名，请关闭检查策略，然后再打开此检查策略。  
  
```sql  
ALTER LOGIN [Mary5] WITH CHECK_POLICY = OFF;  
ALTER LOGIN [Mary5] WITH CHECK_POLICY = ON;  
GO  
```  
  
### <a name="g-changing-the-password-of-a-login-using-hashed"></a>G. 使用 HASHED 更改登录名的密码  
 以下示例将 `TestUser` 登录名的密码更改为已经过哈希运算的值。  
  
**适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
```sql  
ALTER LOGIN TestUser WITH   
PASSWORD = 0x01000CF35567C60BFB41EBDE4CF700A985A13D773D6B45B90900 HASHED ;  
GO  
```  
  
 
  
## <a name="see-also"></a>另请参阅  
 [凭据（数据库引擎）](../../relational-databases/security/authentication-access/credentials-database-engine.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [DROP LOGIN (Transact-SQL)](../../t-sql/statements/drop-login-transact-sql.md)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](../../t-sql/statements/create-credential-transact-sql.md)   
 [EVENTDATA (Transact-SQL)](../../t-sql/functions/eventdata-transact-sql.md)   
 [可扩展密钥管理 &#40;EKM&#41;](../../relational-databases/security/encryption/extensible-key-management-ekm.md)  
  
  


