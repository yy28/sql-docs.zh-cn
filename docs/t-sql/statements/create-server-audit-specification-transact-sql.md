---
title: "创建服务器审核规范 (Transact SQL) |Microsoft 文档"
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
- CREATE_SERVER_AUDIT_SPECIFICATION_TSQL
- CREATE SERVER AUDIT SPECIFICATION
dev_langs:
- TSQL
helpviewer_keywords:
- CREATE SERVER AUDIT SPECIFICATION statement
ms.assetid: db77fa77-fedb-40ac-83e6-06343063e518
caps.latest.revision: 21
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: a76f52bf5c2bf0bd1448fa5f8dea0b7d08c17e9e
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="create-server-audit-specification-transact-sql"></a>CREATE SERVER AUDIT SPECIFICATION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Audit 功能创建服务器审核规范对象。 有关详细信息，请参阅 [SQL Server Audit（数据库引擎）](../../relational-databases/security/auditing/sql-server-audit-database-engine.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
CREATE SERVER AUDIT SPECIFICATION audit_specification_name  
FOR SERVER AUDIT audit_name  
{  
    { ADD ( { audit_action_group_name } )   
    } [, ...n]  
    [ WITH ( STATE = { ON | OFF } ) ]  
}  
[ ; ]  
```  
  
## <a name="arguments"></a>参数  
 *audit_specification_name*  
 服务器审核规范的名称。  
  
 *audit_name*  
 此规范应用到的审核名称。  
  
 *audit_action_group_name*  
 服务器级别可审核操作组的名称。 审核操作组的列表，请参阅[SQL Server 审核操作组和操作](../../relational-databases/security/auditing/sql-server-audit-action-groups-and-actions.md)。  
  
 与**(**状态 **=**  {ON |OFF} **)**  
 允许或禁止审核收集此审核规范的记录。  
  
## <a name="remarks"></a>注释  
 审核必须已存在，才能为它创建服务器审核规范。 服务器审核规范在创建之后处于禁用状态。  
  
## <a name="permissions"></a>Permissions  
 具有 ALTER ANY SERVER AUDIT 权限的用户可以创建服务器审核规范并将其绑定到任何审核。  
  
 它的主体服务器审核规范在创建后，可以即可查看与，控制服务器，或 ALTER ANY SERVER AUDIT 权限、 sysadmin 帐户或具有对审核的显式访问权限的主体。  
  
## <a name="examples"></a>示例  
 下面的示例针对称为 `HIPPA_Audit_Specification` 的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Audit 创建称为 `HIPPA_Audit` 的服务器审核规范，该规范可对失败的登录进行审核。  
  
```  
CREATE SERVER AUDIT SPECIFICATION HIPPA_Audit_Specification  
FOR SERVER AUDIT HIPPA_Audit  
    ADD (FAILED_LOGIN_GROUP);  
GO  
```  
  
 有关如何创建审核的完整示例，请参阅[SQL Server Audit &#40; 数据库引擎 &#41;](../../relational-databases/security/auditing/sql-server-audit-database-engine.md)。  
  
## <a name="see-also"></a>另请参阅  
 [创建服务器审核 &#40;Transact SQL &#41;](../../t-sql/statements/create-server-audit-transact-sql.md)   
 [ALTER SERVER AUDIT &#40;Transact SQL &#41;](../../t-sql/statements/alter-server-audit-transact-sql.md)   
 [DROP SERVER AUDIT &#40;Transact SQL &#41;](../../t-sql/statements/drop-server-audit-transact-sql.md)   
 [ALTER SERVER AUDIT SPECIFICATION &#40;Transact SQL &#41;](../../t-sql/statements/alter-server-audit-specification-transact-sql.md)   
 [删除服务器审核规范 &#40;Transact SQL &#41;](../../t-sql/statements/drop-server-audit-specification-transact-sql.md)   
 [创建数据库审核规范 &#40;Transact SQL &#41;](../../t-sql/statements/create-database-audit-specification-transact-sql.md)   
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
  
  

