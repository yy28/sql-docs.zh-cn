---
title: 自动优化 |Microsoft 文档
description: 了解有关在 SQL Server 和 Azure SQL 数据库的自动调整
ms.custom: ''
ms.date: 08/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: automatic-tuning
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- performance tuning [SQL Server]
ms.assetid: ''
caps.latest.revision: ''
author: jovanpop-msft
ms.author: jovanpop
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2017 || = sqlallproducts-allversions
ms.openlocfilehash: de3984b5005114a2b8644c99706dcce48ab873e0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="automatic-tuning"></a>自动优化
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

  自动优化是一种数据库功能，提供对潜在查询性能问题的深入了解、提出建议解决方案并自动解决已标识的问题。

自动优化[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]会通知你每当潜在的性能问题检测到，并且使你能够应用的纠正措施，或允许[!INCLUDE[ssde_md](../../includes/ssde_md.md)]自动修复性能问题。
自动优化[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]使您能够确定并修复性能问题所致**SQL 计划选择回归**。 自动优化[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]创建必要的索引而删除未使用的索引。

[!INCLUDE[ssde_md](../../includes/ssde_md.md)] 监视数据库上执行，会自动提高工作负荷的性能的查询。 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 具有内置智能机制，可以自动优化并通过动态调整数据库添加到你的工作负荷来提高查询性能。 有两个可用的自动优化功能：

 -  **自动计划更正**(位于[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]和[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)])，用于标识有问题的查询执行计划并修复 SQL 计划性能问题。
 -  **自动索引管理**(仅适用于[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)])，它标识应在数据库中，添加的索引和应删除的索引。

## <a name="why-automatic-tuning"></a>为什么自动优化？

在经典的数据库管理的主要任务之一监视工作负荷，标识关键[!INCLUDE[tsql_md](../../includes/tsql_md.md)]查询时，应添加以提高性能，并且很少使用的索引的索引。 [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 提供详细地了解查询和你需要监视的索引。 但是，持续监视数据库是硬且单调乏味任务，尤其是在处理多个数据库。 管理大量数据库可能无法有效地执行操作。 而不是监视和手动优化你的数据库，则可以考虑委派某些监视和优化操作到[!INCLUDE[ssde_md](../../includes/ssde_md.md)]使用自动优化功能。

### <a name="how-does-automatic-tuning-works"></a>原理自动优化的工作原理是什么？

自动优化是连续的监视和不断地知道你的工作负荷的特征的分析过程，并确定潜在的问题和改进。

![自动优化进程](./media/tuning-process.png)

此过程使动态地适应你的工作负荷通过查找哪些索引和计划可能会提高工作负荷的性能和哪些索引会影响你的工作负荷的数据库。 根据这些结果，自动优化适用提高你的工作负荷的性能的优化操作。 此外，数据库持续监视以确保它可以提高工作负荷的性能的自动优化所做任何更改后的性能。 自动还原的任何操作都未提高性能。 此验证过程是一项重要功能，以确保任何的自动优化所做的更改不会降低你的工作负荷的性能。

## <a name="automatic-plan-correction"></a>自动计划更正

自动计划更正方法是一种自动的优化功能用于标识**SQL 计划选择回归**并自动修复该问题，通过强制最后一个已知良好的计划。

### <a name="what-is-sql-plan-choice-regression"></a>什么是 SQL 计划选择回归？

[!INCLUDE[ssdenoversion_md](../../includes/ssdenoversion_md.md)] 可能使用不同的 SQL 计划来执行[!INCLUDE[tsql_md](../../includes/tsql_md.md)]查询。 查询计划取决于统计信息、 索引和其他因素。 应该用于执行一些的最优计划[!INCLUDE[tsql_md](../../includes/tsql_md.md)]查询可能随时间推移进行更改。 在某些情况下，新的计划可能不好于前一个，而新的计划可能会导致性能回归。

 ![SQL 计划选择回归](media/plan-choice-regression.png "SQL 计划选择回归") 

每当你注意到计划选择回归，你应会发现一些以前良好计划和强制而不是当前的一个使用`sp_query_store_force_plan`过程。
[!INCLUDE[ssde_md](../../includes/ssde_md.md)] 在[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]提供有关回归计划和建议的纠正措施的信息。
此外， [!INCLUDE[ssde_md](../../includes/ssde_md.md)] ，可完全自动执行此过程，并让[!INCLUDE[ssde_md](../../includes/ssde_md.md)]修复发现的任何问题与计划更改相关的。

### <a name="automatic-plan-choice-correction"></a>自动计划选择更正

[!INCLUDE[ssde_md](../../includes/ssde_md.md)] 可以自动切换到最后一个已知良好的计划，每当检测到计划选择回归。

![SQL 计划选择更正](media/force-last-good-plan.png "SQL 计划选择更正") 

[!INCLUDE[ssde_md](../../includes/ssde_md.md)] 自动检测到任何潜在的计划选择回归，其中包括应使用而不是错误的计划的计划。
当[!INCLUDE[ssde_md](../../includes/ssde_md.md)]适用最后一个已知的很好的计划，自动监视强制计划的性能。 如果强制的计划不是回归计划更好的新的计划将 unforced 和[!INCLUDE[ssde_md](../../includes/ssde_md.md)]将编译新的计划。 如果[!INCLUDE[ssde_md](../../includes/ssde_md.md)]验证强制的计划是回归的一个更好，强制的计划则会保留之前 （例如，在下一次的统计信息或架构更改） 重新编译优于回归的计划。

注意： 强制任何计划自动执行不 persit 上重新启动 SQL Server 实例。

### <a name="enabling-automatic-plan-choice-correction"></a>启用自动计划选择更正

可以针对每个数据库启用自动优化，并指定在每次检测到某些计划更改回归时强制使用最近一个良好计划。 使用以下命令启用自动优化：

```sql   
ALTER DATABASE current
SET AUTOMATIC_TUNING ( FORCE_LAST_GOOD_PLAN = ON ); 
```
一旦你启用此选项，[!INCLUDE[ssde_md](../../includes/ssde_md.md)]将会自动强制估计的 CPU 提升高于 10 秒，或在新的计划中的错误数高于建议计划中的错误数的位置的任何建议，并验证强制的计划是当前的一个更好。

### <a name="alternative---manual-plan-choice-correction"></a>替代项-手动计划选择更正

若不使用自动优化，用户必须定期监视系统并查找回归的查询。 如果任何计划回归，用户应发现一些以前良好计划和强制而不是当前的一个使用`sp_query_store_force_plan`过程。 最佳做法是以强制最后一个已知良好的计划，因为旧计划也可能是由于统计信息或索引的更改无效。 强制最后一个已知的良好计划的用户应监视使用强制的计划执行的查询性能，并验证该强制的计划按预期方式工作。 具体取决于监视和分析的结果，应强制计划或用户应找出某些其他方法来优化查询。
因为，手动强制的计划应不永久，强制[!INCLUDE[ssde_md](../../includes/ssde_md.md)]应该能够应用最佳计划。 用户或 DBA 应最终取消强制执行计划使用`sp_query_store_unforce_plan`过程中，并让[!INCLUDE[ssde_md](../../includes/ssde_md.md)]查找最佳计划。

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供所有必要的视图和监视性能和查询存储区中解决问题所需的过程。

在[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)]，你可以找到使用查询存储系统视图的计划选择回归。 在[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]、[!INCLUDE[ssde_md](../../includes/ssde_md.md)]检测并演示了潜在计划选择回归并建议应在应用的操作[sys.dm_db_tuning_recommendations &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-db-tuning-recommendations-transact-sql.md)视图。 该视图显示有关问题，例如标识查询，回归计划的 ID、 已用作基线进行比较，计划的 ID 的详细信息以及问题的重要性的信息和[!INCLUDE[tsql_md](../../includes/tsql_md.md)]可以执行以修复语句问题。

| type | description | datetime | score | 详细信息 | … |
| --- | --- | --- | --- | --- | --- |
| `FORCE_LAST_GOOD_PLAN` | 从 4 ms 更改为 14 ms 的 CPU 时间 | 3/17/2017 | 83 | `queryId` `recommendedPlanId` `regressedPlanId` `T-SQL` |   |
| `FORCE_LAST_GOOD_PLAN` | 从 37 ms 更改为 84 ms 的 CPU 时间 | 3/16/2017 | 26 | `queryId` `recommendedPlanId` `regressedPlanId` `T-SQL` |   |

此视图中的某些列以下列表所示：
 - 类型的建议的操作- `FORCE_LAST_GOOD_PLAN`。
 - 为什么包含信息的说明[!INCLUDE[ssde_md](../../includes/ssde_md.md)]认为此计划更改为潜在的性能回归。
 - 检测到潜在回归时的日期时间。
 - 此建议的分数。 
 - 有关检测到的计划中，回归计划，请解决问题，应强制计划 ID。 ID。 ID 如问题的详细信息 [!INCLUDE[tsql_md](../../includes/tsql_md.md)]
 可能用于修复问题等的脚本。详细信息存储在[JSON 格式](../../relational-databases/json/index.md)。

使用以下查询以获取修复的问题和其他信息的预计脚本获得：

```sql   
SELECT reason, score,
      script = JSON_VALUE(details, '$.implementationDetails.script'),
      planForceDetails.*,
      estimated_gain = (regressedPlanExecutionCount+recommendedPlanExecutionCount)
                  *(regressedPlanCpuTimeAverage-recommendedPlanCpuTimeAverage)/1000000,
      error_prone = IIF(regressedPlanErrorCount>recommendedPlanErrorCount, 'YES','NO')
FROM sys.dm_db_tuning_recommendations
  CROSS APPLY OPENJSON (Details, '$.planForceDetails')
    WITH (  [query_id] int '$.queryId',
            [current plan_id] int '$.regressedPlanId',
            [recommended plan_id] int '$.recommendedPlanId',

            regressedPlanErrorCount int,
            recommendedPlanErrorCount int,

            regressedPlanExecutionCount int,
            regressedPlanCpuTimeAverage float,
            recommendedPlanExecutionCount int,
            recommendedPlanCpuTimeAverage float

          ) as planForceDetails;
```

[!INCLUDE[ssresult-md](../../includes/ssresult-md.md)]     

| reason | score | 脚本 (script) | 查询\_id | 当前计划\_id | 建议计划\_id | 估计\_获得 | 错误\_容易
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 从 3 ms 更改为 46 ms 的 CPU 时间 | 36 | EXEC sp\_查询\_存储\_强制\_计划 12，17; | 12 | 28 | 17 | 11.59 | 0

`estimated_gain` 表示的估计如果建议的计划将执行而不是当前的计划将保存的秒数。 建议的计划应强制而不是当前的计划，如果提升大于 10 秒。 如果有多个错误 （例如，超时或已中止的执行） 比当前计划中建议的计划，列`error_prone`将设置为值`YES`。 错误容易计划是为什么建议的计划应强制而不是当前的另一个原因。

尽管[!INCLUDE[ssde_md](../../includes/ssde_md.md)]提供标识计划选择回归; 连续监视和修复性能问题所需的所有信息可能都是一个乏味的过程。 自动优化可使此过程要容易得多。

注意： 此 DMV 中的数据后重新启动 SQL Server 实例不保留。

## <a name="automatic-index-management"></a>自动索引管理

在[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]，索引管理很容易因为[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]了解有关你的工作负荷，并确保你的数据始终以最佳方式编制索引。 正确的索引的设计必须让您的工作负荷的最佳性能，且自动索引管理可帮助你优化你的索引。 自动索引管理可以是在未正确索引数据库中，修复性能问题或维护和改进对现有的数据库架构的索引。 自动优化[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]执行下列操作：

 - 标识可能会提高性能的表中读取数据的 T-SQL 查询的索引。
 - 标识的冗余索引或索引中可能删除的时间段内未使用。 删除不必要的索引可以提高性能的查询的表中更新数据。

### <a name="why-do-you-need-index-management"></a>为什么需要索引管理？

索引加快某些表; 中读取数据的查询但是，它们将减缓更新数据的查询。 需要仔细分析何时创建索引和哪些列需要包含在索引。 某些索引可能不需要一段时间后。 因此，你将需要定期标识并删除不带来任何好处的索引。 如果您忽略未使用的索引，则更新数据的查询性能会降低而没有一点好处上读取数据的查询。 未使用的索引也会影响系统的整体性能，因为其他更新需要不必要的日志记录。

查找索引可提高性能的查询的从表读取数据并对更新的影响最小的优化集可能需要连续且复杂的分析。

[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] 使用内置智能和分析你的查询的高级的规则确定索引，它将是最适合你当前的工作负荷，并可能会删除索引。 Azure SQL 数据库可确保你能够优化读取数据，与对其他查询的最小化影响查询的索引的最小必要集。

### <a name="automatic-index-management"></a>自动索引管理

除了检测，[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]如何自动将应用标识的建议。 如果您发现的内置规则提高你的数据库的性能，你可能会让[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]自动管理你的索引。

若要使 Azure SQL 数据库中的自动优化，并使自动完全管理工作负荷的优化功能，请参阅[启用 Azure SQL 数据库使用 Azure 门户中的自动调整](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-automatic-tuning-enable)。

当[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]适用创建索引或删除索引建议，它会自动监视受索引的查询的性能。 仅当受影响的查询的性能也得到了改进，将保留新的索引。 如果某些由于缺少的索引，因此运行较慢的查询，将自动重新创建删除的索引。

### <a name="automatic-index-management-considerations"></a>自动索引管理注意事项

创建必要的索引，在所需的操作[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]可能会消耗资源并暂时影响工作负荷性能。 索引创建对工作负荷性能的影响降至最低，Azure SQL 数据库时，可查找适当的时间窗口的任何索引管理操作。 优化操作是推迟如果数据库需要的资源来执行你的工作负荷，当并启动数据库是否拥有足够的未使用的资源可用于维护任务。 在自动索引管理中的一个重要功能是操作的验证。 当 Azure SQL 数据库创建或删除索引时，监视的进程将分析的工作负载以验证操作改进的性能的性能。 如果它未将置于重大进步 – 操作立即还原。 这种方式，Azure SQL Database 可以确保自动操作不会对你的工作负荷的性能产生负面影响。 创建通过自动优化的索引都是透明在基础架构上执行维护操作。 架构更改如删除或重命名列不阻止的自动创建的索引的状态。 自动创建的 Azure SQL 数据库的索引将立即删除时相关的已删除表或列。

### <a name="alternative---manual-index-management"></a>替代项-手动索引管理

不自动索引管理，用户将需要手动查询[sys.dm_db_missing_index_details &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-details-transact-sql.md)视图以查找索引可能会提高性能，请创建索引使用的详细信息此视图，和手动查询性能监视器中提供。 为了找到应删除的索引，用户应监视极少数情况下使用的查找索引的索引操作的使用情况统计的信息。

[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] 可以简化此过程。 [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] 分析你的工作负荷，标识无法使用新索引时，更快地执行的查询并确定未使用或重复的索引。 查找有关应在更改的索引标识的详细信息[在 Azure 门户中查找索引建议](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-advisor-portal)。

## <a name="see-also"></a>另请参阅  
 [ALTER 数据库集 AUTOMATIC_TUNING &#40;Transact SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [sys.database_automatic_tuning_options &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/sys-database-automatic-tuning-options-transact-sql.md)  
 [sys.dm_db_tuning_recommendations &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-tuning-recommendations-transact-sql.md)   
 [sys.dm_db_missing_index_details &#40;Transact SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-details-transact-sql.md)   
 [sp_query_store_force_plan &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-force-plan-transact-sql.md)     
 [sp_query_store_unforce_plan &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-unforce-plan-transact-sql.md)           
 [sys.database_query_store_options &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [JSON 函数](../../relational-databases/json/index.md)
