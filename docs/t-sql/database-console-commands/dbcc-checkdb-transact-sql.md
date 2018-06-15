---
title: DBCC CHECKDB (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 12/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- CHECKDB_TSQL
- DBCC_CHECKDB_TSQL
- DBCC CHECKDB
- CHECKDB
dev_langs:
- TSQL
helpviewer_keywords:
- CHECKDB [DBCC statement]
- database objects [SQL Server], checking
- counting pages
- per-index row counts
- per-table row counts
- DBCC CHECKDB statement
- per-table page counts
- allocation checks
- integrity [SQL Server], database objects
- per-index page counts
- counting rows
- table integrity checks [SQL Server]
- row count accuracy [SQL Server]
- negative counts
- checking database objects
- page count accuracy [SQL Server]
ms.assetid: 2c506167-0b69-49f7-9282-241e411910df
caps.latest.revision: 144
author: uc-msft
ms.author: umajay
manager: craigg
ms.openlocfilehash: 7f270fd58e58b7e6c850a520dff4cd37e2ddb4ec
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
ms.locfileid: "33262940"
---
# <a name="dbcc-checkdb-transact-sql"></a>DBCC CHECKDB (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

通过执行下列操作检查指定数据库中所有对象的逻辑和物理完整性：    
    
-   对数据库运行 [DBCC CHECKALLOC](../../t-sql/database-console-commands/dbcc-checkalloc-transact-sql.md)。    
-   对数据库中的每个表和视图运行 [DBCC CHECKTABLE](../../t-sql/database-console-commands/dbcc-checktable-transact-sql.md)。    
-   对数据库运行 [DBCC CHECKCATALOG](../../t-sql/database-console-commands/dbcc-checkcatalog-transact-sql.md)。    
-   验证数据库中每个索引视图的内容。    
-   使用 FILESTREAM 在文件系统中存储 varbinary(max) 数据时，验证表元数据和文件系统目录和文件之间的链接级一致性。    
-   验证数据库中的 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 数据。    
    
这意味着不必从 DBCC CHECKDB 单独运行 DBCC CHECKALLOC、DBCC CHECKTABLE 或 DBCC CHECKCATALOG 命令。 有关这些命令执行的检查的详细信息，请参阅这些命令的说明。    
 
> [!NOTE]
> DBCC CHECKDB 在包含内存优化表的数据库上受支持，但验证仅在基于磁盘的表上发生。 但是，作为数据库备份和恢复的一部分，将对内存优化文件组中的文件完成 CHECKSUM 验证。    
>     
> 由于 DBCC 修复选项不可用于内存优化表，您必须定期备份数据库并测试备份。 如果内存优化表中出现数据完整性问题，必须从上次已知的正确备份中还原。    

![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)    
    
## <a name="syntax"></a>语法    
    
```    
DBCC CHECKDB     
    [ ( database_name | database_id | 0    
        [ , NOINDEX     
        | , { REPAIR_ALLOW_DATA_LOSS | REPAIR_FAST | REPAIR_REBUILD } ]    
    ) ]    
    [ WITH     
        {    
            [ ALL_ERRORMSGS ]    
            [ , EXTENDED_LOGICAL_CHECKS ]     
            [ , NO_INFOMSGS ]    
            [ , TABLOCK ]    
            [ , ESTIMATEONLY ]    
            [ , { PHYSICAL_ONLY | DATA_PURITY } ]    
            [ , MAXDOP  = number_of_processors ]    
        }    
    ]    
]    
```    
    
## <a name="arguments"></a>参数    
 database_name | database_id | 0  
 要为其运行完整性检查的数据库的名称或 ID。 如果未指定，或者指定为 0，则使用当前数据库。 数据库名称必须符合[标识符](../../relational-databases/databases/database-identifiers.md)规则。  
    
NOINDEX  
 指定不应对用户表的非聚集索引执行会占用很大系统开销的检查。 这将减少总执行时间。 NOINDEX 不影响系统表，因为总是对系统表索引执行完整性检查。  
    
REPAIR_ALLOW_DATA_LOSS | REPAIR_FAST | REPAIR_REBUILD  
 指定 DBCC CHECKDB 修复发现的错误。 仅将 REPAIR 选项作为最后手段使用。 指定的数据库必须处于单用户模式，才能使用以下修复选项之一。  
    
REPAIR_ALLOW_DATA_LOSS  
 尝试修复报告的所有错误。 这些修复可能会导致一些数据丢失。  
    
> [!WARNING]
> REPAIR_ALLOW_DATA_LOSS 选项是受支持的功能，但是，它可能并非总是使数据库处于物理上一致的状态的最佳选项。 如果成功，REPAIR_ALLOW_DATA_LOSS 选项可能会导致一些数据丢失。 实际上，它可能导致的数据丢失多于用户从上次已知成功备份还原数据库导致的数据丢失。 
>
> [!INCLUDE[msCoName](../../includes/msconame-md.md)] 始终建议用户将从上次已知成功备份还原作为从由 DBCC CHECKDB 报告的错误恢复的主要方法。 REPAIR_ALLOW_DATA_LOSS 选项不是从已知成功备份还原的替代方法。 这是一个紧急选项，仅当不可从备份恢复时建议作为“最后手段”使用。    
>     
> 仅能使用 REPAIR_ALLOW_DATA_LOSS 选项修复的某些错误可能涉及释放行、页或一些列页以清除错误。 用户不可再访问或恢复已释放的数据，且无法确定已释放数据的准确内容。 因此，释放任何行或页后参照完整性可能不准确，因为此修复操作不包括检查或维护外键约束。 使用 REPAIR_ALLOW_DATA_LOSS 选项后，用户必须检查其数据库的参考完整性（使用 DBCC CHECKCONSTRAINTS）。    
>     
> 在执行修复之前，请创建属于此数据库的文件的物理副本。 这包括主数据文件 (.mdf)、任意辅助数据文件 (.ndf)、所有事务日志文件 (.ldf) 和构成数据库的其他容器，包括全文目录、文件流文件夹、内存优化数据等。    
>     
> 在执行修复前，请考虑将数据库的状态更改为紧急模式，并尝试从关键表中提取尽可能多的信息并保存这些数据。    
    
REPAIR_FAST  
 保留该语法只是为了向后兼容。 未执行修复操作。  
    
REPAIR_REBUILD  
 执行不会丢失数据的修复。 这包括快速修复（如修复非聚集索引中缺少的行）以及更耗时的修复（如重新生成索引）。  
 此参数不修复涉及 FILESTREAM 数据的错误。  
    
> [!IMPORTANT] 
> 由于具有 REPAIR 选项的 DBCC CHECKDB 被完全记录且可恢复，[!INCLUDE[msCoName](../../includes/msconame-md.md)] 始终建议用户在事务中使用具有 REPAIR 选项的 CHECKDB（运行命令前执行 BEGIN TRANSACTION），这样用户可确认其是否愿意接受操作的结果。 然后用户可执行 COMMIT TRANSACTION 来提交修复操作完成的所有工作。 如果用户不想接受操作的结果，他/她可执行 ROLLBACK TRANSACTION 以撤消修复操作的影响。    
>     
> 若要修复错误，建议您通过备份进行还原。 修复操作不会考虑表本身或表之间可能存在的任何约束。 如果指定的表与一个或多个约束有关，建议您在修复操作后运行 DBCC CHECKCONSTRAINTS。 如果必须使用 REPAIR，则运行不带有修复选项的 DBCC CHECKDB 来查找要使用的修复级别。 如果使用 REPAIR_ALLOW_DATA_LOSS 级别，则建议您在运行带有此选项的 DBCC CHECKDB 之前备份数据库。    
    
ALL_ERRORMSGS  
 显示针对每个对象报告的所有错误。 默认情况下显示所有错误消息。 指定或省略此选项都不起作用。 按对象 ID 对错误消息排序，从 [tempdb 数据库](../../relational-databases/databases/tempdb-database.md)生成的那些消息除外。     

EXTENDED_LOGICAL_CHECKS  
 如果兼容性级别为 100 ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]) 或更高，则对索引视图、XML 索引和空间索引（如果存在）执行逻辑一致性检查。  
 有关详细信息，请参阅本主题后面[备注](#remarks)部分中的“对索引执行逻辑一致性检查”。  
    
NO_INFOMSGS  
 取消显示所有信息性消息。  
    
TABLOCK  
 使 DBCC CHECKDB 获取锁，而不使用内部数据库快照。 这包括一个短期数据库排他 (X) 锁。 TABLOCK 可使 DBCC CHECKDB 在负荷较重的数据库上运行得更快，但 DBCC CHECKDB 运行时会减少数据库上可获得的并发性。  
    
> [!IMPORTANT] 
> TABLOCK 限制执行的检查；DBCC CHECKCATALOG 未对数据库运行并且 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 数据未进行验证。
    
ESTIMATEONLY  
 显示运行包含所有其他指定选项的 DBCC CHECKDB 时所需的 tempdb 空间估计量。 不执行实际数据库检查。  
    
PHYSICAL_ONLY  
 将检查限制为页和记录标头的物理结构完整性以及数据库的分配一致性。 设计该检查是为了以较小的开销检查数据库的物理一致性，但它还可以检测会危及用户数据安全的残缺页、校验和错误以及常见的硬件故障。  
 DBCC CHECKDB 完成运行所需的时间可能比早期版本要长得多。 出现此现象的原因是：  
 -   逻辑检查更加全面。  
 -   要检查的某些基础结构更为复杂。  
 -   引入了许多新的检查以包含新增功能。  
 因此，使用 PHYSICAL_ONLY 选项可能会大幅减少对较大数据库运行 DBCC CHECKDB 所需的时间，所以对需要频繁检查的生产系统，建议使用此选项。 我们仍然建议完整地定期执行 DBCC CHECKDB。 这些运行的执行频率取决于各业务和生产环境特定的因素。    
此参数始终表示 NO_INFOMSGS，不能与任何一个修复选项一同使用。  
    
> [!WARNING] 
> 指定 PHYSICAL_ONLY 会使 DBCC CHECKDB 跳过对 FILESTREAM 数据的所有检查。
    
DATA_PURITY  
 使 DBCC CHECKDB 检查数据库中是否存在无效或越界的列值。 例如，DBCC CHECKDB 检测日期和时间值大于或小于 datetime 数据类型的可接受范围的列，或者小数位数或精度值无效的 decimal 或近似 numeric 数据类型列。  
 默认情况下将启用列值完整性检查，并且不需要使用 DATA_PURITY 选项。 对于从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的早期版本升级的数据库，默认情况下不启用列值检查，直到 DBCC CHECKDB WITH DATA_PURITY 已在数据库中正确运行为止。 然后，DBCC CHECKDB 将默认检查列值完整性。 有关从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的早期版本升级数据库会对 CHECKDB 有何影响的详细信息，请参阅本主题的“备注”部分。  
    
> [!WARNING]
> 如果指定了 PHYSICAL_ONLY，则不执行列完整性检查。
    
 无法使用 DBCC 修复选项来纠正该选项所报告的验证错误。 有关手动更正这些错误的信息，请参阅知识库文章 923247：[解决 SQL Server 2005 和更高版本中的 DBCC 错误 2570](http://support.microsoft.com/kb/923247)。  
    
 MAXDOP  
 适用范围：[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]（[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] SP2 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]）。  
    
 对于语句，替代 sp_configure 的“max degree of parallelism”配置选项。 MAXDOP 可以超出使用 sp_configure 配置的值。 如果 MAXDOP 超出使用资源调控器配置的值，则 [!INCLUDE[ssDEnoversion](../../includes/ssDEnoversion_md.md)] 会使用资源调控器 MAXDOP 值（如 [ALTER WORKLOAD GROUP](../../t-sql/statements/alter-workload-group-transact-sql.md) 中所述）。 当使用 MAXDOP 查询提示时，所有和 max degree of parallelism 配置选项一起使用的语义规则均适用。 有关详细信息，请参阅 [Configure the max degree of parallelism Server Configuration Option](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)。  
 
> [!WARNING] 
> 如果 MAXDOP 设置为零，则 SQL Server 需选择要使用的最大并行度。    

## <a name="remarks"></a>Remarks    
DBCC CHECKDB 不检查禁用的索引。 有关禁用的索引的详细信息，请参阅[禁用索引和约束](../../relational-databases/indexes/disable-indexes-and-constraints.md)。    

如果用户定义类型标记为按字节排序，则该用户定义类型必须只有一个序列化。 在 DBCC CHECKDB 运行期间，如果按字节排序的用户定义类型没有一致的序列化，则会导致错误 2537。 有关详细信息，请参阅[用户定义类型的要求](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types-requirements.md)。    

由于只能以单用户模式修改[资源数据库](../../relational-databases/databases/resource-database.md)，因此不能直接对其运行 DBCC CHECKDB 命令。 但是，当对 [master 数据库](../../relational-databases/databases/master-database.md)执行 DBCC CHECKDB 时，也在内部对资源数据库运行另一个 CHECKDB。 这意味着 DBCC CHECKDB 可能会返回额外的结果。 如果未设置任何选项，或者设置了 PHYSICAL_ONLY 或 ESTIMATEONLY 选项，则命令返回额外的结果集。    

从 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP2 开始，执行 DBCC CHECKDB 不再清除 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的计划缓存。 在 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] SP2 以前，执行 DBCC CHECKDB 会清除计划缓存。 清除计划缓存将导致对所有后续执行计划进行重新编译，并可能会导致查询性能暂时性地突然降低。 
    
## <a name="performing-logical-consistency-checks-on-indexes"></a>对索引执行逻辑一致性检查    
对索引进行的逻辑一致性检查因数据库兼容级别而异，如下所示：
-   如果兼容性级别为 100 ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]) 或更高：    
-   除非指定 NOINDEX，否则 DBCC CHECKDB 对单个表及其所有非聚集索引同时执行物理和逻辑一致性检查。 但是，在默认情况下，仅对 XML 索引、空间索引和索引视图执行物理一致性检查。
-   如果指定了 WITH EXTENDED_LOGICAL_CHECKS，则将对索引视图、XML 索引和空间索引（如果存在）执行逻辑检查。 默认情况下，先执行物理一致性检查，然后执行逻辑一致性检查。 如果还指定了 NOINDEX，则仅执行逻辑检查。
    
这些逻辑一致性检查可对索引对象的内部索引表及其引用的用户表进行交叉检查。 为了查找外部行，将构造内部查询来对内部表和用户表的完整交集执行查询。 运行此查询可能会对性能产生很大影响，并且无法跟踪其进度。 因此，建议您仅在以下情况下才指定 WITH EXTENDED_LOGICAL_CHECKS：怀疑存在与物理损坏无关的索引问题，或者已关闭页级校验并且怀疑存在列级硬件损坏。
-   如果索引为筛选索引，DBCC CHECKDB 将执行一致性检查以验证索引项是否满足筛选谓词的要求。
-   如果兼容级别为 90 或更低，则除非指定 NOINDEX，否则 DBCC CHECKDB 将对单个表或索引视图及其所有非聚集索引和 XML 索引同时执行物理和逻辑一致性检查。 不支持空间索引。  
- 从 SQL Server 2016 开始，不再默认对持久化计算列、UDT 列和筛选索引运行其他检查，以避免昂贵的表达式计算。 此更改显著减少了针对包含这些对象的数据库的 CHECKDB 持续时间。 但是，始终会完成这些对象的物理一致性检查。 仅当指定了 EXTENDED_LOGICAL_CHECKS 选项时，才会在 EXTENDED_LOGICAL_CHECKS 选项中已包含的逻辑检查（索引视图、XML 索引和空间索引）之外，执行表达式计算。   
    
**了解数据库的兼容性级别**
-   [查看或更改数据库的兼容级别](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md)    
    
## <a name="internal-database-snapshot"></a>内部数据库快照    
对于执行这些检查所需要的事务一致性，DBCC CHECKDB 使用内部数据库快照。 这样可以防止在执行这些命令时出现阻塞和并发问题。 有关详细信息，请参阅[查看数据库快照的稀疏文件大小 (Transact-SQL)](../../relational-databases/databases/view-the-size-of-the-sparse-file-of-a-database-snapshot-transact-sql.md) 以及 [DBCC (Transact-SQL)](../../t-sql/database-console-commands/dbcc-transact-sql.md) 中的“DBCC 内部数据库快照使用情况”部分。 如果无法创建快照或指定了 TABLOCK，DBCC CHECKDB 将获取锁以获得所需一致性。 在这种情况下，需要排他数据库锁才能执行分配检查，需要共享表锁才能执行表检查。
如果无法创建内部数据库快照，则对 master 运行 DBCC CHECKDB 时会失败。
对 tempdb 运行 DBCC CHECKDB 不会执行任何分配或目录检查，并且必须获取共享表锁才能执行表检查。 这是因为，为了提高性能，不允许对 tempdb 使用数据库快照。 这意味着，无法获得所需的事务一致性。
在 Microsoft SQL Server 2012 或更早版本中，针对有文件位于 ReFS 格式化卷上的数据库运行 DBCC CHECKDB 命令时，可能会遇到错误消息。 有关详细信息，请参阅知识库文章 2974455：[SQL Server 数据库位于 ReFS 卷上时的 DBCC CHECKDB 行为](https://support.microsoft.com/kb/2974455)    
    
## <a name="checking-and-repairing-filestream-data"></a>检查和修复 FILESTREAM 数据    
对数据库和表启用 FILESTREAM 后，便可选择将 varbinary(max) 二进制大型对象 (BLOB) 存储在文件系统中。 对在文件系统中存储 BLOB 的数据库使用 DBCC CHECKDB 时，DBCC 将检查文件系统和数据库之间的链接级一致性。
例如，如果表包含使用 FILESTREAM 属性的 varbinary(max) 列，则 DBCC CHECKDB 会检查文件系统目录和文件与表行、表列和列值之间是否存在一对一映射。 如果指定 REPAIR_ALLOW_DATA_LOSS 选项，DBCC CHECKDB 便可修复损坏。 为修复 FILESTREAM 损坏，DBCC 将删除缺少文件系统数据的任何表行。
    
## <a name="best-practices"></a>最佳实践    
建议您使用 PHYSICAL_ONLY 选项，以便可以频繁检查生产系统。 使用 PHYSICAL_ONLY 可以极大地缩短对大型数据库运行 DBCC CHECKDB 的运行时间。 同时建议您定期运行没有选项的 DBCC CHECKDB。 应当以什么频率执行这些运行任务将取决于各个企业及其生产环境。
    
## <a name="checking-objects-in-parallel"></a>并行检查对象    
默认情况下，DBCC CHECKDB 对对象执行并行检查。 并行度由查询处理器自动确定。 最大并行度的配置与配置并行查询相同。 若要限制 DBCC 检查可使用的处理器的最大数目，请使用 [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)。 有关详细信息，请参阅 [Configure the max degree of parallelism Server Configuration Option](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)。 通过使用跟踪标志 2528 可以禁用并行检查。 有关详细信息，请参阅[跟踪标志 (Transact-SQL)](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)。
    
> [!NOTE]
> 并非在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的每个版本中均提供此功能。 有关详细信息，请参阅 [SQL Server 2016 的各版本支持的功能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)的“RDBMS 可管理性”部分中的并行一致性检查。    
    
## <a name="understanding-dbcc-error-messages"></a>了解 DBCC 错误消息    
DBCC CHECKDB 命令结束之后，便会将一个消息写入 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 错误日志。 如果 DBCC 命令成功执行，则消息指示成功以及命令的运行时间。 如果 DBCC 命令在完成检查之前由于错误而停止，则消息将指示命令已终止，并指示状态值和命令运行的时间。 下表列出并说明了此消息中可包含的状态值。
    
|State|Description|    
|-----------|-----------------|    
|0|出现错误号 8930。 这表示元数据中存在的损坏终止了 DBCC 命令。|    
|@shouldalert|出现错误号 8967。 存在一个内部 DBCC 错误。|    
|2|在紧急模式数据库修复过程中出错。|    
|3|这表示元数据中存在的损坏终止了 DBCC 命令。|    
|4|检测到断定或访问违规。|    
|5|出现终止了 DBCC 命令的未知错误。|    
    
## <a name="error-reporting"></a>错误报告    
一旦 DBCC CHECKDB 检测到损坏错误，便会在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] LOG 目录中创建转储文件 (`SQLDUMP*nnnn*.txt`)。 如果为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例启用了“功能使用情况数据收集”和“错误报告”功能，该文件将被自动转发给 [!INCLUDE[msCoName](../../includes/msconame-md.md)]。 收集的数据将用于改进 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 功能。
转储文件包含 DBCC CHECKDB 命令的结果以及其他诊断输出数据。 只有 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务帐户和 sysadmin 角色的成员有权进行访问。 默认情况下，sysadmin 角色包含 Windows `BUILTIN\Administrators` 组和本地管理员组的所有成员。 如果数据收集进程失败，DBCC 命令不会失败。
    
## <a name="resolving-errors"></a>纠正错误    
如果 DBCC CHECKDB 报告了任何错误，建议从数据库备份还原数据库，而不运行具有一个 REPAIR 选项的 REPAIR。 如果不存在备份，则运行修复将更正报告的错误。 要使用的修复选项在报告的错误的末尾处指定。 但是，通过使用 REPAIR_ALLOW_DATA_LOSS 选项来更正错误可能需要删除某些页，因此会删除某些数据。    

在某些情况下，可能会在数据库中输入对列的数据类型而言无效或越界的值。 DBCC CHECKDB 可以检测到对所有列数据类型均无效的列值。 因此，对从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的早期版本升级的数据库运行带 DATA_PURITY 选项的 DBCC CHECKDB 可能会显示预先存在的列值错误。 因为 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 不会自动修复这些错误，所以必须手动更新这些列值。 如果 CHECKDB 检测到此类错误，CHECKDB 将返回一个警告、错误号 2570 以及标识受影响的行和手动更正错误的信息。    

修复操作可以在用户事务下执行，以使用户回滚已做的更改。 如果回滚修复，数据库仍会包含错误，因而必须通过备份进行还原。 修复完成后，备份数据库。
    
## <a name="resolving-errors-in-database-emergency-mode"></a>在数据库紧急模式下纠正错误    
如果已通过使用 [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) 语句将数据库设置为紧急模式，那么，假如指定了 REPAIR_ALLOW_DATA_LOSS 选项，则 DBCC CHECKDB 可以对数据库执行某些特殊修复。 这些修复可能允许那些在普通情况下无法恢复的数据库在物理一致状态下重新联机。 这些修复应当是最后手段，并且只有在无法从备份还原数据库时才采用。 如果将数据库设置为紧急模式，则该数据库将标记为 READ_ONLY 并禁用日志记录，而且只有 sysadmin 固定服务器角色的成员才能访问它。
    
> [!NOTE]
> 不能在紧急模式下在用户事务内部运行 DBCC CHECKDB 命令并在执行之后回滚事务。    
    
数据库处于紧急模式并且以 REPAIR_ALLOW_DATA_LOSS 子句运行 DBCC CHECKDB 时，将执行以下操作：
-   DBCC CHECKDB 将使用由于 I/O 或校验和错误而标记为不可访问的页，就如同这些错误没有出现过一样。 这样操作将增加从数据库恢复数据的机会。    
-   DBCC CHECKDB 将尝试使用常规的基于日志的恢复方法恢复数据库。    
-   如果由于事务日志损坏而导致数据库恢复失败，则将重新生成事务日志。 重新生成事务日志可能导致事务一致性丢失。    
    
> [!WARNING]
> REPAIR_ALLOW_DATA_LOSS 选项是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支持的功能。 但是，其可能并非总是使数据库处于物理上一致的状态的最佳选项。 如果成功，REPAIR_ALLOW_DATA_LOSS 选项可能会导致一些数据丢失。 实际上，它可能导致的数据丢失多于用户从上次已知成功备份还原数据库导致的数据丢失。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 始终建议用户将从上次已知成功备份还原作为从由 DBCC CHECKDB 报告的错误恢复的主要方法。 REPAIR_ALLOW_DATA_LOSS 选项不是从已知成功备份还原的替代方法。 这是一个紧急选项，仅当不可从备份恢复时建议作为“最后手段”使用。    
>     
>  重新生成日志后，没有完全的 ACID 保证。    
>     
>  重新生成日志后，将自动执行 DBCC CHECKDB，其将报告并修正物理一致性问题。    
>     
>  必须手动验证逻辑数据一致性和业务逻辑实施的约束。    
>     
>  事务日志大小将保留为其默认大小，必须手动将其调整回其最近大小。    
    
如果 DBCC CHECKDB 命令成功，则数据库将在物理上是一致的，并且数据库状态将设置为 ONLINE。 但是，数据库可能包含一种或多种事务不一致的情况。 我们建议运行 [DBCC CHECKCONSTRAINTS](../../t-sql/database-console-commands/dbcc-checkconstraints-transact-sql.md) 来标识任何业务逻辑缺陷，并立即备份数据库。
如果 DBCC CHECKDB 命令失败，则无法修复数据库。
    
## <a name="running-dbcc-checkdb-with-repairallowdataloss-in-replicated-databases"></a>在复制的数据库中运行具有 REPAIR_ALLOW_DATA_LOSS 的 DBCC CHECKDB    
运行具有 REPAIR_ALLOW_DATA_LOSS 选项的 DBCC CHECKDB 命令可能会影响用户数据库（发布数据库和订阅数据库）以及由复制使用的分发数据库。 发布数据库和订阅数据库包括已发布的表和复制元数据表。 请注意这些数据库中的下列潜在问题：
-   已发布的表。 可能不会复制由 CHECKDB 进程为修复损坏的用户数据而执行的操作：    
-   合并复制使用触发器跟踪对已发布的表所做的更改。 如果 CHECKDB 进程插入、更新或删除了行，则触发器不会激发；因此，更改将不会复制。
-   事务复制使用事务日志跟踪对已发布的表所做的更改。 然后，日志读取器代理将这些更改移动到分发数据库。 某些 DBCC 修复即使记入日志，仍然无法由日志读取器代理复制。 例如，如果数据页由 CHECKDB 进程释放，则日志读取器代理不会将它翻译为 DELETE 语句；因此，更改将不会复制。
-   复制元数据表。 由 CHECKDB 进程为修复损坏的复制元数据表而执行的操作需要删除并重新配置复制。    
    
如果必须对用户数据库或分发数据库运行具有 REPAIR_ALLOW_DATA_LOSS 选项的 DBCC CHECKDB 命令：
1.  停止系统：停止数据库和复制拓扑中所有其他数据库的活动，然后尝试同步所有节点。 有关详细信息，请参阅[停止复制拓扑（复制 Transact-SQL 编程）](../../relational-databases/replication/administration/quiesce-a-replication-topology-replication-transact-sql-programming.md)。    
1.  执行 DBCC CHECKDB。    
1.  如果 DBCC CHECKDB 报表包括分发数据库中任何表或用户数据库中任何复制元数据表的修复，则请删除并重新配置复制。 有关详细信息，请参阅[禁用发布和分发](../../relational-databases/replication/disable-publishing-and-distribution.md)。    
1.  如果 DBCC CHECKDB 报表包括任何已复制表的修复，则请执行数据验证以确定发布数据库和订阅数据库中的数据之间是否存在差异。    
    
## <a name="result-sets"></a>结果集    
DBCC CHECKDB 返回以下结果集。 这些值可能有所不同，除非指定 ESTIMATEONLY、PHYSICAL_ONLY 或 NO_INFOMSGS 选项：
    
```
 DBCC results for 'model'.    
    
 Service Broker Msg 9675, Level 10, State 1: Message Types analyzed: 13.    
    
 Service Broker Msg 9676, Level 10, State 1: Service Contracts analyzed: 5.    
    
 Service Broker Msg 9667, Level 10, State 1: Services analyzed: 3.    
    
 Service Broker Msg 9668, Level 10, State 1: Service Queues analyzed: 3.    
    
 Service Broker Msg 9669, Level 10, State 1: Conversation Endpoints analyzed: 0.    
    
 Service Broker Msg 9674, Level 10, State 1: Conversation Groups analyzed: 0.    
    
 Service Broker Msg 9670, Level 10, State 1: Remote Service Bindings analyzed: 0.    
    
 DBCC results for 'sys.sysrowsetcolumns'.    
    
 There are 630 rows in 7 pages for object 'sys.sysrowsetcolumns'.    
    
 DBCC results for 'sys.sysrowsets'.    
    
 There are 97 rows in 1 pages for object 'sys.sysrowsets'.    
    
 DBCC results for 'sysallocunits'.    
    
 There are 195 rows in 3 pages for object 'sysallocunits'.    
    
 There are 0 rows in 0 pages for object "sys.sysasymkeys".    
    
 DBCC results for 'sys.syssqlguides'.    
    
 There are 0 rows in 0 pages for object "sys.syssqlguides".    
    
 DBCC results for 'sys.queue_messages_1977058079'.    
    
 There are 0 rows in 0 pages for object "sys.queue_messages_1977058079".    
    
 DBCC results for 'sys.queue_messages_2009058193'.    
    
 There are 0 rows in 0 pages for object "sys.queue_messages_2009058193".    
    
 DBCC results for 'sys.queue_messages_2041058307'.    
    
 There are 0 rows in 0 pages for object "sys.queue_messages_2041058307".    
    
 CHECKDB found 0 allocation errors and 0 consistency errors in database 'model'.    
    
 DBCC execution completed. If DBCC printed error messages, contact your system administrator.    
```

指定 NO_INFOMSGS 时，DBCC CHECKDB 返回以下结果集（消息）：
    
```
 The command(s) completed successfully.
 ```
 
指定 PHYSICAL_ONLY 时，DBCC CHECKDB 返回以下结果集：
    
```
 DBCC results for 'model'.    
    
 CHECKDB found 0 allocation errors and 0 consistency errors in database 'master'.  
    
 DBCC execution completed. If DBCC printed error messages, contact your system administrator.
 ```
 
指定 ESTIMATEONLY 时，DBCC CHECKDB 返回以下结果集。
    
```
 Estimated TEMPDB space needed for CHECKALLOC (KB)    
    
 -------------------------------------------------  
    
 13   
    
 (1 row(s) affected)   
    
 Estimated TEMPDB space needed for CHECKTABLES (KB)    
    
 --------------------------------------------------    
    
 57 
    
 (1 row(s) affected)  
    
 DBCC execution completed. If DBCC printed error messages, contact your system administrator.
```
    
## <a name="permissions"></a>权限    
要求具有 sysadmin 固定服务器角色或 db_owner 固定数据库角色的成员身份。
    
## <a name="examples"></a>示例    
    
### <a name="a-checking-both-the-current-and-another-database"></a>A. 检查当前数据库和其他数据库    
下面的示例将对当前数据库和 `DBCC CHECKDB` 数据库执行 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]。
    
```sql    
-- Check the current database.    
DBCC CHECKDB;    
GO    
-- Check the AdventureWorks2012 database without nonclustered indexes.    
DBCC CHECKDB (AdventureWorks2012, NOINDEX);    
GO    
```    
    
### <a name="b-checking-the-current-database-suppressing-informational-messages"></a>B. 检查当前数据库，取消信息性消息    
以下示例检查当前数据库，并取消所有信息性消息。
    
```sql    
DBCC CHECKDB WITH NO_INFOMSGS;    
GO    
```    
    
## <a name="see-also"></a>另请参阅    
[DBCC (Transact-SQL)](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[查看数据库快照的稀疏文件大小 (Transact-SQL)](../../relational-databases/databases/view-the-size-of-the-sparse-file-of-a-database-snapshot-transact-sql.md)  
[sp_helpdb (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-helpdb-transact-sql.md)  
[系统表 (Transact-SQL)](../../relational-databases/system-tables/system-tables-transact-sql.md)  

