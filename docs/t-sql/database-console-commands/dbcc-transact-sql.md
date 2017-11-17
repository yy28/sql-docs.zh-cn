---
title: "DBCC (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 11/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|database-console-commands
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DBCC
- DBCC_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- transactional consistency
- Database Console Command statements
- status information [SQL Server], DBCC statements
- snapshots [SQL Server database snapshots], DBCC statements
- emergency database state [SQL Server]
- TABLOCK
- internal database snapshots [SQL Server]
- reporting DBCC statement progress
- logical consistency of data [SQL Server]
- DBCC statements
- validation statements [SQL Server]
- miscellaneous statements [SQL Server]
- statements [SQL Server], DBCC statements
- DBCC commands [SQL Server]
- result sets [SQL Server], DBCC statements
- maintenance statements [SQL Server]
- physical consistency of data [SQL Server]
- current DBCC statement status
- progress reporting [DBCC statements]
- informational statements [SQL Server]
ms.assetid: c6da8c04-5b6b-459a-9f76-110c92ca8b29
caps.latest.revision: 50
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8e8750f4b44ec206bb5a26586acd6b567f7dac37
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="dbcc-transact-sql"></a>DBCC (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

[!INCLUDE[tsql](../../includes/tsql-md.md)] 编程语言提供 DBCC 语句以作为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的数据库控制台命令。
  
数据库控制台命令语句可分为以下类别。
  
|命令类别|执行|  
|---|---|
|维护|对数据库、索引或文件组进行维护的任务。|  
|杂项|杂项任务，如启用跟踪标志或从内存中删除 DLL。|  
|信息性|收集并显示各种类型信息的任务。|  
|验证|对数据库、表、索引、目录、文件组或数据库页的分配进行的验证操作。|  
  
DBCC 命令使用输入参数并返回值。 所有 DBCC 命令参数都可以接受 Unicode 和 DBCS 文字。
  
## <a name="dbcc-internal-database-snapshot-usage"></a>DBCC 内部数据库快照用法  
以下 DBCC 命令对 [!INCLUDE[ssDE](../../includes/ssde-md.md)]创建的内部只读数据库快照执行操作。 这样可以防止在执行这些命令时出现阻塞和并发问题。 有关详细信息，请参阅[数据库快照 (SQL Server)](../../relational-databases/databases/database-snapshots-sql-server.md)。
- DBCC CHECKALLOC
- DBCC CHECKCATALOG
- DBCC CHECKDB
- DBCC CHECKFILEGROUP
- DBCC CHECKTABLE

在执行这些 DBCC 命令之一时，[!INCLUDE[ssDE](../../includes/ssde-md.md)]创建一个数据库快照，并将其置于在事务上一致的状态。 然后，DBCC 命令对该快照运行检查。 DBCC 命令完成后，将删除该快照。
  
有时，不需要内部数据库快照或无法创建内部数据库快照。 出现这种情况时，将针对实际数据库执行 DBCC 命令。 如果数据库联机，DBCC 命令使用表锁确保它所检查的对象的一致性。 该行为与指定 WITH TABLOCK 选项时的行为相同。
  
执行 DBCC 命令时，不创建内部数据库快照：
-   针对**master**，和的实例[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]在单用户模式下运行。  
-   针对以外的其他数据库**master**，但数据库已放置在单用户模式下使用 ALTER DATABASE 语句。  
-   针对只读数据库。  
-   针对已使用 ALTER DATABASE 语句设置为紧急模式的数据库。  
-   针对**tempdb**。 在这种情况下，由于内部限制不能创建数据库快照。  
-   使用 WITH TABLOCK 选项。 在这种情况下，DBCC 允许该请求但不创建数据库快照。  
  
当针对以下对象执行 DBCC 命令时，该命令将使用表锁而不是内部数据库快照：
-   只读文件组  
-   FAT 文件系统  
-   不支持“命名流”的卷  
-   不支持“备用流”的卷  
  
> [!NOTE]  
>  尝试使用 WITH TABLOCK 选项运行 DBCC CHECKALLOC 或 DBCC CHECKDB 的等价部分时，需要使用数据库 X 锁。 无法在上设置此数据库锁**tempdb**或**master**和所有其他数据库都可能将失败。  
  
> [!NOTE]  
>  DBCC CHECKDB 无法正常工作，这是针对运行时**master**如果无法创建内部数据库快照。  
  
## <a name="progress-reporting-for-dbcc-commands"></a>DBCC 命令的进度报告  
**Sys.dm_exec_requests**目录视图包含有关的进度和 DBCC CHECKDB、 CHECKFILEGROUP 和 CHECKTABLE 命令执行的当前阶段的信息。 **Percent_complete**列指示该命令完成的百分比和**命令**列报告命令的执行的当前阶段。
  
进度单位的定义取决于 DBCC 命令的当前执行阶段。 有时，根据数据库页的粒度报告进度，而在其他阶段，则根据单个数据库或分配修复的粒度报告进度。 下表对每个执行阶段以及命令报告进度的粒度进行了说明。
  
|执行阶段|Description|进度报告粒度|  
|---------------------|-----------------|------------------------------------|  
|DBCC TABLE CHECK|在该阶段中将检查数据库中对象的逻辑和物理一致性。|在数据库页级别报告进度。<br /><br /> 进度报告值都会更新检查每个 1000年数据库页。|  
|DBCC TABLE REPAIR|如果指定 REPAIR_FAST、REPAIR_REBUILD 或 REPAIR_ALLOW_DATA_LOSS 并且存在必须修复的对象错误，则在该阶段执行数据库修复。|在单个修复级别报告进度。<br /><br /> 每次完成修复时更新计数器。|  
|DBCC ALLOC CHECK|在该阶段中将检查数据库中的分配结构。<br /><br /> 注意： DBCC CHECKALLOC 执行相同的检查。|不报告进度|  
|DBCC ALLOC REPAIR|如果指定 REPAIR_FAST、REPAIR_REBUILD 或 REPAIR_ALLOW_DATA_LOSS 并且存在必须修复的分配错误，则在该阶段执行数据库修复。|不报告进度。|  
|DBCC SYS CHECK|在该阶段中将检查数据库系统表。|在数据库页级别报告进度。<br /><br /> 每检查 1000 个数据库页更新进程报告值一次。|  
|DBCC SYS REPAIR|如果指定 REPAIR_FAST、REPAIR_REBUILD 或 REPAIR_ALLOW_DATA_LOSS 并且存在必须修复的系统表错误，则在该阶段执行数据库修复。|在单个修复级别报告进度。<br /><br /> 每次完成修复时更新计数器。|  
|DBCC SSB CHECK|在该阶段中将检查 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Service Broker 对象。<br /><br /> 注意： 执行 DBCC CHECKTABLE 时，此阶段不执行。|不报告进度。|  
|DBCC CHECKCATALOG|在该阶段中将检查数据库目录的一致性。<br /><br /> 注意： 执行 DBCC CHECKTABLE 时，此阶段不执行。|不报告进度。|  
|DBCC IVIEW CHECK|在该阶段中将检查数据库中存在的任何索引视图的逻辑一致性。|在被检查的单个数据库视图级别报告进度。|  
  
## <a name="informational-statements"></a>信息性语句  
  
|||  
|-|-|  
|[DBCC INPUTBUFFER](../../t-sql/database-console-commands/dbcc-inputbuffer-transact-sql.md)|[DBCC SHOWCONTIG](../../t-sql/database-console-commands/dbcc-showcontig-transact-sql.md)|  
|[DBCC OPENTRAN](../../t-sql/database-console-commands/dbcc-opentran-transact-sql.md)|[DBCC SQLPERF](../../t-sql/database-console-commands/dbcc-sqlperf-transact-sql.md)|  
|[DBCC OUTPUTBUFFER](../../t-sql/database-console-commands/dbcc-outputbuffer-transact-sql.md)|[DBCC TRACESTATUS](../../t-sql/database-console-commands/dbcc-tracestatus-transact-sql.md)|  
|[DBCC PROCCACHE](../../t-sql/database-console-commands/dbcc-proccache-transact-sql.md)|[DBCC USEROPTIONS](../../t-sql/database-console-commands/dbcc-useroptions-transact-sql.md)|  
|[DBCC SHOW_STATISTICS](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)||  
  
## <a name="validation-statements"></a>验证语句  
  
|||  
|-|-|  
|[DBCC CHECKALLOC](../../t-sql/database-console-commands/dbcc-checkalloc-transact-sql.md)|[DBCC CHECKFILEGROUP](../../t-sql/database-console-commands/dbcc-checkfilegroup-transact-sql.md)|  
|[DBCC CHECKCATALOG](../../t-sql/database-console-commands/dbcc-checkcatalog-transact-sql.md)|[DBCC CHECKIDENT](../../t-sql/database-console-commands/dbcc-checkident-transact-sql.md)|  
|[DBCC CHECKCONSTRAINTS](../../t-sql/database-console-commands/dbcc-checkconstraints-transact-sql.md)|[DBCC CHECKTABLE](../../t-sql/database-console-commands/dbcc-checktable-transact-sql.md)|  
|[DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)||  
  
## <a name="maintenance-statements"></a>维护语句  
  
|||  
|-|-|  
|[DBCC CLEANTABLE](../../t-sql/database-console-commands/dbcc-cleantable-transact-sql.md)|[DBCC INDEXDEFRAG](../../t-sql/database-console-commands/dbcc-indexdefrag-transact-sql.md)|  
|[DBCC DBREINDEX](../../t-sql/database-console-commands/dbcc-dbreindex-transact-sql.md)|[DBCC SHRINKDATABASE](../../t-sql/database-console-commands/dbcc-shrinkdatabase-transact-sql.md)|  
|[DBCC DROPCLEANBUFFERS](../../t-sql/database-console-commands/dbcc-dropcleanbuffers-transact-sql.md)|[DBCC SHRINKFILE](../../t-sql/database-console-commands/dbcc-shrinkfile-transact-sql.md)|  
|[DBCC FREEPROCCACHE](../../t-sql/database-console-commands/dbcc-freeproccache-transact-sql.md)|[DBCC UPDATEUSAGE](../../t-sql/database-console-commands/dbcc-updateusage-transact-sql.md)|  
  
## <a name="miscellaneous-statements"></a>杂项语句  
  
|||  
|-|-|  
|[DBCC dll 名称 （免费）](../../t-sql/database-console-commands/dbcc-dllname-free-transact-sql.md)|[DBCC 帮助](../../t-sql/database-console-commands/dbcc-help-transact-sql.md)|  
|[DBCC FLUSHAUTHCACHE](../../t-sql/database-console-commands/dbcc-flushauthcache-transact-sql.md)|[DBCC TRACEOFF](../../t-sql/database-console-commands/dbcc-traceoff-transact-sql.md)|  
|[DBCC FREESESSIONCACHE](../../t-sql/database-console-commands/dbcc-freesessioncache-transact-sql.md)|[DBCC TRACEON](../../t-sql/database-console-commands/dbcc-traceon-transact-sql.md)|  
|[DBCC FREESYSTEMCACHE](../../t-sql/database-console-commands/dbcc-freesystemcache-transact-sql.md)|[DBCC CLONEDATABASE](https://support.microsoft.com/en-us/kb/3177838) <br /><br /> **适用于**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Service Pack 2。|  
  
  

