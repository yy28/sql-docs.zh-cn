---
title: "index_option (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 09/08/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- index_option
ms.assetid: 8a14f12d-2fbf-4036-b8b2-8db3354e0eb7
caps.latest.revision: 68
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: cd1366409f9fb0af271b26fad3b8b911f99acc06
ms.openlocfilehash: e7563f9fe992dcf4f9308cccbf11f6310b7925a7
ms.contentlocale: zh-cn
ms.lasthandoff: 09/08/2017

---
# <a name="alter-table-indexoption-transact-sql"></a>ALTER TABLE index_option (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  指定一组可以应用是通过创建约束定义的一部分的索引选项， [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
{   
    PAD_INDEX = { ON | OFF }  
  | FILLFACTOR = fillfactor  
  | IGNORE_DUP_KEY = { ON | OFF }  
  | STATISTICS_NORECOMPUTE = { ON | OFF }  
  | ALLOW_ROW_LOCKS = { ON | OFF }  
  | ALLOW_PAGE_LOCKS = { ON | OFF }  
  | SORT_IN_TEMPDB = { ON | OFF }   
  | ONLINE = { ON | OFF }  
  | MAXDOP = max_degree_of_parallelism  
  | DATA_COMPRESSION = { NONE |ROW | PAGE | COLUMNSTORE | COLUMNSTORE_ARCHIVE }  
      [ ON PARTITIONS ( { <partition_number_expression> | <range> }   
      [ , ...n ] ) ]  
  | ONLINE = { ON [ ( <low_priority_lock_wait> ) ] | OFF }  
}  
  
<range> ::=   
<partition_number_expression> TO <partition_number_expression>  
  
<single_partition_rebuild__option> ::=  
{  
    SORT_IN_TEMPDB = { ON | OFF }  
  | MAXDOP = max_degree_of_parallelism  
  | DATA_COMPRESSION = {NONE | ROW | PAGE | COLUMNSTORE | COLUMNSTORE_ARCHIVE } }  
  | ONLINE = { ON [ ( <low_priority_lock_wait> ) ] | OFF }  
}  
  
<low_priority_lock_wait>::=  
{  
    WAIT_AT_LOW_PRIORITY ( MAX_DURATION = <time> [ MINUTES ] ,   
                           ABORT_AFTER_WAIT = { NONE | SELF | BLOCKERS } )   
}  
```  
  
## <a name="arguments"></a>参数  
 PAD_INDEX  **=**  {ON |**OFF** }  
 **适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 指定索引填充。 默认为 OFF。  
  
 ON  
 FILLFACTOR 指定的可用空间百分比应用于索引的中间级页。  
  
 关闭或*fillfactor*未指定  
 考虑到中间级页上的键集，可以将中间级页几乎填满，但至少要为最大索引行留出足够空间。  
  
 填充因子 **=** *填充因子*  
 **适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 指定一个百分比，指示在[!INCLUDE[ssDE](../../includes/ssde-md.md)]创建或修改索引的过程中，应将每个索引页面的叶级填充到什么程度。 指定的值必须是 1 到 100 之间的整数。 默认值为 0。  
  
> [!NOTE]  
>  填充因子值 0 和 100 在所有方面都是相同的。  
  
 IGNORE_DUP_KEY  **=**  {ON |**OFF** }  
 指定在插入操作尝试向唯一索引插入重复键值时的错误响应。 IGNORE_DUP_KEY 选项仅适用于创建或重新生成索引后发生的插入操作。 选项不起作用时执行[CREATE INDEX](../../t-sql/statements/create-index-transact-sql.md)， [ALTER INDEX](../../t-sql/statements/alter-index-transact-sql.md)，或[更新](../../t-sql/queries/update-transact-sql.md)。 默认为 OFF。  
  
 ON  
 重复的键值插入到唯一索引时，将出现警告消息。 仅违反唯一性约束的行失败。  
  
 OFF  
 重复的键值插入到唯一索引时，将出现错误消息。 整个插入操作将回滚。  
  
 对视图创建索引、 非唯一索引、 XML 索引、 空间索引和筛选的索引，IGNORE_DUP_KEY 不能设置为 ON。  
  
 若要查看 IGNORE_DUP_KEY，使用[sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)。  
  
 在向后兼容的语法中，WITH IGNORE_DUP_KEY 等效于 WITH IGNORE_DUP_KEY = ON。  
  
 STATISTICS_NORECOMPUTE  **=**  {ON |**OFF** }  
 指定是否重新计算统计信息。 默认为 OFF。  
  
 ON  
 不会自动重新计算过时的统计信息。  
  
 OFF  
 启用统计信息自动更新功能。  
  
 ALLOW_ROW_LOCKS  **=**  { **ON** |关闭}  
 **适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 指定是否允许行锁。 默认值为 ON。  
  
 ON  
 在访问索引时允许使用行锁。 [!INCLUDE[ssDE](../../includes/ssde-md.md)]确定何时使用行锁。  
  
 OFF  
 不使用行锁。  
  
 ALLOW_PAGE_LOCKS  **=**  { **ON** |关闭}  
 **适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 指定是否允许使用页锁。 默认值为 ON。  
  
 ON  
 在访问索引时允许使用页锁。 [!INCLUDE[ssDE](../../includes/ssde-md.md)]确定何时使用页锁。  
  
 OFF  
 不使用页锁。  
  
 SORT_IN_TEMPDB  **=**  {ON |**OFF** }  
 **适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 指定是否存储中的排序结果**tempdb**。 默认为 OFF。  
  
 ON  
 用于生成索引的中间排序结果存储在**tempdb**。 这可能会降低仅当创建索引所需的时间**tempdb**位于不同的与用户数据库的磁盘集。 但是，这会增加索引生成期间所使用的磁盘空间量。  
  
 OFF  
 中间排序结果与索引存储在同一数据库中。  
  
 联机 **=**  {ON |**OFF** }  
 **适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 指定在索引操作期间基础表和关联的索引是否可用于查询和数据修改操作。 默认为 OFF。 REBUILD 可作为 ONLINE 操作执行。  
  
> [!NOTE]  
>  不能联机创建唯一的非聚集索引。 这包括由于 UNIQUE 或 PRIMARY KEY 约束而创建的索引。  
  
 ON  
 在索引操作期间不持有长期表锁。 在索引操作的主要阶段，源表上只使用意向共享 (IS) 锁。 这使得能够继续对基础表和索引进行查询或更新。 操作开始时，在很短的时间内对源对象持有共享 (S) 锁。 操作结束时，如果创建非聚集索引，将在短期内获取对源的 S（共享）锁；当联机创建或删除聚集索引时，以及重新生成聚集或非聚集索引时，将在短期内获取 SCH-M（架构修改）锁。 但联机索引锁是短的元数据锁，特别是 Sch-M 锁必须等待此表上的所有阻塞事务完成。 在等待期间，Sch-M 锁在访问同一表时阻止在此锁后等待的所有其他事务。 对本地临时表创建索引时，ONLINE 不能设置为 ON。  
  
> [!NOTE]  
>  联机索引重新生成可以设置*low_priority_lock_wait*此部分后面所述的选项。 *low_priority_lock_wait*期间联机索引重新生成管理 S 和 SCH-M 锁优先级。  
  
 OFF  
 在索引操作期间应用表锁。 这样可以防止所有用户在操作期间访问基础表。 创建、重新生成或删除聚集索引或者重新生成或删除非聚集索引的脱机索引操作将对表获取架构修改 (Sch-M) 锁。 这样可以防止所有用户在操作期间访问基础表。 创建非聚集索引的脱机索引操作将对表获取共享 (S) 锁。 这样可以防止更新基础表，但允许读操作（如 SELECT 语句）。  
  
 有关详细信息，请参阅[联机索引操作的工作原理](../../relational-databases/indexes/how-online-index-operations-work.md)。  
  
> [!NOTE]  
>  在 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的各版本中均不提供联机索引操作。 有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]各版本支持的功能列表，请参阅 [SQL Server 2016 各个版本支持的功能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)。  
  
 MAXDOP  **=**  *max_degree_of_parallelism*  
 **适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 重写**最大并行度**索引操作的持续时间的配置选项。 有关详细信息，请参阅 [配置 max degree of parallelism 服务器配置选项](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md)。 使用 MAXDOP 可以限制在执行并行计划的过程中使用的处理器数量。 最大数量为 64 个处理器。  
  
 *max_degree_of_parallelism*可以是：  
  
 - 1-取消生成并行计划。  
 - \>1-限制对指定数目的并行索引操作中使用的处理器最大数量。  
 - 0 （默认）-使用的实际处理器数或更少基于当前的系统工作负荷。  
  
 有关详细信息，请参阅 [配置并行索引操作](../../relational-databases/indexes/configure-parallel-index-operations.md)。  
  
> [!NOTE]  
>  并行索引操作不可用的每个版本[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]各版本支持的功能列表，请参阅 [SQL Server 2016 各个版本支持的功能](~/sql-server/editions-and-supported-features-for-sql-server-2016.md)。  
  
 DATA_COMPRESSION  
 **适用范围**： [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 为指定的表、分区号或分区范围指定数据压缩选项。 选项如下所示：  
  
 NONE  
 不压缩表或指定的分区。 仅适用于行存储表；不适用于列存储表。  
  
 ROW  
 使用行压缩来压缩表或指定的分区。 仅适用于行存储表；不适用于列存储表。  
  
 PAGE  
 使用页压缩来压缩表或指定的分区。 仅适用于行存储表；不适用于列存储表。  
  
 COLUMNSTORE  
 **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 仅适用于列存储表。 COLUMNSTORE 指定对使用 COLUMNSTORE_ARCHIVE 选项压缩的分区进行解压缩。 当还原数据后时，列存储索引将继续使用适用于所有列存储表的列存储压缩进行压缩。  
  
 COLUMNSTORE_ARCHIVE  
 **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 仅适用于列存储表，这是使用聚集列存储索引存储的表。 进一步 COLUMNSTORE_ARCHIVE 压缩的大小，指定的分区。 这可用于存档，或者用于要求更少存储并且可以付出更多时间来进行存储和检索的其他情形  
  
 有关压缩的详细信息，请参阅[数据压缩](../../relational-databases/data-compression/data-compression.md)。  
  
在分区上**(** { \<partition_number_expression > |\<范围 >}[ **,**... *n*  ] **)** **适用于**:[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]通过[!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 指定对其应用 DATA_COMPRESSION 设置的分区。 如果表未分区，ON PARTITIONS 自变量将生成错误。 如果未提供 ON PARTITIONS 子句，DATA_COMPRESSION 选项适用于已分区表的所有分区。  
  
\<partition_number_expression > 可以通过以下方式指定：  
  
-   提供该编号一个分区，例如： ON PARTITIONS (2)。  
-   提供若干单独分区的分区号并用逗号将它们隔开，例如：ON PARTITIONS (1, 5)。  
-   同时提供范围和单个分区，例如：ON PARTITIONS (2, 4, 6 TO 8)。  
  
\<范围 > 可以指定为分区号分隔逐字，例如： ON PARTITIONS (6 TO 8)。  
  
 若要为不同分区设置不同的数据压缩类型，请多次指定 DATA_COMPRESSION 选项，例如：  
  
```sql  
--For rowstore tables  
REBUILD WITH   
(  
DATA_COMPRESSION = NONE ON PARTITIONS (1),   
DATA_COMPRESSION = ROW ON PARTITIONS (2, 4, 6 TO 8),   
DATA_COMPRESSION = PAGE ON PARTITIONS (3, 5)  
)  
  
--For columnstore tables  
REBUILD WITH   
(  
DATA_COMPRESSION = COLUMNSTORE ON PARTITIONS (1, 3, 5),   
DATA_COMPRESSION = COLUMNSTORE_ARCHIVE ON PARTITIONS (2, 4, 6 TO 8)  
)  
```  
  
**\<single_partition_rebuild__option >**  
 在大多数情况下，重新生成索引将重新生成已分区索引的所有分区。 下面的选项在应用于单个分区时不会重新生成所有分区。  
  
-   SORT_IN_TEMPDB  
-   MAXDOP  
-   DATA_COMPRESSION  
  
**low_priority_lock_wait**  
 **适用范围**： [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 到 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]。  
  
 A**交换机**或联机索引重新生成只要此表没有阻塞操作完成。 *WAIT_AT_LOW_PRIORITY*指示，如果**交换机**或联机索引重新生成操作无法立即完成，再等待。 该操作包含低优先级锁，从而允许其他持有锁与 DDL 语句继续冲突的操作。 省略**等待在低优先级**选项等同于`WAIT_AT_LOW_PRIORITY ( MAX_DURATION = 0 minutes, ABORT_AFTER_WAIT = NONE)`。  
  
MAX_DURATION =*时间*[**分钟**]  
 在等待时间 （以分钟为单位指定的整数值），**交换机**或必须获取的联机索引重新生成锁等待执行 DDL 命令时。 SWITCH 或联机索引重新生成操作试图立即完成。 如果该操作被阻止的**MAX_DURATION**时间、 之一**ABORT_AFTER_WAIT**执行操作。 **MAX_DURATION**时间始终是以分钟和 word**分钟**可以省略。  
  
ABORT_AFTER_WAIT = [**NONE** | **自助** | **BLOCKERS** }]  
 无  
 继续**交换机**或联机索引重新生成操作，而无需更改 （使用正则优先级） 的锁优先级。  
  
SELF  
 退出**交换机**或联机索引重新生成 DDL 操作当前正在执行而不采取任何操作。  
  
BLOCKERS  
 将终止所有当前阻止的用户事务**交换机**或联机索引重新生成 DDL 操作，以便可以继续该操作。  
 阻止程序问题需要**ALTER ANY CONNECTION**权限。  
  
## <a name="remarks"></a>注释  
 索引选项的完整说明，请参阅[CREATE INDEX &#40;Transact SQL &#41;](../../t-sql/statements/create-index-transact-sql.md).  
  
## <a name="see-also"></a>另请参阅  
 [ALTER TABLE (Transact-SQL)](../../t-sql/statements/alter-table-transact-sql.md)   
 [column_constraint &#40;Transact SQL &#41;](../../t-sql/statements/alter-table-column-constraint-transact-sql.md)   
 [computed_column_definition &#40;Transact SQL &#41;](../../t-sql/statements/alter-table-computed-column-definition-transact-sql.md)   
 [table_constraint &#40;Transact SQL &#41;](../../t-sql/statements/alter-table-table-constraint-transact-sql.md)  
  
 

