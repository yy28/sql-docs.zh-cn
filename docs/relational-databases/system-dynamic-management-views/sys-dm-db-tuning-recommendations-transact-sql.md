---
title: sys.dm_db_tuning_recommendations (Transact SQL) |Microsoft 文档
description: 了解如何查找潜在的性能问题，建议在 SQL Server 和 Azure SQL 数据库的修补程序
ms.custom: ''
ms.date: 07/20/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
caps.latest.revision: 37
author: jovanpop-msft
ms.author: jovanpop
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || >= sql-server-2017 || = sqlallproducts-allversions
ms.openlocfilehash: fc933666e31c45fc78fb6d303ca1e7d3b5874d55
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmdbtuningrecommendations-transact-sql"></a>sys.dm\_db\_优化\_建议 (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2017-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2017-asdb-xxxx-xxx-md.md)]

  返回有关详细信息优化建议。  
  
 在 [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] 中，动态管理视图不能公开将影响数据库包含的信息，也不能公开有关用户可以访问的其他数据库的信息。 要避免公开此类信息，需要将包含不属于已连接租户的数据的每一行都筛选掉。

| **列名** | **数据类型** | **Description** |
| --- | --- | --- |
| **名称** | **nvarchar(4000)** | 建议唯一名称。 |
| **类型** | **nvarchar(4000)** | 生成的建议，例如，自动优化选项的名称 `FORCE_LAST_GOOD_PLAN` |
| **reason** | **nvarchar(4000)** | 为什么提供此建议的原因。 |
| **valid\_since** | **datetime2** | 首次生成此建议。 |
| **最后一个\_刷新** | **datetime2** | 此建议生成的最后一个时间。 |
| **状态** | **nvarchar(4000)** | 描述的状态的建议的 JSON 文档。 将可使用以下字段：<br />-   `currentValue` -当前状态的建议。<br />-   `reason` – 介绍的推荐方法是在当前状态的原因的常量。|
| **is\_executable\_action** | **bit** | 1 = 可以对通过数据库执行该建议[!INCLUDE[tsql_md](../../includes/tsql_md.md)]脚本。<br />0 = 不能对数据库执行该建议 (例如： 信息只有或已还原建议) |
| **是\_revertable\_操作** | **bit** | 1 = 建议可自动监视并还原数据库引擎。<br />0 = 不能自动监视和恢复的建议。 大多数&quot;可执行&quot;操作将受到&quot;revertable&quot;。 |
| **execute\_action\_start\_time** | **datetime2** | 应用建议的日期。 |
| **execute\_action\_duration** | **time** | 执行操作的持续时间。 |
| **执行\_操作\_启动\_通过** | **nvarchar(4000)** | `User` = 用户手动强制建议中的计划。 <br /> `System` = 系统自动应用建议。 |
| **执行\_操作\_启动\_时间** | **datetime2** | 应用建议的日期。 |
| **revert\_action\_start\_time** | **datetime2** | 已还原，建议的日期。 |
| **revert\_action\_duration** | **time** | 还原操作的持续时间。 |
| **还原\_操作\_启动\_通过** | **nvarchar(4000)** | `User` = 用户手动 unforced 建议的计划。 <br /> `System` = 系统自动还原建议。 |
| **还原\_操作\_启动\_时间** | **datetime2** | 已还原，建议的日期。 |
| **score** | **int** | 估计值/影响此建议 0-100 上缩放 （越大越好） |
| **详细信息** | **nvarchar(max)** | 包含有关建议的更多详细信息的 JSON 文档。 将可使用以下字段：<br /><br />`planForceDetails`<br />-    `queryId` -查询\_回归的查询 id。<br />-    `regressedPlanId` -plan_id 回归的计划。<br />-   `regressedPlanExecutionCount` 的检测到查询中使用之前回归回归计划执行数。<br />-    `regressedPlanAbortedCount` -回归计划执行期间检测到的错误数。<br />-    `regressedPlanCpuTimeAverage` 的在检测到回归之前使用回归查询平均 CPU 时间。<br />-    `regressedPlanCpuTimeStddev` -检测到的前回归回归查询所使用的 CPU 时间标准偏差。<br />-    `recommendedPlanId` -plan_id 应强制的计划。<br />-   `recommendedPlanExecutionCount`-与在检测到回归之前应强制计划查询的执行数。<br />-    `recommendedPlanAbortedCount` -应强制计划执行期间检测到的错误数。<br />-    `recommendedPlanCpuTimeAverage` 的供 （计算之前检测到回归） 应强制计划执行的查询平均 CPU 时间。<br />-    `recommendedPlanCpuTimeStddev` 检测到的 CPU 时间之前回归回归的查询使用的标准偏差。<br /><br />`implementationDetails`<br />-  `method` 的应该用于更正回归方法。 值始终是`TSql`。<br />-    `script` - [!INCLUDE[tsql_md](../../includes/tsql_md.md)] 应执行强制实施该建议的计划的脚本。 |
  
## <a name="remarks"></a>注释  
 返回的信息`sys.dm_db_tuning_recommendations`时数据库引擎标识潜在的查询性能回归，而且不具有持久性，会更新。 建议保持仅直到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]重新启动。 如果他们想要将其保留在服务器回收后，数据库管理员应定期制作优化建议的备份副本。 

 `currentValue` 字段`state`列可能具有以下值：
 | 状态 | Description |
 |--------|-------------|
 | `Active` | 建议处于活动状态且未尚未应用。 用户可以执行建议脚本并手动执行。 |
 | `Verifying` | 按以下方式应用建议[!INCLUDE[ssde_md](../../includes/ssde_md.md)]并内部验证过程将性能回归的计划的强制计划进行比较。 |
 | `Success` | 已成功应用建议。 |
 | `Reverted` | 由于没有任何显著的性能提升，建议才会恢复。 |
 | `Expired` | 建议已过期，但无法将不再应用。 |

中的 JSON 文档`state`列包含描述为何中的当前状态的建议的原因。 在原因字段中的值可能是： 

| 原因 | Description |
|--------|-------------|
| `SchemaChanged` | 建议已过期，因为被引用表的架构已更改。 |
| `StatisticsChanged`| 由于被引用表的统计信息更改过期建议。 |
| `ForcingFailed` | 建议的计划不能强制某一查询。 查找`last_force_failure_reason`中[sys.query_store_plan](../../relational-databases/system-catalog-views/sys-query-store-plan-transact-sql.md)视图以查找失败的原因。 |
| `AutomaticTuningOptionDisabled` | `FORCE_LAST_GOOD_PLAN` 验证过程中，用户将禁用选项。 启用`FORCE_LAST_GOOD_PLAN`选项使用[ALTER 数据库设置 AUTOMATIC_TUNING &#40;TRANSACT-SQL&#41; ](../../t-sql/statements/alter-database-transact-sql-set-options.md)语句或强制手动使用中的脚本的计划`[details]`列。 |
| `UnsupportedStatementType` | 无法基于该查询强制计划。 是游标不受支持的查询的示例和`INSERT BULK`语句。 |
| `LastGoodPlanForced` | 已成功应用建议。 |
| `AutomaticTuningOptionNotEnabled`| [!INCLUDE[ssde_md](../../includes/ssde_md.md)] 标识潜在性能回归中，但`FORCE_LAST_GOOD_PLAN`未启用选项 – 请参阅[ALTER 数据库设置 AUTOMATIC_TUNING &#40;TRANSACT-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)。 手动应用建议或启用`FORCE_LAST_GOOD_PLAN`选项。 |
| `VerificationAborted`| 验证过程是由于重新启动或 Query Store 清理已中止。 |
| `VerificationForcedQueryRecompile`| 因为没有任何显著的性能改善在重新编译查询。 |
| `PlanForcedByUser`| 用户手动强制计划使用[sp_query_store_force_plan &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-query-store-force-plan-transact-sql.md)过程。 |
| `PlanUnforcedByUser` | 用户手动取消强制计划使用[sp_query_store_unforce_plan &#40;TRANSACT-SQL&#41; ](../../relational-databases/system-stored-procedures/sp-query-store-unforce-plan-transact-sql.md)过程。 |

 在详细信息列的统计信息不会显示运行时计划统计信息 （例如，当前 CPU 时间）。 建议详细信息在的回归检测时执行，并描述原因[!INCLUDE[ssde_md](../../includes/ssde_md.md)]标识性能回归。 使用`regressedPlanId`和`recommendedPlanId`查询[查询存储目录视图](../../relational-databases/performance/how-query-store-collects-data.md)若要查找确切的运行时计划统计信息。

## <a name="using-tuning-recommendations-information"></a>使用优化建议信息  
 可以使用以下查询来获取将解决此问题的 T-SQL 脚本：  
 
```
SELECT name, reason, score,
        JSON_VALUE(details, '$.implementationDetails.script') as script,
        details.* 
FROM sys.dm_db_tuning_recommendations
    CROSS APPLY OPENJSON(details, '$.planForceDetails')
                WITH (  query_id int '$.queryId',
                        regressed_plan_id int '$.regressedPlanId',
                        last_good_plan_id int '$.recommendedPlanId') as details
WHERE JSON_VALUE(state, '$.currentValue') = 'Active'
```
  
 有关可用于查询建议视图中的值的 JSON 函数的详细信息，请参阅[JSON 支持](../../relational-databases/json/index.md)中[!INCLUDE[ssde_md](../../includes/ssde_md.md)]。
  
## <a name="permissions"></a>权限  

上[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，需要`VIEW SERVER STATE`权限。   
上[!INCLUDE[ssSDS_md](../../includes/sssds-md.md)]，需要`VIEW DATABASE STATE`数据库中的权限。   

## <a name="see-also"></a>另请参阅  
 [自动优化](../../relational-databases/automatic-tuning/automatic-tuning.md)   
 [sys.database_automatic_tuning_options &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/sys-database-automatic-tuning-options-transact-sql.md)   
 [sys.database_query_store_options &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/sys-database-query-store-options-transact-sql.md)   
 [JSON 支持](../../relational-databases/json/index.md)
 
