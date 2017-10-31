---
title: "还原 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- REVERT_TSQL
- REVERT
dev_langs:
- TSQL
helpviewer_keywords:
- REVERT statement
- context switching [SQL Server], reverting
- reverting execution context
- REVERT WITH COOKIE statement
- execution context [SQL Server]
- COOKIE clause
ms.assetid: 4688b17a-dfd1-4f03-8db4-273a401f879f
caps.latest.revision: 28
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: aecf422ca2289b2a417147eb402921bb8530d969
ms.openlocfilehash: 033442da3e10fd834963df30ea071a220464de6f
ms.contentlocale: zh-cn
ms.lasthandoff: 10/24/2017

---
# <a name="revert-transact-sql"></a>REVERT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  将执行上下文切换回最后一个 EXECUTE AS 语句的调用方。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
REVERT  
    [ WITH COOKIE = @varbinary_variable ]  
```  
  
## <a name="arguments"></a>参数  
 使用 COOKIE = @*varbinary_variable*  
 指定已创建相应的 cookie [EXECUTE AS](../../t-sql/statements/execute-as-transact-sql.md)独立语句。 *@varbinary_variable*是**varbinary(100)**。  
  
## <a name="remarks"></a>注释  
 可以在诸如存储过程或用户定义函数这样的模块中指定 REVERT，也可将它指定为独立语句。 在模块内部指定时，REVERT 只适用于在模块中定义的 EXECUTE AS 语句。 例如，以下存储过程发出后跟 `EXECUTE AS` 语句的 `REVERT` 语句。  
  
```  
CREATE PROCEDURE dbo.usp_myproc   
  WITH EXECUTE AS CALLER  
AS   
    SELECT SUSER_NAME(), USER_NAME();  
    EXECUTE AS USER = 'guest';  
    SELECT SUSER_NAME(), USER_NAME();  
    REVERT;  
    SELECT SUSER_NAME(), USER_NAME();  
GO  
```  
  
 假定在运行存储过程的会话中，会话的执行上下文显式更改为 `login1`，如下例所示。  
  
```  
  -- Sets the execution context of the session to 'login1'.  
EXECUTE AS LOGIN = 'login1';  
GO  
EXECUTE dbo.usp_myproc;   
```  
  
 `REVERT`内部定义的语句`usp_myproc`切换执行上下文设置内部模块，但不会影响设置外部模块的执行上下文。 就是说，会话的执行上下文将仍然设置为 `login1`。  
  
 指定为独立语句时，REVERT 将应用于在批或会话中定义的 EXECUTE AS 语句。 如果相应的 EXECUTE AS 语句包含 WITH NO REVERT 子句，则 REVERT 无效。 在这种情况下，执行上下文将保持有效状态，直到删除会话。  
  
## <a name="using-revert-with-cookie"></a>使用 REVERT WITH COOKIE  
 EXECUTE 用于设置会话的执行上下文的语句可以包含的可选子句与任何 REVERT COOKIE = @*varbinary_variabl*e。 当运行此语句时，[!INCLUDE[ssDE](../../includes/ssde-md.md)]将传递到 @ cookie*varbinary_variabl*e。 设置执行上下文，如果调用还原使用 COOKIE，语句仅可以还原到前一个上下文 = @*varbinary_variable*语句包含正确 *@varbinary_variable* 值。  
  
 此机制在使用连接池的环境中是有用的。 连接池是一组供跨越多个最终用户的应用程序重用的数据库连接的维护机制。 因为的值传递给 *@varbinary_variable* 已知仅向调用方的 EXECUTE AS 语句 （在此情况下，应用程序），调用方可以保证最终用户，不能更改它们建立的执行上下文它调用应用程序。 恢复执行上下文之后，应用程序可以将上下文切换到另一个主体。  
  
## <a name="permissions"></a>Permissions  
 不需要任何权限。  
  
## <a name="examples"></a>示例  
  
### <a name="a-using-execute-as-and-revert-to-switch-context"></a>A. 使用 EXECUTE AS 和 REVERT 切换上下文  
 以下示例通过使用多个主体创建上下文执行堆栈。 然后使用 REVERT 语句将执行上下文重置为上一个调用方。 将多次执行 REVERT 语句以向上移动堆栈，直到将执行上下文设置为原始调用方为止。  
  
```  
USE AdventureWorks2012;  
GO  
-- Create two temporary principals.  
CREATE LOGIN login1 WITH PASSWORD = 'J345#$)thb';  
CREATE LOGIN login2 WITH PASSWORD = 'Uor80$23b';  
GO  
CREATE USER user1 FOR LOGIN login1;  
CREATE USER user2 FOR LOGIN login2;  
GO  
-- Give IMPERSONATE permissions on user2 to user1  
-- so that user1 can successfully set the execution context to user2.  
GRANT IMPERSONATE ON USER:: user2 TO user1;  
GO  
-- Display current execution context.  
SELECT SUSER_NAME(), USER_NAME();  
-- Set the execution context to login1.   
EXECUTE AS LOGIN = 'login1';  
-- Verify that the execution context is now login1.  
SELECT SUSER_NAME(), USER_NAME();  
-- Login1 sets the execution context to login2.  
EXECUTE AS USER = 'user2';  
-- Display current execution context.  
SELECT SUSER_NAME(), USER_NAME();  
-- The execution context stack now has three principals: the originating caller, login1, and login2.  
-- The following REVERT statements will reset the execution context to the previous context.  
REVERT;  
-- Display the current execution context.  
SELECT SUSER_NAME(), USER_NAME();  
REVERT;  
-- Display the current execution context.  
SELECT SUSER_NAME(), USER_NAME();  
  
-- Remove the temporary principals.  
DROP LOGIN login1;  
DROP LOGIN login2;  
DROP USER user1;  
DROP USER user2;  
GO  
```  
  
### <a name="b-using-the-with-cookie-clause"></a>B. 使用 WITH COOKIE 子句  
 下面的示例设置为指定用户的会话的执行上下文，并指定 WITH NO REVERT COOKIE = @*varbinary_variabl*e 子句。 `REVERT` 语句必须指定传递给 `@cookie` 语句中的 `EXECUTE AS` 变量的值，否则，无法成功将上下文恢复为该调用方。 若要执行此示例，必须存在示例 A 中所创建的 `login1` 登录名和 `user1` 用户。  
  
```  
DECLARE @cookie varbinary(100);  
EXECUTE AS USER = 'user1' WITH COOKIE INTO @cookie;  
-- Store the cookie somewhere safe in your application.  
-- Verify the context switch.  
SELECT SUSER_NAME(), USER_NAME();  
--Display the cookie value.  
SELECT @cookie;  
GO  
-- Use the cookie in the REVERT statement.  
DECLARE @cookie varbinary(100);  
-- Set the cookie value to the one from the SELECT @cookie statement.  
SET @cookie = <value from the SELECT @cookie statement>;  
REVERT WITH COOKIE = @cookie;  
-- Verify the context switch reverted.  
SELECT SUSER_NAME(), USER_NAME();  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [执行 AS &#40;Transact SQL &#41;](../../t-sql/statements/execute-as-transact-sql.md)   
 [EXECUTE AS 子句 (Transact-SQL)](../../t-sql/statements/execute-as-clause-transact-sql.md)   
 [EXECUTE (Transact-SQL)](../../t-sql/language-elements/execute-transact-sql.md)   
 [SUSER_NAME &#40;Transact SQL &#41;](../../t-sql/functions/suser-name-transact-sql.md)   
 [USER_NAME &#40;Transact SQL &#41;](../../t-sql/functions/user-name-transact-sql.md)   
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [CREATE USER (Transact-SQL)](../../t-sql/statements/create-user-transact-sql.md)  
  
  

