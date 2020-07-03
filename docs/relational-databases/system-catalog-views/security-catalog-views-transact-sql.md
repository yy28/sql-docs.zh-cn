---
title: 安全目录视图（Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 02/27/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- cryptography [SQL Server], catalog views
- encryption [SQL Server], catalog views
- catalog views [SQL Server], security
- security catalog views [SQL Server]
ms.assetid: 4d5cf1bf-09a7-4ee0-9dbb-5c584750fc67
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 4282a2f5ac1e312eac7c60df0397e684956fe448
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85897116"
---
# <a name="security-catalog-views-transact-sql"></a>安全性目录视图 (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  安全性信息出现在为性能和实用工具而优化目录视图中。 如果可能，请使用以下目录视图来访问目录元数据。  
  
## <a name="database-level-views"></a>数据库级别的视图  
  
|||  
|-|-|  
|[sys.database_permissions](../../relational-databases/system-catalog-views/sys-database-permissions-transact-sql.md)|[sys.database_scoped_credentials](../../relational-databases/system-catalog-views/sys-database-scoped-credentials-transact-sql.md) |  
|[sys.database_principals](../../relational-databases/system-catalog-views/sys-database-principals-transact-sql.md)|[sys.master_key_passwords](../../relational-databases/system-catalog-views/sys-master-key-passwords-transact-sql.md) |  
|[sys.database_role_members](../../relational-databases/system-catalog-views/sys-database-role-members-transact-sql.md)|[sys.user_token](../../relational-databases/system-catalog-views/sys-user-token-transact-sql.md) |  
  
## <a name="server-level-views"></a>服务器级别的视图  
  
|||  
|-|-|  
|[sys.credentials](../../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)|[sys.server_principals](../../relational-databases/system-catalog-views/sys-server-principals-transact-sql.md)|  
|[sys.login_token](../../relational-databases/system-catalog-views/sys-login-token-transact-sql.md)|[sys.server_role_members](../../relational-databases/system-catalog-views/sys-server-role-members-transact-sql.md)|  
|[sys.securable_classes](../../relational-databases/system-catalog-views/sys-securable-classes-transact-sql.md)|[sys.sql_logins](../../relational-databases/system-catalog-views/sys-sql-logins-transact-sql.md)|  
|[sys.server_permissions](../../relational-databases/system-catalog-views/sys-server-permissions-transact-sql.md)|[sys.system_components_surface_area_configuration](../../relational-databases/system-catalog-views/sys-system-components-surface-area-configuration-transact-sql.md)|  
  
## <a name="encryption-views"></a>加密视图  
  
|||  
|-|-|  
|[sys.asymmetric_keys](../../relational-databases/system-catalog-views/sys-asymmetric-keys-transact-sql.md)|[sys.cryptographic_providers](../../relational-databases/system-catalog-views/sys-cryptographic-providers-transact-sql.md)|  
|[sys.certificates](../../relational-databases/system-catalog-views/sys-certificates-transact-sql.md)|[sys.key_encryptions](../../relational-databases/system-catalog-views/sys-key-encryptions-transact-sql.md)|  
|[sys.column_encryption_key_values](../../relational-databases/system-catalog-views/sys-column-encryption-key-values-transact-sql.md)|[sys.openkeys](../../relational-databases/system-catalog-views/sys-openkeys-transact-sql.md)|  
|[sys.column_encryption_keys](../../relational-databases/system-catalog-views/sys-column-encryption-keys-transact-sql.md)|[sys.security_policies (Transact-SQL)](../../relational-databases/system-catalog-views/sys-security-policies-transact-sql.md)|  
|[sys. column_master_key_definitions](../../relational-databases/system-catalog-views/sys-column-master-keys-transact-sql.md)|[sys.security_predicates (Transact-SQL)](../../relational-databases/system-catalog-views/sys-security-predicates-transact-sql.md)|  
|[sys.crypt_properties](../../relational-databases/system-catalog-views/sys-crypt-properties-transact-sql.md)|[sys.symmetric_keys](../../relational-databases/system-catalog-views/sys-symmetric-keys-transact-sql.md)|  
  
## <a name="sql-server-audit-views"></a>SQL Server 审核视图  
  
|||  
|-|-|  
|[sys.server_audits](../../relational-databases/system-catalog-views/sys-server-audits-transact-sql.md)|[sys.server_file_audits](../../relational-databases/system-catalog-views/sys-server-file-audits-transact-sql.md)|  
|[sys.server_audit_specifications](../../relational-databases/system-catalog-views/sys-server-audit-specifications-transact-sql.md)|[sys.server_audit_specifications_details](../../relational-databases/system-catalog-views/sys-server-audit-specification-details-transact-sql.md)|  
|[sys.database_audit_specifications](../../relational-databases/system-catalog-views/sys-database-audit-specifications-transact-sql.md)|[sys.database_audit_specification_details](../../relational-databases/system-catalog-views/sys-database-audit-specification-details-transact-sql.md)|  
  
## <a name="permissions"></a>权限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQL Server 数据库引擎和 Azure SQL Database 的安全中心](../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)   
 [与安全性相关的动态管理视图和函数 (Transact-SQL)](../../relational-databases/system-dynamic-management-views/security-related-dynamic-management-views-and-functions-transact-sql.md)  
  
  
