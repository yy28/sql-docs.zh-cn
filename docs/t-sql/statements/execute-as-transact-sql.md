---
title: "EXECUTE AS (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- EXECUTE AS
- EXECUTE_AS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- REVERT statement
- WITH NO REVERT clause
- sessions [SQL Server], execution context
- EXECUTE AS
- execution context [SQL Server]
- switching execution context
ms.assetid: 613b8271-7f7d-4378-b7a2-5a7698551dbd
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: b89c78d286feaace6ec6bb2c85e854cb0ddbb5e0
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="execute-as-transact-sql"></a>EXECUTE AS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  设置会话的执行上下文。  
  
 默认情况下，会话在用户登录时开始，在用户注销时结束。 会话过程中的所有操作都受限于对该用户进行的权限检查。 当**EXECUTE AS**运行语句，该会话的执行上下文切换为指定的登录名或用户名称。 上下文切换后，将检查权限而不是呼叫的人该帐户的登录名和用户安全令牌针对**EXECUTE AS**语句。 实际上，在会话或模块的执行期间模拟了用户或登录帐户，或显式恢复了上下文切换。  
  

  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
{ EXEC | EXECUTE } AS <context_specification>  
[;]  
  
<context_specification>::=  
{ LOGIN | USER } = 'name'  
    [ WITH { NO REVERT | COOKIE INTO @varbinary_variable } ]   
| CALLER  
```  
  
## <a name="arguments"></a>参数  
 Login  
 **适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 指定要模拟的执行上下文是一个登录名。 模拟范围处于服务器级别。  
  
> [!NOTE]  
>  此选项不可用在包含的数据库或 SQL 数据库中。  
  
 User  
 指定要模拟的上下文是当前数据库中的用户。 模拟范围只限于当前数据库。 对数据库用户的上下文切换不会继承该用户的服务器级别权限。  
  
> [!IMPORTANT]  
>  当到数据库用户的上下文切换处于活动状态时，任何对数据库以外资源的访问尝试都将导致语句失败。 这包括使用*数据库*语句、 分布式的查询和引用使用三个-或四部分部分组成的标识符的另一个数据库的查询。  
  
  *名称*   
 有效的用户或登录名。 *名称*必须属于**sysadmin**固定服务器角色，或作为中的主体存在[sys.database_principals](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)或[sys.server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)，分别。  
  
 *名称*可以指定为本地变量。  
  
 *名称*必须为一个单独的帐户，并且不能组、 角色、 证书、 密钥或内置帐户，如 NT AUTHORITY\LocalService、 NT AUTHORITY\NetworkService 或 NT AUTHORITY\LocalSystem。  
  
 有关详细信息，请参阅[指定用户或登录名](#_user)本主题中更高版本。  
  
 NO REVERT  
 指定上下文切换不能恢复到以前的上下文。 **NO REVERT**选项仅用于在即席级别。  
  
 有关还原到前一个上下文的详细信息，请参阅[REVERT &#40;Transact SQL &#41;](../../t-sql/statements/revert-transact-sql.md).  
  
 COOKIE 到 **@**  *varbinary_variable*  
 指定仅为执行上下文恢复为以前的上下文，是否调用方 REVERT COOKIE 语句包含正确 **@**  *varbinary_variable*值。 [!INCLUDE[ssDE](../../includes/ssde-md.md)]将传递到 cookie  **@**  *varbinary_variable*。 **COOKIE 到**选项仅用于在即席级别。  
  
 **@***varbinary_variable*是**varbinary （8000)**。  
  
> [!NOTE]  
>  Cookie**输出**参数现记载为**varbinary （8000)**这是正确的最大长度。 但是，目前执行返回**varbinary(100)**。 应用程序应保留**varbinary （8000)** ，以便应用程序将继续正常运行，如果 cookie 返回大小增加的未来版本中。  
  
 CALLER  
 当在模块内部使用时，指定模块内部的语句在模块调用方的上下文中执行。  
  
 当在模块外部使用时，语句没有任何操作。  
  
## <a name="remarks"></a>注释  
 执行上下文中的更改在下列操作之一发生之前一直有效：  
  
-   运行另一个 EXECUTE AS 语句。  
  
-   运行 REVERT 语句。  
  
-   删除会话。  
  
-   命令已执行退出的存储过程或触发器。  
  
可以通过对多个主体多次调用 EXECUTE AS 语句来创建执行上下文堆栈。 在调用时，REVERT 语句将把上下文切换为上下文堆栈中上一级的登录帐户或用户。 此行为的演示，请参阅[示例 A](#_exampleA)。  
  
##  <a name="_user"></a>指定用户或登录名  
 EXECUTE AS 中指定的用户名或登录名\<context_specification > 作为中的主体必须存在**sys.database_principals**或**sys.server_principals**分别，或EXECUTE AS 语句将失败。 此外，还必须为该主体授予 IMPERSONATE 权限。 除非调用方是属于数据库所有者，或者为属于**sysadmin**固定服务器角色，主体必须存在即使当用户访问数据库或实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]通过 Windows 组成员资格。 例如，假设条件如下： 
  
-   **CompanyDomain\SQLUsers**组具有访问权限**销售**数据库。  
  
-   **CompanyDomain\SqlUser1**为属于**SQLUsers**并因此，具有隐式访问**销售**数据库。  
  
 尽管**CompanyDomain\SqlUser1**有权访问通过中的成员资格数据库**SQLUsers**组，该语句`EXECUTE AS USER = 'CompanyDomain\SqlUser1'`失败，因为`CompanyDomain\SqlUser1`不是中的主体数据库中。  
  
如果用户孤立 （不再存在关联的登录名），并且用户未创建与**WITHOUT LOGIN**， **EXECUTE AS**的用户将会失败。  
  
## <a name="best-practice"></a>最佳实践  
 指定具有执行会话中操作所需的最低特权的登录名或用户。 例如，如果只需要数据库级别的权限，则不要指定具有服务器级别权限的登录名；或者除非需要这些权限，否则不要指定数据库所有者帐户。  
  
> [!CAUTION]  
>  只要[!INCLUDE[ssDE](../../includes/ssde-md.md)]可以解析该名称，就可以成功执行 EXECUTE AS 语句。 如果域用户存在，Windows 可能为[!INCLUDE[ssDE](../../includes/ssde-md.md)]解析用户，即使该 Windows 用户无权访问 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 这可能导致这样的情况：无权访问 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的登录名似乎登录了，尽管模拟的登录名仅具有给 public 或 guest 授予的权限。  
  
## <a name="using-with-no-revert"></a>使用 WITH NO REVERT  
 当 EXECUTE AS 语句包含可选的 WITH NO REVERT 子句时，不能通过 REVERT 语句或执行另一个 EXECUTE AS 语句来重置会话的执行上下文。 由该语句设置的上下文在删除会话之前一直保持有效。  
  
 当 WITH NO REVERT COOKIE = @*varbinary_variabl*指定 e 子句， [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] cookie 将值传递给 @*varbinary_variabl*e。 设置执行上下文，如果调用还原使用 COOKIE，语句仅可以还原到前一个上下文 = @*varbinary_variable*语句包含相同 *@varbinary_variable* 值。  
  
 该选项在使用连接池的环境中非常有用。 连接池是指维护一组数据库连接，以使应用程序服务器上的应用程序能够重用它们。 因为的值传递给 *@varbinary_variable* 已知仅向调用方的 EXECUTE AS 语句中，调用方可以保证，它们建立的执行上下文不能更改任何其他人。  
  
## <a name="determining-the-original-login"></a>确定原始登录  
 使用[ORIGINAL_LOGIN](../../t-sql/functions/original-login-transact-sql.md)函数以返回连接到的实例的登录名[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 您可以在具有众多显式或隐式上下文切换的会话中使用该函数返回原始登录的标识。  
  
## <a name="permissions"></a>Permissions  
 若要指定**EXECUTE AS**上一个登录名，调用方必须拥有**IMPERSONATE**上指定的登录名的权限命名并没有必须拒绝**模拟 ANY LOGIN**权限. 若要指定**EXECUTE AS**上的数据库用户，调用方必须拥有**IMPERSONATE**上指定的用户名称的权限。 当**EXECUTE AS CALLER**指定，则**IMPERSONATE**则无需权限。  
  
## <a name="examples"></a>示例  
  
###  <a name="_exampleA"></a> A. 使用 EXECUTE AS 和 REVERT 切换上下文  
 以下示例使用多个主体创建上下文执行堆栈。 然后使用 `REVERT` 语句将执行上下文重置为上一个调用方。 将多次执行 `REVERT` 语句以向上移动堆栈，直到将执行上下文设置为原始调用方为止。  
  
```  
USE AdventureWorks2012;  
GO  
--Create two temporary principals  
CREATE LOGIN login1 WITH PASSWORD = 'J345#$)thb';  
CREATE LOGIN login2 WITH PASSWORD = 'Uor80$23b';  
GO  
CREATE USER user1 FOR LOGIN login1;  
CREATE USER user2 FOR LOGIN login2;  
GO  
--Give IMPERSONATE permissions on user2 to user1  
--so that user1 can successfully set the execution context to user2.  
GRANT IMPERSONATE ON USER:: user2 TO user1;  
GO  
--Display current execution context.  
SELECT SUSER_NAME(), USER_NAME();  
-- Set the execution context to login1.   
EXECUTE AS LOGIN = 'login1';  
--Verify the execution context is now login1.  
SELECT SUSER_NAME(), USER_NAME();  
--Login1 sets the execution context to login2.  
EXECUTE AS USER = 'user2';  
--Display current execution context.  
SELECT SUSER_NAME(), USER_NAME();  
-- The execution context stack now has three principals: the originating caller, login1 and login2.  
--The following REVERT statements will reset the execution context to the previous context.  
REVERT;  
--Display current execution context.  
SELECT SUSER_NAME(), USER_NAME();  
REVERT;  
--Display current execution context.  
SELECT SUSER_NAME(), USER_NAME();  
  
--Remove temporary principals.  
DROP LOGIN login1;  
DROP LOGIN login2;  
DROP USER user1;  
DROP USER user2;  
GO  
```  
  
### <a name="b-using-the-with-cookie-clause"></a>B. 使用 WITH COOKIE 子句  
 下面的示例设置为指定用户的会话的执行上下文，并指定 WITH NO REVERT COOKIE = @*varbinary_variabl*e 子句。 `REVERT` 语句必须指定传递给 `@cookie` 语句中的 `EXECUTE AS` 变量的值，否则，无法成功将上下文恢复为该调用方。 若要执行此示例，必须存在示例 A 中所创建的 `login1` 登录名和 `user1` 用户。  
  
```  
DECLARE @cookie varbinary(8000);  
EXECUTE AS USER = 'user1' WITH COOKIE INTO @cookie;  
-- Store the cookie in a safe location in your application.  
-- Verify the context switch.  
SELECT SUSER_NAME(), USER_NAME();  
--Display the cookie value.  
SELECT @cookie;  
GO  
-- Use the cookie in the REVERT statement.  
DECLARE @cookie varbinary(8000);  
-- Set the cookie value to the one from the SELECT @cookie statement.  
SET @cookie = <value from the SELECT @cookie statement>;  
REVERT WITH COOKIE = @cookie;  
-- Verify the context switch reverted.  
SELECT SUSER_NAME(), USER_NAME();  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [还原 &#40;Transact SQL &#41;](../../t-sql/statements/revert-transact-sql.md)   
 [EXECUTE AS 子句 &#40;Transact SQL &#41;](../../t-sql/statements/execute-as-clause-transact-sql.md)  
  
  

