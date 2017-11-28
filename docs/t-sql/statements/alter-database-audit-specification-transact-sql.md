---
title: "ALTER DATABASE AUDIT SPECIFICATION (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_DATABASE_AUDIT_SPECIFICATION_TSQL
- ALTER DATABASE AUDIT SPECIFICATION
- ALTER_DATABASE_AUDIT_TSQL
- ALTER DATABASE AUDIT
dev_langs: TSQL
helpviewer_keywords: ALTER DATABASE AUDIT SPECIFICATION statement
ms.assetid: 85f4e7e6-a330-4de0-9048-64f386ccc314
caps.latest.revision: "22"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 1fc9148b05ca5b7b77d149e19e937502450ea0d3
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="alter-database-audit-specification-transact-sql"></a>ALTER DATABASE AUDIT SPECIFICATION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 审核功能更改数据库审核规范对象。 有关详细信息，请参阅 [SQL Server Audit（数据库引擎）](../../relational-databases/security/auditing/sql-server-audit-database-engine.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
ALTER DATABASE AUDIT SPECIFICATION audit_specification_name  
{  
    [ FOR SERVER AUDIT audit_name ]  
    [ { { ADD | DROP } (   
           { <audit_action_specification> | audit_action_group_name }   
                )   
      } [, ...n] ]  
    [ WITH ( STATE = { ON | OFF } ) ]  
}  
[ ; ]  
<audit_action_specification>::=  
{  
      <action_specification>[ ,...n ] ON [ class :: ] securable   
     BY principal [ ,...n ]   
}  
  
```  
  
## <a name="arguments"></a>参数  
 *audit_specification_name*  
 审核规范的名称。  
  
 *audit_name*  
 应用此规范的审核的名称。  
  
 *audit_action_specification*  
 一个或多个数据库级别可审核操作的名称。 审核操作组的列表，请参阅[SQL Server 审核操作组和操作](../../relational-databases/security/auditing/sql-server-audit-action-groups-and-actions.md)。  
  
 *audit_action_group_name*  
 一个或多个数据库级别可审核操作组的名称。 审核操作组的列表，请参阅[SQL Server 审核操作组和操作](../../relational-databases/security/auditing/sql-server-audit-action-groups-and-actions.md)。  
  
 *类*  
 安全对象上的类名（如果适用）。  
  
 *安全对象*  
 应用审核操作或审核操作组的数据库中的表、视图或其他安全对象。 有关详细信息，请参阅 [Securables](../../relational-databases/security/securables.md)。  
  
 *列*  
 安全对象上的列名（如果适用）。  
  
 *主体*  
 应用审核操作或审核操作组的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 主体的名称。 有关详细信息，请参阅[主体 &#40; 数据库引擎 &#41;](../../relational-databases/security/authentication-access/principals-database-engine.md)。  
  
 与**(**状态 **=**  {ON |OFF} **)**  
 允许或禁止审核收集此审核规范的记录。 审核规范状态更改必须在用户事务之外进行，并且从 ON 转换到 OFF 时，审核规范的同一语句中不能有其他更改。  
  
## <a name="remarks"></a>注释  
 数据库审核规范是驻留在给定数据库中的非安全对象。 你必须设置为 OFF 选项以便对数据库的更改审核规范的审核规范的状态。 使用 STATE=OFF 以外的任何选项启用审核后，如果执行 ALTER DATABASE AUDIT SPECIFICATION，将接收到错误消息。 有关详细信息，请参阅 [tempdb Database](../../relational-databases/databases/tempdb-database.md)。  
  
## <a name="permissions"></a>Permissions  
 具有 ALTER ANY DATABASE AUDIT 权限的用户可以更改数据库审核规范并将其绑定到任何审核。  
  
 数据库审核规范在创建后，它可以具有 CONTROL SERVER 或 ALTER ANY DATABASE AUDIT 权限、 sysadmin 帐户或具有对审核的显式访问权限的主体的主体中查看。  
  
## <a name="examples"></a>示例  
 下面的示例针对称为 `HIPPA_Audit_DB_Specification` 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 审核更改称为 `SELECT` 的数据库审核规范，该规范审核 `dbo` 用户发出的 `HIPPA_Audit` 语句。  
  
```  
ALTER DATABASE AUDIT SPECIFICATION HIPPA_Audit_DB_Specification  
FOR SERVER AUDIT HIPPA_Audit  
    ADD (SELECT  
         ON OBJECT::dbo.Table1  
         BY dbo)  
    WITH (STATE = ON);  
GO  
```  
  
 有关如何创建审核的完整示例，请参阅[SQL Server Audit &#40; 数据库引擎 &#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md)。  
  
## <a name="see-also"></a>另请参阅  
 [创建服务器审核 &#40;Transact SQL &#41;](../../t-sql/statements/create-server-audit-transact-sql.md)   
 [ALTER SERVER AUDIT &#40;Transact SQL &#41;](../../t-sql/statements/alter-server-audit-transact-sql.md)   
 [DROP SERVER AUDIT &#40;Transact SQL &#41;](../../t-sql/statements/drop-server-audit-transact-sql.md)   
 [创建服务器审核规范 &#40;Transact SQL &#41;](../../t-sql/statements/create-server-audit-specification-transact-sql.md)   
 [ALTER SERVER AUDIT SPECIFICATION &#40;Transact SQL &#41;](../../t-sql/statements/alter-server-audit-specification-transact-sql.md)   
 [删除服务器审核规范 &#40;Transact SQL &#41;](../../t-sql/statements/drop-server-audit-specification-transact-sql.md)   
 [创建数据库审核规范 &#40;Transact SQL &#41;](../../t-sql/statements/create-database-audit-specification-transact-sql.md)   
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
  
  
