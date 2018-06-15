---
title: sys.fn_get_audit_file (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 05/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- fn_get_audit_file_TSQL
- sys.fn_get_audit_file_TSQL
- fn_get_audit_file
- sys.fn_get_audit_file
dev_langs:
- TSQL
helpviewer_keywords:
- sys.fn_get_audit_file function
- fn_get_audit_file function
ms.assetid: d6a78d14-bb1f-4987-b7b6-579ddd4167f5
caps.latest.revision: 27
author: rothja
ms.author: jroth
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: e09491347fec046bef09dc2fca06756998055150
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
ms.locfileid: "33240557"
---
# <a name="sysfngetauditfile-transact-sql"></a>sys.fn_get_audit_file (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  从服务器审核在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中创建的审核文件返回信息。 有关详细信息，请参阅 [SQL Server Audit（数据库引擎）](../../relational-databases/security/auditing/sql-server-audit-database-engine.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
fn_get_audit_file ( file_pattern,   
    { default | initial_file_name | NULL },   
    { default | audit_record_offset | NULL } )  
```  
  
## <a name="arguments"></a>参数  
 *file_pattern*  
 指定要读取的审核文件集的目录（或路径）和文件名。 类型是**nvarchar(260)**。 
 
 - **SQL Server**:
    
    此参数必须包括路径（驱动器盘符或网络共享）和文件名，可以包含通配符。 使用一个星号 （*） 可以用于从审核文件集中收集多个文件。 例如：  
  
    -   **\<路径 >\\ \***  -收集所有审核的指定位置中的文件。  
  
    -   **\<路径 > \LoginsAudit_{GUID}** -收集所有审核具有指定的名称和 GUID 对的文件。  
  
    -   **\<路径 > \LoginsAudit_{GUID}_00_29384.sqlaudit** -收集特定的审核文件。  
  
 - **Azure SQL Database**:
 
    此参数用于指定 blob URL （包括存储终结点和容器）。 虽然它不支持星号通配符，你可以使用部分文件 (blob) 名称前缀 （而不是完整的 blob 名称中） 收集该前缀开头的多个文件 (blob)。 例如：
 
      - **\<Storage_endpoint\>/\<容器\>/\<ServerName\>/\<DatabaseName\> /**  -收集特定数据库的所有审核文件 (blob)。    
      
      - **\<Storage_endpoint\>/\<容器\>/\<ServerName\>/\<DatabaseName\> / \<AuditName\>/\<CreationDate\>/\<FileName\>.xel** -收集特定的审核文件 (blob)。
  
> [!NOTE]  
>  在无文件名模式的情况下传递路径将生成错误。  
  
 *initial_file_name*  
 指定审核文件集中要开始读取审核记录的特定文件的路径和名称。 类型是**nvarchar(260)**。  
  
> [!NOTE]  
>  *Initial_file_name*自变量必须包含有效的条目，或者必须包含既可以是默认 |NULL 值。  
  
 *audit_record_offset*  
 指定一个已知位置，该位置包含为 initial_file_name 指定的文件。 使用此参数时，函数将从缓冲区中紧跟指定偏移量之后的第一个记录开始读取。  
  
> [!NOTE]  
>  *Audit_record_offset*自变量必须包含有效的条目，或者必须包含既可以是默认 |NULL 值。 类型是**bigint**。  
  
## <a name="tables-returned"></a>返回的表  
 下表描述此函数可返回的审核文件内容。  
  
|列名|类型|Description|  
|-----------------|----------|-----------------|  
|event_time|**datetime2**|触发可审核操作的日期和时间。 不可为 null。|  
|sequence_number|**int**|跟踪单个审核记录中的记录顺序，该记录太大而无法放在写入缓冲区中以进行审核。 不可为 null。|  
|action_id|**varchar(4)**|操作的 ID。 不可为 null。|  
|succeeded|**bit**|指示触发事件的操作是否成功。 不可为 null。 对于除登录事件之外的所有事件，它仅报告权限检查（而不是操作）成功或失败。<br /> 1 = 成功<br /> 0 = 失败|  
|permission_bitmask|**varbinary(16)**|在某些操作中，这是授予、拒绝或撤消的权限。|  
|is_column_permission|**bit**|标志，用于指示是否为列级别权限。 不可为 null。 当 permission_bitmask = 0 时返回 0。<br /> 1 = true<br /> 0 = false|  
|session_id|**int**|发生该事件的会话的 ID。 不可为 null。|  
|server_principal_id|**int**|在其中执行操作的登录上下文 ID。 不可为 null。|  
|database_principal_id|**int**|在其中执行操作的数据库用户上下文 ID。 不可为 null。 返回 0，如果此不适用。 例如，如果是服务器操作，则返回 0。|  
|target_server_principal_id|**int**|执行 GRANT/DENY/REVOKE 操作的服务器主体。 不可为 null。 如果不适用，则返回 0。|  
|target_database_principal_id|**int**|执行 GRANT/DENY/REVOKE 操作的数据库主体。 不可为 null。 如果不适用，则返回 0。|  
|object_id|**int**|发生审核的实体的 ID。 其中包括：<br /> 服务器对象<br /> “数据库”<br /> 数据库对象<br /> 架构对象<br /> 不可为 null。 如果实体是服务器本身或者没有在对象级别执行审核，则返回 0。 例如，对于 Authentication，则返回 NULL。|  
|class_type|**varchar(2)**|发生审核的可审核实体的类型。 不可为 null。|  
|session_server_principal_name|**sysname**|会话的服务器主体。 可以为 Null。|  
|server_principal_name|**sysname**|当前登录名。 可以为 Null。|  
|server_principal_sid|**varbinary**|当前登录名 SID。 可以为 Null。|  
|database_principal_name|**sysname**|当前用户。 可以为 Null。 如果不可用，则返回 NULL。|  
|target_server_principal_name|**sysname**|目标登录名的操作。 可以为 Null。 如果不适用，则返回 NULL。|  
|target_server_principal_sid|**varbinary**|目标登录名的 SID。 可以为 Null。 如果不适用，则返回 NULL。|  
|target_database_principal_name|**sysname**|操作的目标用户。 可以为 Null。 如果不适用，则返回 NULL。|  
|server_instance_name|**sysname**|发生审核的服务器实例的名称。 使用标准服务器\实例格式。|  
|database_name|**sysname**|发生此操作的数据库上下文。 可以为 Null。 对于在服务器级别发生的审核，返回 NULL。|  
|schema_name|**sysname**|发生此操作的架构上下文。 可以为 Null。 对于在架构外发生的审核，返回 NULL。|  
|object_name|**sysname**|发生审核的实体的名称。 其中包括：<br /> 服务器对象<br /> “数据库”<br /> 数据库对象<br /> 架构对象<br /> 可以为 Null。 如果实体是 Server 自身或者没有在对象级别执行审核，则返回 NULL。 例如，对于 Authentication，则返回 NULL。|  
|语句|**nvarchar(4000)**|TSQL 语句（如果存在）。 可以为 Null。 如果不适用，则返回 NULL。|  
|additional_information|**nvarchar(4000)**|仅适用于单个事件的唯一信息，以 XML 的形式返回。 有少量的可审核操作包含此类信息。<br /><br /> 对于具有与操作相关联的 TSQL 堆栈的操作，将以 XML 格式显示一个级别的 TSQL 堆栈。 该 XML 格式如下：<br /><br /> `<tsql_stack><frame nest_level = '%u' database_name = '%.*s' schema_name = '%.*s' object_name = '%.*s' /></tsql_stack>`<br /><br /> Frame nest_level 指示框架的当前嵌套级别。 模块名称表示为由三部分组成的格式（database_name、schema_name 和 object_name）。  将分析模块名称，如无效的 xml 字符进行转义`'\<'`， `'>'`， `'/'`， `'_x'`。 它们将作为转义`_xHHHH\_`。 HHHH 代表该字符对应的四位十六进制 UCS-2 代码。<br /><br /> 可以为 Null。 如果事件没有报告其他信息，则返回 NULL。|  
|file_name|**varchar(260)**|作为记录来源的审核日志文件的路径和名称。 不可为 null。|  
|audit_file_offset|**bigint**|包含审核记录的文件中的缓冲区偏移量。 不可为 null。|  
|user_defined_event_id|**int**|**适用范围**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 用户定义的事件 id 作为参数传递**sp_audit_write**。 **NULL**为系统事件 （默认值） 和非零值的用户定义的事件。 有关详细信息，请参阅[sp_audit_write &#40;TRANSACT-SQL&#41;](../../relational-databases/system-stored-procedures/sp-audit-write-transact-sql.md)。|  
|user_defined_information|**nvarchar(4000)**|**适用范围**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。<br /><br /> 用来记录用户想要在中记录的任何额外信息 |通过使用审核日志**sp_audit_write**存储过程。|  
|audit_schema_version |**int** | |  
|sequence_group_id |**varbinary** | **适用于**： 仅 SQL Server （从 2016年开始） |  
|transaction_id |**bigint** | **适用于**： 仅 SQL Server （从 2016年开始） |  
|client_ip |**nvarchar(128)** | **适用于**: Azure SQL DB + SQL Server （从自 2017 年 1 开始） |  
|application_name |**nvarchar(128)** | **适用于**: Azure SQL DB + SQL Server （从自 2017 年 1 开始） |  
|duration_milliseconds |**bigint** | **适用于**： 仅 Azure SQL 数据库 |  
|response_rows |**bigint** | **适用于**： 仅 Azure SQL 数据库 |  
|affected_rows |**bigint** | **适用于**： 仅 Azure SQL 数据库 |  
|connection_id |GUID | **适用于**： 仅 Azure SQL 数据库 |
|data_sensitivity_information |nvarchar(4000) | **适用于**： 仅 Azure SQL 数据库 |
  
## <a name="remarks"></a>注释  
 如果*file_pattern*自变量传递给**fn_get_audit_file**引用的路径或文件不存在，或如果文件不是审核文件， **MSG_INVALID_AUDIT_FILE**返回错误消息。  
  
## <a name="permissions"></a>权限  
 - **SQL Server**： 需要**CONTROL SERVER**权限。  
 - **Azure SQL DB**： 需要**控制数据库**权限。     
    - 服务器管理员可以访问服务器上的所有数据库的审核的日志。
    - 非服务器管理员只能从当前数据库访问审核日志。
    - 不满足上述条件的 blob 将被跳过 （跳过的 blob 的列表将显示在查询输出的消息），并且该函数将仅从为其允许访问的 blob 返回日志。  
  
## <a name="examples"></a>示例

- **SQL Server**

  此示例从名为 `\\serverName\Audit\HIPPA_AUDIT.sqlaudit` 的文件读取。  
  
  ```  
  SELECT * FROM sys.fn_get_audit_file ('\\serverName\Audit\HIPPA_AUDIT.sqlaudit',default,default);  
  GO  
  ```  

- **Azure SQL 数据库**

  此示例从名为的文件中读取`ShiraServer/MayaDB/SqlDbAuditing_Audit/2017-07-14/10_45_22_173_1.xel`:  
  
  ```  
  SELECT * FROM sys.fn_get_audit_file ('https://mystorage.blob.core.windows.net/sqldbauditlogs/ShiraServer/MayaDB/SqlDbAuditing_Audit/2017-07-14/10_45_22_173_1.xel',default,default);
  GO  
  ```  

  此示例将读取从同一个文件与上面一样，但其他 T-SQL 子句 (**顶部**， **ORDER BY**，和**其中**子句进行筛选返回的审核记录函数）：
  
  ```  
  SELECT TOP 10 * FROM sys.fn_get_audit_file ('https://mystorage.blob.core.windows.net/sqldbauditlogs/ShiraServer/MayaDB/SqlDbAuditing_Audit/2017-07-14/10_45_22_173_1.xel',default,default)
  WHERE server_principal_name = 'admin1'
  ORDER BY event_time
  GO
  ```  

  此示例将读取从开头的服务器的日志的所有审核`Sh`: 
  
  ```  
  SELECT * FROM sys.fn_get_audit_file ('https://mystorage.blob.core.windows.net/sqldbauditlogs/Sh',default,default);
  GO  
  ```

有关如何创建审核的完整示例，请参阅 [SQL Server Audit（数据库引擎）](../../relational-databases/security/auditing/sql-server-audit-database-engine.md)。

有关设置 Azure SQL 数据库审核的信息，请参阅[SQL 数据库审核入门](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-auditing)。
  
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
 [sys.server_audits (Transact-SQL)](../../relational-databases/system-catalog-views/sys-server-audits-transact-sql.md)   
 [sys.server_file_audits (Transact-SQL)](../../relational-databases/system-catalog-views/sys-server-file-audits-transact-sql.md)   
 [sys.server_audit_specifications (Transact-SQL)](../../relational-databases/system-catalog-views/sys-server-audit-specifications-transact-sql.md)   
 [sys.server_audit_specification_details (Transact-SQL)](../../relational-databases/system-catalog-views/sys-server-audit-specification-details-transact-sql.md)   
 [sys.database_audit_specifications (Transact-SQL)](../../relational-databases/system-catalog-views/sys-database-audit-specifications-transact-sql.md)   
 [sys.database_audit_specification_details (Transact-SQL)](../../relational-databases/system-catalog-views/sys-database-audit-specification-details-transact-sql.md)   
 [sys.dm_server_audit_status (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-server-audit-status-transact-sql.md)   
 [sys.dm_audit_actions (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-audit-actions-transact-sql.md)   
 [sys.dm_audit_class_type_map (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-audit-class-type-map-transact-sql.md)   
 [创建服务器审核和服务器审核规范](../../relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification.md)  
  
  
