---
title: 内存优化表的统计信息 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e644766d-1d1c-43d7-83ff-8ccfe4f3af9f
caps.latest.revision: 17
author: stevestein
ms.author: sstein
manager: jhubbard
ms.openlocfilehash: d4f9da688927d7e96ac2162eb504e0bc15f27526
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36016358"
---
# <a name="statistics-for-memory-optimized-tables"></a>内存优化表的统计信息
  查询优化器使用有关列的统计信息来创建可提高查询性能的查询计划。 从数据库中的表收集统计信息并将它保存在数据库元数据中。  
  
 统计信息自动创建，但也可以手动创建。 例如，在创建索引时自动对索引键列创建统计信息。 有关创建统计信息的详细信息，请参阅 [Statistics](../statistics/statistics.md)。  
  
 随着行的插入、更新和删除，表数据通常在一段时间后发生变化。 这意味着需要定期更新统计信息。 默认情况下，在优化器确定基于磁盘的表的统计信息可能过期时，自动更新它们。  
  
 默认情况下，不更新针对内存优化表的统计信息。 您需要手动更新它们。 使用[更新统计信息&#40;TRANSACT-SQL&#41; ](/sql/t-sql/statements/update-statistics-transact-sql)单个列、 索引或表。 使用[sp_updatestats &#40;TRANSACT-SQL&#41; ](/sql/relational-databases/system-stored-procedures/sp-updatestats-transact-sql)更新的所有用户和数据库中的内部表的统计信息。  
  
 使用时[CREATE STATISTICS &#40;TRANSACT-SQL&#41; ](/sql/t-sql/statements/create-statistics-transact-sql)或[更新统计信息&#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/update-statistics-transact-sql)，必须指定`NORECOMPUTE`若要禁用自动统计信息内存优化表的更新。 对于基于磁盘的表， [sp_updatestats &#40;TRANSACT-SQL&#41; ](/sql/relational-databases/system-stored-procedures/sp-updatestats-transact-sql)仅更新统计信息，如果表已被修改自上一个[sp_updatestats &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-updatestats-transact-sql)。 对于内存优化表， [sp_updatestats &#40;TRANSACT-SQL&#41; ](/sql/relational-databases/system-stored-procedures/sp-updatestats-transact-sql)始终生成更新的统计信息。 [sp_updatestats &#40;TRANSACT-SQL&#41; ](/sql/relational-databases/system-stored-procedures/sp-updatestats-transact-sql)是一个不错的选择为内存优化表; 否则，你需要知道哪些表有重大更改，因此你可以单独更新统计信息。  
  
 可以通过数据抽样或执行完全扫描生成统计信息。 抽样的统计信息只使用表数据的样本来估计数据分布情况。 完全扫描统计信息扫描整个表以确定数据分布情况。 完全扫描统计信息通常更为准确，但计算时间较长。 抽样的统计信息收集得更快。  
  
 默认情况下，基于磁盘的表使用抽样的统计信息。 内存优化的表仅支持完全扫描统计信息。 使用时[CREATE STATISTICS &#40;TRANSACT-SQL&#41; ](/sql/t-sql/statements/create-statistics-transact-sql)或[更新统计信息&#40;TRANSACT-SQL&#41;](/sql/t-sql/statements/update-statistics-transact-sql)，必须指定`FULLSCAN`选项用于内存优化表。  
  
 对于内存优化表的统计信息还有其他注意事项：  
  
-   使用该表创建内存优化的表的索引。 该表为空时，创建索引键列的统计信息。 因此，在将数据加载到表后，需要更新这些统计信息。  
  
-   对于本机编译的存储过程，在编译该过程时对过程中的查询的执行计划进行优化。 仅当创建该过程和服务器重新启动时才进行这样的优化，在更新统计信息时不进行优化。 因此，这些表需要包含数据的有代表性集且在创建过程前统计信息需要是最新的。 （如果数据库脱机并重新联机，或者如果发生服务器重新启动，将重新编译本机编译的存储过程。）  
  
## <a name="guidelines-for-statistics-when-deploying-memory-optimized-tables"></a>部署内存优化的表时统计信息的指南  
 要确保查询优化器在创建查询计划时具有最新统计信息，请执行以下五个步骤部署内存优化表：  
  
1.  创建表和索引。 索引是中的内联指定`CREATE TABLE`语句。  
  
2.  将数据加载到表。  
  
3.  更新表的统计信息。  
  
4.  创建访问表的存储过程。  
  
5.  运行工作负荷，本机编译的和解释可以包含多种[!INCLUDE[tsql](../../../includes/tsql-md.md)]存储过程，以及即席批处理。  
  
 在加载数据并更新统计信息后创建本机编译的存储过程可确保优化器为内存优化的表提供统计信息。 这将确保在编译过程时生成高效的查询计划。  
  
## <a name="guidelines-for-maintaining-statistics-on-memory-optimized-tables"></a>维护内存优化表的统计信息的指南  
 要保持统计信息最新，请定期更新内存优化表的统计信息。  
  
 如果数据频繁更改，应频繁更新统计信息。 例如，在批处理更新后更新表统计信息。 更新统计信息后，请删除并重新创建本机编译的存储过程，以便它们可以从更新的统计信息中受益。  
  
 实例时都提供 SQL Server 登录名。  
  
 不要在峰值工作负荷期间更新统计信息。  
  
 要更新统计信息：  
  
-   使用[!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]到[创建维护计划](../maintenance-plans/create-a-maintenance-plan.md)与[更新统计信息任务](../maintenance-plans/update-statistics-task-maintenance-plan.md)  
  
-   或如下所述通过 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 脚本更新统计信息。  
  
 若要更新单个内存优化表的统计信息 (*myschema*。 *Mytable*)，运行以下脚本：  
  
```  
UPDATE STATISTICS myschema.Mytable WITH FULLSCAN, NORECOMPUTE  
```  
  
 要更新当前数据库中所有内存优化表的统计信息，请运行以下脚本：  
  
```tsql  
DECLARE @sql NVARCHAR(MAX) = N''  
  
SELECT @sql += N'  
   UPDATE STATISTICS ' + quotename(schema_name(schema_id)) + N'.' + quotename(name) + N' WITH FULLSCAN, NORECOMPUTE'  
FROM sys.tables WHERE is_memory_optimized=1  
  
EXEC sp_executesql @sql  
```  
  
 若要更新数据库中的所有表的统计信息，请运行[sp_updatestats &#40;TRANSACT-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-updatestats-transact-sql)。  
  
 下面的示例报告有关内存优化表的统计信息上次是在何时更新的。 此信息可帮助您决定是否需要更新统计信息。  
  
```tsql  
select t.object_id, t.name, sp.last_updated as 'stats_last_updated'  
from sys.tables t join sys.stats s on t.object_id=s.object_id cross apply sys.dm_db_stats_properties(t.object_id, s.stats_id) sp  
where t.is_memory_optimized=1  
```  
  
## <a name="see-also"></a>请参阅  
 [内存优化表](memory-optimized-tables.md)  
  
  
