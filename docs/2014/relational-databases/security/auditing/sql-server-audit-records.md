---
title: SQL Server 审核记录 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- audit records [SQL Server]
ms.assetid: 7a291015-df15-44fe-8d53-c6d90a157118
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 19e9ba9013d592d752189adadfb761f1741fd91a
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85055463"
---
# <a name="sql-server-audit-records"></a>SQL Server Audit Records
  使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 审核功能，可以对服务器级别和数据库级别事件组和事件进行审核。 有关详细信息，请参阅 [SQL Server Audit（数据库引擎）](sql-server-audit-database-engine.md)。 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 列中的一个值匹配。  
  
 审核由零个或多个审核操作项组成，这些操作项会记录到审核“  目标”。 审核目标可以是二进制文件、Windows 应用程序事件日志或 Windows 安全事件日志。 发送到目标的记录可以包含下表中介绍的元素。  
  
|列名称|说明|类型|始终可用|  
|-----------------|-----------------|----------|----------------------|  
|**event_time**|触发可审核操作的日期/时间。|`datetime2`|是|  
|**sequence_no**|跟踪单个审核记录中的记录顺序，该记录太大而无法放在写入缓冲区中以进行审核。|`int`|是|  
|**action_id**|操作的 ID<br /><br /> 提示：若要将 **action_id** 用作谓词，必须将它从字符串转换为数值。 有关详细信息，请参阅 [Filter SQL Server Audit on action_id / class_type predicate](https://docs.microsoft.com/archive/blogs/sqlsecurity/filter-sql-server-audit-on-action_id-class_type-predicate)（使用 action_id / class_type 谓词筛选 SQL Server 审核）。|`varchar(4)`|是|  
|**成功**|指示触发事件的操作是否成功|`bit`-1 = 成功，0 = 失败|是|  
|**permission_bitmask**|当适用时，显示授予、拒绝或撤消的权限|`bigint`|否|  
|**is_column_permission**|指示列级别权限的标志|`bit`-1 = True，0 = False|否|  
|**session_id**|发生该事件的会话的 ID。|`int`|是|  
|**server_principal_id**|在其中执行操作的登录上下文 ID。|`int`|是|  
|**database_principal_id**|在其中执行操作的数据库用户上下文 ID。|`int`|否|  
|**object_ id**|发生审核的实体的主 ID。 这包括：<br /><br /> 服务器对象<br /><br /> 数据库<br /><br /> 数据库对象<br /><br /> 架构对象|`int`|否|  
|**target_server_principal_id**|可审核操作适用的服务器主体。|`int`|是|  
|**target_database_principal_id**|可审核操作适用的数据库主体。|`int`|否|  
|**class_type**|发生审核的可审核实体的类型。|`varchar(2)`|是|  
|**session_server_principal_name**|会话的服务器主体。|`sysname`|是|  
|**server_principal_name**|当前登录名。|`sysname`|是|  
|**server_principal_sid**|当前登录名 SID。|`varbinary`|是|  
|**database_principal_name**|当前用户。|`sysname`|否|  
|**target_server_principal_name**|操作的目标登录名。|`sysname`|否|  
|**target_server_principal_sid**|目标登录名的 SID。|`varbinary`|否|  
|**target_database_principal_name**|操作的目标用户。|`sysname`|否|  
|**server_instance_name**|发生审核的服务器实例的名称。 使用标准计算机\实例格式。|`nvarchar(120)`|是|  
|**database_name**|发生此操作的数据库上下文。|`sysname`|否|  
|**schema_name**|发生此操作的架构上下文。|`sysname`|否|  
|**object_name**|发生审核的实体的名称。 这包括：<br /><br /> 服务器对象<br /><br /> 数据库<br /><br /> 数据库对象<br /><br /> 架构对象<br /><br /> TSQL 语句（如果有）|`sysname`|否|  
|**语句**|TSQL 语句（如果有）|`nvarchar(4000)`|否|  
|**additional_information**|有关此事件的其他任何信息，存储为 XML。|`nvarchar(4000)`|否|  
  
## <a name="remarks"></a>备注  
 某些操作不填充列的值，这是因为它可能不适用于此操作。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 审核可以为审核记录中的字符字段存储 4000 个数据字符。 当可审核操作返回的 **additional_information** 和 **statement** 值返回的字符超过 4000 个时， **sequence_no** 列用于将多个记录写入到单个审核操作的审核报表中以记录此数据。 流程如下：  
  
-   **statement** 列分为 4000 个字符。  
  
-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 审核作为具有部分数据的审核记录的第一行写入。 所有其他字段在每一行中是重复的。  
  
-   **sequence_no** 值是递增的。  
  
-   此过程将一直重复，直至记录了所有数据为止。  
  
 可以使用 **sequence_no** 值按顺序读取行以及 **event_Time**、 **action_id** 和 **session_id** 列来连接数据，从而标识操作。  
  
## <a name="related-content"></a>相关内容  
 [CREATE SERVER AUDIT (Transact-SQL)](/sql/t-sql/statements/create-server-audit-transact-sql)  
  
 [ALTER SERVER AUDIT (Transact-SQL)](/sql/t-sql/statements/alter-server-audit-specification-transact-sql)  
  
 [DROP SERVER AUDIT (Transact-SQL)](/sql/t-sql/statements/drop-server-audit-transact-sql)  
  
 [CREATE SERVER AUDIT SPECIFICATION (Transact-SQL)](/sql/t-sql/statements/create-server-audit-specification-transact-sql)  
  
 [ALTER SERVER AUDIT SPECIFICATION (Transact-SQL)](/sql/t-sql/statements/alter-server-audit-transact-sql)  
  
 [DROP SERVER AUDIT SPECIFICATION (Transact-SQL)](/sql/t-sql/statements/drop-server-audit-specification-transact-sql)  
  
 [CREATE DATABASE AUDIT SPECIFICATION (Transact-SQL)](/sql/t-sql/statements/create-database-audit-specification-transact-sql)  
  
 [ALTER DATABASE AUDIT SPECIFICATION (Transact-SQL)](/sql/t-sql/statements/alter-database-audit-specification-transact-sql)  
  
 [DROP DATABASE AUDIT SPECIFICATION (Transact-SQL)](/sql/t-sql/statements/drop-database-encryption-key-transact-sql)  
  
 [ALTER AUTHORIZATION (Transact-SQL)](/sql/t-sql/statements/alter-authorization-transact-sql)  
  
 [sys.fn_get_audit_file (Transact-SQL)](/sql/relational-databases/system-functions/sys-fn-get-audit-file-transact-sql)  
  
 [sys.server_audits (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-server-audits-transact-sql)  
  
 [sys.server_file_audits (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-server-file-audits-transact-sql)  
  
 [sys.server_audit_specifications (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-server-audit-specifications-transact-sql)  
  
 [sys.server_audit_specification_details (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-server-audit-specification-details-transact-sql)  
  
 [sys.database_audit_specifications (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-database-audit-specifications-transact-sql)  
  
 [sys.database_audit_specification_details (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-database-audit-specification-details-transact-sql)  
  
 [sys.dm_server_audit_status (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-server-audit-status-transact-sql)  
  
 [sys.dm_audit_actions (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-audit-actions-transact-sql)  
  
 [sys.dm_audit_class_type_map (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-audit-class-type-map-transact-sql)  
  
  
