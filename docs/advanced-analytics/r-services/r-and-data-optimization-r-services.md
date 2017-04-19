---
title: "R 和数据优化 (R Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/10/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b6104878-ed19-47a7-ac37-21e4d6e2a1af
caps.latest.revision: 13
author: jeannt
ms.author: jeannt
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f9ab36f83191dafa2b522fae4542d8965a0915e5
ms.lasthandoff: 04/11/2017

---
# <a name="r-and-data-optimization-r-services"></a>R 和数据优化 (R Services)
本主题介绍如何更新 R 代码，以提高性能或避免已知问题。

## <a name="compute-context"></a>计算上下文

执行分析时，[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 可以使用 __local__ 或 __SQL__ 计算上下文。 使用 __local__ 计算上下文时，将在客户端计算机上执行分析，必须通过网络从 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 提取数据。 这种网络传输造成的性能下降取决于传输的数据大小、网络速度，以及同时发生的其他网络传输数量。

如果计算上下文为 __SQL Server__，将在 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 内部执行分析函数。 数据在分析任务的本地，因此不会造成网络开销。 

处理大型数据集时，始终应该使用 SQL 计算上下文。

## <a name="factors"></a>因子

R 语言会将表中的字符串转换为因子。 许多数据源对象使用 `colInfo` 作为参数来控制列的处理方式。 例如，`c(“fruit” = c(type = “factor”, levels=as.character(c(1:3)), newLevels=c(“apple”, “orange”, “banana”)))` 使用表中的整数 1、2 和 3，并将这些数字视作级别为 `apple`、`orange` 和 `banana` 的因子。 

数据科研人员通常在公式中使用因子变量；但是，当源数据是整数时，使用因子会造成性能下降，因为在运行时，整数将转换为字符串。 但是，如果列包含字符串，你可以事先使用 `colInfo` 指定级别。 在这种情况下，等效的语句为 `c(“fruit” = c(type = “factor”, levels= c(“apple”, “orange”, “banana”)))`，它可以在读取字符串时将字符串视为因子。 

为了避免运行时转换，请考虑将级别作为整数存储在表中，并根据第一个公式示例中所述使用这些级别。 如果模型生成中不存在语义差异，这种方法可能会提高性能。

## <a name="data-transformation"></a>数据转换

数据科研人员通常在分析过程中使用以 R 语言编写的转换函数。 转换函数必须应用到从表中检索的每个行。 在 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 中，这种转换是在批处理模式下发生的，涉及到 R 解释程序与分析引擎之间的通信。 执行转换时，数据将从 SQL 移到分析引擎，再移到 R 解释程序进程，然后转移回去。 因此，根据涉及的数据量，使用转换可能会给算法性能造成严重的负面影响。

更有效的做法是在执行分析之前将所有必要的列放在表或视图中，因为这可以避免在计算期间执行转换。 如果无法将更多的列添加到现有表中，可以考虑创建另一个表或视图来包含转换后的列，然后使用相应的查询来检索数据。

## <a name="batching"></a>批处理

SQL 数据源 (`RxSqlServerData`) 提供一个选项用于通过参数 `rowsPerRead` 指示批大小。 此参数指定要同时处理的行数。 在运行时，算法将在每个批中读取指定的行数。 默认情况下，此参数的值设置为 50,000，确保即使在内存较低的计算机上，也能正常执行算法。 如果计算机的可用内存足够高，将此值增大到 500,000 甚至 1,000,000 可以实现更高的性能，尤其是处理大型表时。 

增大此值并一定总能产生更好的效果，可能需要经过一定的试验才能确定最佳值。 在包含多个进程的大型数据集上，这种做法的优点更为明显（`numTasks` 设置为大于 `1` 的值）。

## <a name="parallel-processing"></a>并行处理

为了提高 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 中 rx 分析函数的运行性能，[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 依赖于使用 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 计算机上可用核心的并行处理。 可通过两种方式使用 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 实现并行化：

* 使用 `sp_execute_external_script` 存储过程运行 R 脚本时，将 `@parallel` 参数设置为 `1`。 对于不使用 RevoScaleR 函数的 R 脚本（通常带有“rx”前缀），这样设置会很有作用。 如果脚本使用 RevoScaleR 函数，将自动处理并行处理，因此不应该将 `@parallel` 设置为 `1`。

    如果 R 脚本可并行化，并且 [!INCLUDE[tsql_md](../../includes/tsql-md.md)] 查询也可并行化，则 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 将创建多个并行进程（最大数量为 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 的__最大并行度 MAXDOP__ 设置），并针对所有进程运行同一个脚本。 每个进程只会接收一部分数据，因此，对于必须查看所有数据的脚本（例如，在训练模型时）而言，这种方式不起作用。 但是，在并行执行批量预测等任务时，这种方式却很有作用。 有关结合 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 使用并行度的详细信息，请参阅 [Using R Code in Transact-SQL](../../advanced-analytics/r-services/using-r-code-in-transact-sql-sql-server-r-services.md)（在 Transact-SQL 中使用 R 代码）中的 __Advanced tips: parallel processing__（高级技巧：并行处理）。

* 结合 SQL Server 计算上下文使用 rx 函数时，请将 `numTasks` 设置为要创建的进程数。 创建的实际进程数由 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 确定，可能会少于请求的数量。 创建的进程数永远不会超过 __MAXDOP__。

    如果 R 脚本可并行化，并且 [!INCLUDE[tsql_md](../../includes/tsql-md.md)] 查询可并行化，则在运行 rx 函数时，[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 将创建多个并行进程。

创建的进程数取决于多种因素，例如，资源监管、当前资源用量、其他会话，以及在 R 脚本中使用的查询的查询执行计划。 

### <a name="query-parallelization"></a>查询并行性

为了确保可以并行分析数据，用于检索数据的查询应该编写为能够出于并行执行目的而呈现自身。 

[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 支持针对 SQL 数据源使用 `RxSqlServerData` 来指定源。 源可以是表或查询。 例如，以下代码示例都定义了基于 SQL 查询的 R 数据源对象：
~~~~
RxSqlServerData(table=”airline”, connectionString = sqlConnString)
~~~~

~~~~
RxSqlServerData(sqlquery=”select [ArrDelay],[CRSDepTime],[DayOfWeek] from airlineWithIndex where rowNum <= 100000”, connectionString = sqlConnString)
~~~~ 

由于分析算法要从表中提取大量数据，因此，必须确保提供给 `RxSqlServerData` 的查询已针对并行执行做出优化。 无法生成并行执行计划的查询可能会导致计算单个进程。

[!INCLUDE[ssManStudioFull_md](../../includes/ssmanstudiofull-md.md)] 可用于分析执行计划，改进查询的性能。 例如，表中的缺失某个索引可能会影响执行查询所要花费的时间。 有关详细信息，请参阅[监视和优化性能](../../relational-databases/performance/monitor-and-tune-for-performance.md)。

另一个可能会影响性能的容易忽视的因素是查询检索的列数超过了所需的数目。 例如，如果某个公式仅基于 3 列，而表中包含 30 列，那么，请不要使用类似于 `select *` 的查询，也不要使用选择的列数超过所需数目的查询。

> [!NOTE]
> 如果在数据源中指定了表而不是查询，[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 将在内部确定要从该表中提取的所需列；但是，这种方法不太可能会导致并行执行。

## <a name="algorithm-parameters"></a>算法参数

许多 rx 训练算法支持用于控制训练模型生成方式的参数。 尽管模型的精确性和正确性非常重要，但算法的性能也同样重要。 可以通过修改模型训练参数来提高计算速度。在许多情况下，可以在不降低精确性和正确性的前提下提高性能。 

例如，`rxDTree` 支持用于控制最大树深的 `maxDepth` 参数。 由于增大 `maxDepth` 可能会降低性能，因此，必须分析增大深度带来的好处以及对性能的影响。 

可以配合 `rxLinMod` 和 `rxLogit` 使用的一个参数是 `cube` 参数。 当公式的第一个因变量是因子变量时，可以使用此参数。 如果 `cube` 设置为 `TRUE`，将使用分块求逆完成回归，与标准的回归计算相比，这可能会提高速度，减少内存用量。 如果公式中有大量的变量，性能提升可能非常明显。

[RevoScaleR](https://msdn.microsoft.com/microsoft-r/scaler/scaler) 用户指南中提供了有关控制各种算法的模型拟合的一些有用信息。 例如，使用 `rxDTree` 时，可以通过调整 `maxNumBins`、`maxDepth`、`maxComplete` 和 `maxSurrogate` 等参数来控制时间复杂性与预测准确性之间的平衡。 将深度增大到 10 或 15 以上可能会使计算开销变得极高。

有关优化 `rxDForest` 和 `rxDTree` 的性能的详细信息，请参阅 [Performance tuning options for rxDForest/rxDTree](https://support.microsoft.com/kb/3104235)（rxDForest/rxDTree 的性能优化选项）。

## <a name="model-and-prediction"></a>模型和预测

完成训练并选择最佳模型后，我们建议将模型存储在数据库中，使其随时可用于预测。 对于需要预测的联机事务处理，从数据库中加载预先计算的模型用于预测的做法非常有效。 示例脚本使用此方法序列化模型并将其存储在数据库表中。 预测时，将从数据库反序列化该模型。

算法生成的某些模型（例如 lm 或 glm）可能很大，尤其是用于大型数据集时。 可存储在 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 中的数据有大小限制。 将模型存储到数据库之前，应该先清理模型。

### <a name="operationalization-using-microsoft-r-server"></a>使用 Microsoft R Server 实现操作化

如果使用存储的模型并在应用程序中集成分析功能实现快速预测对你而言非常重要，则你还可以使用 Microsoft R Server 中的[**操作化**](https://msdn.microsoft.com/microsoft-r/operationalize/about)功能（以前称为 DeployR）。 
+ 数据科研人员可以使用 [**mrsdeploy** 包](https://msdn.microsoft.com/microsoft-r/mrsdeploy/mrsdeploy)来与其他计算机共享 R 代码，并在 Web、桌面、移动和仪表板应用程序中集成 R 分析。 有关详细信息，请参阅 [Getting Started for Data Scientists](https://msdn.microsoft.com/microsoft-r/operationalize/data-scientist-get-started)（数据科研人员入门指南）。
+ 管理员可以管理包、监视计算和 Web 笔记，以及控制 R 作业的安全性。 有关详细信息，请参阅 [Getting Started for Administrators](https://msdn.microsoft.com/microsoft-r/operationalize/admin-get-started)（管理员入门指南）。

## <a name="see-also"></a>另请参阅
[资源监管](../../advanced-analytics/r-services/resource-governance-for-r-services.md)
[资源调控器](../../relational-databases/resource-governor/resource-governor.md)

[CREATE EXTERNAL RESOURCE POOL](../../t-sql/statements/create-external-resource-pool-transact-sql.md)

 [SQL Server R Services 性能优化指南](../../advanced-analytics/r-services/sql-server-r-services-performance-tuning.md)
 
 [R Services 的 SQL Server 配置](../../advanced-analytics/r-services/sql-server-configuration-r-services.md)
 
 [性能案例研究](../../advanced-analytics/r-services/performance-case-study-r-services.md)
 

