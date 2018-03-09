---
title: "创建服务器审核 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 01/22/2018
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
- CREATE_SERVER_AUDIT_TSQL
- SERVER AUDIT
- SERVER_AUDIT_TSQL
- CREATE SERVER AUDIT
dev_langs:
- TSQL
helpviewer_keywords:
- server audit [SQL Server]
- CREATE SERVER AUDIT statement
- audits [SQL Server], creating
ms.assetid: 1c321680-562e-41f1-8eb1-e7fa5ae45cc5
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: b6e637bec3ddcfd7b24bb4f4adb87011bbbe2471
ms.sourcegitcommit: e851f3cab09f8f09a9a4cc0673b513a1c4303d2d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2018
---
# <a name="create-server-audit-transact-sql"></a>CREATE SERVER AUDIT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Audit 创建服务器审核对象。 有关详细信息，请参阅 [SQL Server Audit（数据库引擎）](../../relational-databases/security/auditing/sql-server-audit-database-engine.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
CREATE SERVER AUDIT audit_name  
{  
    TO { [ FILE (<file_options> [ , ...n ] ) ] | APPLICATION_LOG | SECURITY_LOG }  
    [ WITH ( <audit_options> [ , ...n ] ) ]   
    [ WHERE <predicate_expression> ]  
}  
[ ; ]  
  
<file_options>::=  
{  
        FILEPATH = 'os_file_path'  
    [ , MAXSIZE = { max_size { MB | GB | TB } | UNLIMITED } ]  
    [ , { MAX_ROLLOVER_FILES = { integer | UNLIMITED } } | { MAX_FILES = integer } ]  
    [ , RESERVE_DISK_SPACE = { ON | OFF } ]   
}  
  
<audit_options>::=  
{  
    [   QUEUE_DELAY = integer ]  
    [ , ON_FAILURE = { CONTINUE | SHUTDOWN | FAIL_OPERATION } ]  
    [ , AUDIT_GUID = uniqueidentifier ]  
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
 TO { FILE | APPLICATION_LOG | SECURITY_LOG }  
 确定审核目标的位置。 选项包括二进制文件、Windows 应用程序日志或 Windows 安全日志。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 写入到 Windows 安全日志。 有关详细信息，请参阅 [将 SQL Server 审核事件写入安全日志](../../relational-databases/security/auditing/write-sql-server-audit-events-to-the-security-log.md)。  
  
 FILEPATH ='*os_file_path*'  
 审核日志的路径。 文件名是基于审核名称和审核 GUID 生成的。  
  
 MAXSIZE = { *max_size }*  
 指定审核文件可增大到的最大大小。 *Max_size*值必须跟 MB、 GB、 TB 或无限制的整数。 你可以为指定的最小大小*max_size*为 2 MB，最大值为 2,147,483,647 TB。 如果指定为 UNLIMITED，则文件将增长到磁盘变满为止。 （0 也指示 UNLIMITED。）指定低于 2 MB 的值将引发错误 MSG_MAXSIZE_TOO_SMALL。 默认值为 UNLIMITED。  
  
 MAX_ROLLOVER_FILES =*{整数*|不限}  
 指定要保留在文件系统中外加当前文件的最大文件数。 *MAX_ROLLOVER_FILES*值必须是整数或无限制。 默认值为 UNLIMITED。 审核重新启动时，此参数计算 (这可能发生时的实例[!INCLUDE[ssDE](../../includes/ssde-md.md)]重启或审核打开时关闭，然后在再次) 或者时是否需要新的文件，因为已达到最大大小。 当*MAX_ROLLOVER_FILES*计算，如果文件数超过*MAX_ROLLOVER_FILES*设置，删除最旧的文件。 因此，当设置*MAX_ROLLOVER_FILES*为的 0 创建一个新文件每次*MAX_ROLLOVER_FILES*设置进行评估。 只有一个文件是自动时删除*MAX_ROLLOVER_FILES*设置进行评估，因此，在值*MAX_ROLLOVER_FILES*是减少，文件数不收缩除非旧文件手动删除。 可以指定的最大文件数为 2,147,483,647。  
  
 MAX_FILES =*integer*  
 **适用范围**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 指定可创建的审核文件的最大数目。 当达到此限制时，不滚动更新到第一个文件。 当达到 MAX_FILES 限制时，导致附加审核事件生成，任何操作都将失败并出现错误。  
  
 RESERVE_DISK_SPACE = { ON | OFF }  
 此选项会按 MAXSIZE 值为磁盘上的文件预先分配大小。 它仅适用于最大大小不等于无限制。 默认值为 OFF。  
  
 QUEUE_DELAY =*integer*  
 确定在强制处理审核操作之前可以经过的时间（以毫秒为单位）。 值 0 指示同步传递。 可设置的最小延迟值为 1000（1 秒），这是默认值。 最大值为 2,147,483,647（2,147,483.647 秒或者 24 天 20 小时 31 分钟 23.647 秒）。 指定数量无效，将引发 MSG_INVALID_QUEUE_DELAY 错误。  
  
 ON_FAILURE = { CONTINUE | SHUTDOWN | FAIL_OPERATION }  
 指示在目标无法写入审核日志时写入目标的实例是应失败、继续还是停止 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 默认值为 CONTINUE。  
  
 CONTINUE  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 操作将继续。 审核记录将不会保留。 审核将继续尝试登录事件和恢复，如果故障条件得到解决。 选择继续选项可以允许未经审核的活动，这可能违反您的安全策略。 在[!INCLUDE[ssDE](../../includes/ssde-md.md)]的继续操作比维护完整审核更重要时，使用此选项。  
  
SHUTDOWN  
强制的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]才可关闭，如果[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]将数据写入审核目标出于任何原因而失败。 登录名执行`CREATE SERVER AUDIT`语句必须具有`SHUTDOWN`内的权限[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 关机问题仍然存在即使`SHUTDOWN`权限更高版本吊销从正在执行的登录名。 如果用户不具有此权限，然后则语句将失败审核不是会创建和。 在审核失败可能损害系统的安全或完整性时，使用此选项。 有关详细信息，请参阅[关闭](../../t-sql/language-elements/shutdown-transact-sql.md)。  
  
 FAIL_OPERATION  
 如果数据库操作会导致审核的事件，则数据库操作将失败。 可以继续操作，不会导致审核的事件，但是可能会发生任何审核的事件。 审核将继续尝试登录事件和恢复，如果故障条件得到解决。 在维护完整审核比对[!INCLUDE[ssDE](../../includes/ssde-md.md)]的完全访问权限更重要时，使用此选项。  
**适用范围**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。

 AUDIT_GUID =*uniqueidentifier*  
 为了支持数据库镜像之类的方案，审核功能需要一个与在镜像数据库中所找到的 GUID 相匹配的特定 GUID。 创建审核之后，即不能修改该 GUID。  
  
 predicate_expression  
 **适用范围**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 指定用于确定是否应处理事件的谓词表达式。 谓词表达式限制在 3000 个字符，这限制了字符串参数。  
  
 event_field_name  
 **适用范围**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 表示标识谓词源的事件字段的名称。 审核字段描述的[sys.fn_get_audit_file &#40;Transact SQL &#41;](../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md). 所有字段可以都筛选除`file_name`， `audit_file_offset`，和`event_time`。  

> [!NOTE]  
>  虽然`action_id`和`class_type`字段属于类型**varchar**中 sys.fn_get_audit_file，它们仅可与数字时它们是为进行筛选的谓词源。 若要获取要与一起使用的值列表`class_type`，执行以下查询：  
> ```sql
> SELECT spt.[name], spt.[number]
> FROM   [master].[dbo].[spt_values] spt
> WHERE  spt.[type] = N'EOD'
> ORDER BY spt.[name];
> ```


 number  
 **适用范围**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 任何数值类型包括**十进制**。 局限性在于缺少可用物理内存，或数值过大而无法用 64 位整数表示。  
  
 ' string '  
 **适用范围**： [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 进行谓词比较所需的 ANSI 字符串或 Unicode 字符串。 不为谓词比较函数执行隐式字符串类型转换。 传递错误类型会导致出错。  
  
## <a name="remarks"></a>注释  
 服务器审核在创建之后处于禁用状态。  
  
 CREATE SERVER AUDIT 语句位于事务范围内。 如果对事务进行回滚，也将对该语句进行回滚。  
  
## <a name="permissions"></a>权限  
 若要创建、更改或删除服务器审核，主体需要拥有 ALTER ANY SERVER AUDIT 或 CONTROL SERVER 权限。  
  
 在您将审核信息保存到某一文件时，为了避免被篡改，应限制对文件位置的访问。  
  
## <a name="examples"></a>示例  
  
### <a name="a-creating-a-server-audit-with-a-file-target"></a>A. 创建一个以文件为目标的服务器审核  
 下面的示例创建一个名为 `HIPPA_Audit` 的服务器审核，它以二进制文件为目标，而且不带选项。  
  
```sql  
CREATE SERVER AUDIT HIPAA_Audit  
    TO FILE ( FILEPATH ='\\SQLPROD_1\Audit\' );  
```  
  
### <a name="b-creating-a-server-audit-with-a-windows-application-log-target-with-options"></a>B. 创建一个带有选项且以 Windows 应用程序日志为目标的服务器审核  
 下面的示例创建一个名为 `HIPPA_Audit` 的服务器审核，它以 Windows 应用程序日志作为目标集。 每秒向队列中写入一次，在遇到故障时将关闭 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 引擎。  
  
```sql  
CREATE SERVER AUDIT HIPAA_Audit  
    TO APPLICATION_LOG  
    WITH ( QUEUE_DELAY = 1000,  ON_FAILURE = SHUTDOWN);  
```  
  
###  <a name="ExampleWhere"></a> C. 创建包含 WHERE 子句的服务器审核  
 下面的示例将创建用于一个数据库、架构和用于该示例的两个表。 名为的表`DataSchema.SensitiveData`包含机密数据，而访问的表必须记录在审核。 名为 `DataSchema.GeneralData` 的表不包含保密数据。 数据库审核规范将审核对 `DataSchema` 架构中所有对象的访问。 将使用 WHERE 子句创建服务器审核，该子句将服务器审核限制为仅限 `SensitiveData` 表。 服务器审核假定审核文件夹位于`C:\SQLAudit`。  
  
```sql  
CREATE DATABASE TestDB;  
GO  
USE TestDB;  
GO  
CREATE SCHEMA DataSchema;  
GO  
CREATE TABLE DataSchema.GeneralData (ID int PRIMARY KEY, DataField varchar(50) NOT NULL);  
GO  
CREATE TABLE DataSchema.SensitiveData (ID int PRIMARY KEY, DataField varchar(50) NOT NULL);  
GO  
-- Create the server audit in the master database  
USE master;  
GO  
CREATE SERVER AUDIT AuditDataAccess  
    TO FILE ( FILEPATH ='C:\SQLAudit\' )  
    WHERE object_name = 'SensitiveData' ;  
GO  
ALTER SERVER AUDIT AuditDataAccess WITH (STATE = ON);  
GO  
-- Create the database audit specification in the TestDB database  
USE TestDB;  
GO  
CREATE DATABASE AUDIT SPECIFICATION [FilterForSensitiveData]  
FOR SERVER AUDIT [AuditDataAccess]   
ADD (SELECT ON SCHEMA::[DataSchema] BY [public])  
WITH (STATE = ON);  
GO  
-- Trigger the audit event by selecting from tables  
SELECT ID, DataField FROM DataSchema.GeneralData;  
SELECT ID, DataField FROM DataSchema.SensitiveData;  
GO  
-- Check the audit for the filtered content  
SELECT * FROM fn_get_audit_file('C:\SQLAudit\AuditDataAccess_*.sqlaudit',default,default);  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [ALTER SERVER AUDIT &#40;Transact SQL &#41;](../../t-sql/statements/alter-server-audit-transact-sql.md)   
 [DROP SERVER AUDIT &#40;Transact SQL &#41;](../../t-sql/statements/drop-server-audit-transact-sql.md)   
 [创建服务器审核规范 &#40;Transact SQL &#41;](../../t-sql/statements/create-server-audit-specification-transact-sql.md)   
 [ALTER SERVER AUDIT SPECIFICATION &#40;Transact SQL &#41;](../../t-sql/statements/alter-server-audit-specification-transact-sql.md)   
 [删除服务器审核规范 &#40;Transact SQL &#41;](../../t-sql/statements/drop-server-audit-specification-transact-sql.md)   
 [创建数据库审核规范 &#40;Transact SQL &#41;](../../t-sql/statements/create-database-audit-specification-transact-sql.md)   
 [ALTER DATABASE AUDIT SPECIFICATION &#40;Transact SQL &#41;](../../t-sql/statements/alter-database-audit-specification-transact-sql.md)   
 [删除数据库审核规范 &#40;Transact SQL &#41;](../../t-sql/statements/drop-database-audit-specification-transact-sql.md)   
 [ALTER AUTHORIZATION &#40;Transact SQL &#41;](../../t-sql/statements/alter-authorization-transact-sql.md)   
 [sys.fn_get_audit_file &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-get-audit-file-transact-sql.md)   
 [sys.server_audits &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audits-transact-sql.md)   
 [sys.server_file_audits &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-file-audits-transact-sql.md)   
 [sys.server_audit_specifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audit-specifications-transact-sql.md)   
 [sys.server_audit_specification_details &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-server-audit-specification-details-transact-sql.md)   
 [sys.database_audit_specifications &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-audit-specifications-transact-sql.md)   
 [sys.database_audit_specification_details &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-audit-specification-details-transact-sql.md)   
 [sys.dm_server_audit_status &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-server-audit-status-transact-sql.md)   
 [sys.dm_audit_actions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-actions-transact-sql.md)   
 [sys.dm_audit_class_type_map &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-audit-class-type-map-transact-sql.md)   
 [创建服务器审核和服务器审核规范](../../relational-databases/security/auditing/create-a-server-audit-and-server-audit-specification.md)  
  
  
