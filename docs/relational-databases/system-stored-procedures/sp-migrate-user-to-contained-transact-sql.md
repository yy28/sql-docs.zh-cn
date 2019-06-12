---
title: sp_migrate_user_to_contained (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/11/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_migrate_user_to_contained
- sp_migrate_user_to_contained_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_migrate_user_to_contained
ms.assetid: b3a49ff6-46ad-4ee7-b6fe-7e54213dc33e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 9bdab8cd50a16913f37115f0d38c00c5c699bc0f
ms.sourcegitcommit: 113fa84148d6d475c7c1475666ea08ac6965e71c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/11/2019
ms.locfileid: "66836304"
---
# <a name="spmigrateusertocontained-transact-sql"></a>sp_migrate_user_to_contained (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  将映射到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名的数据库用户转换为具有密码的包含数据库用户。 在包含的数据库中，请使用此过程删除安装了该数据库的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的依赖项。 **sp_migrate_user_to_contained**将用户与原始[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]登录名，以便可以为包含的数据库单独管理密码和默认语言等设置。 **sp_migrate_user_to_contained**将包含的数据库移到另一个实例之前，可以使用[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]以取消对当前的依赖关系[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例登录名。  
  
> [!NOTE]
> 使用时要小心**sp_migrate_user_to_contained**，如您将不能反向效果。 仅在包含数据库中使用此过程。 有关详细信息，请参阅 [Contained Databases](../../relational-databases/databases/contained-databases.md)。  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_migrate_user_to_contained [ @username = ] N'user' ,   
    [ @rename = ] { N'copy_login_name' | N'keep_name' } ,   
    [ @disablelogin = ] { N'disable_login' | N'do_not_disable_login' }   
```  
  
## <a name="arguments"></a>参数  
 [ **@username =** ] **N'***user***'**  
 当前包含的数据库中的用户名称，该用户将映射到经过身份验证的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名。 值是**sysname**，默认值为**NULL**。  
  
 [ **@rename =** ] **N'***copy_login_name***'**  | **N'***keep_name***'**  
 如果基于登录名的数据库用户具有不同的用户名与登录名，使用*keep_name*在迁移期间保留的数据库用户名称。 使用*copy_login_name*若要创建新的包含的数据库用户的登录名，而不是用户的名称。 如果基于登录名的数据库用户具有与登录名相同的用户名，这两个选项将创建包含数据库用户而不更改名称。  
  
 [ **@disablelogin =** ] **N'***disable_login***'**  | **N'***do_not_disable_login***'**  
 *disable_login*禁用登录名的 master 数据库中。 若要连接该登录名处于禁用状态时，该连接必须提供包含的数据库名称作为**初始目录**作为连接字符串的一部分。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="remarks"></a>备注  
 **sp_migrate_user_to_contained**创建包含的数据库用户具有密码，而不考虑属性或登录名的权限。 例如，过程可能会成功如果禁用该登录名或用户被拒绝**CONNECT**对数据库的权限。  
  
 **sp_migrate_user_to_contained**具有以下限制。  
  
-   数据库中不能已存在此用户名。  
  
-   无法转换内置用户，例如，dbo 和 guest。  
  
-   不能中指定的用户**EXECUTE AS**子句的已签名的存储过程。  
  
-   用户不能拥有一个存储的过程中包括**EXECUTE AS OWNER**子句。  
  
-   **sp_migrate_user_to_contained**不能在系统数据库中使用。  
  
## <a name="security"></a>安全性  
 在迁移用户时，切勿从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例中禁用或删除所有管理员登录名。 如果删除所有登录名，请参阅[连接到 SQL Server 系统管理员被锁定时](../../database-engine/configure-windows/connect-to-sql-server-when-system-administrators-are-locked-out.md)。  
  
 如果**BUILTIN\Administrators**登录名存在，管理员可以通过启动其应用程序使用连接**以管理员身份运行**选项。  
  
### <a name="permissions"></a>权限  
 要求具有 **CONTROL SERVER** 权限。  
  
## <a name="examples"></a>示例  
  
### <a name="a-migrating-a-single-user"></a>A. 迁移单个用户  
 以下示例将名为 `Barry` 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名迁移到具有密码的包含数据库用户。 该示例不会更改用户名称，并将该登录名保留为已启用。  
  
```sql  
sp_migrate_user_to_contained   
@username = N'Barry',  
@rename = N'keep_name',  
@disablelogin = N'do_not_disable_login' ;  
  
```  
  
### <a name="b-migrating-all-database-users-with-logins-to-contained-database-users-without-logins"></a>B. 将所有具有登录名的数据库用户迁移到没有登录名的包含数据库用户  
 以下示例将所有基于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名的用户迁移到具有密码的包含数据库用户。 该示例不包括未启用的登录名。 必须在包含的数据库中执行该示例。  
  
```sql  
DECLARE @username sysname ;  
DECLARE user_cursor CURSOR  
    FOR   
        SELECT dp.name   
        FROM sys.database_principals AS dp  
        JOIN sys.server_principals AS sp   
        ON dp.sid = sp.sid  
        WHERE dp.authentication_type = 1 AND sp.is_disabled = 0;  
OPEN user_cursor  
FETCH NEXT FROM user_cursor INTO @username  
    WHILE @@FETCH_STATUS = 0  
    BEGIN  
        EXECUTE sp_migrate_user_to_contained   
        @username = @username,  
        @rename = N'keep_name',  
        @disablelogin = N'disable_login';  
    FETCH NEXT FROM user_cursor INTO @username  
    END  
CLOSE user_cursor ;  
DEALLOCATE user_cursor ;  
```  
  
## <a name="see-also"></a>请参阅  
 [Migrate to a Partially Contained Database](../../relational-databases/databases/migrate-to-a-partially-contained-database.md)   
 [包含的数据库](../../relational-databases/databases/contained-databases.md)  
  
  
