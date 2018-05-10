---
title: FileTable 与其他 SQL Server 功能的兼容性 | Microsoft Docs
ms.custom: ''
ms.date: 08/26/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: blob
ms.reviewer: ''
ms.suite: sql
ms.technology:
- dbe-blob
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- FileTables [SQL Server], using with other features
ms.assetid: f12a17e4-bd3d-42b0-b253-efc36876db37
caps.latest.revision: 19
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e4d74fedccd53867721676f8e070f68bcd463a3b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="filetable-compatibility-with-other-sql-server-features"></a>FileTable 与其他 SQL Server 功能的兼容性
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  说明 FileTable 如何与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的其他功能配合使用。  
  
##  <a name="alwayson"></a> AlwaysOn 可用性组和 FileTable  
 在包含 FILESTREAM 或 FileTable 数据的数据库属于某一 AlwaysOn 可用性组时：  
  
-   [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]支持部分 FileTable 功能。 故障转移后，FileTable 数据在主副本上是可访问的，但是在可读辅助副本上不可访问。  
  
    > **注意：**  请注意故障转移后支持所有 FILESTREAM 功能。 FILESTREAM 数据在可读辅助副本和新的主副本上均可访问。  
  
-   FILESTREAM 和 FileTable 函数接受或返回虚拟网络名称 (VNN)，而非计算机名称。 有关这些函数的详细信息，请参阅 [Filestream 和 FileTable 函数 (Transact-SQL)](../../relational-databases/system-functions/filestream-and-filetable-functions-transact-sql.md)。  
  
-   通过文件系统 API 对 FILESTREAM 或 FileTable 数据进行的所有访问都应该使用 VNN，而非计算机名称。 有关详细信息，请参阅 [FILESTREAM 和 FileTable 与 AlwaysOn 可用性组 (SQL Server)](../../database-engine/availability-groups/windows/filestream-and-filetable-with-always-on-availability-groups-sql-server.md)。  
  
##  <a name="OtherPartitioning"></a> 分区和 FileTable  
 FileTable 不支持分区。 通过对多个 FILESTREAM 文件组的支持，在大多数方案中可以解决纯向上扩展问题，而不必使用分区（不像 SQL 2008 FILESTREAM）。  
  
##  <a name="OtherRepl"></a> 复制和 FileTable  
 FileTable 不支持复制和相关功能（包括事务性复制、合并复制、更改数据捕获和更改跟踪）。  
  
##  <a name="OtherIsolation"></a> 事务语义和 FileTable  
 **Windows 应用程序**  
 Windows 应用程序不理解数据库事务，因此 Windows 写操作不提供数据库事务的 ACID 属性。 因此事务性回滚和恢复不适用于 Windows 更新操作。  
  
 **Transact-SQL 应用程序**  
 对于应用于 FileTable 中的 FILESTREAM (file_stream) 列的 TSQL 应用程序，隔离语义与常规用户表中的 FILESTREAM 数据类型相同。  
  
##  <a name="OtherQueryNot"></a> 查询通知和 FileTable  
 查询不能包含对 FileTable、WHERE 子句或查询的任何其他部分中的 FILESTREAM 列的引用。  
  
##  <a name="OtherSelectInto"></a> SELECT INTO 和 FileTable  
 FileTable 中的 SELECT INTO 语句将不在创建的目标表上传播 FileTable 语义（就像常规表中的 FILESTREAM 列一样）。 所有目标表列的行为就像常规列的行为一样。 没有任何 FileTable 语义与之关联。  
  
##  <a name="OtherTriggers"></a> 触发器和 FileTable  
 **DDL（数据定义语言）触发器**  
 对于 DDL 触发器用于 FileTable 没有特别的注意事项。 对于 Create/Alter 数据库操作以及针对 FileTable 的 CREATE/ALTER TABLE 操作，普通 DDL 触发器将被激发。 触发器可以通过调用 EVENTDATA() 函数来检索包括 DDL 命令文本和其他信息的实际事件数据。 不添加新事件，也不更改现有 Eventdata 架构。  
  
 **DML（数据操作语言）触发器**  
 在 DDL 操作过程中，将应用这些限制来创建触发器。  
  
-   FileTable 不支持用于 DML 操作的 INSTEAD OF 触发器。 对包含 FILESTREAM 列的所有表已存在一个限制。  
  
-   FileTable 支持用于 DML 操作的 AFTER 触发器。  
  
-   在 FileTable 上定义的触发器不能更新任何 FileTable（包括父 FileTable）。 存在此限制主要是为了防止在同一事务中触发器与文件系统访问持有的锁发生锁定冲突。  
  
 **非事务性访问及其对触发器的影响**  
 -   在数据库中允许非事务性更新访问时，可以在任何表中执行 FILESTREAM 数据的就地更新，包括该数据库中的 FileTable。 由于这种可能性，FILESTREAM 内容的前像可能不能由触发器使用。  
  
-   对于通过文件系统的非事务性更新操作，SQL Server 将创建一个内部事务来捕获 CloseHandle 操作，任何定义的 DML 触发器可能作为该事务的一部分激发。 将不阻止在触发器主体内对此类事务进行的回滚，但不回滚对该 FILESTREAM 所做的更改。  即使 FILESTREAM 内容可能已经更改，这种回滚仍可能会阻止 Update 触发器激发。  
  
-   除了这些影响外，FileTable 的触发器还需要处理一些其他行为。  
  
    -   通过文件系统对 FileTable 执行非事务性更新操作时，FILESTREAM 内容可能被其他 Win32 操作以独占方式锁定，从而不能通过触发器主体对其进行读/写访问。 在这些情况下，任何在触发器主体中对 FILESTREAM 内容进行访问的尝试都可能导致“共享冲突”错误。 触发器应设计为可正确地处理这类错误。  
  
    -   FILESTREAM 的后像可能不稳定，原因是由于在文件系统访问中允许共享模式，其他非事务性更新也会同时频繁地向 FILESTREAM 写入内容。  
  
-   在恢复操作期间，Win32 句柄的异常终止（如通过管理员或数据库崩溃显式终止 Win32 句柄）将不执行用户触发器，即使 FILESTREAM 内容可能已被异常终止的 Win32 应用程序更改。  
  
##  <a name="OtherViews"></a> 视图和 FileTable  
 **视图**  
 可以像为任何其他表一样为 FileTable 创建视图。 但是对于为 FileTable 创建的视图有以下注意事项：  
  
-   视图将不具有任何 FileTable 语义， 即，视图中的列（包括“文件属性”列）的行为与常规视图列一样，不具有任何特殊语义，对于表示文件/目录的行也是如此。  
  
-   可以基于“可更新视图”语义更新视图，但是基础表约束可能拒绝更新，就像在表中一样。  
  
-   可以通过将文件的路径添加为视图中的显式列，在视图中显示该路径。 例如：  
  
     `CREATE VIEW MP3FILES AS SELECT column1, column2, …, GetFileNamespacePath() AS PATH, column3,…  FROM Documents`  
  
 **索引视图**  
 当前索引视图不能包括 FILESTREAM 列或依赖 FILESTREAM 列的计算/持久计算列。 对于在 FileTable 上定义的视图也同样如此。  
  
##  <a name="OtherSnapshots"></a> 快照隔离和 FileTable  
 已提交读快照隔离 (RCSI) 和快照隔离 (SI) 依赖是否具有可用于读取器的数据快照，甚至正在对数据进行更新时也是如此。 但是，FileTable 允许对文件流数据进行非事务性写访问。 因此，在包含 FileTable 的数据库中使用这些功能存在以下限制：  
  
-   可以更改包含 FileTable 的数据库以启用 RCSI/SI。  
  
-   将对数据库的非事务性访问设置为 FULL 时，在 RCSI 或 SI 下运行的事务将具有以下行为：  
  
    -   对 FileTable file_stream 列的任何 [!INCLUDE[tsql](../../includes/tsql-md.md)] 读取将失败。 对该列的 INSERT 和 UPDATE 仍将成功，前提是这些操作不会从 file_stream 列中读取数据。  
  
    -   如果 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句指定 READCOMMITTEDLOCK 表提示，则读取将成功，并获取对行的锁定而不是使用行版本控制。  
  
    -   事务性的 Win32 FileStream 打开请求也将失败。  
  
    -   非事务性的 FileTable Win32 访问将成功。 将不影响 FileTable 执行的所有内部查询。  
  
    -   无论数据库选项如何（READ_COMMITTED_SNAPSHOT 或 ALLOW_SNAPSHOT_ISOLATION），全文索引编制始终会成功。  
  
##  <a name="readsec"></a> 可读辅助数据库  
 有关快照的注意事项同样适用于可读辅助数据库，如上一节 [快照隔离和 FileTable](#OtherSnapshots)中所述。  
  
##  <a name="CDB"></a> 包含的数据库和 FileTable  
 FileTable 功能所依赖的 FILESTREAM 功能要求在数据库外部的一些配置。 因此，使用 FILESTREAM 或 FileTable 的数据库并未被完全包含。  
  
 如果您想要使用包含的数据库的某些功能（例如包含的用户），则可以将数据库包含设置为 PARTIAL。 但在此情况下，您必须知道某些数据库设置未包含在数据库中，并且在数据库移动时不自动移动。  
  
## <a name="see-also"></a>另请参阅  
 [管理 FileTable](../../relational-databases/blob/manage-filetables.md)  
  
  
