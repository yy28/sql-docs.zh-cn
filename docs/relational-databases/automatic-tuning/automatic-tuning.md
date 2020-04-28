---
title: 自动优化 |Microsoft Docs
description: 了解 SQL Server 和 Azure SQL 数据库中的自动优化
ms.custom: fasttrack-edit
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
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5ce830c3fcd5661a01ecc0ad3ad84bed420be2e0
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "82107979"
---
# <a name="automatic-tuning"></a>自动优化
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

自动优化是一种数据库功能，提供对潜在查询性能问题的深入了解、提出建议解决方案并自动解决已标识的问题。

当检测到[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]潜在性能问题时，自动优化就会通知你，并使你能够应用纠正措施， [!INCLUDE[ssde_md](../../includes/ssde_md.md)]或让你能够自动修复性能问题。 使用中的[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]自动优化，可以确定并修复**查询执行计划选择回归**导致的性能问题。 自动优化[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]还会创建必要的索引并删除未使用的索引。 有关查询执行计划的详细信息，请参阅[执行计划](../../relational-databases/performance/execution-plans.md)。

[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]监视在数据库上执行的查询，并自动提高工作负荷的性能。 [!INCLUDE[ssde_md](../../includes/ssde_md.md)]具有内置的智能机制，可通过动态调整数据库以适应工作负荷，自动优化和提高查询的性能。 有两种自动优化功能可用：

 -  **自动计划更正**：标识有问题的查询执行计划，并修复查询执行计划性能问题。 **适用对象**：[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]（从 [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] 开始）和 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]
 -  **自动索引管理**标识应在数据库中添加的索引以及应删除的索引。 适用于  ：[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]

## <a name="why-automatic-tuning"></a>为什么启用自动优化？

经典数据库管理中的三个主要任务是监视工作负荷，确定关键[!INCLUDE[tsql_md](../../includes/tsql-md.md)]查询，并确定应该添加的索引以提高性能，或者使用不太常用的索引，并可以删除这些索引以提高性能。 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]提供对需要监视的查询和索引的详细见解。 然而，持续监视数据库是一项艰巨且乏味的任务，尤其是在处理多个数据库时。 可能无法高效管理大量数据库。 你可以考虑[!INCLUDE[ssde_md](../../includes/ssde_md.md)]使用自动优化功能将某些监视和优化操作委派给，而不是手动监视和优化数据库。

### <a name="how-does-automatic-tuning-work"></a>自动优化的工作原理是什么？

自动优化是一种持续监视和分析过程，可不断了解工作负荷的特征并识别潜在问题和改进。

![自动优化过程](./media/tuning-process.png)

此过程使数据库能够通过查找哪些索引和计划可提高工作负荷的性能以及哪些索引会影响工作负荷，从而动态适应工作负荷。 根据这些发现，自动优化应用优化操作，提高工作负荷的性能。 此外，自动优化在实现任何更改后会持续监视数据库的性能，以确保它可提高工作负荷的性能。 将会自动还原对改进性能无补的任何操作。 此验证过程是一项关键功能，可确保自动优化所做的任何更改不会降低工作负荷的整体性能。

## <a name="automatic-plan-correction"></a>自动计划更正

自动计划更正是一种自动优化功能，用于识别**执行计划选择回归**，并通过强制使用最近一次正确的计划来自动解决问题。 有关查询执行计划和查询优化器的详细信息，请参阅[查询处理体系结构指南](../../relational-databases/query-processing-architecture-guide.md)。

### <a name="what-is-execution-plan-choice-regression"></a>执行计划的选择回归是什么？

[!INCLUDE[ssdenoversion_md](../../includes/ssdenoversion_md.md)]可能使用不同的执行计划来执行[!INCLUDE[tsql_md](../../includes/tsql-md.md)]查询。 查询计划取决于统计信息、索引和其他因素。 应该用于执行[!INCLUDE[tsql_md](../../includes/tsql-md.md)]查询的最佳计划可能会随时间的变化而变化。 在某些情况下，新计划可能不比上一个计划好，新计划可能会导致性能下降。

 ![查询执行计划选择回归](media/plan-choice-regression.png "查询执行计划选择回归") 

每当你注意到计划选择回归发生时，你应找到上一个良好的计划，并强制其使用而不是当前计划。 这可以通过使用`sp_query_store_force_plan`过程来完成。 中[!INCLUDE[ssde_md](../../includes/ssde_md.md)] [!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]的提供了有关回归计划和建议的纠正措施的信息。 此外， [!INCLUDE[ssde_md](../../includes/ssde_md.md)]还可让你完全自动执行此过程[!INCLUDE[ssde_md](../../includes/ssde_md.md)] ，并修复发现的与计划更改相关的任何问题。

### <a name="automatic-plan-choice-correction"></a>自动计划选择更正

只要[!INCLUDE[ssde_md](../../includes/ssde_md.md)]检测到计划选择回归，就可以自动切换到最近一次已知的正确计划。

![查询执行计划选择更正](media/force-last-good-plan.png "查询执行计划选择更正") 

[!INCLUDE[ssde_md](../../includes/ssde_md.md)]会自动检测任何潜在计划选择回归，包括应使用的计划，而不是错误的计划。 当[!INCLUDE[ssde_md](../../includes/ssde_md.md)]应用最后一个已知良好的计划时，它会自动监视强制计划的性能。 如果强制计划不优于回归计划，则新计划将为 unforced，并且[!INCLUDE[ssde_md](../../includes/ssde_md.md)]将编译新计划。 如果[!INCLUDE[ssde_md](../../includes/ssde_md.md)]验证强制计划是否优于回归计划，则会保留强制计划。 它将保留，直到发生重新编译（例如，在下一个统计信息更新或架构更改时）。

> [!NOTE]
> 任何执行计划自动强制都不会在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例重新启动之间保持。

### <a name="enabling-automatic-plan-choice-correction"></a>启用自动计划选择更正

可以启用每个数据库的自动优化，并指定在检测到某一计划更改回归时，应强制执行最后一个良好计划。 使用以下命令启用自动优化：

```sql   
ALTER DATABASE <yourDatabase>
SET AUTOMATIC_TUNING ( FORCE_LAST_GOOD_PLAN = ON ); 
```

启用此选项后， [!INCLUDE[ssde_md](../../includes/ssde_md.md)]会自动强制执行预计 CPU 增益大于10秒的建议，或新计划中的错误数量大于建议计划中的错误数，并验证强制计划是否比当前计划好。

### <a name="alternative---manual-plan-choice-correction"></a>替代项 - 手动计划选择更正

如果没有自动优化，用户必须定期监视系统，并查找具有回归的查询。 如果任何计划有回归，则用户应找到上一个良好的计划，并使用过程强制执行，而不`sp_query_store_force_plan`是使用当前计划。 最佳做法是强制执行最后一个已知良好的计划，因为较旧的计划可能会因统计信息或索引更改而无效。 强制执行最后一个已知良好计划的用户应监视使用强制计划执行的查询的性能，并验证强制计划是否按预期方式工作。 根据监视和分析的结果，应强制计划，或用户应找到另一种方法来优化查询，例如重写查询。 手动强制计划不应永久强制，因为[!INCLUDE[ssde_md](../../includes/ssde_md.md)]应该能够应用最佳计划。 用户或 DBA 应最终使用`sp_query_store_unforce_plan`过程取消强制执行计划，并让我们[!INCLUDE[ssde_md](../../includes/ssde_md.md)]寻找最佳计划。 

> [!TIP]
> 或者，将**查询与 "强制计划**" 查询存储 "视图结合使用来查找和取消强制执行计划。

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]提供在查询存储中监视性能和解决问题所需的所有必要的视图和过程。

在[!INCLUDE[sssql15-md](../../includes/sssql15-md.md)]中，可以使用查询存储系统视图查找计划选择回归。 在[!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)]中， [!INCLUDE[ssde_md](../../includes/ssde_md.md)]会检测并显示潜在的计划选择回归，并显示应在[&#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-tuning-recommendations-transact-sql.md)视图中应用 dm_db_tuning_recommendations 的推荐操作。 此视图显示有关问题的信息、问题的重要性，以及详细信息，如标识的查询、回归计划的 ID、用作比较基线的计划的 ID 以及可以执行以修复问题的[!INCLUDE[tsql_md](../../includes/tsql-md.md)]语句。

| type | description | datetime | score | 详细信息 | ... |
| --- | --- | --- | --- | --- | --- |
| `FORCE_LAST_GOOD_PLAN` | CPU 时间从4毫秒更改为14毫秒 | 3/17/2017 | 83 | `queryId` `recommendedPlanId` `regressedPlanId` `T-SQL` |   |
| `FORCE_LAST_GOOD_PLAN` | CPU 时间从 37 ms 更改为84毫秒 | 2017 年 3 月 16 日 | 26 | `queryId` `recommendedPlanId` `regressedPlanId` `T-SQL` |   |

下面的列表中介绍了此视图中的某些列：
 - 建议的操作类型-`FORCE_LAST_GOOD_PLAN`
 - 说明，其中包含[!INCLUDE[ssde_md](../../includes/ssde_md.md)]认为此计划更改的潜在性能回归的信息
 - 检测到潜在回归时的日期时间
 - 此建议的分数
 - 详细信息，如检测到的计划的 ID、回归计划的 id、应强制解决该问题的计划的 id、可能应用来修复问题[!INCLUDE[tsql_md](../../includes/tsql-md.md)]的脚本等。详细信息以[JSON 格式](../../relational-databases/json/index.md)存储

使用以下查询来获取一个脚本，该脚本可修复问题和有关估计收益的其他信息：

```sql   
SELECT reason, score,
      script = JSON_VALUE(details, '$.implementationDetails.script'),
      planForceDetails.*,
      estimated_gain = (regressedPlanExecutionCount + recommendedPlanExecutionCount)
                  * (regressedPlanCpuTimeAverage - recommendedPlanCpuTimeAverage)/1000000,
      error_prone = IIF(regressedPlanErrorCount > recommendedPlanErrorCount, 'YES','NO')
FROM sys.dm_db_tuning_recommendations
CROSS APPLY OPENJSON (Details, '$.planForceDetails')
    WITH (  [query_id] int '$.queryId',
            regressedPlanId int '$.regressedPlanId',
            recommendedPlanId int '$.recommendedPlanId',
            regressedPlanErrorCount int,
            recommendedPlanErrorCount int,
            regressedPlanExecutionCount int,
            regressedPlanCpuTimeAverage float,
            recommendedPlanExecutionCount int,
            recommendedPlanCpuTimeAverage float
          ) AS planForceDetails;
```

[!INCLUDE[ssresult-md](../../includes/ssresult-md.md)]     

| reason | score | 脚本 | 查询\_id | 当前计划\_id | 推荐的\_计划 id | 估计\_收益 | 容易\_出错
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| CPU 时间从3毫秒改为46毫秒 | 36 | EXEC sp\_query\_store\_强制\_计划12，17; | 12 | 28 | 17 | 11.59 | 0

列`estimated_gain`表示在建议的计划将用于执行查询（而不是当前计划）时将保存的预计秒数。 如果增益大于10秒，则建议使用建议的计划，而不是当前计划。 如果当前计划中的错误（例如超时或中止执行）比建议计划中的多，则将列`error_prone`设置为值。 `YES` 易出错的计划是指应强制实施建议计划而不是当前计划的另一个原因。

尽管[!INCLUDE[ssde_md](../../includes/ssde_md.md)]提供了标识计划选择回归所需的所有信息，但持续监视和修复性能问题可能会变得枯燥乏味。 自动优化可使此过程变得更加容易。

> [!NOTE]
> Sys. dm_db_tuning_recommendations DMV 中的数据不会在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例重新启动之间保留。

## <a name="automatic-index-management"></a>自动索引管理

在[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]中，索引管理非常简单[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)] ，因为了解工作负荷并确保始终以最佳方式为数据编制索引。 正确的索引设计对于优化工作负荷性能至关重要，而自动索引管理也有助于优化索引。 自动索引管理可修复未正确编制索引的数据库中的性能问题，或者维护并改进现有数据库架构上的索引。 中[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]的自动优化执行以下操作：

 - 标识索引，这些索引可以提高从表[!INCLUDE[tsql_md](../../includes/tsql-md.md)]中读取数据的查询的性能。
 - 标识不能被删除的较长时间段内未使用的冗余索引或索引。 删除不必要的索引可以提高更新表中数据的查询的性能。

### <a name="why-do-you-need-index-management"></a>为什么需要索引管理？

索引加快了某些从表中读取数据的查询，但它们可能会减慢更新数据的查询速度。 需要仔细分析何时创建索引以及需在索引中包含哪些列。 某些时间后可能不需要某些索引。 因此，您需要定期标识并删除这些不会带来任何好处的索引。 如果忽略未使用的索引，则会减少更新数据的查询的性能，而不会对读取数据的查询带来任何好处。 未使用的索引也会影响系统整体性能，因为其他更新会需要不必要的日志记录。

既要改进从表中读取数据的查询的性能，又要最大限度地减少对更新数据的查询的影响，要找出此类最佳索引可能需要持续进行复杂的分析。

[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]使用内置智能和高级规则来分析查询，确定最适合当前工作负荷的索引，并识别可能需要删除的索引。 Azure SQL 数据库可确保你拥有一组最少的必要索引，这些索引可优化读取数据的查询，并对其他查询的影响降至最低。

### <a name="automatic-index-management"></a>自动索引管理

除了检测以外， [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]还可以自动应用标识的建议。 如果发现内置规则可以提高数据库的性能，则可以让[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]自动管理索引。

若要启用自动优化[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]并允许自动优化功能完全管理工作负荷，请参阅[使用 AZURE 门户在 Azure SQL 数据库中启用自动优化](/azure/sql-database/sql-database-automatic-tuning-enable)。

当[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]应用 CREATE INDEX 或 DROP INDEX 建议时，它会自动监视受索引影响的查询的性能。 仅当改进受影响的查询的性能时，才会保留新索引。 如果由于缺少索引而导致某些查询运行较慢，将自动重新创建删除的索引。

### <a name="automatic-index-management-considerations"></a>自动索引管理注意事项

在中创建必要索引所需[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]的操作可能会消耗资源，暂时会影响工作负荷性能。 若要最大程度地降低索引创建对工作[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]负荷性能的影响，可为任何索引管理操作查找相应的时间范围。 如果数据库需要资源来执行工作负荷，并且当数据库有足够多的未使用资源可用于维护任务时重新启动，则会推迟优化操作。 验证操作是自动索引管理中的一项重要功能。 当[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]创建或删除索引时，监视过程会分析工作负荷的性能，以验证操作是否提高了整体性能。 如果它没有显著改进，则会立即还原操作。 这样， [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]就可以确保自动优化操作不会对工作负荷的性能产生负面影响。 自动优化创建的索引对在基础架构上进行的维护操作没有任何影响。 自动创建的索引不会阻止对架构进行更改（如删除或重命名列）。 当删除相关的表或[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]列时，自动创建的索引会立即被删除。

### <a name="alternative---manual-index-management"></a>备选-手动索引管理

如果没有自动索引管理，用户或 DBA 需要手动查询[sys.databases dm_db_missing_index_details &#40;transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-details-transact-sql.md)查看或使用中[!INCLUDE[ssManStudio](../../includes/ssManStudio-md.md)]的 "性能仪表板" 报表查找可能会提高性能的索引，使用此视图中提供的详细信息创建索引，并手动监视查询的性能。 为了找到应删除的索引，用户应监视索引的操作使用情况统计信息，以查找很少使用的索引。

[!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]简化了此过程。 [!INCLUDE[ssazure_md](../../includes/ssazure_md.md)]分析工作负荷，识别可以使用新索引更快执行的查询，并识别未使用或重复的索引。 有关如何识别应更改索引的详细信息，请参阅[在 Azure 门户中查找索引建议](https://docs.microsoft.com/azure/sql-database/sql-database-advisor-portal)。

## <a name="see-also"></a>另请参阅  
 [将数据库集 AUTOMATIC_TUNING &#40;Transact-sql&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [sys. database_automatic_tuning_options &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-database-automatic-tuning-options-transact-sql.md)  
 [sys. dm_db_tuning_recommendations &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-tuning-recommendations-transact-sql.md)   
 [sys. dm_db_missing_index_details &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-missing-index-details-transact-sql.md)   
 [sp_query_store_force_plan &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-query-store-force-plan-transact-sql.md)     
 [sp_query_store_unforce_plan &#40;Transact-sql&#41;](../../relational-databases/system-stored-procedures/sp-query-store-unforce-plan-transact-sql.md)           
 [sys. database_query_store_options &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [JSON 函数](../../relational-databases/json/index.md)    
 [执行计划](../../relational-databases/performance/execution-plans.md)    
 [监视和优化性能](../../relational-databases/performance/monitor-and-tune-for-performance.md)     
 [性能监视和优化工具](../../relational-databases/performance/performance-monitoring-and-tuning-tools.md)     
 [使用查询存储来监视性能](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)  
 [查询优化助手](../../relational-databases/performance/upgrade-dbcompat-using-qta.md)
