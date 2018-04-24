---
title: DBCC SHRINKDATABASE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|database-console-commands
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- DBCC_SHRINKDATABASE_TSQL
- DBCC SHRINKDATABASE
- SHRINKDATABASE_TSQL
- SHRINKDATABASE
dev_langs:
- TSQL
helpviewer_keywords:
- data shrinking [SQL Server]
- shrinking files
- shrinking databases
- DBCC SHRINKDATABASE statement
- decreasing database size
- file shrinking [SQL Server]
- database shrinking [SQL Server]
- logs [SQL Server], shrinking
- reducing database size
ms.assetid: fc976afd-1edb-4341-bf41-c4a42a69772b
caps.latest.revision: 62
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Active
ms.openlocfilehash: 88d4ef4b4af6853320ccf80d9aa5fe67afe28ffa
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="dbcc-shrinkdatabase-transact-sql"></a>DBCC SHRINKDATABASE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

收缩指定数据库中的数据文件和日志文件的大小。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
DBCC SHRINKDATABASE   
( database_name | database_id | 0   
     [ , target_percent ]   
     [ , { NOTRUNCATE | TRUNCATEONLY } ]   
)  
[ WITH NO_INFOMSGS ]  
```  
  
## <a name="arguments"></a>参数  
 database_name | database_id | 0  
 要收缩的数据库的名称或 ID。 如果指定 0，则使用当前数据库。  
  
 *target_percent*  
 数据库收缩后的数据库文件中所需的剩余可用空间百分比。  
  
 NOTRUNCATE  
 通过将已分配的页从文件末尾移动到文件前面的未分配页来压缩数据文件中的数据。 target_percent 为可选。 Azure SQL 数据仓库不支持此选项。 
  
 文件末尾的可用空间不会返回给操作系统，文件的物理大小也不会更改。 因此，指定 NOTRUNCATE 时，数据库看起来未收缩。  
  
 NOTRUNCATE 只适用于数据文件。 日志文件不受影响。  
  
 TRUNCATEONLY  
 将文件末尾的所有可用空间释放给操作系统，但不在文件内部执行任何页移动。 数据文件只收缩到最后分配的区。 如果使用 TRUNCATEONLY 指定，则会忽略 target_percent。 Azure SQL 数据仓库不支持此选项。
  
 TRUNCATEONLY 将影响日志文件。 若要仅截断数据文件，请使用 DBCC SHRINKFILE。  
  
 WITH NO_INFOMSGS  
 取消严重级别从 0 到 10 的所有信息性消息。  
  
## <a name="result-sets"></a>结果集  
下表对结果集中的列进行了说明。
  
|列名|Description|  
|-----------------|-----------------|  
|**DbId**|[!INCLUDE[ssDE](../../includes/ssde-md.md)]试图收缩的文件的数据库标识号。|  
|**FileId**|[!INCLUDE[ssDE](../../includes/ssde-md.md)]尝试收缩的文件的文件标识号。|  
|**CurrentSize**|文件当前占用的 8 KB 页数。|  
|**MinimumSize**|文件最低可以占用的 8 KB 页数。 这与文件的最小大小或最初创建时的大小相对应。|  
|**UsedPages**|文件当前使用的 8 KB 页数。|  
|**EstimatedPages**|[!INCLUDE[ssDE](../../includes/ssde-md.md)]估计文件能够收缩到的 8 KB 页数。|  
  
>[!NOTE]
> [!INCLUDE[ssDE](../../includes/ssde-md.md)]不显示未收缩的文件的行。  
  
## <a name="remarks"></a>Remarks  
若要收缩特定数据库的所有数据和日志文件，请执行 DBCC SHRINKDATABASE 命令。 若要一次收缩一个特定数据库中的一个数据或日志文件，请执行 [DBCC SHRINKFILE](../../t-sql/database-console-commands/dbcc-shrinkfile-transact-sql.md) 命令。
  
若要查看数据库中当前的可用（未分配）空间量，请运行 [sp_spaceused](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md)。
  
可在进程中的任一点停止 DBCC SHRINKDATABASE 操作，任何已完成的工作都将保留。
  
收缩后的数据库不能小于数据库的最小大小。 最小大小是在数据库最初创建时指定的大小，或是使用文件大小更改操作（如 DBCC SHRINKFILE 或 ALTER DATABASE）显式设置的最后大小。 例如，如果数据库最初创建时的大小为 10 MB，后来增长到 100 MB，则该数据库最小只能收缩到 10 MB，即使已经删除数据库的所有数据也是如此。
  
运行 DBCC SHRINKDATABASE 而不指定 NOTRUNCATE 选项或 TRUNCATEONLY 选项等价于带 NOTRUNCATE 运行 DBCC SHRINKDATABASE 操作，然后再带 TRUNCATEONLY 运行 DBCC SHRINKDATABASE 操作。
  
要收缩的数据库不必在单用户模式下；其他的用户仍可以在数据库收缩时对其进行工作。 这也包括系统数据库。
  
不能在备份数据库时收缩数据库。 反之，也不能在数据库执行收缩操作时备份数据库。

>[!NOTE]
> 当前，Azure SQL 数据仓库不支持启用了 TDE 的 DBCC SHRINKDATABASE。
  
## <a name="how-dbcc-shrinkdatabase-works"></a>DBCC SHRINKDATABASE 的工作原理  
DBCC SHRINKDATABASE 以每个文件为单位对数据文件进行收缩。然而，DBCC SHRINKDATABASE 在对日志文件进行收缩时，它将视为所有的日志文件都存在于一个连续的日志池中。 文件始终从末尾开始收缩。
  
假设名为 mydb 的数据库有一个数据文件和两个日志文件。 数据文件和日志文件分别是 10 MB，并且数据文件包含 6 MB 数据。
  
对于每个文件，[!INCLUDE[ssDE](../../includes/ssde-md.md)]都会计算一个目标大小。 这就是文件将要收缩到的大小。 将 target_percent 与 DBCC SHRINKDATABASE 一起指定时，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 计算的目标大小是收缩后文件中的 target_percent 可用空间大小。 例如，如果在收缩 mydb 时将 target_percent 指定为 25，则 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 将此文件的目标大小计算为 8 MB（6 MB 数据加上 2 MB 可用空间）。 因此，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 将任何数据从数据文件的后 2 MB 中移动到数据文件前 8 MB 的可用空间中，然后对该文件进行收缩。
  
假设 mydb 的数据文件包含 7 MB 的数据。 将 target_percent 指定为 30，以允许将此数据文件收缩到可用空间的 30％。 但是，将 target_percent 指定为 40 却不会收缩数据文件，因为 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 收缩文件的目标大小不能小于数据当前占用空间大小。 还可以用另一种方法来考虑此问题：所要求的 40％ 可用空间加上整个数据文件大小的 70％（10 MB 中的 7 MB），超过了 100％。 因为所要求的可用百分比加上数据文件占用的当前百分比大于 100%（多出 10%），所以任何大于 30 的 target_size 都不会收缩此数据文件。
  
对于日志文件，[!INCLUDE[ssDE](../../includes/ssde-md.md)] 使用 target_percent 来计算整个日志的目标大小；因此，target_percent 是收缩操作后日志中的可用空间大小。 之后，整个日志的目标大小转换为每个日志文件的目标大小。
  
DBCC SHRINKDATABASE 尝试立即将每个物理日志文件收缩到其目标大小。 如果虚拟日志中的所有逻辑日志部分都没有超出日志文件的目标大小，则该文件将成功截断，DBCC SHRINKDATABASE 完成且不显示任何消息。 但是，如果部分逻辑日志位于超出目标大小的虚拟日志中，则[!INCLUDE[ssDE](../../includes/ssde-md.md)]将释放尽可能多的空间，并发出一条信息性消息。 该消息说明需要执行哪些操作来将逻辑日志移出位于文件末尾的虚拟日志。 执行该操作以后，DBCC SHRINKDATABASE 可用于释放剩余空间。
  
因为日志文件只能收缩到虚拟日志文件边界，所以可能无法将日志文件收缩到比虚拟日志文件更小（即使现在没有使用该文件）。 虚拟日志文件的大小在创建或扩展这些日志文件时由[!INCLUDE[ssDE](../../includes/ssde-md.md)]动态选择。
  
## <a name="best-practices"></a>最佳实践  
当您计划收缩数据库时，请考虑以下信息：
-   在执行会产生许多未使用空间的操作（如截断表或删除表操作）后，执行收缩操作最有效。  
-   大多数数据库都需要一些可用空间，以供常规日常操作使用。 如果反复收缩数据库并注意到数据库大小变大，则表明收缩的空间是常规操作所必需的。 在这种情况下，反复收缩数据库是一种无谓的操作。  
-   收缩操作不会保留数据库中索引的碎片状态，通常还会在一定程度上增加碎片。 这是不要反复收缩数据库的另一个原因。  
-   除非有特定要求，否则不要将 AUTO_SHRINK 数据库选项设置为 ON。  
  
## <a name="troubleshooting"></a>故障排除  
 在[基于行版本控制的隔离级别](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)下运行的事务可能会阻塞收缩操作。 例如，执行 DBCC SHRINK DATABASE 操作时，如果在基于行版本控制的隔离级别下运行的大型删除操作正在进行中，则收缩操作将等到删除操作完成才会收缩文件。 出现这种情况时，DBCC SHRINKFILE 和 DBCC SHRINKDATABASE 操作会在第一个小时每五分钟将信息性消息（对于 SHRINKDATABASE 为 5202，对于 SHRINKFILE 为 5203）输出到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误日志，之后每一个小时输出一次。 例如，如果错误日志包含以下错误消息：  
  
```sql
DBCC SHRINKDATABASE for database ID 9 is waiting for the snapshot   
transaction with timestamp 15 and other snapshot transactions linked to   
timestamp 15 or with timestamps older than 109 to finish.  
```  
  
这意味着收缩操作被时间戳早于 109 的快照事务阻塞，它是收缩操作所完成的上一事务。 它还说明 [sys.dm_tran_active_snapshot_database_transactions (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-tran-active-snapshot-database-transactions-transact-sql.md) 动态管理视图中的 transaction_sequence_num 或 first_snapshot_sequence_num 列包含值 15。 如果该视图中的 transaction_sequence_num 或 first_snapshot_sequence_num 列包含的数字小于收缩操作完成的上一事务 (109)，则收缩操作将等待这些事务完成。
  
若要解决此问题，请执行下列任务之一：
-   终止阻塞收缩操作的事务。  
-   终止收缩操作。 将保留任何已完成的工作。  
-   不执行任何操作，并允许收缩操作等到阻塞事务完成。  
  
## <a name="permissions"></a>权限  
 要求具有 **sysadmin** 固定服务器角色或 **db_owner** 固定数据库角色的成员身份。  
  
## <a name="examples"></a>示例  
  
### <a name="a-shrinking-a-database-and-specifying-a-percentage-of-free-space"></a>A. 收缩数据库并指定可用空间的百分比  
 以下示例将减小 `UserDB` 用户数据库中数据文件和日志文件的大小，以便在数据库中留出 10% 的可用空间。  
  
```sql  
DBCC SHRINKDATABASE (UserDB, 10);  
GO  
```  
  
### <a name="b-truncating-a-database"></a>B. 截断数据库  
 以下示例使 `AdventureWorks` 示例数据库中的数据和日志文件收缩到最后分配的区。  
  
```sql  
DBCC SHRINKDATABASE (AdventureWorks2012, TRUNCATEONLY);  
```  
  
## <a name="see-also"></a>另请参阅  
[ALTER DATABASE (Transact-SQL)](../../t-sql/statements/alter-database-transact-sql.md)  
[DBCC (Transact-SQL)](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[DBCC SHRINKFILE (Transact-SQL)](../../t-sql/database-console-commands/dbcc-shrinkfile-transact-sql.md)  
[收缩数据库](../../relational-databases/databases/shrink-a-database.md)
  
  
