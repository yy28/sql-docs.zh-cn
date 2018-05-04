---
title: sp_addrolemember (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_addrolemember_TSQL
- sp_addrolemember
dev_langs:
- TSQL
helpviewer_keywords:
- sp_addrolemember
ms.assetid: a583c087-bdb3-46d2-b9e5-3921b3e6d10b
caps.latest.revision: 59
author: edmacauley
ms.author: edmaca
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 893845b0ff19e9d2dba4a5cf55ceee6ac436403e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="spaddrolemember-transact-sql"></a>sp_addrolemember (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  为当前数据库中的数据库角色添加数据库用户、数据库角色、Windows 登录名或 Windows 组。  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 使用[ALTER ROLE](../../t-sql/statements/alter-role-transact-sql.md)相反。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
sp_addrolemember [ @rolename = ] 'role',  
    [ @membername = ] 'security_account'  
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
sp_addrolemember 'role', 'security_account'  
```  
  
## <a name="arguments"></a>参数  
 [ @rolename=] '*角色*  
 当前数据库中的数据库角色的名称。 *角色*是**sysname**，无默认值。  
  
 [ @membername=] '*security_account*  
 添加到该角色中的安全帐户。 *security_account*是**sysname**，无默认值。 *security_account*可以是数据库用户、 数据库角色、 Windows 登录名或 Windows 组。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="remarks"></a>注释  
 使用 sp_addrolemember 添加到角色中的成员会继承该角色的权限。 如果新成员是没有对应数据库用户的 Windows 级主体，则会创建数据库用户，但数据库用户可能不会完全映射到登录名。 始终应检查登录名是否存在以及是否能访问数据库。  
  
 角色不能将自身包含为成员。 即使只有一个或多个中间成员身份间接体现这种成员关系，这种“循环”定义也无效。  
  
 sp_addrolemember 无法向角色添加固定的数据库角色、 固定的服务器角色或 dbo。 sp_addrolemember 不能在用户定义的事务内执行。  
  
 只能使用 sp_addrolemember 将向数据库角色添加成员。 若要将成员添加到服务器角色，使用[sp_addsrvrolemember &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addsrvrolemember-transact-sql.md)。  
  
## <a name="permissions"></a>权限  
 为灵活的数据库角色添加成员需要满足以下条件之一：  
  
-   Db_securityadmin 或 db_owner 固定的数据库角色的成员身份。  
  
-   具有拥有该角色的角色的成员身份。  
  
-   **ALTER ANY ROLE**权限或**ALTER**在角色上的权限。  
  
 向固定数据库角色添加成员要求具有 db_owner 固定数据库角色的成员身份。  
  
## <a name="examples"></a>示例  
  
### <a name="a-adding-a-windows-login"></a>A. 添加 Windows 登录名  
 下面的示例添加的 Windows 登录名`Contoso\Mary5`到`AdventureWorks2012`数据库作为用户`Mary5`。 用户 `Mary5` 随即被添加到 `Production` 角色中。  
  
> [!NOTE]  
>  因为 `Contoso\Mary5` 在 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 数据库中被识别为数据库用户 `Mary5`，所以必须指定用户名 `Mary5`。 如果没有 `Contoso\Mary5` 登录名存在，语句将失败。 请通过使用您的域中的登录名进行测试。  
  
```  
USE AdventureWorks2012;  
GO  
CREATE USER Mary5 FOR LOGIN [Contoso\Mary5] ;  
GO  
```  
  
### <a name="b-adding-a-database-user"></a>B. 添加数据库用户  
 以下示例将数据库用户 `Mary5` 添加到当前数据库的 `Production` 数据库角色中。  
  
```  
EXEC sp_addrolemember 'Production', 'Mary5';  
```  
  
## <a name="examples-includesssdwincludessssdw-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-adding-a-windows-login"></a>C. 添加 Windows 登录名  
 下面的示例添加登录名`LoginMary`到`AdventureWorks2008R2`数据库作为用户`UserMary`。 用户 `UserMary` 随即被添加到 `Production` 角色中。  
  
> [!NOTE]  
>  因为该登录名`LoginMary`数据库用户称为`UserMary`中[!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]数据库，用户名称`UserMary`必须指定。 如果没有 `Mary5` 登录名存在，语句将失败。 登录名和用户通常具有相同的名称。 此示例使用不同的名称来区分影响与用户的登录名的操作。  
  
```  
-- Uses AdventureWorks  
  
CREATE USER UserMary FOR LOGIN LoginMary ;  
GO  
EXEC sp_addrolemember 'Production', 'UserMary'  
```  
  
### <a name="d-adding-a-database-user"></a>D. 添加数据库用户  
 以下示例将数据库用户 `UserMary` 添加到当前数据库的 `Production` 数据库角色中。  
  
```  
EXEC sp_addrolemember 'Production', 'UserMary'  
```  
  
## <a name="see-also"></a>另请参阅  
 [安全存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [sp_addsrvrolemember (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-addsrvrolemember-transact-sql.md)   
 [sp_droprolemember & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md)   
 [sp_grantdbaccess (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-grantdbaccess-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [数据库级别的角色](../../relational-databases/security/authentication-access/database-level-roles.md)  
  
  
