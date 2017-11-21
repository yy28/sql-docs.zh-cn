---
title: "创建数据库审核规范 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE DATABASE AUDIT
- DATABASE_AUDIT_SPECIFICATION_TSQL
- DATABASE AUDIT SPECIFICATION
- CREATE_DATABASE_AUDIT_SPECIFICATION_TSQL
- CREATE_DATABASE_AUDIT_TSQL
- CREATE DATABASE AUDIT SPECIFICATION
dev_langs:
- TSQL
helpviewer_keywords:
- database audit specification
- CREATE DATABASE AUDIT SPECIFICATION statement
ms.assetid: 0544da48-0ca3-4a01-ba4c-940e23dc315b
caps.latest.revision: 26
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a0148505f91cdf572205f34b3854a3c093f5352d
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="create-database-audit-specification-transact-sql"></a>CREATE DATABASE AUDIT SPECIFICATION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 审核功能创建数据库审核规范对象。 有关详细信息，请参阅 [SQL Server Audit（数据库引擎）](../../relational-databases/security/auditing/sql-server-audit-database-engine.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
CREATE DATABASE AUDIT SPECIFICATION audit_specification_name  
{  
    FOR SERVER AUDIT audit_name   
        [ { ADD ( { <audit_action_specification> | audit_action_group_name } )   
      } [, ...n] ]  
    [ WITH ( STATE = { ON | OFF } ) ]  
}  
[ ; ]  
<audit_action_specification>::=  
{  
      action [ ,...n ]ON [ class :: ] securable BY principal [ ,...n ]  
}  
```  
  
## <a name="arguments"></a>参数  
 *audit_specification_name*  
 是审核规范的名称。  
  
 *audit_name*  
 是应用此规范的审核的名称。  
  
 *audit_action_specification*  
 是主体对安全对象执行的应记录到审核中的操作的规范。  
  
 *操作*  
 是一个或多个数据库级别可审核操作的名称。 审核操作的列表，请参阅[SQL Server 审核操作组和操作](../../relational-databases/security/auditing/sql-server-audit-action-groups-and-actions.md)。  
  
 *audit_action_group_name*  
 是一个或多个数据库级别可审核操作组的名称。 审核操作组的列表，请参阅[SQL Server 审核操作组和操作](../../relational-databases/security/auditing/sql-server-audit-action-groups-and-actions.md)。  
  
 *类*  
 是安全对象上的类名（如果适用）。  
  
 *安全对象*  
 是应用审核操作或审核操作组的数据库中的表、视图或其他安全对象。 有关详细信息，请参阅 [Securables](../../relational-databases/security/securables.md)。  
  
 *主体*  
 是在其上应用审核操作或审核操作组主体数据库的名称。 有关详细信息，请参阅[主体 &#40; 数据库引擎 &#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)。  
  
 WITH ( STATE = { ON | OFF } )  
 允许或禁止审核收集此审核规范的记录。  
  
## <a name="remarks"></a>注释  
 数据库审核规范是驻留在给定数据库中的非安全对象。 数据库审核规范在创建之后处于禁用状态。  
  
## <a name="permissions"></a>Permissions  
 使用用户`ALTER ANY DATABASE AUDIT`权限可以创建数据库审核规范并将它们绑定到任何审核。  
  
 数据库审核规范在创建后，它可以查看具有的主体`CONTROL SERVER`，`ALTER ANY DATABASE AUDIT`权限，或`sysadmin`帐户。  
  
## <a name="examples"></a>示例  
 下面的示例创建名为 `Payrole_Security_Audit` 的服务器审核，然后创建名为 `Payrole_Security_Audit` 的数据库审核规范，该规范针对 `SELECT` 数据库中的 `INSERT` 表，审核 `dbo` 用户发出的 `HumanResources.EmployeePayHistory` 和 `AdventureWorks2012` 语句。  
  
```  
USE master ;  
GO  
-- Create the server audit.  
CREATE SERVER AUDIT Payrole_Security_Audit  
    TO FILE ( FILEPATH =   
'C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\DATA' ) ;  
GO  
-- Enable the server audit.  
ALTER SERVER AUDIT Payrole_Security_Audit   
WITH (STATE = ON) ;  
GO  
-- Move to the target database.  
USE AdventureWorks2012 ;  
GO  
-- Create the database audit specification.  
CREATE DATABASE AUDIT SPECIFICATION Audit_Pay_Tables  
FOR SERVER AUDIT Payrole_Security_Audit  
ADD (SELECT , INSERT  
     ON HumanResources.EmployeePayHistory BY dbo )  
WITH (STATE = ON) ;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [创建服务器审核 &#40;Transact SQL &#41;](../../t-sql/statements/create-server-audit-transact-sql.md)   
 [ALTER SERVER AUDIT &#40;Transact SQL &#41;](../../t-sql/statements/alter-server-audit-transact-sql.md)   
 [DROP SERVER AUDIT &#40;Transact SQL &#41;](../../t-sql/statements/drop-server-audit-transact-sql.md)   
 [创建服务器审核规范 &#40;Transact SQL &#41;](../../t-sql/statements/create-server-audit-specification-transact-sql.md)   
 [ALTER SERVER AUDIT SPECIFICATION &#40;Transact SQL &#41;](../../t-sql/statements/alter-server-audit-specification-transact-sql.md)   
 [删除服务器审核规范 &#40;Transact SQL &#41;](../../t-sql/statements/drop-server-audit-specification-transact-sql.md)   
 [创建数据库审核规范 (Transact SQL)](../../t-sql/statements/create-database-audit-specification-transact-sql.md)   
 [ALTER DATABASE AUDIT SPECIFICATION &#40;Transact SQL &#41;](../../t-sql/statements/alter-database-audit-specification-transact-sql.md)   
 [删除数据库审核规范 &#40;Transact SQL &#41;](../../t-sql/statements/drop-database-audit-specification-transact-sql.md)   
 [ALTER AUTHORIZATION &#40;Transact SQL &#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [sys.fn_get_audit_file &#40;Transact SQL &#41;](../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md)   
 [sys.server_audits &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-server-audits-transact-sql.md)   
 [sys.server_file_audits &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-server-file-audits-transact-sql.md)   
 [sys.server_audit_specifications &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-server-audit-specifications-transact-sql.md)   
 [sys.server_audit_specification_details &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-server-audit-specification-details-transact-sql.md)   
 [sys.database_audit_specifications &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-database-audit-specifications-transact-sql.md)   
 [sys.database_audit_specification_details &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-database-audit-specification-details-transact-sql.md)   
 [sys.dm_server_audit_status &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-server-audit-status-transact-sql.md)   
 [sys.dm_audit_actions &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-actions-transact-sql.md)   
 [创建服务器审核和服务器审核规范](../../relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification.md)  
  
  

