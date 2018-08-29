---
title: sys.dm_db_index_physical_stats (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_db_index_physical_stats
- sys.dm_db_index_physical_stats_TSQL
- sys.dm_db_index_physical_stats
- dm_db_index_physical_stats_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_db_index_physical_stats dynamic management function
- fragmentation [SQL Server]
ms.assetid: d294dd8e-82d5-4628-aa2d-e57702230613
caps.latest.revision: 95
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: d42c55b62530a47332e4868c3080f3f21be9be8d
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43085550"
---
# <a name="sysdmdbindexphysicalstats-transact-sql"></a>sys.dm_db_index_physical_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  返回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中指定表或视图的数据和索引的大小和碎片信息。 对于索引，针对每个分区中的 B 树的每个级别，返回与其对应的一行。 对于堆，针对每个分区的 IN_ROW_DATA 分配单元，返回与其对应的一行。 对于大型对象 (LOB) 数据，针对每个分区的 LOB_DATA 分配单元返回与其对应的一行。 如果表中存在行溢出数据，则针对每个分区中的 ROW_OVERFLOW_DATA 分配单元，返回与其对应的一行。 不返回有关 xVelocity 内存优化的列存储索引的信息。  
  
> [!IMPORTANT]
> 如果您查询**sys.dm_db_index_physical_stats**承载 Alwayson 的服务器实例上[可读辅助副本](../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)，可能会遇到 REDO 阻塞问题。 这是因为此动态管理视图获取指定用户表或视图的 IS 锁，而该锁可能阻止 REDO 线程对该用户表或视图的 X 锁请求。  
  
 **sys.dm_db_index_physical_stats**不返回有关内存优化索引的信息。 有关内存优化索引中使用的信息，请参阅[sys.dm_db_xtp_index_stats &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-index-stats-transact-sql.md)。  
  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sys.dm_db_index_physical_stats (   
    { database_id | NULL | 0 | DEFAULT }  
  , { object_id | NULL | 0 | DEFAULT }  
  , { index_id | NULL | 0 | -1 | DEFAULT }  
  , { partition_number | NULL | 0 | DEFAULT }  
  , { mode | NULL | DEFAULT }  
)  
```  
  
## <a name="arguments"></a>参数  
 *database_id* |NULL |0 |默认值  
 是数据库的 ID。 *database_id*是**smallint**。 有效的输入包括数据库的 ID 号、NULL、0 或 DEFAULT。 默认值为 0。 在此上下文中，NULL、0 和 DEFAULT 是等效值。  
  
 指定 NULL 可返回 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例中所有数据库的信息。 如果指定为空， *database_id*，则还必须指定为 NULL *object_id*， *index_id*，以及*partition_number*。  
  
 内置函数[DB_ID](../../t-sql/functions/db-id-transact-sql.md)可以指定。 如果在不指定数据库名称的情况下使用 DB_ID，则当前数据库的兼容级别必须是 90 或更高。  
  
 *object_id* |NULL |0 |默认值  
 索引所在的表或视图的对象 ID。 *object_id* 是 **int**。  
  
 有效的输入包括表和视图的 ID 号、NULL、0 或 DEFAULT。 默认值为 0。 在此上下文中，NULL、0 和 DEFAULT 是等效值。 在[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]，有效的输入也包含 service broker 队列名称或队列内部表名称。 当应用默认的参数 （即所有对象，所有索引，等等），在结果集中包含的所有队列的碎片信息。  
  
 指定 NULL 可返回指定数据库中的所有表和视图的信息。 如果指定为空， *object_id*，则还必须指定为 NULL *index_id*并*partition_number*。  
  
 *index_id* | 0 |NULL |-1 |默认值  
 索引的 ID。 *index_id*是**int**。有效输入包括索引 0 的 ID 号，如果*object_id*是一个堆，NULL，-1 或默认值。 默认值为-1。 为 NULL，-1，并且默认值是在此上下文中的等效值。  
  
 指定 NULL 可返回基表或视图的所有索引的信息。 如果指定为空， *index_id*，则还必须指定为 NULL *partition_number*。  
  
 *partition_number* |NULL |0 |默认值  
 对象中的分区号。 *partition_number*是**int**。有效输入包括*partion_number*索引或堆中，NULL、 0 或 DEFAULT。 默认值为 0。 在此上下文中，NULL、0 和 DEFAULT 是等效值。  
  
 指定 NULL，以返回有关所属对象的所有分区的信息。  
  
 *partition_number* 1 开始。 未分区的索引或堆*partition_number*设置为 1。  
  
 *模式*|NULL |默认值  
 模式的名称。 *模式*指定用于获取统计信息的扫描级别。 *模式*是**sysname**。 有效输入为 DEFAULT、NULL、LIMITED、SAMPLED 或 DETAILED。 默认值 (NULL) 为 LIMITED。  
  
## <a name="table-returned"></a>返回的表  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|database_id|**smallint**|表或视图的数据库 ID。|  
|object_id|**int**|表或视图的索引位于对象 ID。|  
|index_id|**int**|索引的索引 ID。<br /><br /> 0 = 堆。|  
|partition_number|**int**|所属对象内从 1 开始的分区号；表、视图或索引。<br /><br /> 1 = 未分区的索引或堆。|  
|index_type_desc|**nvarchar(60)**|索引类型的说明：<br /><br /> HEAP<br /><br /> CLUSTERED INDEX<br /><br /> NONCLUSTERED INDEX<br /><br /> PRIMARY XML INDEX<br /><br /> SPATIAL INDEX<br /><br /> XML INDEX<br /><br /> 列存储映射索引 （内部）<br /><br /> 列存储 deletebuffer 会完全索引 （内部）<br /><br /> 列存储 DELETEBITMAP 索引 （内部）|  
|hobt_id|**bigint**|堆或 B 树索引或分区的 ID。<br /><br /> 除了返回用户定义的索引的 hobt_id，这还将返回内部的列存储索引的 hobt_id。|  
|alloc_unit_type_desc|**nvarchar(60)**|对分配单元类型的说明：<br /><br /> IN_ROW_DATA<br /><br /> LOB_DATA<br /><br /> ROW_OVERFLOW_DATA<br /><br /> LOB_DATA 分配单元包含类型的列中存储的数据**文本**， **ntext**，**图像**， **varchar （max)**， **nvarchar （max)**， **varbinary （max)**，并**xml**。 有关详细信息，请参阅[数据类型 (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)。<br /><br /> ROW_OVERFLOW_DATA 分配单元包含类型的列中存储的数据**varchar （n)**， **nvarchar(n)**， **varbinary （n)**，和**sql_变体**已推送到行外。|  
|index_depth|**tinyint**|索引级别数。<br /><br /> 1 = 堆，或 LOB_DATA 或 ROW_OVERFLOW_DATA 分配单元。|  
|index_level|**tinyint**|索引的当前级别。<br /><br /> 0 表示索引叶级别、堆以及 LOB_DATA 或 ROW_OVERFLOW_DATA 分配单元。<br /><br /> 大于 0 的值表示非叶索引级别。 *index_level*索引的根级别将是最高。<br /><br /> 索引的非叶级别才处理何时*模式下*= 详细。|  
|avg_fragmentation_in_percent|**float**|索引的逻辑碎片，或 IN_ROW_DATA 分配单元中堆的区碎片。<br /><br /> 此值按百分比计算，并将考虑多个文件。 有关逻辑碎片和区碎片的定义，请参阅“注释”。<br /><br /> 0 表示 LOB_DATA 和 ROW_OVERFLOW_DATA 分配单元。<br /><br /> 为 NULL 时堆*模式下*= SAMPLED。|  
|fragment_count|**bigint**|IN_ROW_DATA 分配单元的叶级别中的碎片数。 有关碎片的详细信息，请参阅“注释”。<br /><br /> 对于索引的非叶级别，以及 LOB_DATA 或 ROW_OVERFLOW_DATA 分配单元，为 NULL。<br /><br /> 为 NULL 时堆*模式下*= SAMPLED。|  
|avg_fragment_size_in_pages|**float**|IN_ROW_DATA 分配单元的叶级别中的一个碎片的平均页数。<br /><br /> 对于索引的非叶级别，以及 LOB_DATA 或 ROW_OVERFLOW_DATA 分配单元，为 NULL。<br /><br /> 为 NULL 时堆*模式下*= SAMPLED。|  
|page_count|**bigint**|索引或数据页的总数。<br /><br /> 对于索引，表示 IN_ROW_DATA 分配单元中 b 树的当前级别中的索引页总数。<br /><br /> 对于堆，表示 IN_ROW_DATA 分配单元中的数据页总数。<br /><br /> 对于 LOB_DATA 或 ROW_OVERFLOW_DATA 分配单元，表示该分配单元中的总页数。|  
|avg_page_space_used_in_percent|**float**|所有页中使用的可用数据存储空间的平均百分比。<br /><br /> 对于索引，平均百分比应用于 IN_ROW_DATA 分配单元中 b 树的当前级别。<br /><br /> 对于堆，表示 IN_ROW_DATA 分配单元中所有数据页的平均百分比。<br /><br /> 对于 LOB_DATA 或 ROW_OVERFLOW DATA 分配单元，表示该分配单元中所有页的平均百分比。<br /><br /> 为 NULL 时*模式下*= 受限。|  
|record_count|**bigint**|总记录数。<br /><br /> 对于索引，记录的总数应用于 IN_ROW_DATA 分配单元中 b 树的当前级别。<br /><br /> 对于堆，表示 IN_ROW_DATA 分配单元中的总记录数。<br /><br /> **注意：** 对于堆，此函数返回的记录数可能不匹配的运行 SELECT COUNT 返回的行数 (\*) 针对堆。 这是因为一行可能包含多个记录。 例如，在某些更新情况下，单个堆行可能由于更新操作而包含一条前推记录和一条被前推记录。 此外，多数大型 LOB 行在 LOB_DATA 存储中拆分为多个记录。<br /><br /> 对于 LOB_DATA 或 ROW_OVERFLOW_DATA 分配单元，表示整个分配单元中总记录数。<br /><br /> 为 NULL 时*模式下*= 受限。|  
|ghost_record_count|**bigint**|分配单元中将被虚影清除任务删除的虚影记录数。<br /><br /> 对于 IN_ROW_DATA 分配单元中索引的非叶级别，为 0。<br /><br /> 为 NULL 时*模式下*= 受限。|  
|version_ghost_record_count|**bigint**|由分配单元中未完成的快照隔离事务保留的虚影记录数。<br /><br /> 对于 IN_ROW_DATA 分配单元中索引的非叶级别，为 0。<br /><br /> 为 NULL 时*模式下*= 受限。|  
|min_record_size_in_bytes|**int**|最小记录大小（字节）。<br /><br /> 对于索引，为 IN_ROW_DATA 分配单元中 b 树当前级别的最小记录大小。<br /><br /> 对于堆，表示 IN_ROW_DATA 分配单元中的最小记录大小。<br /><br /> 对于 LOB_DATA 或 ROW_OVERFLOW_DATA 分配单元，表示整个分配单元中的最小记录大小。<br /><br /> 为 NULL 时*模式下*= 受限。|  
|max_record_size_in_bytes|**int**|最大记录大小（字节）。<br /><br /> 对于索引，分配单元中 b 树当前级别的最大记录大小。<br /><br /> 对于堆，表示 IN_ROW_DATA 分配单元中的最大记录大小。<br /><br /> 对于 LOB_DATA 或 ROW_OVERFLOW_DATA 分配单元，表示整个分配单元中的最大记录大小。<br /><br /> 为 NULL 时*模式下*= 受限。|  
|avg_record_size_in_bytes|**float**|平均记录大小（字节）。<br /><br /> 对于索引，为 IN_ROW_DATA 分配单元中 b 树当前级别的平均记录大小。<br /><br /> 对于堆，表示 IN_ROW_DATA 分配单元中的平均记录大小。<br /><br /> 对于 LOB_DATA 或 ROW_OVERFLOW_DATA 分配单元，表示整个分配单元中的平均记录大小。<br /><br /> 为 NULL 时*模式下*= 受限。|  
|forwarded_record_count|**bigint**|在堆中具有指向另一个数据位置的转向指针的记录数。 （在更新过程中，如果在原始位置存储新行的空间不足，将会出现此状态。）<br /><br /> 除 IN_ROW_DATA 分配单元外，对于堆的其他所有分配单元都为 NULL。<br /><br /> 为 NULL 时堆*模式下*= 受限。|  
|compressed_page_count|**bigint**|压缩页的数目。<br /><br /> 对于堆，新分配的页未进行 PAGE 压缩。 堆在以下两种特殊情况下进行 PAGE 压缩：大量导入数据时和重新生成堆时。 导致页分配的典型 DML 操作不会进行 PAGE 压缩。 当 compressed_page_count 值增长到超过您所需的阈值时，将重新生成堆。<br /><br /> 对于具有聚集索引的表，compressed_page_count 值表示 PAGE 压缩的效率。|  
|hobt_id|BIGINT|**适用范围**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 到 [当前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658)）、 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。<br /><br /> 对于仅限列存储索引，这是跟踪分区内部的列存储数据的行集的 ID。 行集是存储为堆数据或二进制树。 它们具有相同父列存储索引的索引 ID。 有关详细信息，请参阅[sys.internal_partitions &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-internal-partitions-transact-sql.md)。<br /><br /> 则为 NULL|  
|column_store_delete_buffer_state|TINYINT|**适用范围**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 到 [当前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658)）、 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。<br /><br /> 0 = NOT_APPLICABLE<br /><br /> 1 = OPEN<br /><br /> 2 = 排出<br /><br /> 3 = 正在刷新<br /><br /> 4 = 停用<br /><br /> 5 = 就绪|  
|column_store_delete_buff_state_desc||**适用范围**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 到 [当前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658)）、 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]。<br /><br /> NOT_APPLICABLE – 父索引不是列存储索引。<br /><br /> 打开 – deleters 并扫描程序使用此。<br /><br /> 排出 – deleters 排出，但扫描程序仍使用它。<br /><br /> 正在刷新 – 关闭缓冲区和缓冲区中的行是否正写入删除位图。<br /><br /> RETIRING – 中的已关闭的删除缓冲区的行已写入删除位图，但缓冲区已不被截断，因为扫描程序仍在使用它。 新的扫描程序无需使用即将停用的缓冲区，因为打开缓冲区就足够了。<br /><br /> 已准备就绪-此删除缓冲区可供使用。|  
  
## <a name="remarks"></a>Remarks  
 sys.dm_db_index_physical_stats 动态管理函数将替换 DBCC SHOWCONTIG 语句。  
  
## <a name="scanning-modes"></a>扫描模式  
 函数的执行模式将确定为了获取此函数所使用的统计信息数据而执行的扫描级别。 *模式*指定为 LIMITED、 SAMPLED 或 DETAILED。 该函数遍历分配单元的页链，这些分配单元构成表或索引的指定分区。 sys.dm_db_index_physical_stats 只需要一个意向共享 (IS) 表锁，而不考虑它在运行模式。  
  
 LIMITED 模式运行最快，扫描的页数最少。 对于索引，只扫描 B 树的父级别页（即叶级别以上的页）。 对于堆，只检查关联的 PFS 和 IAM 页；并在 LIMITED 模式下扫描堆的数据页。  
  
 在 LIMITED 模式下，compressed_page_count 为 NULL，这是因为[!INCLUDE[ssDE](../../includes/ssde-md.md)]只能扫描 B 树的非叶页和堆的 IAM 和 PFS 页。 使用 SAMPLED 模式可以获取 compressed_page_count，一个估计的值，并使用 DETAILED 的模式可以获取 compressed_page_count 的实际值。 SAMPLED 模式基于索引或堆中所有页面的 1% 样本返回统计信息。 SAMPLED 模式中的结果应视为近似值。 如果索引或堆少于 10,000 页，则使用 DETAILED 模式代替 SAMPLED。  
  
 DETAILED 模式将扫描所有页并返回所有统计信息。  
  
 模式将越来越慢 limited 到 DETAILED，因为在每种模式中执行更多的工作。 若要快速测量表或索引的大小或碎片级别，请使用 LIMITED 模式。 它的速度最快，并且不会为索引 IN_ROW_DATA 分配单元中的每个非叶级别分别返回一行。  
  
## <a name="using-system-functions-to-specify-parameter-values"></a>使用系统函数指定参数值  
 可以使用[!INCLUDE[tsql](../../includes/tsql-md.md)]函数[DB_ID](../../t-sql/functions/db-id-transact-sql.md)并[OBJECT_ID](../../t-sql/functions/object-id-transact-sql.md)若要为指定值*database_id*并*object_id*参数。 但是，将无效的值传递给这些函数可能会导致意外结果。 例如，如果找不到数据库或对象名（因为它们不存在或拼写错误），则两个函数都返回 NULL。 sys.dm_db_index_physical_stats 函数将 NULL 解释为指定所有数据库或所有对象的通配符值。  
  
 此外，sys.dm_db_index_physical_stats 函数调用，并因此在当前数据库的上下文中计算之前处理 OBJECT_ID 函数时，不是在数据库中指定*database_id*。 此行为可能会导致 OBJECT_ID 函数返回 NULL 值；或者，如果当前数据库上下文和指定数据库中都存在对象名，则可能返回一条错误消息。 以下示例演示了这些意外的结果。  
  
```  
USE master;  
GO  
-- In this example, OBJECT_ID is evaluated in the context of the master database.   
-- Because Person.Address does not exist in master, the function returns NULL.  
-- When NULL is specified as an object_id, all objects in the database are returned.  
-- The same results are returned when an object that is not valid is specified.  
SELECT * FROM sys.dm_db_index_physical_stats  
    (DB_ID(N'AdventureWorks'), OBJECT_ID(N'Person.Address'), NULL, NULL , 'DETAILED');  
GO  
-- This example demonstrates the results of specifying a valid object name  
-- that exists in both the current database context and  
-- in the database specified in the database_id parameter of the   
-- sys.dm_db_index_physical_stats function.  
-- An error is returned because the ID value returned by OBJECT_ID does not  
-- match the ID value of the object in the specified database.  
CREATE DATABASE Test;  
GO  
USE Test;  
GO  
CREATE SCHEMA Person;  
GO  
CREATE Table Person.Address(c1 int);  
GO  
USE AdventureWorks2012;  
GO  
SELECT * FROM sys.dm_db_index_physical_stats  
    (DB_ID(N'Test'), OBJECT_ID(N'Person.Address'), NULL, NULL , 'DETAILED');  
GO  
-- Clean up temporary database.  
DROP DATABASE Test;  
GO  
```  
  
### <a name="best-practice"></a>最佳实践  
 请始终确保使用 DB_ID 或 OBJECT_ID 时返回了有效的 ID。 例如，在使用 OBJECT_ID 时，指定由三部分名称如`OBJECT_ID(N'AdventureWorks2012.Person.Address')`，或者测试之前在 sys.dm_db_index_physical_stats 函数中使用这些函数返回的值。 下面的示例 A 和 B 演示了一种指定数据库和对象 ID 的安全方法。  
  
## <a name="detecting-fragmentation"></a>检测碎片  
 在对表进而对表中定义的索引进行数据修改（INSERT、UPDATE 和 DELETE 语句）的整个过程中都会出现碎片。 由于这些修改通常并不在表和索引的行中平均分布，所以每页的填充度会随时间而改变。 对于扫描表的部分或全部索引的查询，这种碎片会导致额外的页读取。 这会妨碍数据的并行扫描。  
  
 索引或堆的碎片级别显示在 avg_fragmentation_in_percent 列中。 对于堆，此值表示堆的区碎片。 对于索引，此值表示索引的逻辑碎片。 与 DBCC SHOWCONTIG 不同，这两种情况下的碎片计算算法都会考虑跨越多个文件的存储，因而结果是精确的。  
  
 **逻辑碎片**  
  
 这是索引的叶级页中出错页所占的百分比。 对于出错页，分配给索引的下一个物理页不是当前叶级页中的下一页指针所指向的页。  
  
 **区碎片**  
  
 这是堆的叶级页中出错区所占的百分比。 出错区是指：包含堆当前页的区在物理上不是包含前一页的区后的下一个区。  
  
 为了获得最佳性能，avg_fragmentation_in_percent 的值应尽可能接近零。 但是，从 0 到 10％ 范围内的值都可以接受。 所有减少碎片的方法（例如重新生成、重新组织或重新创建）都可用于降低这些值。 有关如何分析索引中碎片程度的详细信息，请参阅[重新组织和重新生成索引](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)。  
  
## <a name="reducing-fragmentation-in-an-index"></a>减少索引中的碎片  
 当索引分段的方式导致碎片影响查询性能时，有三种方法可减少碎片：  
  
-   删除并重新创建聚集索引。  
  
     重新创建聚集索引将对数据进行重新分布，从而使数据页填满。 填充度可以使用 CREATE INDEX 中的 FILLFACTOR 选项进行配置。 这种方法的缺点是索引在删除和重新创建周期内为脱机状态，并且操作属原子级。 如果中断索引创建，则不能重新创建索引。 有关详细信息，请参阅 [CREATE INDEX (Transact-SQL)](../../t-sql/statements/create-index-transact-sql.md)。  
  
-   使用 ALTER INDEX REORGANIZE（代替 DBCC INDEXDEFRAG）按逻辑顺序重新排序索引的叶级页。 由于这是联机操作，因此在语句运行时仍可使用索引。 中断此操作时不会丢失已经完成的任务。 此方法的缺点是在重新组织数据方面不如索引重新生成操作的效果好，而且不更新统计信息。  
  
-   使用 ALTER INDEX REBUILD（代替 DBCC DBREINDEX）联机或脱机重新生成索引。 有关详细信息，请参阅 [ALTER INDEX (Transact-SQL)](../../t-sql/statements/alter-index-transact-sql.md)。  
  
 不需要仅因为碎片的原因而重新组织或重新生成索引。 碎片的主要影响是，在索引扫描过程中会降低页的预读吞吐量。 这将导致响应时间变长。 如果含有碎片的表或索引中的查询工作负荷不涉及扫描（因为工作负荷主要是单独查找），则删除碎片可能不起作用。 有关详细信息，请参阅此[Microsoft 网站上](http://go.microsoft.com/fwlink/?linkid=31012)。  
  
> [!NOTE]  
>  如果对索引进行部分或完全移动在收缩操作，则运行 DBCC SHRINKFILE 或 DBCC SHRINKDATABASE 可能产生碎片。 因此，如果必须执行收缩操作，则应在删除碎片之前进行。  
  
## <a name="reducing-fragmentation-in-a-heap"></a>减少堆中的碎片  
 若要减少堆的区碎片，请对表创建聚集索引，然后删除该索引。 在创建聚集索引时将重新分布数据。 同时会考虑数据库中可用空间的分布，从而使其尽可能优化。 当删除聚集索引以重新创建堆时，数据不会移动并保持最佳位置。 有关如何执行这些操作的信息，请参阅[CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md)并[DROP INDEX](../../t-sql/statements/drop-index-transact-sql.md)。  
  
> [!CAUTION]  
>  通过创建并删除某一表的聚集索引，会对该表两次重新生成所有非聚集索引。  
  
## <a name="compacting-large-object-data"></a>压缩大型对象数据  
 默认情况下，ALTER INDEX REORGANIZE 语句将压缩包含大型对象 (LOB) 数据的页。 因为不会释放空的 LOB 页，所以在删除大量 LOB 数据或 LOB 列时，压缩此数据可改善磁盘空间使用情况。  
  
 重新组织指定的聚集索引将压缩聚集索引中包含的所有 LOB 列。 重新组织非聚集索引将压缩作为索引中非键（已包括）列的所有 LOB 列。 如果语句中指定 ALL，则将对与指定表或视图关联的所有索引进行重新组织。 此外，将压缩与聚集索引、基础表或带有包含列的非聚集索引关联的所有 LOB 列。  
  
## <a name="evaluating-disk-space-use"></a>评估磁盘空间使用状况  
 avg_page_space_used_in_percent 列指示页填充度。 为了使磁盘使用状况达到最优，对于没有很多随机插入的索引，此值应接近 100％。 但是，对于具有很多随机插入且页很满的索引，其页拆分数将不断增加。 这将导致更多的碎片。 因此，为了减少页拆分，此值应小于 100％。 使用指定的 FILLFACTOR 选项重新生成索引可以改变页填充度，以便符合索引中的查询模式。 有关填充因子的详细信息，请参阅[为索引指定填充因子](../../relational-databases/indexes/specify-fill-factor-for-an-index.md)。 此外，ALTER INDEX REORGANIZE 还试图通过将页填充到上一次指定的 FILLFACTOR 来压缩索引。 这会增加 avg_space_used_in_percent 的值。 请注意，ALTER INDEX REORGANIZE 不会降低页填充度。 相反，必须执行索引重新生成。  
  
## <a name="evaluating-index-fragments"></a>评估索引碎片  
 碎片由分配单元中同一文件内的物理连续的叶级页组成。 一个索引至少有一个碎片。 索引可以包含的最大碎片数等于索引的叶级别页数。 碎片越大，意味着读取相同页数所需的磁盘 I/O 越少。 因此，avg_fragment_size_in_pages 值越大，范围扫描的性能越好。 avg_fragment_size_in_pages 和 avg_fragmentation_in_percent 值成反比。 因此，重新生成或重新组织索引会减少碎片数量，但同时增大碎片大小。  
  
## <a name="limitations-and-restrictions"></a>限制和局限  
 不返回聚集列存储索引的数据。  
  
## <a name="permissions"></a>Permissions  
 需要下列权限：  
  
-   对数据库中的指定对象具有 CONTROL 权限。  
  
-   VIEW DATABASE STATE 权限返回有关指定的数据库中的所有对象的信息通过使用对象通配符 @*object_id*= NULL。  
  
-   VIEW SERVER STATE 权限，以返回有关所有数据库的信息通过使用数据库通配符 @*database_id* = NULL。  
  
 授予 VIEW DATABASE STATE 权限允许返回数据库中的所有对象，而不考虑对特定对象拒绝的任何 CONTROL 权限。  
  
 拒绝 VIEW DATABASE STATE 将禁止返回数据库中的所有对象，而不管对特定对象授予的任何 CONTROL 权限。 此外，当数据库通配符 @*database_id*= 指定了 NULL，则省略数据库。  
  
 有关详细信息，请参阅[动态管理视图和函数&#40;TRANSACT-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)。  
  
## <a name="examples"></a>示例  
  
### <a name="a-returning-information-about-a-specified-table"></a>A. 返回有关指定表的信息  
 下面的示例将返回 `Person.Address` 表的所有索引和分区的大小和碎片统计信息。 为了获得最佳性能并限制返回的统计信息，扫描模式设置为 `'LIMITED'`。 执行此查询至少需要对 `Person.Address` 表拥有 CONTROL 权限。  
  
```  
DECLARE @db_id SMALLINT;  
DECLARE @object_id INT;  
  
SET @db_id = DB_ID(N'AdventureWorks2012');  
SET @object_id = OBJECT_ID(N'AdventureWorks2012.Person.Address');  
  
IF @db_id IS NULL  
BEGIN;  
    PRINT N'Invalid database';  
END;  
ELSE IF @object_id IS NULL  
BEGIN;  
    PRINT N'Invalid object';  
END;  
ELSE  
BEGIN;  
    SELECT * FROM sys.dm_db_index_physical_stats(@db_id, @object_id, NULL, NULL , 'LIMITED');  
END;  
GO  
  
```  
  
### <a name="b-returning-information-about-a-heap"></a>B. 返回关于堆的信息  
 以下示例将返回有关 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 数据库中 `dbo.DatabaseLog` 堆的所有统计信息。 由于表包含 LOB 数据，因此除了对存储堆的数据页的 `LOB_DATA` 返回与其对应的一行外，还对 `IN_ROW_ALLOCATION_UNIT` 分配单元返回与其对应的一行。 执行此查询至少需要对 `dbo.DatabaseLog` 表拥有 CONTROL 权限。  
  
```  
DECLARE @db_id SMALLINT;  
DECLARE @object_id INT;  
SET @db_id = DB_ID(N'AdventureWorks2012');  
SET @object_id = OBJECT_ID(N'AdventureWorks2012.dbo.DatabaseLog');  
IF @object_id IS NULL   
BEGIN;  
    PRINT N'Invalid object';  
END;  
ELSE  
BEGIN;  
    SELECT * FROM sys.dm_db_index_physical_stats(@db_id, @object_id, 0, NULL , 'DETAILED');  
END;  
GO  
  
```  
  
### <a name="c-returning-information-for-all-databases"></a>C. 返回所有数据库的信息  
 下面的示例通过为所有参数指定通配符 `NULL`，返回有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例中所有表和索引的所有统计信息。 执行此查询需要 VIEW SERVER STATE 权限。  
  
```  
SELECT * FROM sys.dm_db_index_physical_stats (NULL, NULL, NULL, NULL, NULL);  
GO  
  
```  
  
### <a name="d-using-sysdmdbindexphysicalstats-in-a-script-to-rebuild-or-reorganize-indexes"></a>D. 使用脚本中的 sys.dm_db_index_physical_stats 重新生成或重新组织索引  
 以下示例将自动重新组织或重新生成数据库中平均碎片超过 10％ 的所有分区。 执行此查询需要 VIEW DATABASE STATE 权限。 此示例在不指定数据库名称的情况下，指定 `DB_ID` 作为第一个参数。 如果当前数据库的兼容级别为 80 或更低，则会产生错误。 若要纠正此错误，请用有效的数据库名称替换 `DB_ID()`。 有关数据库兼容性级别的详细信息，请参阅[ALTER DATABASE 兼容性级别&#40;TRANSACT-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)。  
  
```  
-- Ensure a USE <databasename> statement has been executed first.  
SET NOCOUNT ON;  
DECLARE @objectid int;  
DECLARE @indexid int;  
DECLARE @partitioncount bigint;  
DECLARE @schemaname nvarchar(130);   
DECLARE @objectname nvarchar(130);   
DECLARE @indexname nvarchar(130);   
DECLARE @partitionnum bigint;  
DECLARE @partitions bigint;  
DECLARE @frag float;  
DECLARE @command nvarchar(4000);   
-- Conditionally select tables and indexes from the sys.dm_db_index_physical_stats function   
-- and convert object and index IDs to names.  
SELECT  
    object_id AS objectid,  
    index_id AS indexid,  
    partition_number AS partitionnum,  
    avg_fragmentation_in_percent AS frag  
INTO #work_to_do  
FROM sys.dm_db_index_physical_stats (DB_ID(), NULL, NULL , NULL, 'LIMITED')  
WHERE avg_fragmentation_in_percent > 10.0 AND index_id > 0;  
  
-- Declare the cursor for the list of partitions to be processed.  
DECLARE partitions CURSOR FOR SELECT * FROM #work_to_do;  
  
-- Open the cursor.  
OPEN partitions;  
  
-- Loop through the partitions.  
WHILE (1=1)  
    BEGIN;  
        FETCH NEXT  
           FROM partitions  
           INTO @objectid, @indexid, @partitionnum, @frag;  
        IF @@FETCH_STATUS < 0 BREAK;  
        SELECT @objectname = QUOTENAME(o.name), @schemaname = QUOTENAME(s.name)  
        FROM sys.objects AS o  
        JOIN sys.schemas as s ON s.schema_id = o.schema_id  
        WHERE o.object_id = @objectid;  
        SELECT @indexname = QUOTENAME(name)  
        FROM sys.indexes  
        WHERE  object_id = @objectid AND index_id = @indexid;  
        SELECT @partitioncount = count (*)  
        FROM sys.partitions  
        WHERE object_id = @objectid AND index_id = @indexid;  
  
-- 30 is an arbitrary decision point at which to switch between reorganizing and rebuilding.  
        IF @frag < 30.0  
            SET @command = N'ALTER INDEX ' + @indexname + N' ON ' + @schemaname + N'.' + @objectname + N' REORGANIZE';  
        IF @frag >= 30.0  
            SET @command = N'ALTER INDEX ' + @indexname + N' ON ' + @schemaname + N'.' + @objectname + N' REBUILD';  
        IF @partitioncount > 1  
            SET @command = @command + N' PARTITION=' + CAST(@partitionnum AS nvarchar(10));  
        EXEC (@command);  
        PRINT N'Executed: ' + @command;  
    END;  
  
-- Close and deallocate the cursor.  
CLOSE partitions;  
DEALLOCATE partitions;  
  
-- Drop the temporary table.  
DROP TABLE #work_to_do;  
GO  
  
```  
  
### <a name="e-using-sysdmdbindexphysicalstats-to-show-the-number-of-page-compressed-pages"></a>E. 使用 sys.dm_db_index_physical_stats 显示页压缩页的数目  
 下面的示例演示如何显示行和页已压缩的页，以及如何将已压缩页数与总页数进行比较。 此信息可用于确定压缩为索引或表提供的好处。  
  
```  
SELECT o.name,  
    ips.partition_number,  
    ips.index_type_desc,  
    ips.record_count, ips.avg_record_size_in_bytes,  
    ips.min_record_size_in_bytes,  
    ips.max_record_size_in_bytes,  
    ips.page_count, ips.compressed_page_count  
FROM sys.dm_db_index_physical_stats ( DB_ID(), NULL, NULL, NULL, 'DETAILED') ips  
JOIN sys.objects o on o.object_id = ips.object_id  
ORDER BY record_count DESC;  
```  
  
### <a name="f-using-sysdmdbindexphysicalstats-in-sampled-mode"></a>F. 在 SAMPLED 模式中使用 sys.dm_db_index_physical_stats  
 下面的示例显示 SAMPLED 模式如何返回与 DETAILED 模式结果不同的近似值。  
  
```  
CREATE TABLE t3 (col1 int PRIMARY KEY, col2 varchar(500)) WITH(DATA_COMPRESSION = PAGE);  
GO  
BEGIN TRAN  
DECLARE @idx int = 0;  
WHILE @idx < 1000000  
BEGIN  
    INSERT INTO t3 (col1, col2)   
    VALUES (@idx,   
    REPLICATE ('a', 100) + CAST (@idx as varchar(10)) + REPLICATE ('a', 380))  
    SET @idx = @idx + 1  
END  
COMMIT;  
GO  
SELECT page_count, compressed_page_count, forwarded_record_count, *   
FROM sys.dm_db_index_physical_stats (db_id(),   
    object_id ('t3'), null, null, 'SAMPLED');  
SELECT page_count, compressed_page_count, forwarded_record_count, *   
FROM sys.dm_db_index_physical_stats (db_id(),   
    object_id ('t3'), null, null, 'DETAILED');  
```  
  
### <a name="g-querying-service-broker-queues-for-index-fragmentation"></a>G. 查询索引碎片的 service broker 队列  
  
||  
|-|  
|**适用范围**： [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] 到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。|  
  
 下面的示例显示了如何查询碎片 server broker 队列。  
  
```  
--Using queue internal table name   
select * from sys.dm_db_index_physical_stats (db_id(), object_id ('sys.queue_messages_549576996'), default, default, default)   
  
--Using queue name directly  
select * from sys.dm_db_index_physical_stats (db_id(), object_id ('ExpenseQueue'), default, default, default)  
  
```  
  
## <a name="see-also"></a>请参阅  
 [动态管理视图和函数 (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [与索引相关的动态管理视图和函数 &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/index-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_db_index_operational_stats (Transact-SQL)](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md)   
 [sys.dm_db_index_usage_stats &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-usage-stats-transact-sql.md)   
 [sys.dm_db_partition_stats &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-partition-stats-transact-sql.md)   
 [sys.allocation_units &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-allocation-units-transact-sql.md)   
 [系统视图&#40;Transact SQL&#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)  
  
  

