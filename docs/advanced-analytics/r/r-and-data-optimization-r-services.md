---
title: 数据优化的性能优化
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 95cbcd152e9f7665191e44b7c6d704d2b0c63037
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470037"
---
# <a name="performance-for-r-services---data-optimization"></a>R Services 的性能-数据优化
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文是一系列文章中的第三篇, 介绍了基于两例研究的 R Services 的性能优化。 本文介绍 SQL Server 中运行的 R 或 Python 脚本的性能优化。 它还介绍了可用于更新 R 代码的方法, 这些方法可以提高性能并避免已知问题。

## <a name="choosing-a-compute-context"></a>选择计算上下文

在 SQL Server 2016 和2017中, 可以在运行 R 或 Python 脚本时使用**本地**计算上下文或**SQL**计算上下文。

使用**本地**计算上下文时, 将在计算机上执行分析, 而不是在服务器上执行。 因此, 如果从 SQL Server 获取要在代码中使用的数据, 则必须通过网络获取数据。 这种网络传输造成的性能下降取决于传输的数据大小、网络速度，以及同时发生的其他网络传输数量。

使用**SQL Server 计算上下文**时, 将在服务器上执行代码。 如果要从 SQL Server 获取数据, 则数据应在运行分析的服务器本地, 因此不会引入任何网络开销。 如果需要从其他源导入数据, 请考虑事先安排 ETL。

处理大型数据集时，始终应该使用 SQL 计算上下文。

## <a name="factors"></a>因子

R 语言具有*因素*的概念, 这是分类数据的特殊变量。 数据科学家通常会在其公式中使用系数变量, 因为将分类变量作为因素进行处理可确保机器学习功能正确处理数据。 有关详细信息, 请[参阅 R for 进一步:系数变量](https://www.dummies.com/programming/r/how-to-look-at-the-structure-of-a-factor-in-r/)。

按照设计, 可将因素变量从字符串转换为整数, 并再次返回以进行存储或处理。 R `data.frame`函数将所有字符串作为因子变量处理, 除非将参数*stringsAsFactors*设置为**False**。 这意味着字符串会自动转换为整数进行处理, 然后再映射回原始字符串。

如果系数的源数据存储为整数, 则性能可能会降低, 因为 R 会在运行时将系数整数转换为字符串, 然后执行其自身的内部字符串到整数的转换。

若要避免此类运行时转换, 请考虑将值存储为 SQL Server 表中的整数, 并使用_colInfo_参数为用作因子的列指定级别。 RevoScaleR 中的大多数数据源对象均采用参数_colInfo_。 您可以使用此参数来命名数据源使用的变量, 指定其类型, 并定义变量级别或对列值的转换。

例如, 以下 R 函数调用从表中获取整数1、2和 3, 但将值映射到级别为 "apple"、"橙色" 和 "香蕉" 的因子。

```R
c("fruit" = c(type = "factor", levels=as.character(c(1:3)), newLevels=c("apple", "orange", "banana")))
```

如果源列包含字符串, 则使用_colInfo_参数提前指定更高的级别总是更为有效。 例如, 下面的 R 代码在读取字符串时将其视为因素。

```R
c("fruit" = c(type = "factor", levels= c("apple", "orange", "banana")))
```

如果模型生成没有语义差异, 则后一种方法可以提高性能。

## <a name="data-transformations"></a>数据转换

数据科研人员通常在分析过程中使用以 R 语言编写的转换函数。 转换函数应用于从表中检索到的每一行。 在 SQL Server 中, 此类转换应用于批中检索到的所有行, 这需要 R 解释器和分析引擎之间的通信。 执行转换时，数据将从 SQL 移到分析引擎，再移到 R 解释程序进程，然后转移回去。

出于此原因, 在 R 代码中使用转换会对算法的性能产生严重影响, 具体取决于所涉及的数据量。

在执行分析之前, 必须在表或视图中具有所有必需的列, 并避免在计算过程中进行转换。 如果无法将更多的列添加到现有表中，可以考虑创建另一个表或视图来包含转换后的列，然后使用相应的查询来检索数据。

## <a name="batch-row-reads"></a>批处理行读取

如果在代码中使用 SQL Server 数据源`RxSqlServerData`(), 则建议尝试使用参数_rowsPerRead_来指定批大小。 此参数定义查询的行数, 然后将其发送到外部脚本进行处理。 在运行时, 该算法仅查看每个批处理中的指定行数。

能够控制一次处理的数据量, 可以帮助您解决或避免问题。 例如, 如果输入数据集的宽度非常宽 (包含多个列), 或者数据集具有几个大型列 (例如 "自由文本"), 则可以减少批大小, 以避免将数据分页出内存。

默认情况下, 此参数的值设置为 50000, 以确保即使在内存不足的计算机上也能提供相当高的性能。 如果服务器有足够的可用内存, 则将此值增大到500000甚至一百万可以获得更好的性能, 尤其是对于大型表。

增大批大小的优点在大型数据集上以及可在多个进程上运行的任务中变得很明显。 但是, 增大此值并不会始终产生最佳结果。 建议您试验您的数据和算法来确定最佳值。

## <a name="parallel-processing"></a>并行处理

为了提高**rx**分析函数的性能, 您可以利用 SQL Server 的能力, 使用服务器计算机上的可用内核并行执行任务。

在 SQL Server 中, 有两种方法可实现与 R 的并行化:

-   **使用\@并行。** 使用 `sp_execute_external_script` 存储过程运行 R 脚本时，将 `@parallel` 参数设置为 `1`。 如果 R 脚本**不**使用具有其他处理机制的 RevoScaleR 函数, 则这是最佳方法。 如果脚本使用 RevoScaleR 函数 (通常带有前缀 "rx"), 则会自动执行并行处理, 无需显式设置`@parallel`为。 `1`

    如果 R 脚本可并行化, 并且如果 SQL 查询可并行化, 则数据库引擎会创建多个并行进程。 可创建的最大进程数等于实例的**最大并行度**(MAXDOP) 设置。 然后, 所有进程都运行相同的脚本, 但只接收部分数据。
    
    因此, 此方法对于必须查看所有数据的脚本 (例如, 在训练模型时) 不起作用。 但是，在并行执行批量预测等任务时，这种方式却很有作用。 有关使用并行的`sp_execute_external_script`详细信息, 请参阅[在 transact-sql 中使用 R 代码](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)的**高级提示: 并行处理**部分。

-   **使用 numTasks = 1。** 在 SQL Server 计算上下文中使用**rx**函数时, 请将_numTasks_参数的值设置为你要创建的进程数。 创建的进程数永远不能超过**MAXDOP**;但是, 创建的进程的实际数量由数据库引擎确定, 可能小于你请求的进程数。

    如果 R 脚本可并行化, 并且可以并行化 SQL 查询, 则在运行 rx 函数时 SQL Server 会创建多个并行进程。 创建的实际进程数取决于各种因素, 例如资源调控、资源的当前使用情况、其他会话以及用于 R 脚本的查询的查询执行计划。

## <a name="query-parallelization"></a>查询并行化

在 Microsoft R 中, 可以通过将数据定义为 RxSqlServerData 数据源对象来处理 SQL Server 数据源。

基于整个表或视图创建数据源:

```R
RxSqlServerData(table= "airline", connectionString = sqlConnString)
```

创建基于 SQL 查询的数据源:

```R
RxSqlServerData(sqlQuery= "SELECT [ArrDelay],[CRSDepTime],[DayOfWeek] FROM  airlineWithIndex WHERE rowNum <= 100000", connectionString = sqlConnString)
```

> [!NOTE]
> 如果在数据源而不是查询中指定了表, 则 R Services 使用内部试探法来确定要从表中提取的必需列;但是, 这种方法不太可能导致并行执行。

为了确保数据可以并行分析, 用于检索数据的查询应该以数据库引擎可以创建并行查询计划的方式进行分帧。 如果代码或算法使用大量数据, 请确保为并行执行优化了给定`RxSqlServerData`的查询。 无法生成并行执行计划的查询可能会导致计算单个进程。

如果需要处理大型数据集, 请在运行 R 代码之前使用 Management Studio 或其他 SQL 查询分析器来分析执行计划。 然后, 执行任何建议的步骤来提高查询性能。 例如，表中的缺失某个索引可能会影响执行查询所要花费的时间。 有关详细信息, 请参阅[监视和优化性能](../../relational-databases/performance/monitor-and-tune-for-performance.md)。

可能影响性能的另一个常见错误是, 查询检索的列比所需的列多。 例如, 如果公式仅基于三列, 但您的源表包含30列, 则您不需要移动数据。

 + 避免使用`SELECT *`!
 + 花些时间查看数据集中的列, 并仅识别分析所需的列
 + 从查询中删除包含与 R 代码不兼容的数据类型的任何列, 如 GUID 和 rowguid
 + 检查不支持的日期和时间格式
 + 不加载表, 而是创建一个视图来选择特定值或强制转换列以避免转换错误

## <a name="optimizing-the-machine-learning-algorithm"></a>优化机器学习算法

本部分提供特定于 Microsoft R 中的 RevoScaleR 和其他选项的其他提示和资源。

> [!TIP]
> 有关 R 优化的一般讨论超出了本文的讨论范围。 但是, 如果您需要更快地编写代码, 我们建议您将[inferno 》](https://www.burns-stat.com/pages/Tutor/R_inferno.pdf)。 它包含 R 中的编程构造和鲜艳语言和详细信息的常见缺陷, 并提供了多个特定的 R 编程技术示例。

### <a name="optimizations-for-revoscaler"></a>RevoScaleR 的优化

许多 RevoScaleR 算法都支持参数以控制如何生成定型模型。 尽管模型的准确性和正确性非常重要, 但算法的性能可能也同样重要。 若要在准确性与定型时间之间取得适当的平衡, 可以修改参数以提高计算速度, 在许多情况下, 可以提高性能, 而无需降低准确性或正确性。

+ [rxDTree](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdtree)

    `rxDTree``maxDepth`支持参数, 该参数控制决策树的深度。 随着`maxDepth`增加, 性能可能会下降, 因此, 请务必分析提高深度与降低性能的好处。

    `maxNumBins`还可以通过调整`maxDepth` `maxComplete`、、和`maxSurrogate`等参数来控制时间复杂性和预测准确性之间的平衡。 将深度增大到 10 或 15 以上可能会使计算开销变得极高。

+ [rxLinMod](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlinmod)

    如果公式中`cube`的第一个依赖变量是系数变量, 则尝试使用该参数。
    
    当`cube`设置为`TRUE`时, 将使用已分区的反向执行回归, 这可能比标准回归计算更快, 使用的内存更少。 如果公式中有大量的变量，性能提升可能非常明显。

+ [rxLogit](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlogit)

    如果第一个从属变量是系数变量, 请使用参数。`cube`
    
    当`cube`设置为`TRUE`时, 算法将使用已分区的反向, 这可能会更快, 使用更少的内存。 如果公式中有大量的变量，性能提升可能非常明显。

有关 RevoScaleR 优化的其他指导, 请参阅以下文章:

+ 支持文章:[RxDForest 和 rxDTree 的性能优化选项](https://support.microsoft.com/kb/3104235)

+ 用于控制模型的方法适合提升树模型:[使用随机梯度提升来估算模型](https://docs.microsoft.com/r-server/r/how-to-revoscaler-boosting)

+ 概述 RevoScaleR 如何移动和处理数据:[在 ScaleR 中编写自定义分块算法](https://docs.microsoft.com/r-server/r/how-to-developer-write-chunking-algorithms)

+ RevoScaleR 的编程模型:[管理 RevoScaleR 中的线程](https://docs.microsoft.com/r-server/r/how-to-developer-manage-threads)

+ [RxDForest](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdforest)的函数引用

+ [RxBTrees](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxbtrees)的函数引用

### <a name="use-microsoftml"></a>使用 MicrosoftML

我们还建议你查看新的**MicrosoftML**包, 它提供可使用 RevoScaleR 提供的计算上下文和转换的可缩放机器学习算法。

+ [MicrosoftML 入门](https://docs.microsoft.com/r-server/r/concept-what-is-the-microsoftml-package)

+ [如何选择 MicrosoftML 算法](https://docs.microsoft.com/r-server/r/how-to-choose-microsoftml-algorithms-cheatsheet)

### <a name="operationalize-a-solution-using-microsoft-r-server"></a>使用 Microsoft R Server 操作解决方案

如果你的方案涉及使用存储的模型进行快速预测, 或者将机器学习集成到应用程序中, 则可以使用 Microsoft R Server 中的[操作化](https://docs.microsoft.com/r-server/what-is-operationalization)功能 (以前称为 DeployR)。

+ 作为**数据**专家, 使用[mrsdeploy 包](https://docs.microsoft.com/r-server/r-reference/mrsdeploy/mrsdeploy-package)与其他计算机共享 r 代码, 并在 web、桌面、移动和仪表板应用程序中集成 r 分析:[如何在 R Server 中发布和管理 R web 服务](https://docs.microsoft.com/r-server/operationalize/how-to-deploy-web-service-publish-manage-in-r)

+ 以**管理员身份**了解如何管理包、监视 web 节点和计算节点, 以及控制 R 作业的安全性:[如何与 R 交互并使用 web 服务](https://docs.microsoft.com/r-server/operationalize/how-to-consume-web-service-interact-in-r)

## <a name="articles-in-this-series"></a>本系列文章

[R 的性能优化-简介](sql-server-r-services-performance-tuning.md)

[R SQL Server 配置的性能优化](sql-server-configuration-r-services.md)

[R-R 代码和数据优化的性能优化](r-and-data-optimization-r-services.md)

[性能优化-案例研究结果](performance-case-study-r-services.md)
