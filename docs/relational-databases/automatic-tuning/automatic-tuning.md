---
title: 自动优化 |Microsoft Docs
description: 了解如何在 SQL Server 和 Azure SQL 数据库自动优化
ms.custom: ''
ms.date: 08/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- performance tuning [SQL Server]
ms.assetid: ''
author: jovanpop-msft
ms.author: jovanpop
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a196ef879c176fe731fe85b2de7962d70edff7b4
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/28/2018
ms.locfileid: "52541175"
---
# <a name="automatic-tuning"></a>自动优化
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

自动优化是一种数据库功能，提供对潜在查询性能问题的深入了解、提出建议解决方案并自动解决已标识的问题。

[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] 中的自动优化功能可在检测到潜在性能问题时发出通知，并允许你实施修正措施或使[!INCLUDE[ssde_md](../../includes/ssde_md.md)]自动修复性能问题。
中的自动优化[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]使您能够识别并修复性能问题所致**查询执行计划选择回归**。 中的自动优化[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]还会创建必要的索引并删除未使用的索引。 有关查询执行计划的详细信息，请参阅[执行计划](../../relational-databases/performance/execution-plans.md)。

[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]监视器上，对数据库和自动执行的查询可以提高工作负荷的性能。 [!INCLUDE[ssde_md](../../includes/ssde_md.md)]具有内置智能机制，可以自动优化和提高查询性能的动态适应工作负荷的数据库。 有可用的两个自动优化功能：

 -  **自动计划更正**标识有问题的查询执行计划并修复查询执行计划性能问题。 **适用对象**：[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (从开始[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]) 和 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]
 -  **自动索引管理**标识应在数据库中，添加的索引以及应删除的索引。 适用于：[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

## <a name="why-automatic-tuning"></a>为什么自动优化？

三个经典数据库管理的主要任务监视工作负荷，识别关键[!INCLUDE[tsql_md](../../includes/tsql-md.md)]查询时，添加了以提高性能，并标识应为很少使用的索引。 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]提供的查询和索引需要监视的详细的见解。 但是，持续监视数据库是一个艰巨且乏味的任务，尤其是在处理多个数据库。 管理大量的数据库可能无法高效地完成。 而不是手动监视和优化你的数据库，可以考虑委派某些监视和优化操作[!INCLUDE[ssde_md](../../includes/ssde_md.md)]使用自动优化功能。

### <a name="how-does-automatic-tuning-work"></a>自动优化工作原理？

自动优化是一种持续监视和不断学习的特征的工作负荷的分析过程和识别潜在的问题和改进。

![自动优化过程](./media/tuning-process.png)

此过程使数据库能够动态地适应你的工作负荷通过查找哪些索引和计划可能会提高性能的工作负荷和哪些索引会影响工作负荷。 根据这些结果，自动优化应用优化操作可提高性能的工作负荷。 此外，数据库持续监视进行的自动优化，以确保它可以提高工作负荷性能的任何更改后的性能。 未提高性能的任何操作都将自动还原。 此验证过程是一项重要功能，以确保自动优化做出任何更改不会降低工作负荷的性能。

## <a name="automatic-plan-correction"></a>自动计划更正

自动计划更正是一种自动优化功能，用于标识**执行计划选择回归**自动强制将最后一个已知完好的计划，从而解决该问题。 有关查询执行计划和查询优化器的详细信息，请参阅[查询处理体系结构指南](../../relational-databases/query-processing-architecture-guide.md)。

### <a name="what-is-execution-plan-choice-regression"></a>执行计划选择回归是什么？

[!INCLUDE[ssdenoversion_md](../../includes/ssdenoversion_md.md)]可能会使用不同的执行计划来执行[!INCLUDE[tsql_md](../../includes/tsql-md.md)]查询。 查询计划取决于统计信息、 索引和其他因素。 应该用于执行某些的最优计划[!INCLUDE[tsql_md](../../includes/tsql-md.md)]查询可能会随着时间的推移发生更改。 在某些情况下，新的计划不能比以前更好，新的计划可能会导致性能回归。

 ![查询执行计划选择回归](media/plan-choice-regression.png "查询执行计划选择回归") 

每当您注意到计划选择回归，您会发现一些以前的良好计划，并强制而不是当前的一个使用`sp_query_store_force_plan`过程。
[!INCLUDE[ssde_md](../../includes/ssde_md.md)] 在[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]提供有关回归计划和建议的纠正操作的信息。
此外，[!INCLUDE[ssde_md](../../includes/ssde_md.md)]使您能够完全自动执行此过程，让[!INCLUDE[ssde_md](../../includes/ssde_md.md)]修复发现的任何问题的计划更改。

### <a name="automatic-plan-choice-correction"></a>自动计划选择更正

[!INCLUDE[ssde_md](../../includes/ssde_md.md)] 可以自动切换到最后一个已知完好的计划，每当检测到计划选择回归。

![查询执行计划选择更正](media/force-last-good-plan.png "查询执行计划选择更正") 

[!INCLUDE[ssde_md](../../includes/ssde_md.md)] 会自动检测任何潜在的计划选择回归，包括应使用而不是错误的计划的计划。
当[!INCLUDE[ssde_md](../../includes/ssde_md.md)]应用最近一个其已知的良好计划，会自动监视强制计划的性能。 如果不强制的计划优于回归计划，新计划将取消强制和[!INCLUDE[ssde_md](../../includes/ssde_md.md)]将编译新计划。 如果[!INCLUDE[ssde_md](../../includes/ssde_md.md)]验证强制的计划优于回归计划，将保留强制的计划，如果它是优于回归计划，直到重新编译发生 （例如，在下一次统计信息更新或架构更改）。

> [!NOTE]
> 不会强制任何执行计划自动保留的重启之间[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例。

### <a name="enabling-automatic-plan-choice-correction"></a>启用自动计划选择更正

可以针对每个数据库启用自动优化，并指定在每次检测到某些计划更改回归时强制使用最近一个良好计划。 使用以下命令启用自动优化：

```sql   
ALTER DATABASE current
SET AUTOMATIC_TUNING ( FORCE_LAST_GOOD_PLAN = ON ); 
```

一旦启用此选项，[!INCLUDE[ssde_md](../../includes/ssde_md.md)]将会自动强制执行任何建议估计的 CPU 性能提升超过 10 秒，或在新的计划中的错误数高于建议计划中的错误数，并验证强制的计划优于当前。

### <a name="alternative---manual-plan-choice-correction"></a>替代项-手动计划选择更正

若不使用自动优化，用户必须定期监视系统并查找回归的查询。 如果任何计划回归，用户应找到某些以前的良好计划，并强制而不是当前的一个使用`sp_query_store_force_plan`过程。 最佳做法是强制实施最后一个已知完好的计划，因为较旧的计划也可能是由于统计信息或索引的更改无效。 强制最后一个已知完好的计划的用户应监视使用强制的计划执行的查询的性能，并验证该强制的计划按预期方式工作。 具体取决于监视和分析结果，应强制执行计划，或用户应找到通过其他方式来优化查询。
手动强制执行的计划不应被强迫下去，因为[!INCLUDE[ssde_md](../../includes/ssde_md.md)]应该能够应用最佳计划。 用户或数据库管理员应最终取消强制执行计划使用`sp_query_store_unforce_plan`过程中，并让[!INCLUDE[ssde_md](../../includes/ssde_md.md)]找到最佳的计划。 

> [!TIP]
> Alternativelly，使用**强制计划与查询**Query Store 视图来查找和取消强制执行计划。

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提供所有必要的视图和监视性能和查询存储中解决问题所需的过程。

在[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)]，可以找到计划选择回归使用查询存储系统视图。 在中[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]，则[!INCLUDE[ssde_md](../../includes/ssde_md.md)]检测并显示潜在的计划选择回归并建议应在应用的操作[sys.dm_db_tuning_recommendations &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-db-tuning-recommendations-transact-sql.md)视图。 该视图显示有关问题、 问题和详细信息，例如确定查询回归计划的 ID，用作比较基准进行比较，计划的 ID 的重要性和[!INCLUDE[tsql_md](../../includes/tsql-md.md)]语句可以执行以修复出现问题。

| type | description | DATETIME | score | 详细信息 | ... |
| --- | --- | --- | --- | --- | --- |
| `FORCE_LAST_GOOD_PLAN` | 从 4 毫秒更改为 14 毫秒的 CPU 时间 | 3/17/2017 | 83 | `queryId` `recommendedPlanId` `regressedPlanId` `T-SQL` |   |
| `FORCE_LAST_GOOD_PLAN` | 从 37 ms 更改为 84 毫秒的 CPU 时间 | 3/16/2017 | 26 | `queryId` `recommendedPlanId` `regressedPlanId` `T-SQL` |   |

以下列表中描述了此视图中的某些列：
 - 建议的操作的类型 `FORCE_LAST_GOOD_PLAN`
 - 为什么要包含的信息的说明[!INCLUDE[ssde_md](../../includes/ssde_md.md)]认为此计划更改是一个潜在的性能回归
 - 检测到潜在回归时的日期时间
 - 此建议的分数
 - 有关检测到的计划回归计划修复该问题，应强制计划的 ID 的 ID 的 ID 等问题的详细信息[!INCLUDE[tsql_md](../../includes/tsql-md.md)]脚本可能会应用若要修复的问题，等等。详细信息存储在[JSON 格式](../../relational-databases/json/index.md)

使用以下查询以获取修复的问题和其他信息的估计脚本获得：

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
| 从 3 毫秒更改为 46 毫秒的 CPU 时间 | 36 | EXEC sp\_查询\_存储\_强制\_计划 12，17; | 12 | 28 | 17 | 11.59 | 0

`estimated_gain` 表示的估计如果建议的计划将执行而不是当前计划将保存的秒数。 如果性能提升超过 10 秒，则应而不是当前的计划强制执行建议的计划。 如果有更多的错误 （例如，超时或已中止的执行） 比当前计划中推荐的计划，列`error_prone`将设置为值`YES`。 错误容易计划是为什么建议应强制执行计划，而不是当前的另一个原因。

尽管[!INCLUDE[ssde_md](../../includes/ssde_md.md)]提供标识计划选择回归; 持续监视和修复性能问题所需的所有信息可能都是一个乏味的过程。 自动优化让这一过程容易得多。

> [!NOTE]
> Sys.dm_db_tuning_recommendations DMV 中的数据不会保留的重启之间[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例。

## <a name="automatic-index-management"></a>自动索引管理

在中[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]，索引管理很容易，因为[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]了解工作负荷，并确保你的数据始终以最佳方式编制索引。 正确的索引设计是工作负荷的最佳性能的关键在于，自动索引管理可帮助您优化索引。 自动索引管理可以修复未正确编制索引的数据库中的性能问题或维护并改进现有数据库架构的索引。 中的自动优化[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]将执行以下操作：

 - 标识可能会提高性能的索引在[!INCLUDE[tsql_md](../../includes/tsql-md.md)]从表中读取数据的查询。
 - 标识冗余的索引或未使用的可能删除的时间段内的索引。 删除不必要的索引可以提高性能的查询以便更新表中的数据。

### <a name="why-do-you-need-index-management"></a>为什么需要索引管理？

索引能加速某些从表中读取数据的查询；但是，索引会减慢更新数据的查询。 需要仔细分析何时创建索引，以及哪些列需要包含在索引中。 某些索引可能在一段时间后便不再需要。 因此，需要定期识别并删除没有任何益处的索引。 如果忽略未使用的索引，用于更新数据的查询的性能将会降低，并且对用于读取数据的查询没有任何益处。 未使用的索引还会影响系统的整体性能，因为其他更新需要不必要的日志记录。

查找索引可提高性能的查询，从你的表中读取数据并对更新的最小影响的最佳集合可能需要持续进行复杂分析。

[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] 使用内置智能和分析你的查询的高级的规则确定将是最适合于你当前的工作负荷的索引和索引可能会被删除。 Azure SQL 数据库可确保您具有需要少量的优化读取数据，而对其他查询的影响降至最低的查询的索引。

### <a name="automatic-index-management"></a>自动索引管理

除了检测，[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]可以自动应用标识的建议。 如果您发现该内置规则提高数据库性能，你可能会用[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]自动管理索引。

若要启用中的自动优化[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]并允许自动优化功能完全管理你的工作负荷，请参阅[启用 Azure SQL 数据库使用 Azure 门户中的自动优化](/azure/sql-database/sql-database-automatic-tuning-enable)。

当[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]应用创建索引或删除索引建议，会自动监视索引影响的查询的性能。 仅当受影响的查询的性能也得到了改进，将保留新的索引。 如果有一些查询，用于运行较慢，由于没有索引，将自动重新创建删除的索引。

### <a name="automatic-index-management-considerations"></a>自动索引管理注意事项

若要创建必要索引中的所需的操作[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]可能会消耗资源并暂时影响工作负荷的性能。 索引创建对工作负荷性能的影响降至最低[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]为任何索引管理操作找到适当的时间窗口。 优化操作是推迟如果数据库需要资源来执行工作负荷，并启动时在数据库有足够可用于维护任务的未使用的资源。 自动索引管理中的一个重要功能是验证操作。 当[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]创建或删除索引，监视进程将分析工作负荷，以验证操作性能提升了性能。 如果它没有带来显著的改进-立即还原操作。 这样一来，[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]可确保自动操作不会对工作负荷的性能产生负面影响。 创建的自动优化索引是透明的基础架构上执行维护操作。 架构更改，例如删除或重命名列不会阻止通过自动创建的索引存在。 会自动创建的索引[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]立即时是否删除相关的已删除表或列。

### <a name="alternative---manual-index-management"></a>替代项-手动索引管理

不自动索引管理，用户将需要手动查询[sys.dm_db_missing_index_details &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-details-transact-sql.md)视图，以查找索引可能会提高性能，请创建索引使用的详细信息此视图中，以及手动监视性能的查询中提供。 若要查找应删除的索引，用户应监视很少使用的查找索引的索引操作的使用情况统计的信息。

[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] 可以简化此过程。 [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] 分析工作负荷，标识无法与新的索引，更快地执行的查询，并确定未使用或重复的索引。 查找有关标识应在进行更改的索引的详细信息[Azure 门户中查找索引建议](https://docs.microsoft.com/azure/sql-database/sql-database-advisor-portal)。

## <a name="see-also"></a>请参阅  
 [ALTER DATABASE SET AUTOMATIC_TUNING &#40;Transact SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [sys.database_automatic_tuning_options &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-automatic-tuning-options-transact-sql.md)  
 [sys.dm_db_tuning_recommendations &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-tuning-recommendations-transact-sql.md)   
 [sys.dm_db_missing_index_details &#40;TRANSACT-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-details-transact-sql.md)   
 [sp_query_store_force_plan &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-force-plan-transact-sql.md)     
 [sp_query_store_unforce_plan &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-unforce-plan-transact-sql.md)           
 [sys.database_query_store_options &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [JSON 函数](../../relational-databases/json/index.md)    
 [执行计划](../../relational-databases/performance/execution-plans.md)    
 [监视和优化性能](../../relational-databases/performance/monitor-and-tune-for-performance.md)     
 [性能监视和优化工具](../../relational-databases/performance/performance-monitoring-and-tuning-tools.md)     
 [使用查询存储来监视性能](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)  
 [查询优化助手](../../relational-databases/performance/upgrade-dbcompat-using-qta.md)
