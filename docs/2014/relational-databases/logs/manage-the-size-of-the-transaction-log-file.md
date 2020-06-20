---
title: 管理事务日志文件的大小 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- transaction logs [SQL Server], size management
ms.assetid: 3a70e606-303f-47a8-96d4-2456a18d4297
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 219ba0605d60bab0b13675f7f9f7ff01cace5755
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/18/2020
ms.locfileid: "85049739"
---
# <a name="manage-the-size-of-the-transaction-log-file"></a>管理事务日志文件的大小
  在某些情况下，物理收缩或扩展 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库的事务日志的物理日志文件非常有用。 本主题包含与下列各项有关的信息：如何监视 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 事务日志大小、收缩事务日志、添加或扩大事务日志文件、优化 **tempdb** 事务日志增长率以及控制事务日志文件的增长。  
  
  
##  <a name="monitor-log-space-use"></a><a name="MonitorSpaceUse"></a>监视日志空间使用情况  
 可以使用 DBCC SQLPERF (LOGSPACE) 监视日志空间使用情况。 此命令返回有关当前使用的日志空间量的信息，并指示何时需要截断事务日志。 有关详细信息，请参阅 [DBCC SQLPERF (Transact-SQL)](/sql/t-sql/database-console-commands/dbcc-sqlperf-transact-sql)。 若要了解有关日志文件的当前大小、最大大小以及此文件的自动增长选项的信息，还可以在 **sys.database_files** 中针对此日志文件使用 **size**、**max_size** 和 **growth** 等列。 有关详细信息，请参阅 [sys.database_files (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-database-files-transact-sql)。  
  
> [!IMPORTANT]  
>  建议避免日志磁盘重载。  
  
  
##  <a name="shrink-the-size-of-the-log-file"></a><a name="ShrinkSize"></a>缩小日志文件的大小  
 若要减少物理日志文件的物理大小，则必须收缩日志文件。 如果您知道事务日志文件包含将不需要的未使用空间，则此方法很有用。 仅当数据库处于联机状态，而且至少一个虚拟日志文件可用时，才会发生收缩日志文件。 在某些情况下，直到下一个日志截断后，才能收缩日志。  
  
> [!NOTE]  
>  能够延长虚拟日志文件活动时间的因素（如长时间运行的事务）可以限制甚至阻止日志收缩。 有关延迟日志截断的因素的信息，请参阅[事务日志 (SQL Server)](the-transaction-log-sql-server.md)。  
  
 收缩日志文件可删除一个或多个不包含逻辑日志任何部分的虚拟日志文件（即“不活动的虚拟日志文件” **）。 在收缩事务日志文件时，将从日志文件的末端删除足够的不活动虚拟日志文件，以便将日志减小到接近目标大小。  
  
 **收缩日志文件（而不收缩数据库文件）**  
  
-   [DBCC SHRINKFILE (Transact-SQL)](/sql/t-sql/database-console-commands/dbcc-shrinkfile-transact-sql)  
  
-   [收缩文件](../databases/shrink-a-file.md)  
  
 **监视日志文件收缩事件**  
  
-   [日志文件自动收缩事件类](../event-classes/log-file-auto-shrink-event-class.md)。  
  
 `To monitor log space`  
  
-   [DBCC SQLPERF (Transact-SQL)](/sql/t-sql/database-console-commands/dbcc-sqlperf-transact-sql)  
  
-   [sys.database_files (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-database-files-transact-sql)（请参阅日志文件或文件的 **size**、**max_size** 和 **growth** 列。）  
  
> [!NOTE]  
>  收缩数据库和日志文件可以设置为自动发生。 但是，我们建议不使用自动收缩，且 `autoshrink` 数据库属性默认情况下设置为 FALSE。 如果 `autoshrink` 设置为 TRUE，则仅当其空间的 25% 以上未使用时，自动收缩才会减少文件的大小。 文件将收缩至未使用空间占文件 25% 的大小，或者收缩至文件的原始大小，以两者中较大者为准。 有关更改属性设置的信息 `autoshrink` ，请参阅[查看或更改数据库的属性](../databases/view-or-change-the-properties-of-a-database.md)-使用 "**选项**" 页上的 "**自动收缩**" 属性或 "[更改数据库集选项" &#40;transact-sql&#41;](/sql/t-sql/statements/alter-database-transact-sql-set-options)-使用 AUTO_SHRINK 选项。  
  
  
##  <a name="add-or-enlarge-a-log-file"></a><a name="AddOrEnlarge"></a>添加或扩大日志文件  
 可以通过扩大现有的日志文件（如果磁盘空间允许）或将日志文件添加至数据库（尤其是其他磁盘上的数据库）来获得空间。  
  
-   若要将日志文件添加至数据库，请使用 ALTER DATABASE 语句的 ADD LOG FILE 子句。 添加日志文件可以使日志获得空间。  
  
-   若要扩大日志文件，请使用 ALTER DATABASE 语句的 MODIFY FILE 子句，并指定 SIZE 和 MAXSIZE 语法。 有关详细信息，请参阅 [ALTER DATABASE (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql)。  
  
  
##  <a name="optimize-the-size-of-the-tempdb-transaction-log"></a><a name="tempdbOptimize"></a>优化 tempdb 事务日志的大小  
 重新启动服务器实例可以将 **tempdb** 数据库的事务日志调整到自动增长之前的原始大小。 这会降低 **tempdb** 事务日志的性能。 您可以通过在启动或重新启动服务器实例之后增加 **tempdb** 事务日志的大小来避免此开销。 有关详细信息，请参阅 [tempdb Database](../databases/tempdb-database.md)。  
  
  
##  <a name="control-the-growth-of-a-transaction-log-file"></a><a name="ControlGrowth"></a>控制事务日志文件的增长  
 可使用 [ALTER DATABASE (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql) 语句管理事务日志文件的增长。 注意以下事项：  
  
-   若要更改当前文件大小（以 KB、MB、GB 和 TB 为单位），请使用 SIZE 选项。  
  
-   若要更改增量，请使用 FILEGROWTH 选项。 如果值为 0，则表明自动增长已设置为关闭，且不允许增加空间。 日志文件的小幅度自动增长量可能降低性能。 因此，为了避免经常向日志文件中扩充内容，应该采用足够大的文件增量。 通常，采用 10% 的默认增量较为合适。  
  
     有关更改日志文件的文件增长属性的信息，请参阅[ALTER DATABASE &#40;transact-sql&#41;](/sql/t-sql/statements/alter-database-transact-sql)。  
  
-   若要控制日志文件的最大大小（以 KB、MB、GB 和 TB 为单位）或将增长设置为 UNLIMITED，请使用 MAXSIZE 选项。  
  
  
## <a name="see-also"></a>另请参阅  
 [BACKUP (Transact-SQL)](/sql/t-sql/statements/backup-transact-sql)   
 [解决事务日志已满的问题（SQL Server 错误 9002）](troubleshoot-a-full-transaction-log-sql-server-error-9002.md)  
  
  
