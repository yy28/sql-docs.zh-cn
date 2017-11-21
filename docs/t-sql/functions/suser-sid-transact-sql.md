---
title: "SUSER_SID (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/29/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- SUSER_SID
- SUSER_SID_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- logins [SQL Server], users
- SIDs [SQL Server]
- security identifiers [SQL Server]
- users [SQL Server], logins
- 15401 (Database Engine error)
- IDs [SQL Server], logins
- identification numbers [SQL Server], logins
- SUSER_SID function
ms.assetid: 57b42a74-94e1-4326-85f1-701b9de53c7d
caps.latest.revision: 31
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ab02d47027f970e05820bc377d72f60938b52b62
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="susersid-transact-sql"></a>SUSER_SID (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  返回指定登录名的安全标识号 (SID)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
SUSER_SID ( [ 'login' ] [ , Param2 ] )   
```  
  
## <a name="arguments"></a>参数  
  *登录*   
**适用于**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 用户的登录名。 *登录名*是**sysname**。 *登录名*，这是可选的可以是[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登录名或[!INCLUDE[msCoName](../../includes/msconame-md.md)]Windows 用户或组。 如果*登录*是未指定，则返回有关当前安全上下文信息。 如果此参数包含词 NULL，将返回 NULL。  
  
 *Param2*  
**适用于**:[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 指定是否验证登录名。 *Param2*属于类型**int** ，是可选的。 当*Param2*为 0，不验证的登录名。 当*Param2*未指定为 0，Windows 登录名进行验证是完全相同的登录名存储在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
## <a name="return-types"></a>返回类型  
 **varbinary(85)**  
  
## <a name="remarks"></a>注释  
 SUSER_SID 在 ALTER TABLE 或 CREATE TABLE 中可用作 DEFAULT 约束。 SUSER_SID 可以在选择列表、WHERE 子句和任何允许使用表达式的地方使用。 SUSER_SID 必须始终后跟括号，即使在未指定参数的情况下也是如此。  
  
 在无参数的情况下调用时，SUSER_SID 将返回当前安全上下文的 SID。 当通过使用 EXECUTE AS 切换上下文的批处理中无参数调用时，SUSER_SID 将返回模拟上下文的 SID。 从模拟上下文中调用时，SUSER_SID(ORIGINAL_LOGIN()) 将返回原始上下文的 SID。  
  
 当 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 排序规则和 Windows 排序规则不同时，如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 Windows 以不同格式存储登录名，SUSER_SID 可能会失败。 例如，如果 Windows 计算机 TestComputer 具有登录名 User，而 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将该登录名存储为 TESTCOMPUTER\User，则查找登录名 TestComputer\User 可能无法正确解析该登录名。 若要跳过此验证的登录名，使用*Param2*。 排序规则不同通常是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误 15401 的原因：  
  
 `Windows NT user or group '%s' not found. Check the name again.`  
  
## <a name="examples"></a>示例  
  
### <a name="a-using-susersid"></a>A. 使用 SUSER_SID  
 下面的示例返回当前安全上下文的安全标识号 (SID)。  
  
```  
SELECT SUSER_SID('sa');  
```  
  
### <a name="b-using-susersid-with-a-specific-login"></a>B. 将 SUSER_SID 用于特定的登录名  
 下面的示例返回的安全标识号[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]`sa`登录名。  
  
**适用于**:[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
```  
SELECT SUSER_SID('sa');  
GO  
```  
  
### <a name="c-using-susersid-with-a-windows-user-name"></a>C. 对 Windows 用户名使用 SUSER_SID  
 以下示例返回 Windows 用户 `London\Workstation1` 的安全标识号。  
  
**适用于**:[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
```  
SELECT SUSER_SID('London\Workstation1');  
GO  
```  
  
### <a name="d-using-susersid-as-a-default-constraint"></a>D. 将 SUSER_SID 用作 DEFAULT 约束  
 下面的示例在 `SUSER_SID` 语句中使用 `DEFAULT` 作为 `CREATE TABLE` 约束。  
  
```  
USE AdventureWorks2012;  
GO  
CREATE TABLE sid_example  
(  
login_sid   varbinary(85) DEFAULT SUSER_SID(),  
login_name  varchar(30) DEFAULT SYSTEM_USER,  
login_dept  varchar(10) DEFAULT 'SALES',  
login_date  datetime DEFAULT GETDATE()  
);   
GO  
INSERT sid_example DEFAULT VALUES;  
GO  
```  
  
### <a name="e-comparing-the-windows-login-name-to-the-login-name-stored-in-sql-server"></a>E. 将 Windows 登录名与在 SQL Server 中存储的登录名进行比较  
 下面的示例演示如何使用*Param2*从 Windows 获取 SID，并使用该 SID 作为输入到`SUSER_SNAME`函数。 该示例以在 Windows 中存储的格式 (`TestComputer\User`) 提供登录名，并且以在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (`TESTCOMPUTER\User`) 中存储的格式返回登录名。  
  
**适用于**:[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
```  
SELECT SUSER_SNAME(SUSER_SID('TestComputer\User', 0));  
```  
  
## <a name="see-also"></a>另请参阅  
 [ORIGINAL_LOGIN &#40;Transact SQL &#41;](../../t-sql/functions/original-login-transact-sql.md)   
 [CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md)   
 [binary 和 varbinary &#40;Transact SQL &#41;](../../t-sql/data-types/binary-and-varbinary-transact-sql.md)   
 [系统函数 &#40;Transact SQL &#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)  
  
  

