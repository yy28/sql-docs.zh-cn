---
title: 系统database_principals（转算-SQL） |微软文档
ms.custom: ''
ms.date: 10/27/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- database_principals
- database_principals_TSQL
- sys.database_principals
- sys.database_principals_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.database_principals catalog view
ms.assetid: 8cb239e9-eb8c-4109-9cec-0d35de95fa0e
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: feed483cf3ee08c0652e55de51b1f73fc087ed39
ms.sourcegitcommit: 7ed12a64f7f76d47f5519bf1015d19481dd4b33a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2020
ms.locfileid: "80873113"
---
# <a name="sysdatabase_principals-transact-sql"></a>sys.database_principals (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中的每个安全主体返回一行。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|主体名称，在数据库中唯一。|  
|**principal_id**|**Int**|主体 ID，在数据库中唯一。|  
|**type**|**字符 （1）**|主体类型：<br /><br /> A = 应用程序角色<br /><br /> C = 映射到证书的用户<br /><br /> E = Azure 活动目录的外部用户<br /><br /> G = Windows 组<br /><br /> K = 映射到非对称密钥的用户<br /><br /> R = 数据库角色<br /><br /> S = SQL 用户<br /><br /> U = Windows 用户<br /><br /> X = Azure 活动目录组或应用程序的外部组|  
|**type_desc**|**nvarchar(60)**|主体类型的说明。<br /><br /> APPLICATION_ROLE<br /><br /> CERTIFICATE_MAPPED_USER<br /><br /> EXTERNAL_USER<br /><br /> WINDOWS_GROUP<br /><br /> ASYMMETRIC_KEY_MAPPED_USER<br /><br /> DATABASE_ROLE<br /><br /> SQL_USER<br /><br /> WINDOWS_USER<br /><br /> EXTERNAL_GROUPS|  
|**default_schema_name**|**sysname**|当 SQL 名称不指定架构时要使用的名称。 对于非 S、U 或 A 类型的主体，为 Null。|  
|**create_date**|**datetime**|主体的创建时间。|  
|**modify_date**|**datetime**|上次修改主体的时间。|  
|**owning_principal_id**|**Int**|拥有此主体的主体的 ID。 默认情况下，所有固定数据库角色均归**dbo**所有。|  
|**sid**|**瓦二进制 （85）**|主体的 SID（安全标识符）。  SYS 和 INFORMATION SCHEMAS 为 NULL。|  
|**is_fixed_role**|**bit**|如果为 1，则该行表示与下面的某个固定数据库角色对应的条目：db_owner、db_accessadmin、db_datareader、db_datawriter、db_ddladmin、db_securityadmin、db_backupoperator、db_denydatareader、db_denydatawriter。|  
|**authentication_type**|**Int**|**适用于**：[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]及更高版本。<br /><br /> 指示身份验证类型。 以下是可能的值及其说明。<br /><br /> 0 ： 无身份验证<br />1 ： 实例身份验证<br />2 ： 数据库身份验证<br />3 ： 窗口身份验证<br />4 ： Azure 活动目录身份验证|  
|**authentication_type_desc**|**nvarchar(60)**|**适用于**：[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]及更高版本。<br /><br /> 身份验证类型说明。 以下是可能的值及其说明。<br /><br /> 无 ：无身份验证<br />实例 ： 实例身份验证<br />数据库 ： 数据库身份验证<br />窗口 ： 窗口身份验证<br />外部：Azure 活动目录身份验证|  
|**default_language_name**|**sysname**|**适用于**：[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]及更高版本。<br /><br /> 指示此主体的默认语言。|  
|**default_language_lcid**|**Int**|**适用于**：[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]及更高版本。<br /><br /> 指示此主体的默认 LCID。|  
|**allow_encrypted_value_modifications**|**bit**|**适用于**：[!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)]及更高[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]版本。<br /><br /> 取消在大容量复制操作期间对服务器进行加密元数据检查。 这使用户能够在表或数据库之间批量复制使用"始终加密"加密的数据，而无需解密数据。 默认为 OFF。 |      
  
## <a name="remarks"></a>备注  
 *PasswordLastSetTime*属性在 SQL Server 的所有受支持配置上都可用，但仅当 SQL Server 在 Windows Server 2003 或更高版本上运行并且启用了CHECK_POLICY和CHECK_EXPIRATION时，其他属性才可用。 有关详细信息，请参阅[密码策略](../../relational-databases/security/password-policy.md)。
在主体已被丢弃且因此不能保证不断增加的情况下，可以重复使用principal_id的值。
  
## <a name="permissions"></a>权限  
 任何用户都可以查看自己的用户名称、系统用户和固定的数据库角色。 要查看其他用户，需要获取 ALTER ANY USER 或相关的用户权限。 要查看用户定义的角色，需要获取 ALTER ANY ROLE 或相关的角色成员身份。  
  
## <a name="examples"></a>示例  
  
### <a name="a-listing-all-the-permissions-of-database-principals"></a>A：列出数据库主体的所有权限  
 以下查询将列出明确对数据库主体授予或拒绝的权限。  
  
> [!IMPORTANT]  
>  固定数据库角色的权限不会出现在 sys.database_permissions 中。 因此，数据库主体可能具有此处未列出的其他权限。  
  
```  
SELECT pr.principal_id, pr.name, pr.type_desc,   
    pr.authentication_type_desc, pe.state_desc, pe.permission_name  
FROM sys.database_principals AS pr  
JOIN sys.database_permissions AS pe  
    ON pe.grantee_principal_id = pr.principal_id;  
```  
  
### <a name="b-listing-permissions-on-schema-objects-within-a-database"></a>B：列出对数据库中架构对象的权限  
 以下查询将 sys.database_principals 和 sys.database_permissions 与 sys.objects 和 sys.schemas 联接，以列出对特定架构对象授予或拒绝的权限。  
  
```  
SELECT pr.principal_id, pr.name, pr.type_desc,   
    pr.authentication_type_desc, pe.state_desc,   
    pe.permission_name, s.name + '.' + o.name AS ObjectName  
FROM sys.database_principals AS pr  
JOIN sys.database_permissions AS pe  
    ON pe.grantee_principal_id = pr.principal_id  
JOIN sys.objects AS o  
    ON pe.major_id = o.object_id  
JOIN sys.schemas AS s  
    ON o.schema_id = s.schema_id;  
```  
  
## <a name="examples-sssdwfull-and-sspdw"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="c-listing-all-the-permissions-of-database-principals"></a>C： 列出数据库主体的所有权限  
 以下查询将列出明确对数据库主体授予或拒绝的权限。  
  
> [!IMPORTANT]  
>  固定数据库角色的权限不显示在 中`sys.database_permissions`。 因此，数据库主体可能具有此处未列出的其他权限。  
  
```  
SELECT pr.principal_id, pr.name, pr.type_desc,   
    pr.authentication_type_desc, pe.state_desc, pe.permission_name  
FROM sys.database_principals AS pr  
JOIN sys.database_permissions AS pe  
    ON pe.grantee_principal_id = pr.principal_id;  
```  
  
### <a name="d-listing-permissions-on-schema-objects-within-a-database"></a>D：列出数据库中的架构对象的权限  
 以下`sys.database_principals`查询联接`sys.database_permissions`并到`sys.objects`和`sys.schemas`列出授予或拒绝特定架构对象的权限。  
  
```  
SELECT pr.principal_id, pr.name, pr.type_desc,   
    pr.authentication_type_desc, pe.state_desc,   
    pe.permission_name, s.name + '.' + o.name AS ObjectName  
FROM sys.database_principals AS pr  
JOIN sys.database_permissions AS pe  
    ON pe.grantee_principal_id = pr.principal_id  
JOIN sys.objects AS o  
    ON pe.major_id = o.object_id  
JOIN sys.schemas AS s  
    ON o.schema_id = s.schema_id;  
```  
  
## <a name="see-also"></a>另请参阅  
 [主体&#40;数据库引擎&#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)   
 [系统server_principals&#40;交易-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)   
 [安全目录视图&#40;交易-SQL&#41;](../../relational-databases/system-catalog-views/security-catalog-views-transact-sql.md)   
 [包含数据库用户 - 使数据库可移植](../../relational-databases/security/contained-database-users-making-your-database-portable.md)   
 [使用 Azure 活动目录身份验证连接到 SQL 数据库](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication)  
  
  


