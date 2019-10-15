---
title: sp_lock （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_lock_TSQL
- sp_lock
dev_langs:
- TSQL
helpviewer_keywords:
- sp_lock
ms.assetid: 9eaa0ec2-2ad9-457c-ae48-8da92a03dcb0
author: stevestein
ms.author: sstein
ms.openlocfilehash: c31148d09621caf9fd2ebc83a9b629f320418995
ms.sourcegitcommit: 43c3d8939f6f7b0ddc493d8e7a643eb7db634535
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/14/2019
ms.locfileid: "72305127"
---
# <a name="sp_lock-transact-sql"></a>sp_lock (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  报告有关锁的信息。  
  
> [!IMPORTANT]  
> [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] 若要获取有关 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 中的锁的信息，请使用[_tran_locks](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md)动态管理视图。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
sp_lock [ [ @spid1 = ] 'session ID1' ] [ , [@spid2 = ] 'session ID2' ]  
[ ; ]  
```  
  
## <a name="arguments"></a>参数  
@no__t 是用户要锁定信息的**sys.databases _exec_sessions**中的 @no__t 1 会话 ID 号。 *SESSION ID1*的值为**int** ，默认值为 NULL。 执行**sp_who**以获取有关会话的进程信息。 如果未指定*SESSION ID1* ，则显示有关所有锁的信息。  
  
`[ @spid2 = ] 'session ID2'` 是 ID1 **_exec_sessions**中的另一个 @no__t 的会话 ID 号，该 ID 可能与*会话*同时具有锁，并且用户还需要信息。 *SESSION ID2*的值为**int** ，默认值为 NULL。  
  
## <a name="return-code-values"></a>返回代码值  
 0（成功）  
  
## <a name="result-sets"></a>结果集  
 **Sp_lock**结果集对于由 **\@spid1**和 **@no__t 4spid2**参数中指定的会话所持有的每个锁，都包含一行。 如果既没有指定 **\@spid1** @no__t 也没有指定**3spid2** ，则结果集会报告 @no__t 的实例中当前处于活动状态的所有会话的锁。  
  
|列名|数据类型|描述|  
|-----------------|---------------|-----------------|  
|**spid**|**smallint**|请求锁的进程的[!INCLUDE[ssDE](../../includes/ssde-md.md)]会话 ID 号。|  
|**dbid**|**smallint**|保留锁的数据库的标识号。 可以使用 DB_NAME() 函数来标识数据库。|  
|**ObjId**|**int**|持有锁的对象的标识号。 可以在相关数据库中使用 OBJECT_NAME() 函数来标识对象。 值为 99 时是一种特殊情况，表示用于记录数据库中页分配的其中一个系统页的锁。|  
|**IndId**|**smallint**|持有锁的索引的标识号。|  
|类型|**nchar(4)**|锁的类型：<br /><br /> RID = 表中单个行的锁，由行标识符 (RID) 标识。<br /><br /> KEY = 索引内保护可串行事务中一系列键的锁。<br /><br /> PAG = 数据页或索引页的锁。<br /><br /> EXT = 对某区的锁。<br /><br /> TAB = 整个表（包括所有数据和索引）的锁。<br /><br /> DB = 数据库的锁。<br /><br /> FIL = 数据库文件的锁。<br /><br /> APP = 指定的应用程序资源的锁。<br /><br /> MD = 元数据或目录信息的锁。<br /><br /> HBT = 堆或 B 树（HoBT）上的锁。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中此信息不完整。<br /><br /> AU = 分配单元的锁。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中此信息不完整。|  
|**资源**|**nchar(32)**|标识被锁定资源的值。 值的格式取决于在 "**类型**" 列中标识的资源类型：<br /><br /> **类型**负值**资源**负值<br /><br /> 去掉格式为 fileid： pagenumber： rid 的标识符，其中 fileid 标识包含页的文件，pagenumber 标识包含该行的页，rid 标识该页上的特定行。 fileid 匹配**database_files**目录视图中的**file_id**列。<br /><br /> 按键@No__t 在内部使用的十六进制数。<br /><br /> PAG格式为 fileid： pagenumber 的数字，其中 fileid 标识包含该页的文件，pagenumber 标识该页。<br /><br /> 宋体一个数字，用于标识范围中的第一页。 该数字的格式为 fileid:pagenumber。<br /><br /> "选项卡由于表已在**ObjId**列中标识，因此未提供任何信息。<br /><br /> 数据库由于已在**dbid**列中标识了数据库，因此未提供任何信息。<br /><br /> FIL文件的标识符，与**database_files**目录视图中的**file_id**列相匹配。<br /><br /> 应用要锁定的应用程序资源的唯一标识符。 格式为 DbPrincipleId @no__t： > \<hashed > 值，格式为。<br /><br /> MD：随资源类型而变化。 有关详细信息，请参阅**resource_description** [_tran_locks &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md)中的说明。<br /><br /> HBT未提供任何信息。 改用**sys.databases _tran_locks**动态管理视图。<br /><br /> AU未提供任何信息。 改用**sys.databases _tran_locks**动态管理视图。|  
|**模式**|**nvarchar(8)**|所请求的锁模式。 可以是：<br /><br /> NULL = 不授予对资源的访问权限。 用作占位符。<br /><br /> Sch-S = 架构稳定性。 确保在任何会话持有对架构元素（例如表或索引）的架构稳定性锁时，不删除该架构元素。<br /><br /> Sch-M = 架构修改。 必须由要更改指定资源架构的任何会话持有。 确保没有其他会话正在引用所指示的对象。<br /><br /> S = 共享。 授予持有锁的会话对资源的共享访问权限。<br /><br /> U = 更新。 指示对最终可能更新的资源获取的更新锁。 用于防止一种常见的死锁，这种死锁在多个会话锁定资源以便稍后对资源进行更新时发生。<br /><br /> X = 排他。 授予持有锁的会话对资源的独占访问权限。<br /><br /> IS = 意向共享。 指示有意将 S 锁放置在锁层次结构中的某个从属资源上。<br /><br /> IU = 意向更新。 指示有意将 U 锁放置在锁层次结构中的某个从属资源上。<br /><br /> IX = 意向排他。 指示有意将 X 锁放置在锁层次结构中的某个从属资源上。<br /><br /> SIU = 共享意向更新。 指示对有意在锁层次结构中的从属资源上获取更新锁的资源进行共享访问。<br /><br /> SIX = 共享意向排他。 指示对有意在锁层次结构中的从属资源上获取排他锁的资源进行共享访问。<br /><br /> UIX = 更新意向排他。 指示对有意在锁层次结构中的从属资源上获取排他锁的资源持有的更新锁。<br /><br /> BU = 大容量更新。 用于大容量操作。<br /><br /> RangeS_S = 共享键范围和共享资源锁。 指示可串行范围扫描。<br /><br /> RangeS_U = 共享键范围和更新资源锁。 指示可串行更新扫描。<br /><br /> RangeI_N = 插入键范围和 Null 资源锁。 用于在将新键插入索引前测试范围。<br /><br /> RangeI_S = 键范围转换锁。 由 RangeI_N 和 S 锁的重叠创建。<br /><br /> RangeI_U = 由 RangeI_N 和 U 锁的重叠创建的键范围转换锁。<br /><br /> RangeI_X = 由 RangeI_N 和 X 锁的重叠创建的键范围转换锁。<br /><br /> RangeX_S = 由 RangeI_N 和 RangeS_S 锁的重叠创建的键范围转换锁 住.<br /><br /> RangeX_U = 由 RangeI_N 和 RangeS_U 锁的重叠创建的键范围转换锁。<br /><br /> RangeX_X = 排他键范围和排他资源锁。 这是在更新范围中的键时使用的转换锁。|  
|**“状态”**|**nvarchar(5)**|锁的请求状态：<br /><br /> CNVRT:锁定正在从另一种模式转换，但该转换被另一个具有冲突模式的锁定的进程阻止。<br /><br /> 准予已获取锁。<br /><br /> 再锁被另一个进程阻止，该进程持有处于冲突模式的锁。|  
  
## <a name="remarks"></a>备注  
 用户可以通过下列方式控制读取操作的锁定：  
  
-   使用 SET TRANSACTION ISOLATION LEVEL 指定会话的锁定级别。 有关语法和限制，请参阅[设置事务隔离&#40;级别 transact-sql&#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)。  
  
-   使用锁定表提示来为 FROM 子句中引用的各个表指定锁定级别。 有关语法和限制，请参阅[表&#40;提示 transact-sql&#41;](../../t-sql/queries/hints-transact-sql-table.md)。  
  
 所有没有与会话相关联的分布式事务都是孤立事务。 [!INCLUDE[ssDE](../../includes/ssde-md.md)]为所有孤立的分布式事务赋予 SPID 值 -2，这使得用户能够更容易标识阻塞的分布式事务。 有关详细信息，请参阅 [使用标记的事务一致地恢复相关的数据库的事务（完全恢复模式）](../../relational-databases/backup-restore/use-marked-transactions-to-recover-related-databases-consistently.md)。  
  
## <a name="permissions"></a>权限  
 需要 VIEW SERVER STATE 权限。  
  
## <a name="examples"></a>示例  
  
### <a name="a-listing-all-locks"></a>A. 列出所有锁  
 以下示例显示[!INCLUDE[ssDE](../../includes/ssde-md.md)]实例当前持有的所有锁的信息。  
  
```sql  
USE master;  
GO  
EXEC sp_lock;  
GO  
```  
  
### <a name="b-listing-a-lock-from-a-single-server-process"></a>B. 列出单服务器进程的锁  
 以下示例显示进程 ID `53` 的信息（其中包括锁信息）。  
  
```sql  
USE master;  
GO  
EXEC sp_lock 53;  
GO  
```  
  
## <a name="see-also"></a>请参阅  
 [sys.dm_tran_locks (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-tran-locks-transact-sql.md)   
 [DB_NAME (Transact-SQL)](../../t-sql/functions/db-name-transact-sql.md)   
 [KILL (Transact-SQL)](../../t-sql/language-elements/kill-transact-sql.md)   
 [OBJECT_NAME (Transact-SQL)](../../t-sql/functions/object-name-transact-sql.md)   
 [sp_who (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-who-transact-sql.md)   
 [sys.database_files (Transact-SQL)](../../relational-databases/system-catalog-views/sys-database-files-transact-sql.md)   
 [sys.databases _os_tasks &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-tasks-transact-sql.md)   
 [sys.dm_os_threads &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-threads-transact-sql.md)  
  
  
