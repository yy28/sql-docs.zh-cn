---
title: "R Services 的结果和资源的性能 |Microsoft 文档"
ms.custom: 
ms.date: 11/09/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0e902312-ad9c-480d-b82f-b871cd1052d9
caps.latest.revision: "8"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 65e3ca0b62da2a8412b92485316074a5f52fa080
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="performance-for-r-services-results-and-resources"></a>R 服务的性能： 结果和资源

本文是第四个和最后一个序列中，它描述 R Services 的性能优化。 本文总结了方法、 发现和的两个测试各种优化方法的案例研究的结论。

两个案例研究具有不同的目的：

+ 第一个案例研究，由 R Services 开发团队中，查找要测量的特定优化技术的影响
+ 第二个案例研究，由数据科学家团队，体验过多个方法，以确定特定的大容量评分方案的最佳的优化。

本主题列出的第一个案例研究的详细的结果。 对于第二个案例研究，摘要描述整体结果。 在本主题末尾是与所有脚本和示例数据，以及原始作者使用的资源的链接。

## <a name="performance-case-study-airline-dataset"></a>性能案例研究： 航班数据集

由 SQL Server R Services 开发团队本案例研究测试各种优化的效果。 创建单个 rxLogit 模型和评分执行航班数据集。 在训练和评分要评估各个影响的进程中应用了优化。

- Github:[示例数据和脚本](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning)有关 SQL Server 优化研究

### <a name="test-methods"></a>测试方法

1. 航班数据集中包含 10 分钟行单个的表。 它下载和大容量加载到 SQL Server。
2. 进行了六个表的副本。
3. 各种修改已应用到表，若要测试 SQL Server 功能，如 page 压缩，行压缩，索引，纵栏表数据存储区等的副本。
4. 每个优化已应用之前和之后进行测量性能。

| 表名| Description|
|------|------|
| *airline* | 使用 `rxDataStep` 从原始 xdf 文件转换的数据|                          |
| *airlineWithIntCol*   | *DayOfWeek* 已转换为整数而不是字符串。 另外，添加了 *rowNum* 列。|
| *airlineWithIndex*    | 数据与 *airlineWithIntCol* 表相同，但使用 *rowNum* 列添加了单个聚集索引。|
| *airlineWithPageComp* | 数据与 *airlineWithIndex* 表相同，但已启用页压缩。 另外，添加了基于 *CRSDepTime* 和 *ArrDelay* 计算得出的两个列：*CRSDepHour* 和 *Late*。 |
| *airlineWithRowComp*  | 数据与 *airlineWithIndex* 表相同，但已启用行压缩。 另外，添加了基于 *CRSDepTime* 和 *ArrDelay* 计算得出的两个列：*CRSDepHour* 和 *Late*。 |
| *airlineColumnar*     | 包含单个聚集索引的纵栏表存储。 此表中填充了来自已清理的 csv 文件中的数据。|

每个测试都包括下列步骤：

1. 运行每项测试之前已引发 R 垃圾回收。
2. 创建逻辑回归模型基于的表数据。 每项测试的 *rowsPerRead* 值设置为 500000。
3. 使用经过训练的模型生成评分
4. 每个测试运行六倍。 第一次运行 （"冷运行"） 的时间而被丢弃。 若要允许偶尔离群值，**最大**还删除剩余的五个运行之间的时间。 已使用四次剩余运行的平均值来计算每项测试的平均消耗运行时。
5. 使用已运行的测试*reportProgress*参数，并且值 3 （= 报表计时和进度）。 每个输出文件包含有关 IO、 转换时间和计算时间所用的时间信息。 这些时间可用于故障排除和诊断。
6. 控制台输出也已定向到输出目录中的文件。
7. 测试脚本中要计算的平均时间，通过运行这些文件处理时间。

例如，下面的结果是从单个测试的时间。 主要关注的时间是“总读取时间”（IO 时间）和“转换时间”（设置计算进程所产生的开销）。

**示例计时**

```
Running IntCol Test. Using airlineWithIntCol table.
run 1 took 3.66 seconds
run 2 took 3.44 seconds
run 3 took 3.44 seconds
run 4 took 3.44 seconds
run 5 took 3.45 seconds
run 6 took 3.75 seconds
  
Average Time: 3.4425
metric time pct
1 Total time 3.4425 100.00
2 Overall compute time 2.8512 82.82
3 Total read time 2.5378 73.72
4 Transition time 0.5913 17.18
5 Total non IO time 0.3134 9.10
```

我们建议你下载和修改测试脚本，以帮助你解决问题与 R 服务或使用 RevoScaleR 函数。

### <a name="test-results-all"></a>测试结果 （全部）

本部分比较为每个测试之前和之后的结果。

#### <a name="data-size-with-compression-and-a-columnar-table-store"></a>与压缩和纵栏表的表存储的数据大小

第一个测试比较使用压缩和纵栏表的表，以减少数据的大小。

| 表名            | “行”     | 保留   | data       | index_size | 未使用  | 节省率（保留） |
|-----------------------|----------|------------|------------|------------|---------|---------------------|
| *airlineWithIndex*    | 10000000 | 2978816 KB | 2972160 KB | 6128 KB    | 528 KB  | 0                   |
| *airlineWithPageComp* | 10000000 | 625784 KB  | 623744 KB  | 1352 KB    | 688 KB  | 79%                 |
| *airlineWithRowComp*  | 10000000 | 1262520 KB | 1258880 KB | 2552 KB    | 1088 KB | 58%                 |
| *airlineColumnar*     | 9999999  | 201992 KB  | 201624 KB  | 不适用        | 368 KB  | 93%                 |

**结论**

数据大小的最大减少是通过应用页压缩后跟一个列存储索引来实现。

#### <a name="effects-of-compression"></a>压缩效果

此测试比较行压缩、 页压缩和未压缩的好处。 模型进行定型使用`rxLinMod`上三个不同的数据的表中的数据。 对所有表使用了相同的公式和查询。

| 表名            | 测试名称       | numTasks | 平均时间 |
|-----------------------|-----------------|----------|--------------|
| *airlineWithIndex*    | NoCompression   | @shouldalert        | 5.6775       |
|                       | NoCompression-并行| 4        | 5.1775       |
| *airlineWithPageComp* | PageCompression | @shouldalert        | 6.7875       |
|                       | PageCompression-并行 | 4        | 5.3225       |
| *airlineWithRowComp*  | RowCompression  | @shouldalert        | 6.1325       |
|                       | RowCompression-并行  | 4        | 5.2375       |

**结论**

压缩单独似乎未帮助。 在此示例中，增加了的 CPU 处理压缩补偿 IO 时间减少。

但是，如果将 *numTasks* 设置为 4 以便并行运行测试，则平均时间将会减少。

对于较大的数据集，压缩效果可能更明显。 压缩取决于数据集和值，因此可能需要进行试验，确定压缩对数据集产生的影响。

### <a name="effect-of-windows-power-plan-options"></a>Windows 电源计划选项的效果

在此试验中，已将 `rxLinMod` 用于 *airlineWithIntCol* 表。 Windows 电源计划已设置为**平衡**或**高性能**。 在所有测试轮次中，*numTasks* 设置为 1。 已运行六倍，并在要调查的结果的变化这两个电源选项下，两次执行测试。

**高性能**电源选项：

| 测试名称 | 运行 \# | 占用时间 | 平均时间 |
|-----------|--------|--------------|--------------|
| IntCol    | @shouldalert      | 3.57 秒 |              |
|           | 2      | 3.45 秒 |              |
|           | 3      | 3.45 秒 |              |
|           | 4      | 3.55 秒 |              |
|           | 5      | 3.55 秒 |              |
|           | 6      | 3.45 秒 |              |
|           |        |              | 3.475        |
|           | @shouldalert      | 3.45 秒 |              |
|           | 2      | 3.53 秒 |              |
|           | 3      | 3.63 秒 |              |
|           | 4      | 3.49 秒 |              |
|           | 5      | 3.54 秒 |              |
|           | 6      | 3.47 秒 |              |
|           |        |              | 3.5075       |

“平衡”电源选项：

| 测试名称 | 运行 \# | 占用时间 | 平均时间 |
|-----------|--------|--------------|--------------|
| IntCol    | @shouldalert      | 3.89 秒 |              |
|           | 2      | 4.15 秒 |              |
|           | 3      | 3.77 秒 |              |
|           | 4      | 5 秒    |              |
|           | 5      | 3.92 秒 |              |
|           | 6      | 3.8 秒  |              |
|           |        |              | 3.91         |
|           | @shouldalert      | 3.82 秒 |              |
|           | 2      | 3.84 秒 |              |
|           | 3      | 3.86 秒 |              |
|           | 4      | 4.07 秒 |              |
|           | 5      | 4.86 秒 |              |
|           | 6      | 3.75 秒 |              |
|           |        |              | 3.88         |

**结论**

使用 Windows 时，执行时间将是更一致、 更快**高性能**电源计划。

#### <a name="using-integer-vs-strings-in-formulas"></a>在公式中使用字符串与整数

此测试评估修改的 R 代码，以避免常见的问题，使用字符串因素的影响。 具体而言，模型进行定型使用`rxLinMod`使用两个表： 第一个因素存储为字符串; 在第二个表中，因素都存储为整数。

+ 有关*航班*表中，[DayOfWeek] 列包含字符串。 _ColInfo_参数用于指定因素级别 （星期一、 星期二、...）

+  有关*airlineWithIndex*表，[DayOfWeek] 是一个整数。 _ColInfo_未指定参数。

+ 在这两种情况下，都使用了同一个公式：`ArrDelay ~ CRSDepTime + DayOfWeek`。

| 表名          | 测试名称   | 平均时间 |
|---------------------|-------------|--------------|
| *航班*           | *FactorCol* | 10.72        |
| *airlineWithIntCol* | *IntCol*    | 3.4475       |

**结论**

使用有关的因素的整数，而不是字符串时带来明显的好处。

### <a name="avoiding-transformation-functions"></a>避免转换函数

在此测试中，模型进行定型使用`rxLinMod`，但两个运行之间更改代码的时间：

+ 在首次运行，作为模型生成的一部分应用了转换函数。 
+ 在第二个运行中，功能值预计算和均可用，以便不转换函数是必需的。

| 测试名称             | 平均时间 |
|-----------------------|--------------|
| WithTransformation    | 5.1675       |
| WithoutTransformation | 4.7          |

**结论**

训练时间是短时**不**使用转换函数。 换而言之，模型进行定型速度更快时使用预计算并持久化表中的列。

节省的空间预计会更高版本，如果有许多更多的转换，数据集是更大 (\> 100 米)。

### <a name="using-columnar-store"></a>使用纵栏表存储

此测试评估使用列式数据存储和索引的性能优势。 相同的模型进行定型使用`rxLinMod`和无需数据进行转换。

+ 在首次运行，使用标准的行存储区数据表。
+ 在第二个运行中，使用列存储。

| 表名         | 测试名称 | 平均时间 |
|--------------------|-----------|--------------|
| *airlineWithIndex* | RowStore  | 4.67         |
| *airlineColumnar*  | ColStore  | 4.555        |

**结论**

性能会更好与纵栏表比应用商店使用的标准行存储区。 性能存在显著差异可能会出现在大型数据集上 (\> 100 米)。

### <a name="effect-of-using-the-cube-parameter"></a>使用多维数据集参数效果

此测试的目的是为了确定是否使用预计算中 RevoScaleR 选项**多维数据集**参数可以提高性能。 模型进行定型使用`rxLinMod`，使用以下公式：

```R
ArrDelay ~ Origin:DayOfWeek + Month + DayofMonth + CRSDepTime
```

在表中，因素*DayOfWeek*存储为字符串。

| 测试名称     | 多维数据集参数 | numTasks | 平均时间 | 单行预测 (ArrDelay_Pred) |
|---------------|----------------|----------|--------------|---------------------------------|
| CubeArgEffect | `cube = F`     | @shouldalert        | 91.0725      | 9.959204                        |
|               |                | 4        | 44.09        | 9.959204                        |
|               | `cube = T`     | @shouldalert        | 21.1125      | 9.959204                        |
|               |                | 4        | 8.08         | 9.959204                        |

**结论**

多维数据集参数自变量的使用清楚地可以提高性能。

### <a name="effect-of-changing-maxdepth-for-rxdtree-models"></a>更改 maxDepth rxDTree 模型的效果

在此试验`rxDTree`算法用于创建模型上*airlineColumnar*表。 在此项测试中，*numTasks* 设置为 4。 几个不同值的*maxDepth*用于演示如何更改的树深度影响运行的时。

| 测试名称       | maxDepth | 平均时间 |
|-----------------|----------|--------------|
| TreeDepthEffect | @shouldalert        | 10.1975      |
|                 | 2        | 13.2575      |
|                 | 4        | 19.27        |
|                 | 8        | 45.5775      |
|                 | 16       | 339.54       |

**结论**

随着树深度的增加，指数级增长会增加的节点的总数。 经过的时间用于创建模型还显著增加。

### <a name="prediction-on-a-stored-model"></a>存储模型的预测

而不生成当前正在执行代码的一部分，则此测试的目的是为了确定评分经过训练的模型保存到一个 SQL Server 表时的性能影响。 评分，从数据库加载存储的模型以及在内存 （本地计算上下文） 中使用的一个行数据帧创建预测。

测试结果显示的时间来保存模型，并加载模型和预测所花费的时间。

| 表名 | 测试名称 | 平均时间（训练模型） | 保存/加载模型花费的时间|
|------------|------------|------------|------------|
| airline    | SaveModel| 21.59| 2.08|
| airline    | LoadModelAndPredict | | 2.09（包括预测花费的时间） |

**结论**

从表加载训练的模型是一种更快的方法来执行预测。 我们建议你避免创建模型和执行在同一个脚本评分。

## <a name="case-study-optimization-for-the-resume-matching-task"></a>案例研究： 恢复匹配任务的优化

恢复匹配模型开发的由 Microsoft 数据科学家 Ke Huang 来测试 SQL Server 中的 R 代码的性能，通过执行这样帮助数据科学家创建可缩放的企业级解决方案。

### <a name="methods"></a>方法

对 RevoScaleR 和 MicrosoftML 封装了用于定型涉及大型数据集的复杂 R 解决方案中的预测模型。 SQL 查询和 R 代码都是相同的所有测试。 已安装的 SQL server 的单个 Azure VM 上执行了测试。 作者然后进行比较，评分时间使用和不使用 SQL Server 提供的以下优化：

- 内存中表
- ssNoVersion
- Resource Governor

若要评估的软件 NUMA 对 R 脚本执行的影响，数据科学团队，请测试 20 的物理内核数与 Azure 虚拟机上安装解决方案。 在这些物理核心、 四个软件 NUMA 节点中，自动创建： 每个节点包含五个内核。

在恢复匹配方案中，以评估对 R 作业的影响强制实施 CPU 关联。 四个**SQL 资源池**和第四个**外部资源池**而创建，但未指定 CPU 关联，以确保将每个节点中使用一组相同的 Cpu。

每个资源池已分配给不同的工作负荷组中，以优化硬件利用率。 原因是该软件 NUMA 和 CPU 关联无法划分的物理 NUMA 节点; 中的物理内存因此，通过定义所有软 NUMA 节点基于同一个物理 NUMA 节点都必须使用内存在同一个操作系统内存块。 换而言之，没有任何内存到处理器的关联。

以下过程用于创建此配置：

1. 减少默认情况下分配给 SQL Server 的内存量。

2. 创建用于并行运行 R 作业的四个新池。

3. 创建四个工作负荷组，以便每个工作负荷组都与资源池相关联。

4. 使用新的工作负荷组和分配，重新启动资源调控器。

5. 创建用户定义的分类器函数 (UDF) 可分配给不同的工作负荷组上的不同任务。

6. 更新资源调控器配置，以对相应的工作负荷组使用的函数。

### <a name="results"></a>结果

必须在恢复匹配中研究的最佳性能的配置时，如下所示：

-   有四个内部资源池 （适用于 SQL Server)

-   （对于外部脚本的作业） 的四个外部资源池

-   每个资源池都与特定工作负荷组关联

-   每个资源池分配给不同的 Cpu

-   （有关 SQL Server) 的最大内部内存使用量 = 30%

-   以供 R 会话的最大内存 = 70%

对于恢复匹配模型中，外部脚本使用已大量并没有任何其他数据库引擎服务运行。 因此，分配给外部脚本的资源已增加到 70%，证明脚本性能的最佳配置。

此配置已到达通过动手试验不同的值。 如果你使用不同的硬件或另一种解决方案，最佳的配置可能不同。 始终通过试验来查找你的用例的最佳配置 ！

在优化的解决方案中，已 20 核心计算机上在 8.5 秒内评分的数据 （与 100 功能） 1.1 万行。 优化显著改进了从评分时间方面的性能。

结果还建议**数功能**评分的时间有很大的影响。 预测模型中使用更多的功能时，可以更加明显改善。

我们建议你阅读此博客文章和随附教程有关的详细讨论。

-   [SQL Server 中的机器学习的优化提示和技巧](https://azure.microsoft.com/blog/optimization-tips-and-tricks-on-azure-sql-server-for-machine-learning-services/)

许多用户首次加载 R （或 Python） 运行时没有小暂停记录。 出于此原因，这些测试中所述的首次运行的时间是通常测量但更高版本被丢弃。 后续缓存可能会导致显著的性能差异第一个和第二次运行。 此外还有一些系统开销时 SQL Server 和外部运行时，之间移动数据时尤其是通过网络，而不是直接从 SQL Server 正在加载传递数据。

对于所有这些原因，没有用于缓解此初始加载期间，任何单个解决方案因为性能影响的变化较大取决于任务。 例如，缓存为评分批; 中的单行更行执行因此，连续评分的操作是要快得多，模型和 R 运行时都不重新加载。 你还可以使用[本机评分](../sql-native-scoring.md)以免完全加载 R 运行时。

对于定型大的模型，或在大的批次评分，则开销可能会与从避免数据移动或流式处理和并行处理的提升相比最小。 请参阅以下最近的日志和其他性能指南的示例：

+ [使用 SQL Server 2016 R Services 的贷款分类](https://blogs.msdn.microsoft.com/microsoftrservertigerteam/2016/09/27/loan-classification-using-sql-server-2016-r-services/)
+ [使用 R Services 的早期客户体验](https://blogs.msdn.microsoft.com/sqlcat/2016/06/16/early-customer-experiences-with-sql-server-r-services/)
+ [使用 R 来检测欺诈行为在每秒 1 百万个事务](http://blog.revolutionanalytics.com/2016/09/fraud-detection.html/)

## <a name="resources"></a>Resources

以下是信息、 工具和脚本在这些测试的开发中使用的链接。

+ 性能测试脚本和数据的链接：[示例数据和 SQL Server 优化研究的脚本](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning)

+ 描述恢复匹配解决方案的文章：[优化提示和技巧 for SQL Server R Services](https://azure.microsoft.com/blog/optimization-tips-and-tricks-on-azure-sql-server-for-machine-learning-services/)

+ 在 SQL 优化用于恢复匹配的解决方案的脚本： [GitHub 存储库](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/SQLOptimizationTips)

### <a name="learn-about-windows-server-management"></a>了解 Windows server 管理

+ [如何确定 64 位版本 Windows 的合适页面文件大小](https://support.microsoft.com/kb/2860880)

+ [了解 NUMA](https://technet.microsoft.com/library/ms178144.aspx)

+ [SQL Server 如何支持 NUMA](https://technet.microsoft.com/library/ms180954.aspx)

+ [Soft NUMA](https://docs.microsoft.com/sql/database-engine/configure-windows/soft-numa-sql-server)

### <a name="learn-about-sql-server-optimizations"></a>了解有关 SQL Server 优化

+ [重新组织和重新生成索引](../../relational-databases\indexes\reorganize-and-rebuild-indexes.md)

+ [内存优化表简介](https://docs.microsoft.com/sql/relational-databases/in-memory-oltp/introduction-to-memory-optimized-tables)

+ [演示： 内存中 OLTP 的性能改进](https://docs.microsoft.com/sql/relational-databases/in-memory-oltp/demonstration-performance-improvement-of-in-memory-oltp)

+ [数据压缩](../../relational-databases/data-compression/data-compression.md)

+ [对表或索引启用压缩](../../relational-databases/data-compression/enable-compression-on-a-table-or-index.md)

+ [对表或索引禁用压缩](../../relational-databases/data-compression/disable-compression-on-a-table-or-index.md)

### <a name="learn-about-managing-sql-server"></a>了解如何管理 SQL Server

+ [监视和优化性能](../../relational-databases/performance/monitor-and-tune-for-performance.md)

+ [资源调控器](../../relational-databases/resource-governor/resource-governor.md)

+ [引入了资源调控器](https://technet.microsoft.com/library/bb895232.aspx)

+ [R Services 的资源调控](resource-governance-for-r-services.md)

+ [如何为 R 创建资源池](how-to-create-a-resource-pool-for-r.md)

+ [配置资源调控器的示例](https://blog.sqlauthority.com/2012/06/04/sql-server-simple-example-to-configure-resource-governor-introduction-to-resource-governor/)

### <a name="tools"></a>工具

+ [DISKSPD 存储负载生成器/性能测试工具](https://github.com/microsoft/diskspd)

+ [FSUtil 实用工具参考](https://technet.microsoft.com/library/cc753059.aspx)


## <a name="other-articles-in-this-series"></a>本系列中的其他文章

[性能优化 R – 简介](sql-server-r-services-performance-tuning.md)

[性能优化 R-SQL Server 配置](sql-server-configuration-r-services.md)

[性能优化 R-R 代码和数据优化](r-and-data-optimization-r-services.md)

[性能优化的案例研究结果](performance-case-study-r-services.md)
