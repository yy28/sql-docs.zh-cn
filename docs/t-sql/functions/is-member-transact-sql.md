---
title: IS_MEMBER (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/29/2017
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
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: e14fc4cf70066c21a8a837760d4325a19ae4ff1c
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="ismember-transact-sql"></a>IS_MEMBER (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  指示当前用户是否为指定 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 组或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库角色的成员。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
IS_MEMBER ( { 'group' | 'role' } )  
```  
  
## <a name="arguments"></a>参数  
 **'** group **'**  
适用范围：[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]、
  
 正在检查的 Windows 组的名称；必须采用格式 Domain\\Group。 group 的数据类型为 sysname。  
  
 'role'  
 要检查的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 角色的名称。 role 的数据类型为 sysname，它可以包括数据库固定角色或用户定义的角色，但不能包括服务器角色。  
  
## <a name="return-types"></a>返回类型  
 **int**  
  
## <a name="remarks"></a>Remarks  
 IS_MEMBER 返回以下值。  
  
|返回值|Description|  
|------------------|-----------------|  
|0|当前用户不是 group 或 role 的成员。|  
|@shouldalert|当前用户是 group 或 role 的成员。|  
|NULL|group 或 role 无效。 在由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名或使用应用程序角色的登录名查询时，对于 Windows 组返回 NULL。|  
  
 IS_MEMBER 通过检查 Windows 创建的访问令牌来确定 Windows 组成员身份。 该访问标记不反映在用户连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例后对组成员身份进行的更改。 Windows 组成员身份不能由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名或 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 应用程序角色查询。  
  
 若要在数据库角色中添加和删除成员，请使用 [ALTER ROLE (Transact-SQL)](../../t-sql/statements/alter-role-transact-sql.md)。 若要在服务器角色中添加和删除成员，请使用 [ALTER SERVER ROLE (Transact-SQL)](../../t-sql/statements/alter-server-role-transact-sql.md)。  
  
 此函数计算角色成员身份，而不是基础权限。 例如，db_owner 固定数据库角色具有 CONTROL DATABASE 权限。 如果用户具有 CONTROL DATABASE 权限，但不是该角色的成员，此函数将正确报告用户不是 db_owner 角色的成员，即使用户具有相同的权限也是如此。  
  
 sysadmin 固定服务器角色的成员均以 dbo 用户身份进入每个数据库。 检查 sysadmin 固定服务器角色成员的权限会检查 dbo 的权限，而不是原始登录名。 由于 dbo 无法添加到数据库角色且在 Windows 组中不存在，因此 dbo 将始终返回 0（或者如果角色不存在，则为 NULL）。  
  
## <a name="related-functions"></a>相关函数  
 若要确定另一个 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名是否为数据库角色的成员，请使用 [IS_ROLEMEMBER (Transact-SQL)](../../t-sql/functions/is-rolemember-transact-sql.md)。 若要确定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名是否为服务器角色的成员，请使用 [IS_SRVROLEMEMBER (Transact-SQL)](../../t-sql/functions/is-srvrolemember-transact-sql.md)。  
  
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
 [IS_SRVROLEMEMBER (Transact-SQL)](../../t-sql/functions/is-srvrolemember-transact-sql.md)   
 [主体（数据库引擎）](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [安全性目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [安全函数 (Transact-SQL)](../../t-sql/functions/security-functions-transact-sql.md)  
  
  
