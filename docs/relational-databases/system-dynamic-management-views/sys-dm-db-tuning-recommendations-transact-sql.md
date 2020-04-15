---
title: 系统dm_db_tuning_recommendations（转算-SQL） |微软文档
description: 了解如何在 SQL Server 和 Azure SQL 数据库中查找潜在的性能问题和建议修复程序
ms.custom: ''
ms.date: 07/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_db_tuning_recommendations
- dm_db_tuning_recommendations
- sys.dm_db_tuning_recommendations_TSQL
- dm_db_tuning_recommendations_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- database tuning recommendations feature [SQL Server], sys.dm_db_tuning_recommendations dynamic management view
- sys.dm_db_tuning_recommendations dynamic management view
ms.assetid: ced484ae-7c17-4613-a3f9-6d8aba65a110
author: jovanpop-msft
ms.author: jovanpop
monikerRange: =azuresqldb-current||>=sql-server-2017||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e8c18ce07ba5e36dcbdb5750db77edf17495c7b9
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285457"
---
# <a name="sysdm_db_tuning_recommendations-transact-sql"></a>sys.dm\_\_db\_调优建议（转算 SQL）
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

  返回有关调优建议的详细信息。  
  
 在 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 中，动态管理视图不能公开将影响数据库包含的信息，也不能公开有关用户可以访问的其他数据库的信息。 为避免公开此信息，将筛选出包含不属于连接租户的数据的每一行。

| **列名称** | **数据类型** | **说明** |
| --- | --- | --- |
| name  | **恩瓦尔查尔 （4000）** | 推荐的唯一名称。 |
| **type** | **恩瓦尔查尔 （4000）** | 生成建议的自动调优选项的名称，例如，`FORCE_LAST_GOOD_PLAN` |
| **reason** | **恩瓦尔查尔 （4000）** | 提供这项建议的原因。 |
| **有效\_，因为** | **datetime2** | 首次生成此建议。 |
| **上次\_刷新** | **datetime2** | 上次生成此建议时。 |
| **状态** | **恩瓦尔查尔 （4000）** | 描述建议的状态的 JSON 文档。 以下字段可用：<br />-   `currentValue`- 建议的当前状态。<br />-   `reason`- 描述建议处于当前状态的原因的常量。|
| **是\_可\_执行操作** | **位** | 1 = 建议可以通过[!INCLUDE[tsql_md](../../includes/tsql-md.md)]脚本针对数据库执行。<br />0 = 不能针对数据库执行建议（例如：仅信息或还原建议） |
| **可\_还原\_操作** | **位** | 1 = 建议可以自动监视并由数据库引擎还原。<br />0 = 无法自动监视和还原建议。 大多数&quot;可&quot;执行操作将&quot;可&quot;还原。 |
| **执行\_操作\_开始\_时间** | **datetime2** | 应用建议的日期。 |
| **执行\_操作\_持续时间** | **time** | 执行操作的持续时间。 |
| **\_执行\_\_由** | **恩瓦尔查尔 （4000）** | `User`• 建议中的用户手动强制计划。 <br /> `System`* 系统自动应用建议。 |
| **执行\_操作\_启动\_时间** | **datetime2** | 应用建议的日期。 |
| **还原\_操作\_开始\_时间** | **datetime2** | 恢复建议的日期。 |
| **还原\_操作\_持续时间** | **time** | 还原操作的持续时间。 |
| **\_还原\_\_由** | **恩瓦尔查尔 （4000）** | `User`• 用户手动非强制推荐计划。 <br /> `System`• 系统会自动还原建议。 |
| **还原\_操作\_启动\_时间** | **datetime2** | 恢复建议的日期。 |
| **得分** | **Int** | 此建议在 0-100 比额表上的估计值/影响（越大越好） |
| **细节** | **恩瓦尔恰尔（最大）** | 包含有关建议的更多详细信息的 JSON 文档。 以下字段可用：<br /><br />`planForceDetails`<br />-    `queryId`-\_回归查询的查询 ID。<br />-    `regressedPlanId`- plan_id倒退计划。<br />-   `regressedPlanExecutionCount`- 在检测到回归之前，使用回归计划执行查询的次数。<br />-    `regressedPlanAbortedCount`- 执行回归计划期间检测到的错误数。<br />-    `regressedPlanCpuTimeAverage`- 在检测到回归之前，回归查询消耗的平均 CPU 时间（以微秒为单位）。<br />-    `regressedPlanCpuTimeStddev`- 在检测到回归之前，回归查询消耗的 CPU 时间的标准偏差。<br />-    `recommendedPlanId`- plan_id应该强制的计划。<br />-   `recommendedPlanExecutionCount`- 查询的执行次数，在检测到回归之前应强制执行计划。<br />-    `recommendedPlanAbortedCount`- 执行应强制执行计划期间检测到的错误数。<br />-    `recommendedPlanCpuTimeAverage`- 使用应强制执行的计划执行的查询消耗的平均 CPU 时间（以微秒为单位）（在检测到回归之前计算）。<br />-    `recommendedPlanCpuTimeStddev`在检测到回归之前，回归查询消耗的 CPU 时间的标准偏差。<br /><br />`implementationDetails`<br />-  `method`- 应用于更正回归的方法。 价值总是`TSql`。<br />-    `script` - [!INCLUDE[tsql_md](../../includes/tsql-md.md)]应执行以强制建议计划的脚本。 |
  
## <a name="remarks"></a>备注  
 返回的信息`sys.dm_db_tuning_recommendations`将在数据库引擎标识潜在的查询性能回归时更新，并且不会持久化。 建议仅保留到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]重新启动为止。 如果数据库管理员希望在服务器回收后保留调优建议，则应定期制作该建议的备份副本。 

 `currentValue`列中的`state`字段可能具有以下值：
 
 | 状态 | 说明 |
 |--------|-------------|
 | `Active` | 建议处于活动状态，尚未应用。 用户可以采用推荐脚本并手动执行它。 |
 | `Verifying` | 建议由 应用[!INCLUDE[ssde_md](../../includes/ssde_md.md)]，内部验证过程将强制计划的性能与递减计划进行比较。 |
 | `Success` | 已成功应用建议。 |
 | `Reverted` | 建议被还原，因为没有显著的性能提升。 |
 | `Expired` | 建议已过期，无法再应用。 |

列中的`state`JSON 文档包含描述建议处于当前状态的原因。 原因字段中的值可能是： 

| 原因 | 描述 |
|--------|-------------|
| `SchemaChanged` | 建议已过期，因为引用表的架构已更改。 如果在新架构上检测到新的查询计划回归，将创建新建议。 |
| `StatisticsChanged`| 由于引用的表上的统计信息更改，建议已过期。 如果根据新统计信息检测到新的查询计划回归，将创建新建议。 |
| `ForcingFailed` | 不能强制查询上建议的计划。 `last_force_failure_reason`在[sys.query_store_plan](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)视图中查找失败的原因。 |
| `AutomaticTuningOptionDisabled` | `FORCE_LAST_GOOD_PLAN`在验证过程中，用户禁用了选项。 使用`FORCE_LAST_GOOD_PLAN` [ALTER 数据库集AUTOMATIC_TUNING&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)语句启用选项，或强制使用列`[details]`中的脚本手动操作计划。 |
| `UnsupportedStatementType` | 无法强制在查询上进行计划。 不支持的查询的示例包括游标和`INSERT BULK`语句。 |
| `LastGoodPlanForced` | 已成功应用建议。 |
| `AutomaticTuningOptionNotEnabled`| [!INCLUDE[ssde_md](../../includes/ssde_md.md)]已识别潜在的性能回归，但`FORCE_LAST_GOOD_PLAN`未启用该选项 - 请参阅[ALTER 数据库集AUTOMATIC_TUNING&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)。 手动应用建议或启用`FORCE_LAST_GOOD_PLAN`选项。 |
| `VerificationAborted`| 由于重新启动或查询存储清理，验证过程将中止。 |
| `VerificationForcedQueryRecompile`| 重新编译查询，因为性能没有显著改善。 |
| `PlanForcedByUser`| 用户使用[sp_query_store_force_plan&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-force-plan-transact-sql.md)过程手动强制计划。 如果用户明确决定强制某些计划，数据库引擎将不会应用该建议。 |
| `PlanUnforcedByUser` | 用户使用[sp_query_store_unforce_plan&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-query-store-unforce-plan-transact-sql.md)过程手动取消强制计划。 由于用户显式还原了建议的计划，因此数据库引擎将继续使用当前计划，并在将来发生某些计划回归时生成新的建议。 |

 详细信息列中的统计信息不显示运行时计划统计信息（例如，当前 CPU 时间）。 建议详细信息在回归检测时获取，并说明标识的性能回归原因[!INCLUDE[ssde_md](../../includes/ssde_md.md)]。 使用`regressedPlanId``recommendedPlanId`和 查询[存储目录视图](../../relational-databases/performance/how-query-store-collects-data.md)以查找准确的运行时计划统计信息。

## <a name="examples-of-using-tuning-recommendations-information"></a>使用调优建议信息的示例  

### <a name="example-1"></a>示例 1
下面获取生成的[!INCLUDE[tsql](../../includes/tsql-md.md)]脚本，该脚本强制为任何给定查询制定良好的计划：  
 
```sql
SELECT name, reason, score,
    JSON_VALUE(details, '$.implementationDetails.script') AS script,
    details.* 
FROM sys.dm_db_tuning_recommendations
CROSS APPLY OPENJSON(details, '$.planForceDetails')
    WITH (  [query_id] int '$.queryId',
            regressed_plan_id int '$.regressedPlanId',
            last_good_plan_id int '$.recommendedPlanId') AS details
WHERE JSON_VALUE(state, '$.currentValue') = 'Active';
```
### <a name="example-2"></a>示例 2
下面获取生成的[!INCLUDE[tsql](../../includes/tsql-md.md)]脚本，该脚本强制为任何给定查询制定好计划，并获取有关估计收益的其他信息：

```sql
SELECT reason, score,
      script = JSON_VALUE(details, '$.implementationDetails.script'),
      planForceDetails.*,
      estimated_gain = (regressedPlanExecutionCount + recommendedPlanExecutionCount)
                  *(regressedPlanCpuTimeAverage - recommendedPlanCpuTimeAverage)/1000000,
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

### <a name="example-3"></a>示例 3
下面获取生成的[!INCLUDE[tsql](../../includes/tsql-md.md)]脚本，该脚本强制为任何给定查询制定好计划，并获取包含查询文本和存储在查询存储中的查询计划的其他信息：

```sql
WITH cte_db_tuning_recommendations
AS (SELECT reason,
        score,
        query_id,
        regressedPlanId,
        recommendedPlanId,
        current_state = JSON_VALUE(state, '$.currentValue'),
        current_state_reason = JSON_VALUE(state, '$.reason'),
        script = JSON_VALUE(details, '$.implementationDetails.script'),
        estimated_gain = (regressedPlanExecutionCount + recommendedPlanExecutionCount)
                * (regressedPlanCpuTimeAverage - recommendedPlanCpuTimeAverage)/1000000,
        error_prone = IIF(regressedPlanErrorCount > recommendedPlanErrorCount, 'YES','NO')
    FROM sys.dm_db_tuning_recommendations
    CROSS APPLY OPENJSON(Details, '$.planForceDetails')
    WITH ([query_id] int '$.queryId',
        regressedPlanId int '$.regressedPlanId',
        recommendedPlanId int '$.recommendedPlanId',
        regressedPlanErrorCount int,    
        recommendedPlanErrorCount int,
        regressedPlanExecutionCount int,
        regressedPlanCpuTimeAverage float,
        recommendedPlanExecutionCount int,
        recommendedPlanCpuTimeAverage float
        )
    )
SELECT qsq.query_id,
    qsqt.query_sql_text,
    dtr.*,
    CAST(rp.query_plan AS XML) AS RegressedPlan,
    CAST(sp.query_plan AS XML) AS SuggestedPlan
FROM cte_db_tuning_recommendations AS dtr
INNER JOIN sys.query_store_plan AS rp ON rp.query_id = dtr.query_id
    AND rp.plan_id = dtr.regressedPlanId
INNER JOIN sys.query_store_plan AS sp ON sp.query_id = dtr.query_id
    AND sp.plan_id = dtr.recommendedPlanId
INNER JOIN sys.query_store_query AS qsq ON qsq.query_id = rp.query_id
INNER JOIN sys.query_store_query_text AS qsqt ON qsqt.query_text_id = qsq.query_text_id;
```

有关可用于查询建议视图中的值的 JSON 函数的详细信息，请参阅 中的[!INCLUDE[ssde_md](../../includes/ssde_md.md)] [JSON 支持](../../relational-databases/json/index.md)。
  
## <a name="permissions"></a>权限  

需要`VIEW SERVER STATE`中的[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]权限。   
需要`VIEW DATABASE STATE`中的[!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]数据库的权限。   

## <a name="see-also"></a>另请参阅  
 [自动调谐](../../relational-databases/automatic-tuning/automatic-tuning.md)   
 [系统database_automatic_tuning_options&#40;转算-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-automatic-tuning-options-transact-sql.md)   
 [系统database_query_store_options&#40;转瞬即发-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [JSON 支持](../../relational-databases/json/index.md)
 
