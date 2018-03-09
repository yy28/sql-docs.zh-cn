---
title: "IS_ROLEMEMBER (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- IS_ROLEMEMBER
- IS_ROLEMEMBER_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- roles [SQL Server], members
- IS_ROLEMEMBER function
- members [SQL Server], verifying
ms.assetid: 73efa688-ae91-4014-98bc-1cabe47321f7
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: fd8574c27bea00127096dc1f0040c8c3f93e96cb
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="isrolemember-transact-sql"></a>IS_ROLEMEMBER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  指示指定的数据库主体是否为指定数据库角色的成员。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
IS_ROLEMEMBER ( 'role' [ , 'database_principal' ] )  
```  
  
## <a name="arguments"></a>参数  
  *角色*   
 要检查的数据库角色的名称。 *角色*是**sysname**。  
  
  *database_principal*   
 要检查的数据库用户、数据库角色或应用程序角色的名称。 *database_principal*是**sysname**，默认值为 NULL。 如果未指定值，则结果视当前执行上下文而定。 如果此参数包含词 NULL，将返回 NULL。  
  
## <a name="return-types"></a>返回类型  
 **int**  
  
|返回值|Description|  
|------------------|-----------------|  
|0|*database_principal*不是成员的*角色*。|  
|1|*database_principal*为属于*角色*。|  
|NULL|*database_principal*或*角色*无效，或者您没有权限查看的角色成员资格。|  
  
## <a name="remarks"></a>注释  
 请使用 IS_ROLEMEMBER 确定当前用户是否可以执行需要数据库角色权限的操作。  
  
 如果*database_principal*如 Contoso\Mary5、 IS_ROLEMEMBER 将返回 NULL，除非基于 Windows 登录名， *database_principal*已授予或拒绝直接访问[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
 如果可选*database_principal*参数是未提供，并且如果*database_principal*取决于 Windows 域登录名，它可能通过在 Windows 组的成员资格数据库角色的成员. 要解析这种间接成员身份，IS_ROLEMEMBER 将从域控制器中请求 Windows 组成员身份信息。 如果无法访问域控制器或域控制器没有响应，则 IS_ROLEMEMBER 在返回角色成员身份信息时只考虑用户及其本地组。 如果指定的用户不是当前用户，则 IS_ROLEMEMBER 返回的值可能不同于验证器（如 Active Directory）上次进行的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据更新。  
  
 如果可选*database_principal*提供参数、 正在查询的数据库主体必须存在于 sys.database_principals，或 IS_ROLEMEMBER 将返回 NULL。 这指示*database_principal*不在此数据库中有效。  
  
 当*database_principal*参数是根据一个域登录名或基于 Windows 组和域控制器不可访问、 IS_ROLEMEMBER 对的调用将失败，并且可能会返回不正确或不完整的数据。  
  
 如果域控制器不可用，并且可以在本地对 Windows 主体进行身份验证时（例如本地 Windows 帐户或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名），对 IS_ROLEMEMBER 的调用将返回准确的信息。  
  
 **IS_ROLEMEMBER**始终返回 0，在使用 Windows 组作为数据库主体自变量，并且此 Windows 组是另一个 Windows 组，即，反过来，指定的数据库角色的成员的成员。  
  
 用户帐户控制 (UAC) 中找到[!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)]和 Windows Server 2008 也可能返回不同的结果。 这取决于用户在访问服务器时是作为 Windows 组成员还是特定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 用户。  
  
 此函数计算角色成员身份，而不是基础权限。 例如， **db_owner**固定的数据库角色具有**控制数据库**权限。 如果用户具有**控制数据库**权限但不是角色的成员，此函数将正确地报告用户不是成员的**db_owner**角色，即使用户具有相同权限。  
  
## <a name="related-functions"></a>相关函数  
 若要确定当前用户是否为指定的 Windows 组的成员或[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库角色，使用[IS_MEMBER &#40;Transact SQL &#41;](../../t-sql/functions/is-member-transact-sql.md). 若要确定是否[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登录名是服务器角色的成员，请使用[IS_SRVROLEMEMBER &#40;Transact SQL &#41;](../../t-sql/functions/is-srvrolemember-transact-sql.md).  
  
## <a name="permissions"></a>Permissions  
 要求具有数据库角色的 VIEW DEFINITION 权限。  
  
## <a name="examples"></a>示例  
 以下示例指示当前用户是否为 `db_datareader` 固定数据库角色的成员。  
  
```  
IF IS_ROLEMEMBER ('db_datareader') = 1  
   print 'Current user is a member of the db_datareader role'  
ELSE IF IS_ROLEMEMBER ('db_datareader') = 0  
   print 'Current user is NOT a member of the db_datareader role'  
ELSE IF IS_ROLEMEMBER ('db_datareader') IS NULL  
   print 'ERROR: The database role specified is not valid.';  
```  
  
## <a name="see-also"></a>另请参阅  
 [创建角色 &#40;Transact SQL &#41;](../../t-sql/statements/create-role-transact-sql.md)   
 [ALTER 角色 &#40;Transact SQL &#41;](../../t-sql/statements/alter-role-transact-sql.md)   
 [删除角色 &#40;Transact SQL &#41;](../../t-sql/statements/drop-role-transact-sql.md)   
 [创建服务器角色 &#40;Transact SQL &#41;](../../t-sql/statements/create-server-role-transact-sql.md)   
 [ALTER SERVER 角色 &#40;Transact SQL &#41;](../../t-sql/statements/alter-server-role-transact-sql.md)   
 [删除服务器角色 &#40;Transact SQL &#41;](../../t-sql/statements/drop-server-role-transact-sql.md)   
 [IS_MEMBER &#40;Transact SQL &#41;](../../t-sql/functions/is-member-transact-sql.md)   
 [IS_SRVROLEMEMBER &#40;Transact SQL &#41;](../../t-sql/functions/is-srvrolemember-transact-sql.md)   
 [安全函数 (Transact-SQL)](../../t-sql/functions/security-functions-transact-sql.md)  
  
  
