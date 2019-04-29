---
title: 管理 FileTable | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: filestream
ms.topic: conceptual
helpviewer_keywords:
- FileTables [SQL Server], security
- FileTables [SQL Server], managing access
ms.assetid: 93af982c-b4fe-4be0-8268-11f86dae27e1
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2e8522cde5be0ccc34f858ce6bff945433af11ac
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62874790"
---
# <a name="manage-filetables"></a>管理 FileTable
  说明用于管理 FileTable 的常见管理任务。  
  
##  <a name="HowToEnumerate"></a> 如何：获取 Filetable 和相关的对象的列表  
 若要获取 FileTable 的列表，请查询下列目录视图之一：  
  
-   [sys.filetables (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-filetables-transact-sql)  
  
-   [sys.tables (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-tables-transact-sql)（检查 **is_filetable** 列的值。）  
  
```sql  
SELECT * FROM sys.filetables;  
GO  
  
SELECT * FROM sys.tables WHERE is_filetable = 1;  
GO  
```  
  
 若要获取在创建关联的 FileTable 时创建的系统定义对象的列表，请查询目录视图 [sys.filetable_system_defined_objects (Transact-SQL) ](/sql/relational-databases/system-catalog-views/sys-filetable-system-defined-objects-transact-sql)。  
  
```sql  
SELECT object_id, OBJECT_NAME(object_id) AS 'Object Name'  
    FROM sys.filetable_system_defined_objects  
    WHERE object_id = filetable_object_id;  
GO  
```  
  
##  <a name="BasicsDisabling"></a> 禁用和重新启用数据库级别的非事务性访问权限  
 若要获取执行某些管理任务所需的独占访问权限，可能必须暂时禁用非事务性访问权限。  
  
 **更改非事务性访问级别时 ALTER DATABASE 语句的行为**  
  
-   只要存在与请求的操作冲突的打开的文件句柄，在将非事务性访问权限设置为 READ_ONLY 或 OFF 时，ALTER DATABASE 命令就不会向用户返回控制。 与此操作冲突的文件句柄包括下列内容：  
  
    -   当您将访问权限设置为 **NONE**时，则包括所有打开的文件句柄。  
  
    -   当你将访问权限设置为 **READ_ONLY**时，则包括打开以供写入访问的所有文件句柄。  
  
     有关终止打开的文件句柄的信息，请参阅本主题中的 [终止与 FileTable 关联的打开的文件句柄](#BasicsKilling) 。  
  
     如果 ALTER DATABASE 命令被取消或因超时而结束，则不更改事务性访问级别。  
  
-   如果调用带 WITH \<termination> 子句 (ROLLBACK AFTER integer [ SECONDS ] | ROLLBACK IMMEDIATE | NO_WAIT) 的 ALTER DATABASE 语句，则将终止所有打开的非事务性文件句柄。  
  
> [!WARNING]  
>  终止打开的文件句柄可能会导致用户丢失未保存的数据。 此行为与文件系统自身的行为一致。  
  
 **禁用非事务性访问的影响**  
  
 更改数据库级别的非事务性访问级别会对数据库级别目录下的 FileTable 目录产生下列影响：  
  
-   当您将访问权限设置为 **NONE**时，将不再能够访问或看到所有 FileTable 目录及其内容。  
  
-   将访问权限设置为 **READ_ONLY**时，所有 FileTable 目录及其内容还是只读的。  
  
 在实例级别禁用 FILESTREAM 将会对该实例上的数据库级别目录及其下的 FileTable 目录产生下列影响：  
  
-   如果在实例级别禁用 FILESTREAM，将看不到该实例上的任何数据库级别目录。  
  
###  <a name="HowToDisable"></a> 如何：禁用再重新启用数据库级别的非事务性访问权限  
 有关详细信息，请参阅 [ALTER DATABASE SET 选项 (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql-set-options)。  
  
 **禁用完全非事务性访问权限**  
 调用 **ALTER DATABASE** 语句并将 **NON_TRANSACTED_ACCESS 的值设置** 为 **READ_ONLY** 或 **OFF**。  
  
```sql  
-- Disable write access.  
ALTER DATABASE database_name  
    SET FILESTREAM ( NON_TRANSACTED_ACCESS = READ_ONLY );  
GO  
  
-- Disable non-transactional access.  
ALTER DATABASE database_name  
    SET FILESTREAM ( NON_TRANSACTED_ACCESS = OFF );  
GO  
```  
  
 **重新启用完全非事务性访问权限**  
 调用 **ALTER DATABASE** 语句并将 **NON_TRANSACTED_ACCESS** 的值设置为 **FULL**。  
  
```sql  
ALTER DATABASE database_name  
    SET FILESTREAM ( NON_TRANSACTED_ACCESS = FULL );  
GO  
```  
  
###  <a name="visible"></a> 如何：确保在数据库中的 Filetable 的可见性  
 当满足以下所有条件时，则可看到数据库级别目录及其下的 FileTable 目录：  
  
1.  在实例级别启用 FILESTREAM。  
  
2.  在数据库级别启用非事务性访问。  
  
3.  在数据库级别指定了有效目录。  
  
##  <a name="BasicsEnabling"></a> 禁用和重新启用表级别 FileTable 命名空间  
 禁用 FileTable 命名空间将会禁用所有系统定义的约束并触发使用 FileTable 创建的约束。 在必须通过使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] 操作大规模重新组织 FileTable 而不产生强制 FileTable 语义的开销时，这一点很有用。 但是，这些操作会将 FileTable 置于不一致的状态，会阻止重新启用 FileTable 命名空间。  
  
 禁用 FileTable 命名空间具有下列结果：  
  
-   FileTable 列和数据被从表中物理删除。  
  
-   FileTable 目录及其包含的文件和目录不再出现在文件系统中，且不可用于文件 I/O 访问。  
  
-   无法删除和重新创建系统定义的 FileTable 列；但是，对于 DML 操作，它们的行为与普通列无异。  
  
-   打开的文件句柄可防止 FileTable 约束被禁用，因为此操作需要使用表上的架构锁。  
  
-   强制所有 FileTable 语义的操作（包括系统定义的约束和触发器）在 FileTable 命名空间被禁用后停止。  
  
 重新启用 FileTable 命名空间会产生下列结果：  
  
-   检查 FileTable 以了解一致性。 如果找到不一致处，则引发错误且 FileTable 保持禁用状态；否则，将重新启用 FileTable。  
  
-   强制 FileTable 语义的操作（包括系统定义的约束和触发器）将恢复。  
  
-   FileTable 目录及其包含的文件和目录将在文件系统中再次可见，且可用于文件 I/O 访问。  
  
###  <a name="HowToEnableNS"></a> 如何：禁用再重新启用表级别 FileTable Namespace  
 使用 **{ ENABLE | DISABLE } FILETABLE_NAMESPACE** 选项调用 ALTER TABLE 语句。  
  
 **禁用 FileTable 命名空间**  
 ```sql  
ALTER TABLE filetable_name  
    DISABLE FILETABLE_NAMESPACE;  
GO  
```  
  
 **重新启用 FileTable 命名空间**  
 ```sql  
ALTER TABLE filetable_name  
    ENABLE FILETABLE_NAMESPACE;  
GO  
```  
  
##  <a name="BasicsKilling"></a> 终止与 FileTable 关联的打开的文件句柄  
 FileTable 中存储的文件的打开句柄可以阻止某些管理任务所需的独占访问。 若要启用紧急任务，您可能要终止与一个或多个 FileTable 关联的打开的文件句柄。  
  
> [!WARNING]  
>  终止打开的文件句柄可能会导致用户丢失未保存的数据。 此行为与文件系统自身的行为一致。  
  
###  <a name="HowToListOpen"></a> 如何：获取与 FileTable 关联的打开的文件句柄的列表  
 查询目录视图 [sys.dm_filestream_non_transacted_handles (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-filestream-non-transacted-handles-transact-sql)。  
  
```sql  
SELECT * FROM sys.dm_filestream_non_transacted_handles;  
GO  
```  
  
###  <a name="HowToKill"></a> 如何：终止与 FileTable 关联的打开的文件句柄  
 使用相应参数调用存储过程 [sp_kill_filestream_non_transacted_handles (Transact-SQL)](/sql/relational-databases/system-stored-procedures/filestream-and-filetable-sp-kill-filestream-non-transacted-handles) 以终止数据库或 FileTable 中所有打开的文件句柄或终止特定句柄。  
  
```  
USE database_name;  
  
-- Kill all open handles in all the filetables in the database.  
EXEC sp_kill_filestream_non_transacted_handles;  
GO  
  
-- Kill all open handles in a single filetable.  
EXEC sp_kill_filestream_non_transacted_handles @table_name = 'filetable_name';  
GO  
  
-- Kill a single handle.  
EXEC sp_kill_filestream_non_transacted_handles @handle_id = integer_handle_id;  
GO  
```  
  
###  <a name="HowToIdentifyLocks"></a> 如何：识别锁 Filetable 持有  
 FileTable 持有的大多数锁与应用程序打开的文件相对应。  
  
 **确定打开的文件和关联锁**  
 将动态管理视图 [sys.dm_tran_locks (Transact SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql) 中的 **request_owner_id** 字段与 [sys.dm_filestream_non_transacted_handles (Transact SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-filestream-non-transacted-handles-transact-sql)中的 **fcb_id** 字段进行联接。 在某些情况下，锁并不对应单个打开的文件句柄。  
  
```sql  
SELECT opened_file_name  
    FROM sys.dm_filestream_non_transacted_handles  
    WHERE fcb_id IN  
        ( SELECT request_owner_id FROM sys.dm_tran_locks );  
GO  
```  
  
##  <a name="BasicsSecurity"></a> FileTable 安全性  
 存储在 FileTable 中的文件和目录仅受 SQL Server 安全机制的保护。 将对文件系统访问和 [!INCLUDE[tsql](../../includes/tsql-md.md)] 访问强制实施基于表和列的安全性。 不支持 Windows 文件系统安全 API 和 ACL 设置。  
  
 由于文件数据作为 FILESTREAM 列存储在 FileTable 中，因此还将对 FileTable 应用 FILESTREAM 文件组和容器所适用的安全性和访问权限。  
  
 **FileTable 安全性和 Transact-SQL 访问**  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] 将像对任何其他表一样保护对 FileTable 中数据的访问。 对访问或更改数据的每个操作进行相应的表级别和列级别安全检查。  
  
 **FileTable 安全性和文件系统访问**  
 文件系统 API 需要对 FileTable 中整个行的相应 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 权限（表级别权限）来打开存储在 FileTable 中的文件或目录的句柄。 如果用户对 FileTable 中的任何列没有相应的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 权限，则将拒绝文件系统访问。  
  
##  <a name="OtherBackup"></a> 备份和 FileTable  
 当您使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 备份 FileTable 时，FILESTREAM 数据将与数据库中的结构化数据一起备份。 如果您不想将 FILESTREAM 数据与关系数据一起备份，则可以使用部分备份将 FILESTREAM 文件组排除在外。  
  
 **FileTable 备份的事务一致性**  
  
 很多管理工具和操作（包括备份、日志备份和事务性复制）通过读取事务日志来读取事务上一致的数据。 此时，它们读取作为事务的一部分更新的任意 FILESTREAM 数据。 未在数据库级别启用非事务性访问时，这些工具和操作在确保完全事务一致性下工作。  
  
 但是，启用完全非事务性访问时，FileTable 可以包含比工具或进程从事务日志读取的事务更新（通过非事务性更新）更晚的数据。 这意味着对特定事务进行的“时间点”还原操作包含的 FILESTREAM 数据可能比该事务更新。 在 FileTable 上允许非事务性更新时，这是预期的行为。  
  
##  <a name="Monitor"></a> SQL Server Profiler 和 FileTable  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Profiler 可为存储在 FileTable 中的文件捕获跟踪输出中的 Windows 文件打开和文件关闭操作。  
  
##  <a name="OtherAuditing"></a> 审核和 FileTable  
 可以像对任何其他表一样对 FileTable 进行审核。 但是，Win32 访问模式不是基于集的操作。 将文件系统中的单个操作转换为多个 Transact-SQL DML 操作。 例如，在 Microsoft Word 中打开文件将转换为多个打开/关闭/创建/重命名/删除操作和相应的 Transact-SQL DML 活动。 这将导致冗长的审核记录，很难将文件系统操作和相应的 Transact-SQL DML 审核记录关联。  
  
##  <a name="OtherDBCC"></a> DBCC 和 FileTable  
 可以使用 DBCC CHECKCONSTRAINTS 验证 FileTable 上的约束，包括系统定义的约束。  
  
## <a name="see-also"></a>请参阅  
 [FileTable 与其他 SQL Server 功能的兼容性](filetable-compatibility-with-other-sql-server-features.md)   
 [FileTable DDL、函数、存储过程和视图](../views/views.md)  
  
  
