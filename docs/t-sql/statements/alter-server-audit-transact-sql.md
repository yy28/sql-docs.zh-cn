---
title: "ALTER SERVER AUDIT (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_SERVER_AUDIT_TSQL
- ALTER SERVER AUDIT
dev_langs:
- TSQL
helpviewer_keywords:
- server audit [SQL Server]
- audits [SQL Server], specification
- ALTER SERVER AUDIT statement
ms.assetid: 63426d31-7a5c-4378-aa9e-afcf4f64ceb3
caps.latest.revision: 43
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6d2522a2876165f8e18222f2268dad091a6ba342
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="alter-server-audit--transact-sql"></a>ALTER SERVER AUDIT (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Audit 功能更改服务器审核对象。 有关详细信息，请参阅 [SQL Server Audit（数据库引擎）](../../relational-databases/security/auditing/sql-server-audit-database-engine.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
ALTER SERVER AUDIT audit_name  
{  
    [ TO { { FILE ( <file_options> [, ...n] ) } | APPLICATION_LOG | SECURITY_LOG } ]  
    [ WITH ( <audit_options> [ , ...n] ) ]   
    [ WHERE <predicate_expression> ]  
}  
| REMOVE WHERE  
| MODIFY NAME = new_audit_name  
[ ; ]  
  
<file_options>::=  
{  
      FILEPATH = 'os_file_path'   
    | MAXSIZE = { max_size { MB | GB | TB } | UNLIMITED }   
    | MAX_ROLLOVER_FILES = { integer | UNLIMITED }   
    | MAX_FILES = integer   
    | RESERVE_DISK_SPACE = { ON | OFF }   
}  
  
<audit_options>::=  
{  
      QUEUE_DELAY = integer   
    | ON_FAILURE = { CONTINUE | SHUTDOWN | FAIL_OPERATION }   
    | STATE = = { ON | OFF }   
}  
  
<predicate_expression>::=  
{  
    [NOT ] <predicate_factor>   
    [ { AND | OR } [NOT ] { <predicate_factor> } ]   
    [,...n ]  
}  
  
<predicate_factor>::=   
    event_field_name { = | < > | ! = | > | > = | < | < = } { number | ' string ' }  
```  
  
## <a name="arguments"></a>参数  
 TO { FILE | APPLICATION_LOG | SECURITY }  
 确定审核目标的位置。 可用的选项包括二进制文件、Windows 应用程序日志或 Windows 安全日志。  
  
 FILEPATH **=***os_file_path*  
 审核记录的路径。 文件名是基于审核名称和审核 GUID 生成的。  
  
 MAXSIZE  **=**  *max_size*  
 指定审核文件可增大到的最大大小。 *Max_size*值必须跟一个整数**MB**， **GB**， **TB**，或**无限制**。 你可以为指定的最小大小*max_size*为 2 **MB**最大值为 2,147,483,647 **TB**。 当**无限制**指定，则该文件增长，直到磁盘已满。 指定值低于 2MB 引发 MSG_MAXSIZE_TOO_SMALL 错误。 默认值是**无限制**。  
  
 MAX_ROLLOVER_FILES  **=** *整数* | **无限制**  
 指定要保留在文件系统中的最大文件数。 当 MAX_ROLLOVER_FILES 的设置 = 0，对创建的滚动更新文件数没有限制。 默认值为 0。 可以指定的最大文件数为 2,147,483,647。  
  
 MAX_FILES =*整数*  
 指定可创建的审核文件的最大数目。 不会不会累计到第一个文件时达到的限制。 当达到 MAX_FILES 限制时，导致生成附加审核事件任何操作都将失败并出现错误。  
**适用范围**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 RESERVE_DISK_SPACE  **=**  {ON |关闭}  
 此选项会按 MAXSIZE 值为磁盘上的文件预先分配大小。 仅在 MAXSIZE 不等于 UNLIMITED 时适用。 默认值为 OFF。  
  
 QUEUE_DELAY  **=** *整数*  
 确定在强制处理审核操作之前可能经过的时间（以毫秒为单位）。 值 0 指示同步传递。 可设置的最小延迟值为 1000（1 秒），这是默认值。 最大值为 2,147,483,647（2,147,483.647 秒或者 24 天 20 小时 31 分钟 23.647 秒）。 指定数量无效，将引发错误 MSG_INVALID_QUEUE_DELAY。  
  
 ON_FAILURE  **=**  {继续 |关闭 |FAIL_OPERATION}  
 指示在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 无法写入审核日志时写入目标的实例是应失败、继续还是停止。  
  
 CONTINUE  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 操作将继续。 审核记录将不会保留。 审核将继续尝试登录事件和恢复，如果故障条件得到解决。 选择继续选项可以允许未经审核的活动，这可能违反您的安全策略。 在[!INCLUDE[ssDE](../../includes/ssde-md.md)]的继续操作比维护完整审核更重要时，使用此选项。  
  
SHUTDOWN  
强制的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]才可关闭，如果[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]将数据写入审核目标出于任何原因而失败。 登录名执行`ALTER`语句必须具有`SHUTDOWN`内的权限[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 关机问题仍然存在即使`SHUTDOWN`权限更高版本吊销从正在执行的登录名。 如果用户不具有此权限，然后该语句将失败，并将不会修改审核。 在审核失败可能损害系统的安全或完整性时，使用此选项。 有关详细信息，请参阅[关闭](../../t-sql/language-elements/shutdown-transact-sql.md)。 
  
 FAIL_OPERATION  
 如果数据库操作会导致审核的事件，则数据库操作将失败。 可以继续操作，不会导致审核的事件，但是可能会发生任何审核的事件。 审核将继续尝试登录事件和恢复，如果故障条件得到解决。 在维护完整审核比对[!INCLUDE[ssDE](../../includes/ssde-md.md)]的完全访问权限更重要时，使用此选项。  
 **适用范围**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。   
  
 状态 **=**  {ON |关闭}  
 启用或禁用审核收集记录。 更改运行的审核的状态（从 ON 到 OFF）将创建审核停止时的审核项、停止审核的主体以及停止审核的时间。  
  
 MODIFY NAME = *new_audit_name*  
 更改审核的名称。 不能与任何其他选项一起使用。  
  
 predicate_expression  
 指定用于确定是否应处理事件的谓词表达式。 谓词表达式限制在 3000 个字符，这限制了字符串参数。  
 **适用范围**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 event_field_name  
 表示标识谓词源的事件字段的名称。 审核字段描述的[sys.fn_get_audit_file &#40;Transact SQL &#41;](../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md). 除 `file_name` 和 `audit_file_offset` 之外的所有字段都可以进行审核。  
 **适用范围**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 number  
 任何数值类型包括**十进制**。 局限性在于缺少可用物理内存，或数值过大而无法用 64 位整数表示。  
 **适用范围**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 ' string '  
 进行谓词比较所需的 ANSI 字符串或 Unicode 字符串。 不为谓词比较函数执行隐式字符串类型转换。 传递错误类型会导致出错。  
 **适用范围**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
## <a name="remarks"></a>注释  
 调用 ALTER AUDIT 时，必须指定至少一个 TO、WITH 或 MODIFY NAME 子句。  
  
 为了更改审核，必须将审核的状态设置为 OFF 选项。 如果启用审核后状态以外的其他任何选项与 ALTER AUDIT 运行 = OFF，你收到 MSG_NEED_AUDIT_DISABLED 错误消息。  
  
 无需停止审核即可添加、更改和删除审核规范。  
  
 创建审核后无法更改审核的 GUID。  
  
## <a name="permissions"></a>Permissions  
 若要创建、更改或删除服务器审核主体，必须具有 ALTER ANY SERVER AUDIT 或 CONTROL SERVER 权限。  
  
## <a name="examples"></a>示例  
  
### <a name="a-changing-a-server-audit-name"></a>A. 更改服务器审核名称  
 下面的示例将服务器审核 `HIPPA_Audit` 的名称更改为 `HIPAA_Audit_Old`。  
  
```  
USE master  
GO  
ALTER SERVER AUDIT HIPAA_Audit  
WITH (STATE = OFF);  
GO  
ALTER SERVER AUDIT HIPAA_Audit  
MODIFY NAME = HIPAA_Audit_Old;  
GO  
ALTER SERVER AUDIT HIPAA_Audit_Old  
WITH (STATE = ON);  
GO  
```  
  
### <a name="b-changing-a-server-audit-target"></a>B. 更改服务器审核目标  
 下面的示例将名为 `HIPPA_Audit` 的服务器审核更改为以文件为目标。  
  
```  
USE master  
GO  
ALTER SERVER AUDIT HIPAA_Audit  
WITH (STATE = OFF);  
GO  
ALTER SERVER AUDIT HIPAA_Audit  
TO FILE (FILEPATH ='\\SQLPROD_1\Audit\',  
          MAXSIZE = 1000 MB,  
          RESERVE_DISK_SPACE=OFF)  
WITH (QUEUE_DELAY = 1000,  
       ON_FAILURE = CONTINUE);  
GO  
ALTER SERVER AUDIT HIPAA_Audit  
WITH (STATE = ON);  
GO  
```  
  
### <a name="c-changing-a-server-audit-where-clause"></a>C. 更改服务器审核 WHERE 子句  
 下面的示例修改 where 子句中的示例 C 创建[CREATE SERVER AUDIT &#40;Transact SQL &#41;](../../t-sql/statements/create-server-audit-transact-sql.md). 如果 27 的情况下，新的 WHERE 子句筛选用户定义的事件的状态。  
  
```tsql  
ALTER SERVER AUDIT [FilterForSensitiveData] WITH (STATE = OFF)  
GO  
ALTER SERVER AUDIT [FilterForSensitiveData]  
WHERE user_defined_event_id = 27;  
GO  
ALTER SERVER AUDIT [FilterForSensitiveData] WITH (STATE = ON);  
GO  
```  
  
### <a name="d-removing-a-where-clause"></a>D. 删除 WHERE 子句  
 下面的示例将删除 WHERE 子句谓词表达式。  
  
```tsql  
ALTER SERVER AUDIT [FilterForSensitiveData] WITH (STATE = OFF)  
GO  
ALTER SERVER AUDIT [FilterForSensitiveData]  
REMOVE WHERE;  
GO  
ALTER SERVER AUDIT [FilterForSensitiveData] WITH (STATE = ON);  
GO  
```  
  
### <a name="e-renaming-a-server-audit"></a>E. 重命名服务器审核  
 下面的示例将服务器审核名称从 `FilterForSensitiveData` 更改为 `AuditDataAccess`。  
  
```tsql  
ALTER SERVER AUDIT [FilterForSensitiveData] WITH (STATE = OFF)  
GO  
ALTER SERVER AUDIT [FilterForSensitiveData]  
MODIFY NAME = AuditDataAccess;  
GO  
ALTER SERVER AUDIT [AuditDataAccess] WITH (STATE = ON);  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [DROP SERVER AUDIT &#40;Transact SQL &#41;](../../t-sql/statements/drop-server-audit-transact-sql.md)   
 [创建服务器审核规范 &#40;Transact SQL &#41;](../../t-sql/statements/create-server-audit-specification-transact-sql.md)   
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
  
  

