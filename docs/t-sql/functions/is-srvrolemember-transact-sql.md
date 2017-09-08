---
title: "IS_SRVROLEMEMBER (Transact SQL) |Microsoft 文档"
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
- IS_SRVROLEMEMBER_TSQL
- IS_SRVROLEMEMBER
dev_langs:
- TSQL
helpviewer_keywords:
- roles [SQL Server], members
- IS_SRVROLEMEMBER function
- members [SQL Server], verifying
ms.assetid: 3241a44a-6958-415b-b8b7-2a1207c36ab3
caps.latest.revision: 65
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: c26c0c1f4cb6a22f50cdc6a87d7a31f25b65e138
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="issrvrolemember-transact-sql"></a>IS_SRVROLEMEMBER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  指示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名是否为指定服务器角色的成员。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
IS_SRVROLEMEMBER ( 'role' [ , 'login' ] )  
```  
  
## <a name="arguments"></a>参数  
  *角色*   
 要检查的服务器角色的名称。 *角色*是**sysname**。  
  
 有效值为*角色*是用户定义的服务器角色和以下固定服务器角色：  
  
|||  
|-|-|  
|sysadmin|serveradmin|  
|dbcreator|setupadmin|  
|bulkadmin|securityadmin|  
|diskadmin|**适用范围**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> public|  
|processadmin||  
  
  *登录*   
 是的名称[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登录名来检查。 *登录名*是**sysname**，默认值为 NULL。 如果未不指定任何值，结果基于当前的执行上下文。 如果此参数包含词 NULL，将返回 NULL。  
  
## <a name="return-types"></a>返回类型  
 **int**  
  
|返回值|Description|  
|------------------|-----------------|  
|0|*登录名*不是成员的*角色*。<br /><br /> 在[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]，此语句始终返回 0。|  
|1|*登录名*为属于*角色*。|  
|NULL|*角色*或*登录*无效，或者您没有权限查看的角色成员资格。|  
  
## <a name="remarks"></a>注释  
 UseIS_SRVROLEMEMBER 以确定当前用户是否可以执行的操作需要的服务器角色的权限。  
  
 如果为指定 Windows 登录名，例如 Contoso\Mary5，*登录*， **IS_SRVROLEMEMBER**返回**NULL**，除非授予或拒绝直接访问权限登录名[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 如果可选*登录*参数是未提供，并且如果*登录*是 Windows 域登录名，它可能是通过在 Windows 组的成员资格固定的服务器角色的成员。 要解析这种间接成员身份，IS_SRVROLEMEMBER 将从域控制器中请求 Windows 组成员身份信息。 如果域控制器不可访问或不响应， **IS_SRVROLEMEMBER**的适用于用户和其本地组的记帐返回角色成员身份信息。 如果指定的用户不是当前用户，则 IS_SRVROLEMEMBER 返回的值可能不同于验证器（例如 Active Directory）对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 进行的最后一次数据更新。  
  
 如果提供了可选的 login 参数，则 sys.server_principals 中必须存在要查询的 Windows 登录名，否则 IS_SRVROLEMEMBER 将返回 NULL。 这指示该登录名无效。  
  
 如果登录名参数为域登录名或基于 Windows 组，且无法访问域控制器，则对 IS_SRVROLEMEMBER 的调用将失败，并可能返回不正确或不完整的数据。  
  
 如果域控制器不可用，则当 Windows 主体可在本地进行身份验证时（例如本地 Windows 帐户或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名），对 IS_SRVROLEMEMBER 的调用将返回准确的信息。  
  
 **IS_SRVROLEMEMBER**始终返回 0，在使用 Windows 组为登录名参数，并且此 Windows 组是另一个 Windows 组，即，反过来，指定的服务器角色的成员的成员。  
  
 用户帐户控制 (UAC) 设置还可能会导致返回不同的结果。 这取决于用户在访问服务器时是作为 Windows 组成员还是特定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用户。  
  
 此函数计算角色成员身份，而不是基础权限。 例如， **sysadmin**固定的服务器角色具有**CONTROL SERVER**权限。 如果用户具有**CONTROL SERVER**权限但不是角色的成员，此函数将正确地报告用户不是成员的**sysadmin**角色，即使用户具有相同权限。  
  
## <a name="related-functions"></a>相关函数  
 若要确定当前用户是否为指定的 Windows 组的成员或[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库角色，使用[IS_MEMBER &#40;Transact SQL &#41;](../../t-sql/functions/is-member-transact-sql.md). 若要确定是否[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登录名是数据库角色的成员，请使用[IS_ROLEMEMBER &#40;Transact SQL &#41;](../../t-sql/functions/is-rolemember-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 要求具有服务器角色的 VIEW DEFINITION 权限。  
  
## <a name="examples"></a>示例  
 以下示例指示当前用户的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名是 `sysadmin` 固定服务器角色的成员。  
  
```  
IF IS_SRVROLEMEMBER ('sysadmin') = 1  
   print 'Current user''s login is a member of the sysadmin role'  
ELSE IF IS_SRVROLEMEMBER ('sysadmin') = 0  
   print 'Current user''s login is NOT a member of the sysadmin role'  
ELSE IF IS_SRVROLEMEMBER ('sysadmin') IS NULL  
   print 'ERROR: The server role specified is not valid.';  
```  
  
 下面的示例指示 Pat 的域登录名是否为属于**diskadmin**固定的服务器角色。  
  
```  
SELECT IS_SRVROLEMEMBER('diskadmin', 'Contoso\Pat');  
```  
  
## <a name="see-also"></a>另请参阅  
 [IS_MEMBER &#40;Transact SQL &#41;](../../t-sql/functions/is-member-transact-sql.md)   
 [安全函数 (Transact-SQL)](../../t-sql/functions/security-functions-transact-sql.md)  
  
  
