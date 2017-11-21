---
title: "LOGINPROPERTY (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- BadPasswordCount_TSQL
- BadPasswordTime_TSQL
- IsLockedIsMustChange
- PasswordLastSetTime
- LOGINPROPERTY_TSQL
- LockoutTime
- BadPasswordCount
- PasswordHash
- HistoryLengthIsExpired
- LockoutTime_TSQL
- PasswordHash_TSQL
- HistoryLengthIsExpired_TSQL
- PasswordLastSetTime_TSQL
- BadPasswordTime
- IsLockedIsMustChange_TSQL
- LOGINPROPERTY
dev_langs:
- TSQL
helpviewer_keywords:
- default database
- LOGINPROPERTY function
ms.assetid: b34df777-79b0-49a5-88db-b99998479a5d
caps.latest.revision: 42
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 31cbf502614fb348f35474237009f444ed294384
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="loginproperty-transact-sql"></a>LOGINPROPERTY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回有关登录策略设置的信息。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
LOGINPROPERTY ( 'login_name' , 'property_name' )  
```  
  
## <a name="arguments"></a>参数  
 *login_name*  
 将返回登录属性状态的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名。  
  
 *属性名*  
 一个表达式，包含要为登录名返回的属性信息。 *propertyname*可以是以下值之一。  
  
|值|Description|  
|-----------|-----------------|  
|**BadPasswordCount**|返回尝试以不正确密码连续登录的次数。|  
|**BadPasswordTime**|返回上次尝试以不正确密码登录的时间。|  
|**DaysUntilExpiration**|返回密码过期前的天数。|  
|**DefaultDatabase**|返回[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登录名默认数据库中元数据存储或**master**如果不指定任何数据库。 返回 NULL 非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]设置用户 （例如，Windows 身份验证用户）。|  
|**DefaultLanguage**|返回存储在元数据中的登录默认语言。 返回 NULL 非[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]设置的用户，例如，Windows 身份验证的用户。|  
|**HistoryLength**|返回使用密码策略强制机制跟踪登录名的密码数。 如果未强制执行密码策略，则为 0。 恢复密码策略实施将从 1 重新开始。|  
|**IsExpired**|指示登录名是否已过期。|  
|**IsLocked**|指示登录名是否已锁定。|  
|**IsMustChange**|指示登录名在下次连接时是否必须更改其密码。|  
|**' Lockouttime '**|返回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名由于超过允许的失败登录尝试次数而被锁定的日期。|  
|**PasswordHash**|返回密码的哈希。|  
|**PasswordLastSetTime**|返回设置当前密码时的日期。|  
|**PasswordHashAlgorithm**|返回用于对密码执行哈希操作的算法。|  
  
## <a name="returns"></a>返回  
 数据类型取决于所请求的值。  
  
 **IsLocked**， **IsExpired**，和**IsMustChange**属于类型**int**。  
  
-   1（如果登录名处于指定状态）。  
  
-   0（如果登录名不处于指定状态）。  
  
 **BadPasswordCount**和**HistoryLength**属于类型**int**。  
  
 **BadPasswordTime**， **'lockouttime'**， **PasswordLastSetTime**属于类型**datetime**。  
  
 **PasswordHash**属于类型**varbinary**。  
  
 NULL（如果登录名不是有效的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名）。  
  
 **DaysUntilExpiration**属于类型**int**。  
  
-   如果登录名已过期或者它将在查询的当日过期，则为 0。  
  
-   如果 Windows 中的本地安全策略使密码永不过期，则为 -1。  
  
-   如果登录名的 CHECK_POLICY 或 CHECK_EXPIRATION 设置为 OFF，或者操作系统不支持该密码策略，则为 NULL。  
  
 **PasswordHashAlgorithm**属于 int 类型。  
  
-   0（如果是 SQL7.0 哈希）  
  
-   如果 sha-1 哈希值为 1  
  
-   2（如果是 SHA-2 哈希）  
  
-   NULL（如果登录名不是有效的 SQL Server 登录名）  
  
## <a name="remarks"></a>注释  
 此内置函数返回有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名的密码策略设置的信息。 属性的名称不是区分大小写，因此属性名称如**BadPasswordCount**和**badpasswordcount**是等效的。 值**PasswordHash、 PasswordHashAlgorithm**，和**PasswordLastSetTime**属性上的所有支持的配置有[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，但其他属性都只是时可用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]上运行[!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)]以及是否启用 CHECK_POLICY 和 CHECK_EXPIRATION。 有关详细信息，请参阅 [Password Policy](../../relational-databases/security/password-policy.md)。  
  
## <a name="permissions"></a>Permissions  
 需要对登录名具有 VIEW 权限。 请求密码哈希时，还需要 CONTROL SERVER 权限。  
  
## <a name="examples"></a>示例  
  
### <a name="a-checking-whether-a-login-must-change-its-password"></a>A. 检查登录名是否必须更改其密码  
 下面的示例检查是否[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登录`John3`必须连接到的实例在下一步时更改其密码[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
```  
SELECT LOGINPROPERTY('John3', 'IsMustChange');  
GO  
```  
  
### <a name="b-checking-whether-a-login-is-locked-out"></a>B. 检查登录名是否已锁定  
 以下示例检查 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名 `John3` 是否已锁定。  
  
```  
SELECT LOGINPROPERTY('John3', 'IsLocked');  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [CREATE LOGIN &#40;Transact-SQL&#41;](../../t-sql/statements/create-login-transact-sql.md)   
 [sys.server_principals (Transact-SQL)](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)  
  
  

