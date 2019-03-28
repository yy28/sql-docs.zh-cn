---
title: 性能优化的数据优化-SQL Server 机器学习服务
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 4fdc699437ef44d32e944d810e9e38571d20472c
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58510884"
---
# <a name="performance-for-r-services---data-optimization"></a>R Services-数据优化性能
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文是介绍了性能优化基于两个案例研究的 R Services 的一系列中的第三。 本文介绍适用于 R 的性能优化或 SQL Server 中运行的 Python 脚本。 它还介绍了可用于更新 R 代码，来提高性能并避免已知的问题的方法。

## <a name="choosing-a-compute-context"></a>选择计算上下文

在 SQL Server 2016 和 2017年中，您可以使用**本地**或**SQL**运行 R 或 Python 脚本时计算上下文。

使用时**本地**计算上下文，分析您的计算机上并不是服务器上执行。 因此，如果从 SQL Server 以使用在代码中获取数据，必须通过网络中提取的数据。 这种网络传输造成的性能下降取决于传输的数据大小、网络速度，以及同时发生的其他网络传输数量。

使用时**SQL Server 计算上下文**，在服务器上执行的代码。 如果从 SQL Server 中获取数据，数据应运行分析的服务器的本地，因此会造成任何网络开销。 如果需要从其他源导入数据，请考虑预先排列 ETL。

处理大型数据集时，始终应该使用 SQL 计算上下文。

## <a name="factors"></a>因子

R 语言提供的概念*因素*，这是为分类数据的特殊变量。 数据科学家通常在公式中使用因子变量，因为处理分类变量作为因素可确保数据由机器学习函数中正确处理。 有关详细信息，请参阅[for Dummies R:因子变量](https://www.dummies.com/programming/r/how-to-look-at-the-structure-of-a-factor-in-r/)。

根据设计，因子变量可以从字符串转换为整数和后再次进行存储或处理。 R`data.frame`函数作为因子变量，除非可处理的所有字符串自变量*stringsasfactors 设*设置为**False**。 这意味着字符串是自动转换为整数进行处理，并随后映射回原始字符串。

如果源数据中的因素存储为一个整数，则可能会降低性能，因为 R 运行时，将身份整数转换为字符串，然后执行其自身内部字符串到整数的转换。

若要避免这种运行时转换，请考虑将值存储为整数在 SQL Server 表中，并使用_colInfo_参数，以指定列用作因子级别。 RevoScaleR 中的大多数数据源对象使用参数_colInfo_。 使用此参数命名数据源使用的变量，指定其类型，以及定义变量级别或转换的列的值。

例如，以下 R 函数调用从表中获取整数 1、 2 和 3，但映射的值为一个因子级别"apple"、"橙色"和"banana"。

```R
c("fruit" = c(type = "factor", levels=as.character(c(1:3)), newLevels=c("apple", "orange", "banana")))
```

当源列包含字符串时，它是始终的详细信息指定事先使用级别高效_colInfo_参数。 例如，下面的 R 代码将字符串视为因素在被读取。

```R
c("fruit" = c(type = "factor", levels= c("apple", "orange", "banana")))
```

如果模型生成中的没有语义差异后, 一种方法可能导致更好的性能。

## <a name="data-transformations"></a>数据转换

数据科研人员通常在分析过程中使用以 R 语言编写的转换函数。 转换函数应用于从表中检索每个行。 在 SQL Server 中，此类转换不适用于在一个批处理中，这要求 R 解释器和分析引擎之间的通信中检索到的所有行。 执行转换时，数据将从 SQL 移到分析引擎，再移到 R 解释程序进程，然后转移回去。

出于此原因，在 R 代码中使用转换可以具有的算法，具体取决于涉及的数据量的性能明显负面影响。

它是具有所有必要的列中的表或视图，然后再执行分析，并在计算期间避免转换更有效。 如果无法将更多的列添加到现有表中，可以考虑创建另一个表或视图来包含转换后的列，然后使用相应的查询来检索数据。

## <a name="batch-row-reads"></a>批处理行读取

如果你使用 SQL Server 数据源 (`RxSqlServerData`) 在代码中，我们建议您尝试使用参数_rowsPerRead_指定批大小。 此参数定义查询，然后发送到外部脚本进行处理的行的数。 在运行时，该算法会看到仅指定的每个批中的行数。

若要控制每次处理的数据量的功能可以帮助您解决或避免出现问题。 例如，如果输入数据集是非常宽 （有许多列），或者如果数据集具有几个大型列 （如自定义文本），则可以降低批处理大小，以避免内存不足的分页数据。

默认情况下，此参数的值设置为 50000，以确保即使在内存不足的计算机上的不错的性能。 如果服务器具有足够的可用内存，此值增大到 500,000 个成员或甚至 1,000,000 可以产生更好的性能，尤其是对于大型表。

增加批大小变得很明显，大量的数据集，并可在多个进程运行的任务中的好处。 但是，增加此值不一定总能产生最佳结果。 我们建议你试用你的数据和算法来确定最佳值。

## <a name="parallel-processing"></a>并行处理

若要提高的性能**rx**分析函数，你可以利用 SQL Server 能够使用在服务器计算机上的可用内核并行执行任务。

有两种方法来实现在 SQL Server 中使用 R 的并行化：

-   **使用\@并行。** 使用 `sp_execute_external_script` 存储过程运行 R 脚本时，将 `@parallel` 参数设置为 `1`。 这是最好的方法，如果 R 脚本的作用**不**使用 RevoScaleR 函数，它们具有其他机制进行处理。 如果您的脚本使用 RevoScaleR 函数 （通常带有"rx"前缀）、 自动执行并行处理，且并不需要显式设置`@parallel`到`1`。

    如果可以并行执行 R 脚本，并且可以并行执行的 SQL 查询，数据库引擎将创建多个并行进程。 可以创建的进程的最大数目是否等于**最大并行度**(MAXDOP) 实例的设置。 所有进程然后运行同一个脚本，但收到只有部分数据。
    
    因此，此方法不是有用的脚本必须查看所有数据，例如在定型模型。 但是，在并行执行批量预测等任务时，这种方式却很有作用。 有关详细信息使用与并行度`sp_execute_external_script`，请参阅**高级技巧： 并行处理**部分[TRANSACT-SQL 中使用 R 代码](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)。

-   **使用 numTasks = 1。** 使用时**rx**函数在 SQL Server 计算上下文中，将设置的值_numTasks_到想要创建的进程数参数。 创建的进程数永远不能超过**MAXDOP**; 但是，实际创建的进程数由数据库引擎和可能低于您请求。

    如果可以并行执行 R 脚本，并且可以并行执行的 SQL 查询，然后 SQL Server 创建多个并行进程运行 rx 函数时。 进程创建的实际数目取决于许多因素，例如，资源监管、 当前使用情况的资源、 其他会话和使用 R 脚本使用的查询的查询执行计划。

## <a name="query-parallelization"></a>查询并行度

在 Microsoft R 中，您可以使用 SQL Server 数据源通过定义为 RxSqlServerData 数据源对象的数据。

创建基于整个表或视图的数据源：

```R
RxSqlServerData(table= "airline", connectionString = sqlConnString)
```

创建基于 SQL 的查询的数据源：

```R
RxSqlServerData(sqlQuery= "SELECT [ArrDelay],[CRSDepTime],[DayOfWeek] FROM  airlineWithIndex WHERE rowNum <= 100000", connectionString = sqlConnString)
```

> [!NOTE]
> 如果数据源而不是查询中指定一个表，则 R Services 使用内部试探法来确定所需的列来提取表;但是，此方法不太可能导致并行执行。

若要确保可以并行分析的数据，用于检索数据的查询应括在数据库引擎可以创建一个并行查询计划的方式。 如果代码或算法使用的大量数据，请确保提供给查询`RxSqlServerData`适用于并行执行。 无法生成并行执行计划的查询可能会导致计算单个进程。

如果需要处理大型数据集，使用 Management Studio 或在运行 R 代码中之前, 的另一个 SQL 查询分析器来分析执行计划。 然后，执行任何建议的步骤来提高查询性能。 例如，表中的缺失某个索引可能会影响执行查询所要花费的时间。 有关详细信息，请参阅[监视和优化性能](../../relational-databases/performance/monitor-and-tune-for-performance.md)。

可能会影响性能的另一个常见错误是，查询将检索多于所需的列数。 例如，如果公式根据只有三个列，但在源表中包含 30 列，您要将数据移动不必要地。

 + 避免使用`SELECT *`！
 + 需要一些时间才能查看数据集中的列，并确定不仅仅需要进行分析
 + 从查询中删除包含数据类型与 R 代码，例如 GUID 和 rowguid 不兼容的任何列
 + 检查不受支持的日期和时间格式
 + 而不是加载一个表，请创建一个视图，可选择特定值或转换列，以免转换错误

## <a name="optimizing-the-machine-learning-algorithm"></a>优化机器学习算法

本部分提供的其他提示和特定于 RevoScaleR 和其他选项在 Microsoft R 中的资源

> [!TIP]
> R 优化的一般讨论已超出本文的范围。 但是，如果需要更快地使您的代码，我们建议热门文章[R Inferno](https://www.burns-stat.com/pages/Tutor/R_inferno.pdf)。 它介绍了在 R 中的编程构造和鲜艳的语言和详细信息中的常见缺陷，并提供了许多特定示例的 R 编程技术。

### <a name="optimizations-for-revoscaler"></a>对于 RevoScaleR 的优化

许多 RevoScaleR 算法支持使用参数来控制如何生成训练的模型。 重要的精确性和正确性的模型时，算法的性能可能也同样重要。 若要获取适当的平衡准确性和训练时间之间，可以修改参数以提高速度的计算，并在许多情况下，在不降低精确性和正确性的情况下提高性能。

+ [rxDTree](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdtree)

    `rxDTree` 支持`maxDepth`参数，它控制决策树的深度。 作为`maxDepth`是增加，可能会降低性能，所以务必要分析的增加的深度与损害性能优势。

    您还可以控制时间复杂性与预测准确性通过如调整参数之间的平衡`maxNumBins`， `maxDepth`， `maxComplete`，和`maxSurrogate`。 将深度增大到 10 或 15 以上可能会使计算开销变得极高。

+ [rxLinMod](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlinmod)

    请尝试使用`cube`参数，如果在公式中的第一个相关变量是因子变量。
    
    当`cube`设置为`TRUE`，使用分块求逆，它可能会更快，使用更少的内存比标准回归计算执行回归。 如果公式中有大量的变量，性能提升可能非常明显。

+ [rxLogit](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlogit)

    使用`cube`参数，如果第一个因变量是因子变量。
    
    当`cube`设置为`TRUE`，该算法使用分块求逆，它可能会更快，使用更少的内存。 如果公式中有大量的变量，性能提升可能非常明显。

RevoScaleR 优化的其他指南，请参阅以下文章：

+ 支持文章：[RxDForest 和 rxDTree 用于性能调整选项](https://support.microsoft.com/kb/3104235)

+ 用于控制提升的树模型中容纳不下的模型的方法：[估计使用随机渐进提升模型](https://docs.microsoft.com/r-server/r/how-to-revoscaler-boosting)

+ RevoScaleR 如何移动并处理数据的概述：[ScaleR 中编写块区的自定义算法](https://docs.microsoft.com/r-server/r/how-to-developer-write-chunking-algorithms)

+ RevoScaleR 的编程模型：[管理 RevoScaleR 中的线程](https://docs.microsoft.com/r-server/r/how-to-developer-manage-threads)

+ 函数的参考[rxDForest](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdforest)

+ 函数的参考[rxBTrees](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxbtrees)

### <a name="use-microsoftml"></a>Use MicrosoftML

我们还建议你查看到新**MicrosoftML**包，其中提供了可以使用计算上下文和提供的 RevoScaleR 的转换的可缩放的机器学习算法。

+ [开始使用 MicrosoftML](https://docs.microsoft.com/r-server/r/concept-what-is-the-microsoftml-package)

+ [如何选择 MicrosoftML 算法](https://docs.microsoft.com/r-server/r/how-to-choose-microsoftml-algorithms-cheatsheet)

### <a name="operationalize-a-solution-using-microsoft-r-server"></a>使用 Microsoft R Server 解决方案

如果你的方案涉及使用存储的模型的快速预测，或者将机器学习集成到应用程序，您可以使用[操作化](https://docs.microsoft.com/r-server/what-is-operationalization)（以前称为 DeployR） 的 Microsoft R Server 中的功能。

+ 作为**数据科学家**，使用[mrsdeploy 包](https://docs.microsoft.com/r-server/r-reference/mrsdeploy/mrsdeploy-package)可以与其他计算机共享 R 代码中集成 R 分析 web、 桌面、 移动和仪表板应用程序内：[如何发布和管理 R R Server 中的 web 服务](https://docs.microsoft.com/r-server/operationalize/how-to-deploy-web-service-publish-manage-in-r)

+ 作为**管理员**，了解如何管理包、 监视 web 节点和计算节点，以及控制 R 作业的安全性：[在 R 中如何与之交互，并使用 web services](https://docs.microsoft.com/r-server/operationalize/how-to-consume-web-service-interact-in-r)

## <a name="articles-in-this-series"></a>本系列文章

[性能优化适用于 R 的简介](sql-server-r-services-performance-tuning.md)

[R 的 SQL Server 配置的性能优化](sql-server-configuration-r-services.md)

[R-R 的性能优化的代码和数据优化](r-and-data-optimization-r-services.md)

[性能优化-案例研究结果](performance-case-study-r-services.md)
