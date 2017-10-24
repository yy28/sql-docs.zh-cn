---
title: "ORIGINAL_LOGIN (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ORIGINAL_LOGIN_TSQL
- ORIGINAL_LOGIN
dev_langs:
- TSQL
helpviewer_keywords:
- logins [SQL Server], context switches
- context switching [SQL Server], login names
- original login names [SQL Server]
- ORIGINAL_LOGIN function
- names [SQL Server], logins
ms.assetid: ddfb0991-cde3-4b97-a5b7-ee450133f160
caps.latest.revision: 18
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b1f97da47505e5c812e43f4481d9f36027bf14c9
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="originallogin-transact-sql"></a>ORIGINAL_LOGIN (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的登录名。 您可以在具有众多显式或隐式上下文切换的会话中使用该函数返回原始登录的标识。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
ORIGINAL_LOGIN( )  
```  
  
## <a name="return-types"></a>返回类型  
 **sysname**  
  
## <a name="remarks"></a>注释  
 该函数在审核原始连接上下文的标识时非常有用。 而函数如[SESSION_USER](../../t-sql/functions/session-user-transact-sql.md)和[CURRENT_USER](../../t-sql/functions/current-user-transact-sql.md)返回当前正在执行上下文 ORIGINAL_LOGIN 返回的第一次连接到的的实例的登录名标识[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]该会话中。  
  
 返回 NULL 上[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。  
  
## <a name="examples"></a>示例  
 以下示例将当前会话的执行上下文从语句的调用方切换到 `login1`。 函数 `SUSER_SNAME` 和 `ORIGINAL_LOGIN` 用于返回当前会话用户（上下文切换到的用户）和原始登录帐户。  
  
```  
USE AdventureWorks2012;  
GO  
--Create a temporary login and user.  
CREATE LOGIN login1 WITH PASSWORD = 'J345#$)thb';  
CREATE USER user1 FOR LOGIN login1;  
GO  
--Execute a context switch to the temporary login account.  
DECLARE @original_login sysname;  
DECLARE @current_context sysname;  
EXECUTE AS LOGIN = 'login1';  
SET @original_login = ORIGINAL_LOGIN();  
SET @current_context = SUSER_SNAME();  
SELECT 'The current executing context is: '+ @current_context;  
SELECT 'The original login in this session was: '+ @original_login  
GO  
-- Return to the original execution context  
-- and remove the temporary principal.  
REVERT;  
GO  
DROP LOGIN login1;  
DROP USER user1;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [执行 AS &#40;Transact SQL &#41;](../../t-sql/statements/execute-as-transact-sql.md)   
 [还原 &#40;Transact SQL &#41;](../../t-sql/statements/revert-transact-sql.md)  
  
  

