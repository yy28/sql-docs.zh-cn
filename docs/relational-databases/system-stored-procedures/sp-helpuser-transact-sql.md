---
title: "sp_helpuser (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_helpuser
- sp_helpuser_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_helpuser
ms.assetid: 9c70b41d-ef4c-43df-92da-bd534c287ca1
caps.latest.revision: "29"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2dcf314d52fd7d20dae8ad8ddb163a331a89d52c
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2017
---
# <a name="sphelpuser-transact-sql"></a>sp_helpuser (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  报告有关当前数据库中数据库级主体的信息。  
  
> [!IMPORTANT]  
>  **sp_helpuser**不返回有关在中引入的安全对象的信息[!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]。 使用[sys.database_principals](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)相反。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_helpuser [ [ @name_in_db = ] 'security_account' ]  
```  
  
## <a name="arguments"></a>参数  
 [  **@name_in_db =** ] *security_account*  
 当前数据库中数据库用户或数据库角色的名称。 *security_account*必须存在于当前数据库。 *security_account*是**sysname**，默认值为 NULL。 如果*security_account*未指定， **sp_helpuser**返回有关所有数据库主体的信息。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）或 1（失败）  
  
## <a name="result-sets"></a>结果集  
 下表显示的结果集时都不用户帐户也不是[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]为指定 Windows 用户或*security_account*。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**UserName**|**sysname**|当前数据库中的用户。|  
|**RoleName**|**sysname**|向其角色**用户名**所属。|  
|**LoginName**|**sysname**|登录名的**用户名**。|  
|**DefDBName**|**sysname**|默认数据库**用户名**。|  
|**DefSchemaName**|**sysname**|数据库用户的默认架构。|  
|**UserID**|**int**|ID**用户名**当前数据库中。|  
|**SID**|**int**|用户的安全标识号 (SID)。|  
  
 下表显示未指定用户帐户，并且当前数据库中存在别名时的结果集。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**LoginName**|**sysname**|当前数据库中已经化名为用户名的登录名。|  
|**UserNameAliasedTo**|**sysname**|当前数据库中登录名要化名为的用户名。|  
  
 下表显示的结果集时为指定角色*security_account*。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**Role_name**|**sysname**|当前数据库中角色的名称。|  
|**Role_id**|**int**|当前数据库中角色的角色 ID。|  
|**Users_in_role**|**sysname**|当前数据库中角色的成员。|  
|**用户 Id**|**int**|角色的成员的用户 ID。|  
  
## <a name="remarks"></a>注释  
 若要查看数据库角色的成员资格有关的信息，请使用[sys.database_role_members](../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)。 若要查看有关服务器角色成员的信息，请使用[sys.server_role_members](../../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md)，而若要查看有关服务器级别主体的信息，请使用[sys.server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)。  
  
## <a name="permissions"></a>Permissions  
 要求 **公共** 角色具有成员身份。  
  
 返回的信息取决于对元数据的访问权限的限制。 主体对其不具有权限的实体将不会显示。 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="examples"></a>示例  
  
### <a name="a-listing-all-users"></a>A. 列出所有用户  
 以下示例列出当前数据库中的所有用户。  
  
```  
EXEC sp_helpuser;  
```  
  
### <a name="b-listing-information-for-a-single-user"></a>B. 列出单个用户的信息  
 以下示例列出有关用户数据库所有者 (`dbo`) 的信息。  
  
```  
EXEC sp_helpuser 'dbo';  
```  
  
### <a name="c-listing-information-for-a-database-role"></a>C. 列出某个数据库角色的信息  
 以下示例列出有关 `db_securityadmin` 固定数据库角色的信息。  
  
```  
EXEC sp_helpuser 'db_securityadmin';  
```  
  
## <a name="see-also"></a>另请参阅  
 [安全存储过程 &#40;Transact SQL &#41;](../../relational-databases/system-stored-procedures/security-stored-procedures-transact-sql.md)   
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [主体（数据库引擎）](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [sys.database_principals (Transact-SQL)](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)   
 [sys.database_role_members (Transact-SQL)](../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)   
 [sys.server_principals (Transact-SQL)](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [sys.server_role_members (Transact-SQL)](../../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md)  
  
  
