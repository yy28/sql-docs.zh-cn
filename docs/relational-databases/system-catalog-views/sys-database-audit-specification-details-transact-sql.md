---
description: sys.database_audit_specification_details (Transact-SQL)
title: sys. database_audit_specification_details (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 04/05/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- database_audit_specification_details
- sys.database_audit_specification_details_TSQL
- sys.database_audit_specification_details
- database_audit_specification_details_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.database_audit_specification_details catalog view
ms.assetid: 03fc60a9-1696-4109-b15e-a50046310859
author: markingmyname
ms.author: maghan
ms.openlocfilehash: c8bc8e09e9f48a7fc37b1ba0f1d308f3e17fde46
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/08/2020
ms.locfileid: "89542609"
---
# <a name="sysdatabase_audit_specification_details-transact-sql"></a>sys.database_audit_specification_details (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  包含所有数据库的服务器实例上 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 审核中的数据库审核规范的相关信息。 有关详细信息，请参阅 [SQL Server Audit（数据库引擎）](../../relational-databases/security/auditing/sql-server-audit-database-engine.md)。 有关所有 audit_action_id 及其名称的列表，请查询 [dm_audit_actions sys.databases &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-actions-transact-sql.md)。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**database_specification_id**|**int**|审核规范的 ID。|  
|**audit_action_id**|**int**|审核操作的 ID。|  
|**audit_action_name**|**Sysname**|审核操作或审核操作组的名称|  
|**类**|**int**|标识要审核的对象的类型。|  
|**class_ desc**|**Nvarchar (60) **|正审核的对象的类的说明：<br /><br /> - SCHEMA<br /><br /> - TABLE|  
|**major_id**|**int**|正审核的对象的主 ID，如表审核操作的表 ID。|  
|**minor_id**|**Int**|正审核的对象的辅助 ID（如表审核操作的列 ID），根据类进行解释。|  
|**audited_principal_id**|**int**|正审核的主体。|  
|**audited_result**|**Nvarchar (60) **|审核操作的结果：<br /><br /> - SUCCESS AND FAILURE - SUCCESS<br /><br /> - FAILURE|  
|**is_group**|**bit**|显示该对象是否为组：<br /><br /> 0 - 不是组<br /><br /> 1 - 组|  
  
## <a name="permissions"></a>权限  
 具有 **ALTER ANY DATABASE AUDIT** 或 **VIEW DEFINITION** 权限的主体、 **dbo** 角色和 **db_owners** 固定数据库角色的成员都有权访问此目录视图。 此外，不能拒绝主体 **VIEW DEFINITION** 权限。  
  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另请参阅  
 [CREATE SERVER AUDIT (Transact-SQL)](../../t-sql/statements/create-server-audit-transact-sql.md)   
 [ALTER SERVER AUDIT (Transact-SQL)](../../t-sql/statements/alter-server-audit-transact-sql.md)   
 [DROP SERVER AUDIT (Transact-SQL)](../../t-sql/statements/drop-server-audit-transact-sql.md)   
 [CREATE SERVER AUDIT SPECIFICATION (Transact-SQL)](../../t-sql/statements/create-server-audit-specification-transact-sql.md)   
 [ALTER SERVER AUDIT SPECIFICATION (Transact-SQL)](../../t-sql/statements/alter-server-audit-specification-transact-sql.md)   
 [DROP SERVER AUDIT SPECIFICATION (Transact-SQL)](../../t-sql/statements/drop-server-audit-specification-transact-sql.md)   
 [CREATE DATABASE AUDIT SPECIFICATION (Transact-SQL)](../../t-sql/statements/create-database-audit-specification-transact-sql.md)   
 [ALTER DATABASE AUDIT SPECIFICATION (Transact-SQL)](../../t-sql/statements/alter-database-audit-specification-transact-sql.md)   
 [DROP DATABASE AUDIT SPECIFICATION (Transact-SQL)](../../t-sql/statements/drop-database-audit-specification-transact-sql.md)   
 [ALTER AUTHORIZATION (Transact-SQL)](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [sys.fn_get_audit_file (Transact-SQL)](../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md)   
 [sys.server_audits (Transact-SQL)](../../relational-databases/system-catalog-views/sys-server-audits-transact-sql.md)   
 [sys.server_file_audits (Transact-SQL)](../../relational-databases/system-catalog-views/sys-server-file-audits-transact-sql.md)   
 [sys.server_audit_specifications (Transact-SQL)](../../relational-databases/system-catalog-views/sys-server-audit-specifications-transact-sql.md)   
 [sys.server_audit_specification_details (Transact-SQL)](../../relational-databases/system-catalog-views/sys-server-audit-specification-details-transact-sql.md)   
 [sys.database_audit_specifications (Transact-SQL)](../../relational-databases/system-catalog-views/sys-database-audit-specifications-transact-sql.md)   
 [sys.dm_server_audit_status (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-server-audit-status-transact-sql.md)   
 [sys.dm_audit_actions (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-audit-actions-transact-sql.md)   
 [sys.dm_audit_class_type_map (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-audit-class-type-map-transact-sql.md)   
 [创建服务器审核和服务器审核规范](../../relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification.md)  
  
  
