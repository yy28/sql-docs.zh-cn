---
title: "USER_NAME (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- USER_NAME
- USER_NAME_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- usernames [SQL Server]
- IDs [SQL Server], databases
- USER_NAME function
- users [SQL Server], database username
- names [SQL Server], database users
- identification numbers [SQL Server], databases
- database usernames [SQL Server]
ms.assetid: ab32d644-4228-449a-9ef0-5a975c305775
caps.latest.revision: 37
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: aecf422ca2289b2a417147eb402921bb8530d969
ms.openlocfilehash: f51938b0f918a1a85955df4038ded45480bd1a45
ms.contentlocale: zh-cn
ms.lasthandoff: 10/24/2017

---
# <a name="username-transact-sql"></a>USER_NAME (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  根据指定的标识号返回数据库用户名。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
USER_NAME ( [ id ] )  
```  
  
## <a name="arguments"></a>参数  
 *id*  
 与数据库用户关联的标识号。 *id*是**int**。需要使用括号。  
  
## <a name="return-types"></a>返回类型  
 **nvarchar(256)**  
  
## <a name="remarks"></a>注释  
 当*id*是省略，则假定为当前用户的当前上下文中。 如果参数包含的单词 NULL 将返回 NULL。当 USER_NAME 调用而无需指定*id*后 EXECUTE 语句中 USER_NAME 返回模拟的用户的名称。 如果 Windows 主体通过某组中的成员身份访问数据库，则 USER_NAME 将返回 Windows 主体的名称，而不是该组的名称。  
  
## <a name="examples"></a>示例  
  
### <a name="a-using-username"></a>A. 使用 USER_NAME  
 以下示例将返回用户 ID 为 `13` 的用户名。  
  
```  
SELECT USER_NAME(13);  
GO  
```  
  
### <a name="b-using-username-without-an-id"></a>B. 使用不指定 ID 的 USER_NAME  
 以下示例在不指定 ID 的情况下查找当前用户的名称。  
  
```  
SELECT USER_NAME();  
GO  
```  
  
 下面是为属于 sysadmin 固定服务器角色成员的用户返回的结果集。  
  
 ```
------------------------------  
dbo  
  
(1 row(s) affected)
```  
  
### <a name="c-using-username-in-the-where-clause"></a>C. 在 WHERE 子句中使用 USER_NAME  
 以下示例在 `sysusers` 中查找行，该行的名称与将 `USER_NAME` 系统函数应用于用户标识号 `1` 而得出的结果相同。  
  
```  
SELECT name FROM sysusers WHERE name = USER_NAME(1);  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
name  
------------------------------  
dbo  
  
(1 row(s) affected)
```  
  
### <a name="d-calling-username-during-impersonation-with-execute-as"></a>D. 在使用 EXECUTE AS 的模拟过程中调用 USER_NAME  
 以下示例显示模拟过程中 `USER_NAME` 的行为方式。  
  
```  
SELECT USER_NAME();  
GO  
EXECUTE AS USER = 'Zelig';  
GO  
SELECT USER_NAME();  
GO  
REVERT;  
GO  
SELECT USER_NAME();  
GO  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
 ```
DBO  
Zelig  
DBO
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="e-using-username-without-an-id"></a>E. 使用不指定 ID 的 USER_NAME  
 以下示例在不指定 ID 的情况下查找当前用户的名称。  
  
```  
SELECT USER_NAME();  
```  
  
 下面是当前登录的用户的结果集。  
  
```  
------------------------------   
User7                              
```  
  
### <a name="f-using-username-in-the-where-clause"></a>F. 在 WHERE 子句中使用 USER_NAME  
 以下示例在 `sysusers` 中查找行，该行的名称与将 `USER_NAME` 系统函数应用于用户标识号 `1` 而得出的结果相同。  
  
```  
SELECT name FROM sysusers WHERE name = USER_NAME(1);  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
name                             
------------------------------   
User7                              
```  
  
## <a name="see-also"></a>另请参阅  
 [ALTER TABLE (Transact-SQL)](../../t-sql/statements/alter-table-transact-sql.md)   
 [CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)   
 [CURRENT_TIMESTAMP &#40;Transact SQL &#41;](../../t-sql/functions/current-timestamp-transact-sql.md)   
 [CURRENT_USER &#40;Transact SQL &#41;](../../t-sql/functions/current-user-transact-sql.md)   
 [SESSION_USER &#40;Transact SQL &#41;](../../t-sql/functions/session-user-transact-sql.md)   
 [System Functions (Transact-SQL)](../../relational-databases/system-functions/system-functions-for-transact-sql.md)   
 [SYSTEM_USER &#40;Transact SQL &#41;](../../t-sql/functions/system-user-transact-sql.md)  
  
  


