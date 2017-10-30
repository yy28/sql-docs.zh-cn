---
title: "R Services-数据优化的性能 |Microsoft 文档"
ms.custom: 
ms.date: 07/12/2017
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
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: df91cedac15da65bee9c9aa38c3c747e04f6d60d
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="performance-for-r-services---data-optimization"></a>R Services-数据优化的性能

本文是介绍 R 服务基于两个案例研究的性能优化的一系列中的第三。 本文讨论的 R 性能优化或 Python 脚本在 SQL Server 中运行。 它还介绍了可用于更新你的 R 代码，同时以提升性能并避免已知的问题的方法。

## <a name="choosing-a-compute-context"></a>选择计算上下文

在 SQL Server 2016 和自 2017 年中，你可以使用**本地**或**SQL**运行 R 或 Python 脚本时计算上下文。

使用时**本地**计算上下文，分析会执行您的计算机上，并不在服务器上。 因此，如果您从 SQL Server 以使用你的代码中获取数据，必须通过网络中提取数据。 这种网络传输造成的性能下降取决于传输的数据大小、网络速度，以及同时发生的其他网络传输数量。

使用时**SQL Server 计算上下文**，在服务器上执行的代码。 如果您从 SQL Server 中获取数据，应将运行分析，在服务器本地数据，并因此引入任何网络开销。 如果你需要从其他源导入数据，请考虑预先排列 ETL。

处理大型数据集时，始终应该使用 SQL 计算上下文。

## <a name="factors"></a>因子

R 语言提供"因素"，是的分类数据的特殊变量的概念。 数据科研人员通常在其公式中使用因素变量，因为处理分类变量作为因素，可确保数据由机器学习函数进行正确处理。 有关详细信息，请参阅 [虚拟值的 R： 因素变量] (http://www.dummies.com/programming/r/how-to-look-at-the-structure-of-a-factor-in-r/)。

按照设计，因素变量可以从字符串转换为整数和回后再次存储或处理。 R`data.frame`函数作为因素变量处理所有字符串，除非参数*stringsAsFactors*设置为**False**。 这意味着是字符串的自动转换为整数以进行处理，并且随后映射回原始字符串。

如果因素的源数据存储为整数，性能会降低，因为 R 运行时，将因素整数转换为字符串，然后执行其自身内部字符串到整数的转换。

若要避免这种运行时转换，请考虑将值存储为整数在 SQL Server 表中，并使用_colInfo_参数来指定用作因素的列的级别。 RevoScaleR 中的大多数数据源对象接收参数_colInfo_。 使用此参数命名数据源使用的变量，指定其类型，并定义的列的值的变量级别或转换。

例如，以下的 R 函数调用从表中获取整数 1、 2 和 3，但映射的值与因子的级别"apple"、"橙色"和"香蕉"。

```R
c("fruit" = c(type = "factor", levels=as.character(c(1:3)), newLevels=c("apple", "orange", "banana")))
```

当源列包含字符串时，始终会指定事先使用级别高效_colInfo_参数。 例如，下面的 R 代码将字符串视为因素在被读取。

```R
c("fruit" = c(type = "factor", levels= c("apple", "orange", "banana")))
```

如果不没有在模型生成任何语义差异后, 一种方法可以导致更好的性能。

## <a name="data-transformations"></a>数据转换

数据科研人员通常在分析过程中使用以 R 语言编写的转换函数。 转换函数应用于从表中检索每个行。 在 SQL Server，此类转换将应用于在一个批处理，这需要的 R 解释程序和分析引擎之间的通信中检索的所有行。 执行转换时，数据将从 SQL 移到分析引擎，再移到 R 解释程序进程，然后转移回去。

为此，作为 R 代码的一部分使用转换可以具有的算法，具体取决于涉及的数据量的性能将显著负面影响。

它会更加高效，具有所有必需的列中的表或视图，然后再执行分析，并在计算期间避免转换。 如果无法将更多的列添加到现有表中，可以考虑创建另一个表或视图来包含转换后的列，然后使用相应的查询来检索数据。

## <a name="batch-row-reads"></a>批处理行读取

如果你使用 SQL Server 数据源 (`RxSqlServerData`) 在代码中，我们建议你尝试使用参数_rowsPerRead_来指定批大小。 此参数定义查询，然后发送到外部脚本进行处理的行的数。 在运行时，算法会看到仅指定的每个批中的行数。

能够控制一次处理的数据量可以帮助你解决或避免出现问题。 例如，如果输入数据集是范围很大 （具有许多列），或者，如果数据集具有几个大型列 （如可用的文本），则可以降低批处理大小，以避免内存不足的分页数据。

默认情况下，此参数的值设置为 50000，以确保不错的性能，甚至在内存不足的计算机上。 如果服务器具有足够的可用内存，则增加此值为 500000 或甚至万个可以产生更好的性能，尤其是对于大型表。

增加批大小变得对大型数据集，并可以在多个进程运行的任务中非常明显的好处。 但是，增加此值才会始终产生最佳结果。 我们建议使用你的数据和算法来确定最佳的值进行试验。

## <a name="parallel-processing"></a>并行处理

若要提高的性能**rx**分析函数，你可以利用 SQL Server 能够使用在服务器计算机上的可用内核的并行执行任务。

有两种方法来实现并行化，使用 SQL Server 中的 R:

-   **使用\@并行。** 使用 `sp_execute_external_script` 存储过程运行 R 脚本时，将 `@parallel` 参数设置为 `1`。 这是最好的方法，如果 R 脚本执行**不**使用 RevoScaleR 函数，它们具有其他机制进行处理。 如果你的脚本使用 RevoScaleR 函数 （通常前缀为"rx"）、 自动执行并行处理，并且不需要显式设置`@parallel`到`1`。

    如果 R 脚本可以并行化，并且可以并行化 SQL 查询，数据库引擎将创建多个并行的进程。 可以创建的进程的最大数等于**最大并行度**(MAXDOP) 实例的设置。 所有进程然后运行同一个脚本，但收到仅部分的数据。
    
    因此，此方法不是有用的脚本，必须将所有数据，例如，当为模型定型。 但是，在并行执行批量预测等任务时，这种方式却很有作用。 有关详细信息使用使用并行`sp_execute_external_script`，请参阅**高级提示： 并行处理**部分[TRANSACT-SQL 中使用 R 代码](../tutorials/rtsql-using-r-code-in-transact-sql-quickstart.md)。

-   **使用 numTasks = 1。** 使用时**rx**在 SQL Server 计算上下文中，函数将设置的值_numTasks_参数到想要创建的进程数。 创建的进程数绝不会超过**MAXDOP**; 但是，由数据库引擎确定创建的进程的实际数目，并可能小于你请求。

    如果 R 脚本可以并行化，并且可以并行化 SQL 查询，，SQL Server 会创建多个并行的进程运行 rx 函数时。 创建的进程的实际数取决于各种因素，例如资源调控、 资源、 其他会话中，以及使用 R 脚本所使用的查询的查询执行计划的当前使用情况。

## <a name="query-parallelization"></a>查询并行度

在 Microsoft R 中，你可使用 SQL Server 数据源通过 RxSqlServerData 数据源对象定义你的数据。

创建基于整个表或视图的数据源：

```R
RxSqlServerData(table= "airline", connectionString = sqlConnString)
```

创建基于 SQL 查询的数据源：

```R
RxSqlServerData(sqlQuery= "SELECT [ArrDelay],[CRSDepTime],[DayOfWeek] FROM  airlineWithIndex WHERE rowNum <= 100000", connectionString = sqlConnString)
```

> [!NOTE]
> 如果在数据源而不是查询中指定了表，R Services 将使用内部试探法来确定要从表; 获取的必需列但是，这种方法是不太可能导致并行执行。

若要确保可以并行分析数据，用于检索数据的查询应分帧数据库引擎可以创建并行查询计划的方式。 如果代码或算法使用的大量数据，请确保提供给查询`RxSqlServerData`非常适合并行执行。 无法生成并行执行计划的查询可能会导致计算单个进程。

如果你需要处理大型数据集，使用 Management Studio 或另一个 SQL 查询分析器中的运行 R 代码，请先分析的执行计划。 然后，执行任何建议的步骤来提高查询性能。 例如，表中的缺失某个索引可能会影响执行查询所要花费的时间。 有关详细信息，请参阅[监视和优化性能](../../relational-databases/performance/monitor-and-tune-for-performance.md)。

可能会影响性能的另一个常见错误是查询检索多于所需的列数。 例如，如果公式基于只有三个列，但你源表具有 30 列，您正在不必要地移动数据。

 + 避免使用`SELECT *`！
 + 需要一些时间来查看数据集中的列并确定只有所需的分析
 + 从你的查询中删除任何包含与 R 代码，例如 GUID 和 rowguid 不兼容的数据类型的列
 + 检查不受支持的日期和时间格式
 + 而不是加载表，创建一个视图，选择特定值或强制转换列，以免转换错误

## <a name="optimizing-the-machine-learning-algorithm"></a>优化机器学习算法

本部分提供的其他提示和特定于 RevoScaleR 和 Microsoft。 中的其他选项的资源

> [!TIP]
> 本文的范围超出了 R 优化的常规讨论。 但是，如果你需要使代码更快，我们建议热门文章， [R Inferno](http://www.burns-stat.com/pages/Tutor/R_inferno.pdf)。 它介绍 R 中的编程构造以及鲜艳语言和的详细信息，常见的问题，并提供了许多特定示例的 R 编程技术。

### <a name="optimizations-for-revoscaler"></a>RevoScaleR 的优化

许多 RevoScaleR 算法支持参数来控制如何生成训练的模型。 重要的准确性和正确性的模型时，该算法的性能可能同样重要。 若要获取准确性和训练时间之间的最佳平衡，你可以修改的参数以提高速度的计算，并在许多情况下，而不会降低准确性和正确性提高性能。

+ [rxDTree](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdtree)

    `rxDTree`支持`maxDepth`参数，它控制决策树的深度。 作为`maxDepth`是增加，性能可能会降低，因此务必要分析的增加的深度与采用性能优势。

    你还可以控制通过如调整参数的时间复杂性和预测准确性之间的平衡`maxNumBins`， `maxDepth`， `maxComplete`，和`maxSurrogate`。 将深度增大到 10 或 15 以上可能会使计算开销变得极高。

+ [rxLinMod](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlinmod)

    请尝试使用`cube`参数如果公式中的第一个依赖变量是一个因素变量。
    
    当`cube`设置为`TRUE`，使用分区函数，它可能更快，使用标准回归计算小于内存反函数执行回归。 如果公式中有大量的变量，性能提升可能非常明显。

+ [rxLogit](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxlogit)

    使用`cube`参数如果第一个依赖变量是一个因素变量。
    
    当`cube`设置为`TRUE`，该算法使用分区的逆，它可能更快，使用较少的内存。 如果公式中有大量的变量，性能提升可能非常明显。

RevoScaleR 优化的其他指南，请参阅以下文章：

+ 支持文章：[性能优化 rxDForest 和 rxDTree 选项](https://support.microsoft.com/kb/3104235)

+ 用于控制模型的方法适合提升的树模型中：[估计模型使用随机渐进提升](https://docs.microsoft.com/r-server/r/how-to-revoscaler-boosting)

+ 概述如何 RevoScaleR 移动，以及处理数据：[在 ScaleR 中编写自定义的分块算法](https://docs.microsoft.com/r-server/r/how-to-developer-write-chunking-algorithms)

+ RevoScaleR 的编程模型：[管理 RevoScaleR 中的线程](https://docs.microsoft.com/r-server/r/how-to-developer-manage-threads)

+ 函数的参考[rxDForest](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxdforest)

+ 函数的参考[rxBTrees](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxbtrees)

### <a name="use-microsoftml"></a>使用 MicrosoftML

我们还建议你查看到新**MicrosoftML**包，其中提供计算上下文和提供的 RevoScaleR 的转换可以使用的可缩放的机器学习算法。

+ [要开始使用 MicrosoftML](https://docs.microsoft.com/r-server/r/concept-what-is-the-microsoftml-package)

+ [如何选择 MicrosoftML 算法](https://docs.microsoft.com/r-server/r/how-to-choose-microsoftml-algorithms-cheatsheet)

### <a name="operationalize-a-solution-using-microsoft-r-server"></a>具有可操作性使用 Microsoft R Server 的解决方案

如果你的方案涉及使用存储的模型中，快速预测，或者将机器学习集成到应用程序，你可以使用[操作化](https://docs.microsoft.com/r-server/what-is-operationalization)Microsoft R Server （以前称为 DeployR） 中的功能。

+ 作为**数据科学家**，使用[mrsdeploy 包](https://docs.microsoft.com/r-server/r-reference/mrsdeploy/mrsdeploy-package)与其他计算机共享 R 代码和将其集成 web、 桌面、 移动和仪表板应用程序内的 R 分析：[如何发布和管理 R R Server 中的 web 服务](https://docs.microsoft.com/r-server/operationalize/how-to-deploy-web-service-publish-manage-in-r)

+ 作为**管理员**时，了解如何管理包，请监视 web 节点计算节点，并控制在 R 作业上的安全：[如何与交互和使用 R 中的 web 服务](https://docs.microsoft.com/r-server/operationalize/how-to-consume-web-service-interact-in-r)

## <a name="articles-in-this-series"></a>本系列文章

[性能优化 R – 简介](sql-server-r-services-performance-tuning.md)

[性能优化 R-SQL Server 配置](sql-server-configuration-r-services.md)

[性能优化 R-R 代码和数据优化](r-and-data-optimization-r-services.md)

[性能优化的案例研究结果](performance-case-study-r-services.md)

