---
title: "IS_MEMBER (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 07/29/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- IS_MEMBER
- IS_MEMBER_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- database roles [SQL Server], members
- current member status
- roles [SQL Server], members
- testing member status
- members [SQL Server]
- checking member status
- IS_MEMBER function
- verifying member status
- groups [SQL Server], members
- members [SQL Server], verifying
ms.assetid: 77cb68a0-19b7-4fe1-ab17-e5587699631b
caps.latest.revision: 25
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 472d8f1cc258fdc57ef454fbb35f51e3f83b288d
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="ismember-transact-sql"></a>IS_MEMBER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  指示当前用户是否为指定的成员[!INCLUDE[msCoName](../../includes/msconame-md.md)]Windows 组或[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库角色。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
IS_MEMBER ( { 'group' | 'role' } )  
```  
  
## <a name="arguments"></a>参数  
  *组*   
**适用于**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]
  
 是要检查; 的 Windows 组的名称必须采用格式*域*\\*组*。 *组*是**sysname**。  
  
  *角色*   
 是的名称[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]要检查的角色。 *角色*是**sysname**并且可以包括数据库固定角色或用户定义的角色，但不是能在服务器角色。  
  
## <a name="return-types"></a>返回类型  
 **int**  
  
## <a name="remarks"></a>注释  
 IS_MEMBER 返回以下值。  
  
|返回值|Description|  
|------------------|-----------------|  
|0|当前用户不属于*组*或*角色*。|  
|1|当前用户为属于*组*或*角色*。|  
|NULL|任一*组*或*角色*无效。 在由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名或使用应用程序角色的登录名查询时，对于 Windows 组返回 NULL。|  
  
 IS_MEMBER 通过检查 Windows 创建的访问令牌来确定 Windows 组成员身份。 该访问标记不反映在用户连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例后对组成员身份进行的更改。 Windows 组成员身份不能由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 应用程序角色查询。  
  
 若要添加和删除数据库角色的成员，请使用[ALTER ROLE &#40;Transact SQL &#41;](../../t-sql/statements/alter-role-transact-sql.md). 若要添加和删除服务器角色的成员，请使用[ALTER SERVER ROLE &#40;Transact SQL &#41;](../../t-sql/statements/alter-server-role-transact-sql.md).  
  
 此函数计算角色成员身份，而不是基础权限。 例如， **db_owner**固定的数据库角色具有**控制数据库**权限。 如果用户具有**控制数据库**权限但不是角色的成员，此函数将正确地报告用户不是成员的**db_owner**角色，即使用户具有相同权限。  
  
 成员**sysadmin**固定的服务器角色输入作为每个数据库**dbo**用户。 检查权限的成员**sysadmin**固定的服务器角色，检查权限**dbo**，不是原始的登录名。 由于**dbo**无法添加到数据库角色和 Windows 组中不存在**dbo**将始终返回 0 个 （或如果角色不存在则为 NULL）。  
  
## <a name="related-functions"></a>相关函数  
 若要确定是否另一个[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登录名是数据库角色的成员，请使用[IS_ROLEMEMBER &#40;Transact SQL &#41;](../../t-sql/functions/is-rolemember-transact-sql.md). 若要确定是否[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登录名是服务器角色的成员，请使用[IS_SRVROLEMEMBER &#40;Transact SQL &#41;](../../t-sql/functions/is-srvrolemember-transact-sql.md).  
  
## <a name="examples"></a>示例  
 以下示例检查当前用户是否为数据库角色或 Windows 域组的成员。  
  
```  
-- Test membership in db_owner and print appropriate message.  
IF IS_MEMBER ('db_owner') = 1  
   PRINT 'Current user is a member of the db_owner role'  
ELSE IF IS_MEMBER ('db_owner') = 0  
   PRINT 'Current user is NOT a member of the db_owner role'  
ELSE IF IS_MEMBER ('db_owner') IS NULL  
   PRINT 'ERROR: Invalid group / role specified';  
GO  
  
-- Execute SELECT if user is a member of ADVWORKS\Shipping.  
IF IS_MEMBER ('ADVWORKS\Shipping') = 1  
   SELECT 'User ' + USER + ' is a member of ADVWORKS\Shipping.';   
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [IS_SRVROLEMEMBER &#40;Transact SQL &#41;](../../t-sql/functions/is-srvrolemember-transact-sql.md)   
 [主体（数据库引擎）](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [安全性目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [安全函数 (Transact-SQL)](../../t-sql/functions/security-functions-transact-sql.md)  
  
  

