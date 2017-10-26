---
title: "管理事务日志文件大小 | Microsoft Docs"
ms.custom: 
ms.date: 05/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-transaction-log
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- transaction logs [SQL Server], size management
ms.assetid: 3a70e606-303f-47a8-96d4-2456a18d4297
caps.latest.revision: 23
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Active
ms.translationtype: HT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: 9076e3fbddd2af5459e4d8895ce969c61a4315ad
ms.contentlocale: zh-cn
ms.lasthandoff: 09/27/2017

---
# <a name="manage-the-size-of-the-transaction-log-file"></a>管理事务日志文件的大小
本主题介绍如何监视 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 事务日志大小、收缩事务日志、添加或扩大事务日志文件、优化 tempdb 事务日志增长率以及控制事务日志文件的增长。  

  ##  <a name="MonitorSpaceUse"></a> 监视日志空间使用情况  
使用 [DBCC SQLPERF (LOGSPACE)](https://docs.microsoft.com/sql/t-sql/database-console-commands/dbcc-sqlperf-transact-sql) 监视日志空间使用情况。 此命令返回有关当前使用的日志空间量的信息，并指示何时需要截断事务日志。 有关详细信息，请参阅 [DBCC SQLPERF Transact-SQL](../../t-sql/database-console-commands/dbcc-sqlperf-transact-sql.md)。 若要了解有关日志文件的当前大小、最大大小以及文件的自动增长选项的信息，还可以在 sys.database_files 中针对此日志文件使用 size、max_size 和 growth 等列。 有关详细信息，请参阅 [sys.database_files (Transact-SQL)](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)。  
  
**重要说明！** 避免日志磁盘重载！  

  
##  <a name="ShrinkSize"></a> 收缩日志文件大小  
 若要减少物理日志文件的物理大小，则必须收缩日志文件。 知道事务日志文件包含未使用空间时，此方法很有用。 仅当数据库处于联机状态，而且至少一个虚拟日志文件可用时，才能收缩日志文件。 在某些情况下，直到下一个日志截断后，才能收缩日志。  
  
> [!NOTE]
>  能够延长虚拟日志文件活动时间的因素（如长时间运行的事务）可以限制甚至阻止日志收缩。 有关延迟日志截断的因素的信息，请参阅[事务日志 (SQL Server)](../../relational-databases/logs/the-transaction-log-sql-server.md)。  
  
 收缩日志文件可删除一个或多个不包含逻辑日志任何部分的虚拟日志文件（即 *不活动的虚拟日志文件*）。 收缩事务日志文件时，将从日志文件末端删除不活动的虚拟日志文件，以将日志减小到接近目标大小。  
  
 **收缩日志文件（而不收缩数据库文件）**  
  
-   [DBCC SHRINKFILE (Transact-SQL)](../../t-sql/database-console-commands/dbcc-shrinkfile-transact-sql.md)  
  
-   [收缩文件](../../relational-databases/databases/shrink-a-file.md)  
  
 **监视日志文件收缩事件**  
  
-   [Log File Auto Shrink Event Class](../../relational-databases/event-classes/log-file-auto-shrink-event-class.md)。  
  
 **监视日志空间**  
  
-   [DBCC SQLPERF (Transact-SQL)](../../t-sql/database-console-commands/dbcc-sqlperf-transact-sql.md)  
  
-   [sys.database_files (Transact-SQL)](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)（请参阅日志文件或文件的 **size**、**max_size** 和 **growth** 列。）  
  
> [!NOTE]
>  可将日志文件设置为自动收缩。 但是，我们建议不使用自动收缩，且 **autoshrink** 数据库属性默认情况下设置为 FALSE。 如果 **autoshrink** 设置为 TRUE，则仅当其空间的 25% 以上未使用时，自动收缩才会减少文件的大小。 文件将收缩至未使用空间占文件 25% 的大小，或者收缩至文件的原始大小，以两者中较大者为准。 有关更改 **autoshrink** 属性设置的信息，请参阅[查看或更改数据库的属性](../../relational-databases/databases/view-or-change-the-properties-of-a-database.md) - 在 “选项” 页面使用 **Auto Shrink** 属性 - 或 [ALTER DATABASE SET 选项 (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql-set-options.md) - 使用 AUTO_SHRINK 选项。  
  

##  <a name="AddOrEnlarge"></a> 添加或扩大日志文件  
 可以通过扩大现有日志文件（如果磁盘空间允许）或将日志文件添加至数据库（尤其是其他磁盘上的数据库）来获得空间。  
  
-   若要将日志文件添加至数据库，请使用 ALTER DATABASE 语句的 ADD LOG FILE 子句。 添加日志文件可以使日志获得空间。  
  
-   若要扩大日志文件，请使用 ALTER DATABASE 语句的 MODIFY FILE 子句，并指定 SIZE 和 MAXSIZE 语法。 有关详细信息，请参阅 [ALTER DATABASE (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql.md)。  
    
  
##  <a name="tempdbOptimize"></a> 优化 tempdb 事务日志的大小  
 重新启动服务器实例可以将 **tempdb** 数据库的事务日志调整到自动增长之前的原始大小。 这会降低 **tempdb** 事务日志的性能。 您可以通过在启动或重新启动服务器实例之后增加 **tempdb** 事务日志的大小来避免此开销。 有关详细信息，请参阅 [tempdb Database](../../relational-databases/databases/tempdb-database.md)。  
  
  
##  <a name="ControlGrowth"></a> 控制事务日志文件的增长  
 可使用 [ALTER DATABASE (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql.md) 语句管理事务日志文件的增长。 请注意以下事项：  
  
-   若要更改当前文件大小（以 KB、MB、GB 和 TB 为单位），请使用 SIZE 选项。  
  -   若要更改增量，请使用 FILEGROWTH 选项。 如果值为 0，则表明自动增长已设置为关闭，且不允许增加空间。 日志文件的小幅度自动增长量可能降低性能。 因此，为了避免经常向日志文件中扩充内容，应该采用足够大的文件增量。 通常，采用 10% 的默认增量较为合适。  

有关更改日志文件的文件增长属性的信息，请参阅 [ALTER DATABASE (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql.md)。  
  
-   若要控制日志文件的最大大小（以 KB、MB、GB 和 TB 为单位）或将增长设置为 UNLIMITED，请使用 MAXSIZE 选项。  
  
  
## <a name="see-also"></a>另请参阅  
 [BACKUP (Transact-SQL)](../../t-sql/statements/backup-transact-sql.md)   
 [解决事务日志已满的问题（SQL Server 错误 9002）](../../relational-databases/logs/troubleshoot-a-full-transaction-log-sql-server-error-9002.md)  
  
  

