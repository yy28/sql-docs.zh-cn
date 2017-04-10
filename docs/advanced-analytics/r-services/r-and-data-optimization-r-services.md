---
title: "R 和数据优化 (R Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/10/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b6104878-ed19-47a7-ac37-21e4d6e2a1af
caps.latest.revision: 13
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 10
---
# R 和数据优化 (R Services)
本主题介绍用于更新您的 R 代码，以改进性能或避免已知的问题的方法。

## 计算上下文

[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 可以使用两个 __本地__ 或 __SQL__ 执行分析时计算上下文。 当使用 __本地__ 都在客户端计算机上进行计算的上下文中，分析和数据必须从获取 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 通过网络。 输入此网络传输取决于传输的数据大小，速度的网络，并在同一时间发生的其他网络传输，而导致性能下降。

如果计算上下文是 __SQL Server__, ，则分析函数执行内部 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]。 数据是分析任务中，本地的因此不引入任何网络开销。 

当处理大型数据集，应始终使用 SQL 计算上下文。

## 因素

R 语言将字符串转换因素为表中。 多个数据源对象需要 `colInfo` 作为参数，以控制如何处理这些列。 例如， `c(“fruit” = c(type = “factor”, levels=as.character(c(1:3)), newLevels=c(“apple”, “orange”, “banana”)))` 将使用整数 1、 2 和 3 从表并将它们视为具有级别的因素 `apple`, ，`orange`, ，和 `banana`。 

数据科学家通常使用因素变量在其公式;但是，当源数据是一个整数时，使用因素将产生的性能造成影响，因为在运行时的整数转换为字符串。 但是，如果列不包含字符串，则可以指定事先使用级别 `colInfo`。 在这种情况下，将等效语句  `c(“fruit” = c(type = “factor”, levels= c(“apple”, “orange”, “banana”)))`, ，将字符串视为因素在被读取。 

若要避免运行的时转换，请考虑为表中的整数存储级别和使用这些公式的第一个示例中所述。 如果不没有在模型生成任何语义差异，这种方法会导致更好的性能。

## 数据转换

数据科学家通常使用在 R 中作为分析的一部分而编写的转换函数。 转换函数必须应用于从表中检索每个行。 在 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], ，此转换发生在批处理模式下，涉及的 R 解释程序和分析引擎之间的通信。 若要执行该转换，数据从 SQL 到分析引擎移动，然后移动到 R 解释程序进程并返回。 因此，使用转换可以头明显负面影响算法的性能，具体取决于数据量影响。

它是具有所有必需的列中的表或视图，然后再执行分析，因为这可以避免转换时的计算效率更高。 如果不能将其他列添加到现有表，则可以考虑用转换后的列创建另一个表或视图，并使用相应的查询来检索数据。

## 批处理

SQL 数据源 (`RxSqlServerData`) 具有一个选项来指示批次大小使用参数 `rowsPerRead`。 此参数指定要一次处理行的数。 在运行时，算法将读取指定的每个批中的行编号。 默认情况下，此参数的值设置为 50000，以确保这些算法可以即便在内存不足的计算机上执行。 如果计算机具有足够的可用内存，则该值增加到 500000 个成员或万个甚至可以产生更好的性能，尤其是对于大型表。 

增加此值可能不总是会产生更好的结果，可能需要进行一些试验来确定最佳值。 此好处将是在大型数据集上使用多个进程更为明显 (`numTasks` 将设置为一个值大于 `1`)。

## 并行处理

若要提高运行 rx 分析函数内的性能 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], ，[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 依赖于使用可用的内核上并行处理 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 机。 有两种方法来实现并行化与 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]:

* 当使用 `sp_execute_external_script` 存储的过程可以运行 R 脚本，设置 `@parallel` 参数 `1`。 这可用于不使用 RevoScaleR 函数，它通常带有"rx"前缀的 R 脚本。 如果该脚本使用 RevoScaleR 函数、 自动处理并行处理，并且不应设置 `@parallel` 到 `1`。

    如果 R 脚本可以实现并行化，并且如果 [!INCLUDE[tsql_md](../../includes/tsql-md.md)] 查询可并行化，然后 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 将创建多个并行的进程 (最多 __最大并行 MAXDOP 度__ 设置 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)],，) 和所有进程中运行同一个脚本。 每个进程只接收一部分数据，因此这不是有用的脚本必须看到的所有数据，如在训练模型时。 但是，它可并行执行任务，如批预测时。 有关详细信息使用的并行性 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md), ，请参阅 __高级技巧︰ 并行处理__ 部分 [TRANSACT-SQL 中使用 R 代码](../../advanced-analytics/r-services/using-r-code-in-transact-sql-sql-server-r-services.md)。

* 使用 rx 函数时使用 SQL Server 计算上下文，设置 `numTasks` 到您要创建的进程数。 创建进程的实际数量由 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], ，并且可能小于所请求。 创建的进程数绝不会超过 __MAXDOP__。

    如果 R 脚本可以实现并行化，并且如果 [!INCLUDE[tsql_md](../../includes/tsql-md.md)] 查询可并行化，然后 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 运行 rx 函数时，将创建多个并行的进程。

将创建的进程数取决于多种因素，例如对资源进行监管、 资源、 其他会话和使用 R 脚本使用的查询的查询执行计划的当前使用情况。 

### 查询并行度

若要确保可以并行分析数据，用于检索数据的查询应分帧的方式，它可将自身呈现为支持并行执行。 

[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 支持使用 SQL 数据源使用 `RxSqlServerData` 以指定的源。 源可以是表或查询。 例如，下面的代码示例这两个定义基于 SQL 查询的 R 数据源对象︰
~~~~
RxSqlServerData(table=”airline”, connectionString = sqlConnString)
~~~~

~~~~
RxSqlServerData(sqlquery=”select [ArrDelay],[CRSDepTime],[DayOfWeek] from airlineWithIndex where rowNum <= 100000”, connectionString = sqlConnString)
~~~~ 

如分析算法拉出大量的表中的数据，请务必确保提供给查询 `RxSqlServerData` 并行执行的优化。 不会导致并行执行计划的查询可能会导致计算单个进程。

[!INCLUDE[ssManStudioFull_md](../../includes/ssmanstudiofull-md.md)] 可以用于分析执行计划，并改进查询性能。 例如，表中的缺失索引可能会影响所需执行的查询的时间。 请参阅 [监视和优化性能](../../relational-databases/performance/monitor-and-tune-for-performance.md) 有关详细信息。

该查询将检索多于所需的列时，可能会影响性能的另一个监督。 例如，如果公式基于仅 3 列，并且表中包含 30 列，请执行不使用查询如 `select *` 或选择多于所需的列数。

> [!NOTE]
> 如果数据源而不是一个查询中指定了表 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 内部确定必需的列，以从表中提取的; 但是，此方法不太可能会导致并行执行。

## 算法参数

许多 rx 定型算法都支持参数来控制定型模型的生成方式。 虽然的准确性和正确性的模型很重要，算法的性能可能会同样重要。 您可以修改 parametersthe 模型定型参数以提高速度计算，并且在许多情况下，您可能能够提高性能，而不会降低准确性和正确性。 

例如， `rxDTree` 支持 `maxDepth` 参数，它控制的最大的树深度。 作为 `maxDepth` 是增加，性能可能会降低，因此务必要分析的增加对性能的影响与深度的好处。 

可以与使用的参数之一 `rxLinMod` 和 `rxLogit` 是 `cube` 参数。 该公式的第一个的因变量是一个因素变量时，则可以使用此参数。 如果 `cube` 设置为 `TRUE`, ，完成回归使用分区的反转，可能会更快，并使用的内存少于标准回归计算。 如果公式中有大量的变量，则性能提升可能非常大。

 [RevoScaleR](https://msdn.microsoft.com/microsoft-r/scaler/scaler) 用户指南具有控制模型适合于各种算法的一些有用信息。 例如，对于 `rxDTree` 可以控制时间复杂性和预测准确性通过如调整参数之间的平衡 `maxNumBins`, ，`maxDepth`, ，`maxComplete`, ，和 `maxSurrogate`。 增加到超过 10 或 15 的深度可以使计算耗费大量资源。

有关详细信息优化性能 `rxDForest` 和 `rxDTree`, ，请参阅 [性能优化选项 rxDForest/rxDTree](https://support.microsoft.com/kb/3104235)。

## 模型和预测

一旦已完成了培训并选择最佳模型中，我们建议将模型存储在数据库中，以便它随时可供预测。 对于需要预测的联机事务处理，从该预测的数据库加载预先计算的模型是非常有效。 示例脚本使用此方法进行序列化和将模型存储在数据库表。 用于预测，该模型是从数据库执行反序列化。

尤其是在大型数据集上使用时，生成的算法，如 lm 或 glm 某些模型可能会很大。 以下是可以存储在数据的大小限制 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]。 应将其存储到数据库之前清理此模型。

> [!NOTE] 如果使用存储的模型并将分析集成到应用程序的快速预测文件是一个重要的方案，我们建议 __DeployR__。 可用来轻松地集成 web、 桌面、 移动和仪表板应用程序内部的 R 分析。 具体而言，非常适合存储模型，然后再执行使用存储的模型的单个行预测。 有关详细信息，请参阅 [有关 DeployR](https://msdn.microsoft.com/microsoft-r/rserver/deployr-about)。

## 另请参阅
[对资源进行监管](../../advanced-analytics/r-services/resource-governance-for-r-services.md)
[资源调控器](../../relational-databases/resource-governor/resource-governor.md)

[创建外部的资源池](../../t-sql/statements/create-external-resource-pool-transact-sql.md)

 [SQL Server R 服务性能优化指南](../../advanced-analytics/r-services/sql-server-r-services-performance-tuning.md)
 
 [R 服务的 SQL Server 配置](../../advanced-analytics/r-services/sql-server-configuration-r-services.md)
 
 [性能案例研究](../../advanced-analytics/r-services/performance-case-study-r-services.md)
 