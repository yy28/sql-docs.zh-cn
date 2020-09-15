---
title: 结果的性能优化
description: 本文总结了测试各种优化方法的两个案例研究的方法、结果和结论。
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 03/29/2019
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: a6afdda3975fc8f6c269f9c1fcbca35318f0c4da
ms.sourcegitcommit: 9b41725d6db9957dd7928a3620fe4db41eb51c6e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2020
ms.locfileid: "88179988"
---
# <a name="performance-for-r-services-results-and-resources"></a>R Services 的性能：结果和资源
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

本文是系列文章中的第四篇也是最后一篇文章，这些文章介绍了 R Services 的性能优化。 本文总结了测试各种优化方法的两个案例研究的方法、结果和结论。

这两个案例研究具有不同的目标：

+ 由 R Services 开发团队进行的第一个案例研究试图衡量特定优化技术的影响
+ 由数据科学家团队进行的第二个案例研究尝试了多种方法以确定针对特定大量评分方案的最佳优化。

本主题列出了第一个案例研究的详细结果。 对于第二个案例研究，将以摘要形式介绍总体发现。 本主题末尾的链接指向所有脚本和示例数据，以及原作者使用的资源。

## <a name="performance-case-study-airline-dataset"></a>性能案例研究：航空公司数据集

由 SQL Server R Services 开发团队进行的此案例研究测试了各种优化的效果。 创建了单个 rxLogit 模型并对航空公司数据集进行评分。 在定型和评分过程中应用了优化，以评估各个影响。

- GitHub：用于 SQL Server 优化研究的[示例数据和脚本](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning)

### <a name="test-methods"></a>测试方法

1. 航空公司数据集包含一个 10M 行的单个表。 已将其下载并大容量加载到 SQL Server 中。
2. 已制成 6 份表副本。
3. 对表的副本应用了各种修改以测试 SQL Server 功能，如页压缩、行压缩、索引、纵栏式数据存储等。
4. 在应用每个优化之前和之后测量性能。

| 表名称| 说明|
|------|------|
| *airline* | 使用 `rxDataStep` 从原始 xdf 文件转换的数据|                          |
| *airlineWithIntCol*   | *DayOfWeek* 已转换为整数而不是字符串。 另外，添加了 *rowNum* 列。|
| *airlineWithIndex*    | 数据与 *airlineWithIntCol* 表相同，但使用 *rowNum* 列添加了单个聚集索引。|
| *airlineWithPageComp* | 数据与 *airlineWithIndex* 表相同，但已启用页压缩。 另外，添加了基于 *CRSDepTime* 和 *ArrDelay* 计算得出的两个列：*CRSDepHour* 和 *Late*。 |
| *airlineWithRowComp*  | 数据与 *airlineWithIndex* 表相同，但已启用行压缩。 另外，添加了基于 *CRSDepTime* 和 *ArrDelay* 计算得出的两个列：*CRSDepHour* 和 *Late*。 |
| *airlineColumnar*     | 包含单个聚集索引的纵栏表存储。 此表中填充了来自已清理的 csv 文件中的数据。|

每项测试包括以下步骤：

1. 运行每项测试之前已引发 R 垃圾回收。
2. 基于表数据创建了逻辑回归模型。 每项测试的 *rowsPerRead* 值设置为 500000。
3. 使用已定型模型生成分数
4. 每项测试运行六次。 首次运行（“冷运行”）的时间已丢弃。 为了允许偶发离群值，剩余五次运行中的最长时间也已丢弃  。 已使用四次剩余运行的平均值来计算每项测试的平均消耗运行时。
5. 使用值 3（= 报告时间和进度）的 reportProgress 参数运行测试  。 每个输出文件都包含有关 IO 所用时间、转换时间和计算时间的信息。 这些时间可用于故障排除和诊断。
6. 控制台输出也定向到输出目录中的某个文件。
7. 测试脚本处理这些文件中的时间以计算运行的平均时间。

例如，下面的结果是来自单个测试的时间。 主要关注的时间是“总读取时间”（IO 时间）和“转换时间”（设置计算进程所产生的开销）。  

**样本计时**

```text
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

建议下载并修改测试脚本，以帮助对 R Services 或 RevoScaleR 函数的问题进行故障排除。

### <a name="test-results-all"></a>测试结果（全部）

本节比较每个测试的前后结果。

#### <a name="data-size-with-compression-and-a-columnar-table-store"></a>使用压缩和纵栏式表存储的数据大小

第一个测试在减小数据大小方面，对使用压缩和纵栏式表进行了比较。

| 表名称            | “行”     | 保留   | 数据       | index_size | 未使用  | 节省率（保留） |
|-----------------------|----------|------------|------------|------------|---------|---------------------|
| *airlineWithIndex*    | 10000000 | 2978816 KB | 2972160 KB | 6128 KB    | 528 KB  | 0                   |
| *airlineWithPageComp* | 10000000 | 625784 KB  | 623744 KB  | 1352 KB    | 688 KB  | 79%                 |
| *airlineWithRowComp*  | 10000000 | 1262520 KB | 1258880 KB | 2552 KB    | 1088 KB | 58%                 |
| *airlineColumnar*     | 9999999  | 201992 KB  | 201624 KB  | 不适用        | 368 KB  | 93%                 |

**结论**

通过应用列存储索引，然后进行页压缩，可以最大程度地减小数据大小。

#### <a name="effects-of-compression"></a>压缩效果

此测试比较了行压缩、页压缩和无压缩的优点。 通过对来自三个不同数据表的数据使用 `rxLinMod` 定型了模型。 对所有表使用了相同的公式和查询。

| 表名称            | 测试名称       | numTasks | 平均时间 |
|-----------------------|-----------------|----------|--------------|
| *airlineWithIndex*    | NoCompression   | 1        | 5.6775       |
|                       | NoCompression - 并行| 4        | 5.1775       |
| *airlineWithPageComp* | PageCompression | 1        | 6.7875       |
|                       | PageCompression - 并行 | 4        | 5.3225       |
| *airlineWithRowComp*  | RowCompression  | 1        | 6.1325       |
|                       | RowCompression - 并行  | 4        | 5.2375       |

**结论**

仅压缩似乎没有帮助。 在此示例中，用于处理压缩的 CPU 中的增加量补偿了 IO 时间中的减少量。

但是，如果将 *numTasks* 设置为 4 以便并行运行测试，则平均时间将会减少。

对于较大的数据集，压缩效果可能更明显。 压缩取决于数据集和值，因此可能需要进行试验，确定压缩对数据集产生的影响。

### <a name="effect-of-windows-power-plan-options"></a>Windows 电源计划选项的影响

在此试验中，已将 `rxLinMod` 用于 *airlineWithIntCol* 表。 Windows 电源计划已设置为“平衡”或“高性能”   。 在所有测试轮次中，*numTasks* 设置为 1。 测试运行了六次，并在同时使用两种电源选项的条件下执行了两次，以调查结果的可变性。

“高性能”电源选项  ：

| 测试名称 | \#运行 | 占用时间 | 平均时间 |
|-----------|--------|--------------|--------------|
| IntCol    | 1      | 3.57 秒 |              |
|           | 2      | 3.45 秒 |              |
|           | 3      | 3.45 秒 |              |
|           | 4      | 3.55 秒 |              |
|           | 5      | 3.55 秒 |              |
|           | 6      | 3.45 秒 |              |
|           |        |              | 3.475        |
|           | 1      | 3.45 秒 |              |
|           | 2      | 3.53 秒 |              |
|           | 3      | 3.63 秒 |              |
|           | 4      | 3.49 秒 |              |
|           | 5      | 3.54 秒 |              |
|           | 6      | 3.47 秒 |              |
|           |        |              | 3.5075       |

“平衡”电源选项： 

| 测试名称 | \#运行 | 占用时间 | 平均时间 |
|-----------|--------|--------------|--------------|
| IntCol    | 1      | 3.89 秒 |              |
|           | 2      | 4.15 秒 |              |
|           | 3      | 3.77 秒 |              |
|           | 4      | 5 秒    |              |
|           | 5      | 3.92 秒 |              |
|           | 6      | 3.8 秒  |              |
|           |        |              | 3.91         |
|           | 1      | 3.82 秒 |              |
|           | 2      | 3.84 秒 |              |
|           | 3      | 3.86 秒 |              |
|           | 4      | 4.07 秒 |              |
|           | 5      | 4.86 秒 |              |
|           | 6      | 3.75 秒 |              |
|           |        |              | 3.88         |

**结论**

使用 Windows“高性能”电源计划时，执行时间更一致且速度更快  。

#### <a name="using-integer-vs-strings-in-formulas"></a>在公式中使用整数与字符串

此测试评估了修改 R 代码以避免字符串因素引起的常见问题的影响。 具体而言，通过以下两个表使用 `rxLinMod` 定型模型：在第一个表中，因素存储为字符串；在第二个表中，因素存储为整数。

+ 对于 airline 表，[DayOfWeek] 列包含字符串  。 colInfo 参数用于指定因素级别（星期一、星期二…） 

+  对于 airlineWithIndex 表，[DayOfWeek] 为整数  。 未指定 colInfo 参数  。

+ 在这两种情况下，都使用了同一个公式：`ArrDelay ~ CRSDepTime + DayOfWeek`。

| 表名称          | 测试名称   | 平均时间 |
|---------------------|-------------|--------------|
| *Airline*           | *FactorCol* | 10.72        |
| *airlineWithIntCol* | *IntCol*    | 3.4475       |

**结论**

使用整数而不是字符串作为因素时，有一个明显的优点。

### <a name="avoiding-transformation-functions"></a>避免转换函数

在此测试中，已使用 `rxLinMod` 定型了模型，但在两次运行之间更改了代码：

+ 在第一次运行中，转换函数作为模型生成的一部分进行应用。 
+ 在第二次运行中，功能值已预计算且可用，因此不需要转换函数。

| 测试名称             | 平均时间 |
|-----------------------|--------------|
| WithTransformation    | 5.1675       |
| WithoutTransformation | 4.7          |

**结论**

不使用转换功能时，定型时间更短  。 换言之，使用经过预计算并保留在表中的列时，模型的定型速度更快。

如果有更多的转换且数据集更大 (\> 100M)，则节省量预计会更高。

### <a name="using-columnar-store"></a>使用纵栏式存储

此测试评估了使用纵栏式数据存储和索引的性能优势。 使用 `rxLinMod` 定型了同一模型，但无数据转换。

+ 在第一次运行中，数据表使用标准行存储。
+ 在第二次运行中，使用纵栏式存储。

| 表名称         | 测试名称 | 平均时间 |
|--------------------|-----------|--------------|
| *airlineWithIndex* | RowStore  | 4.67         |
| *airlineColumnar*  | ColStore  | 4.555        |

**结论**

与标准行存储相比，纵栏式存储的性能更好。 对于更大的数据集 (\> 100 M)，性能方面可能会产生显著差异。

### <a name="effect-of-using-the-cube-parameter"></a>使用多维数据集参数的效果

此测试的目的是确定 RevoScaleR 中使用预计算多维数据集参数的选项是否可以提高性能  。 通过以下公式使用 `rxLinMod` 定型模型：

```R
ArrDelay ~ Origin:DayOfWeek + Month + DayofMonth + CRSDepTime
```

在表中，DayOfWeek 因素会存储为字符串  。

| 测试名称     | 多维数据集参数 | numTasks | 平均时间 | 单行预测 (ArrDelay_Pred) |
|---------------|----------------|----------|--------------|---------------------------------|
| CubeArgEffect | `cube = F`     | 1        | 91.0725      | 9.959204                        |
|               |                | 4        | 44.09        | 9.959204                        |
|               | `cube = T`     | 1        | 21.1125      | 9.959204                        |
|               |                | 4        | 8.08         | 9.959204                        |

**结论**

使用多维数据集参数变量明显提高了性能。

### <a name="effect-of-changing-maxdepth-for-rxdtree-models"></a>更改 rxDTree 模型 maxDepth 的效果

在此实验中，使用 `rxDTree` 算法在 airlineColumnar 表上创建模型  。 在此项测试中，*numTasks* 设置为 4。 maxDepth 的几个不同值用于演示更改树深度如何影响运行时  。

| 测试名称       | maxDepth | 平均时间 |
|-----------------|----------|--------------|
| TreeDepthEffect | 1        | 10.1975      |
|                 | 2        | 13.2575      |
|                 | 4        | 19.27        |
|                 | 8        | 45.5775      |
|                 | 16       | 339.54       |

**结论**

随着树深度的增加，节点总数呈指数增加。 创建模型所用的时间也显著增加。

### <a name="prediction-on-a-stored-model"></a>预测存储模型

此测试的目的是在将已定型模型保存到 SQL Server 表而不作为当前执行代码的一部分生成时，确定对评分产生的性能影响。 对于评分，可从数据库加载存储模型，并且使用内存中的单行数据帧（本地计算上下文）创建预测。

测试结果显示了保存模型的时间，以及加载模型和进行预测所花费的时间。

| 表名称 | 测试名称 | 平均时间（训练模型） | 保存/加载模型花费的时间|
|------------|------------|------------|------------|
| 航空公司    | SaveModel| 21.59| 2.08|
| 航空公司    | LoadModelAndPredict | | 2.09（包括预测花费的时间） |

**结论**

从表中加载已定型模型显然是执行预测的更快方法。 建议避免在同一脚本中创建模型并执行评分。

## <a name="case-study-optimization-for-the-resume-matching-task"></a>案例研究：恢复匹配任务的优化

恢复匹配模型由 Microsoft 数据科学家 Ke Huang 开发，用于测试 SQL Server 中 R 代码的性能，并通过执行此操作帮助数据科学家创建可缩放的企业级解决方案。

### <a name="methods"></a>方法

RevoScaleR 和 MicrosoftML 包都用于在涉及大型数据集的复杂 R 解决方案中定型预测模型。 所有测试中的 SQL 查询和 R 代码都相同。 在安装了 SQL Server 的单个 Azure VM 上进行了测试。 然后，作者比较了有无 SQL Server 提供的以下优化情况下的评分时间：

- 内存中表
- ssNoVersion
- Resource Governor

为评估 soft-NUMA 对 R 脚本执行的影响，数据科学团队在具有 20 个物理内核的 Azure 虚拟机上测试了解决方案。 在这些物理内核上，自动创建了四个 soft-NUMA 节点，以使每个节点包含五个内核。

在恢复匹配方案中强制执行 CPU 关联，以评估对 R 作业的影响。 创建四个 SQL 资源池和四个外部资源池，并指定 CPU 关联以确保每个节点中使用同一组 CPU   。

每个资源池都已分配给不同的工作负荷组，以优化硬件利用率。 原因在于，Soft-NUMA 和 CPU 关联无法在物理 NUMA 节点中划分物理内存；因此，根据定义，基于同一物理 NUMA 节点的所有 soft NUMA 节点必须使用同一 OS 内存块中的内存。 换句话说，没有内存到处理器的关联。

使用以下过程创建此配置：

1. 减少默认分配给 SQL Server 的内存量。

2. 创建四个新池以并行运行 R 作业。

3. 创建四个工作负荷组，使每个工作负荷组与一个资源池相关联。

4. 使用新的工作负荷组和分配重启 Resource Governor。

5. 创建用户定义的分类器函数 (UDF)，以便在不同的工作负荷组上分配不同的任务。

6. 更新 Resource Governor 配置，将函数用于适当的工作负荷组。

### <a name="results"></a>结果

在恢复匹配研究中具有最佳性能的配置如下所示：

-   四个内部资源池（用于 SQL Server）

-   四个外部资源池（用于外部脚本作业）

-   每个资源池都与一个特定的工作负荷组相关联

-   每个资源池分配给不同的 CPU

-   最大内部内存使用率（用于 SQL Server）= 30%

-   R 会话使用的最大内存 = 70%

对于恢复匹配模式，外部脚本使用率很大，且不会有其他数据库引擎服务运行。 因此，分配给外部脚本的资源增加到 70%，这证明了脚本性能的最佳配置。

通过试验不同的值来达到此配置。 如果使用不同的硬件或不同的解决方案，则最佳配置可能会有所不同。 始终试验以找到适合你的情况的最佳配置！

在优化的解决方案中，可在 8.5 秒内对一台 20 核计算机上的 110 万行数据（包含 100 个功能）进行评分。 在评分时间方面，优化显著提高了性能。

结果还表明，功能数量对评分时间具有重大影响  。 在预测模型中使用更多功能时，这种改进更显著。

建议阅读此博客文章和随附的教程以进行详细讨论。

-   [SQL Server 中机器学习的优化提示和技巧](https://azure.microsoft.com/blog/optimization-tips-and-tricks-on-azure-sql-server-for-machine-learning-services/)

许多用户已经注意到，第一次加载 R（或 Python）运行时的时候，会有稍微的暂停。 如这些测试中所述，出于此原因，通常会测量第一次运行的时间，但随后将其丢弃。 后续的高速缓存可能会导致第一次运行和第二次运行之间出现明显的性能差异。 在 SQL Server 和外部运行时之间移动数据时还存在一些开销，如果数据通过网络传递而不是直接从 SQL Server 中加载时，则尤其如此。

出于上述所有原因，不存在用于缓解此初始加载时间的单一解决方案，因为性能影响因任务不同而具有明显差异。 例如，为批中的单行评分执行高速缓存；因此，连续评分操作的速度要快得多，且模型和 R 运行时都不会重载。 还可以使用[本机评分](../predictions/native-scoring-predict-transact-sql.md)以避免完全加载 R 运行时。

对于定型大型模型或对大量批进行评分，与避免数据移动或避免流式处理和并行处理所产生的收益相比，其开销可能是最小的。 请参阅此博客文章，了解更多性能指导：

+ [使用 R 以每秒一百万次事务的速率检测欺诈](https://blog.revolutionanalytics.com/2016/09/fraud-detection.html/)

## <a name="resources"></a>资源

以下是指向在开发这些测试的过程中使用到的信息、工具和脚本的链接。

+ 性能测试脚本和指向数据的链接：[用于 SQL Server 优化研究的示例数据和脚本](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning)

+ 介绍恢复匹配解决方案的文章：[用于 SQL Server R Services 的优化提示和技巧](https://azure.microsoft.com/blog/optimization-tips-and-tricks-on-azure-sql-server-for-machine-learning-services/)

+ SQL 优化中用于恢复匹配解决方案的脚本：[GitHub 存储库](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/SQLOptimizationTips-Resume-Matching)

### <a name="learn-about-windows-server-management"></a>了解 Windows Server 管理

+ [如何确定 64 位版本 Windows 的合适页面文件大小](https://support.microsoft.com/kb/2860880)

+ [了解 NUMA](https://technet.microsoft.com/library/ms178144.aspx)

+ [SQL Server 如何支持 NUMA](https://technet.microsoft.com/library/ms180954.aspx)

+ [Soft NUMA](https://docs.microsoft.com/sql/database-engine/configure-windows/soft-numa-sql-server)

### <a name="learn-about-sql-server-optimizations"></a>了解 SQL Server 优化

+ [重新组织和重新生成索引](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)

+ [内存优化表简介](https://docs.microsoft.com/sql/relational-databases/in-memory-oltp/introduction-to-memory-optimized-tables)

+ [演示：内存中 OLTP 的性能改进](https://docs.microsoft.com/sql/relational-databases/in-memory-oltp/demonstration-performance-improvement-of-in-memory-oltp)

+ [Data compression](../../relational-databases/data-compression/data-compression.md)（数据压缩）

+ [对表或索引启用压缩](../../relational-databases/data-compression/enable-compression-on-a-table-or-index.md)

+ [对表或索引禁用压缩](../../relational-databases/data-compression/disable-compression-on-a-table-or-index.md)

### <a name="learn-about-managing-sql-server"></a>了解如何管理 SQL Server

+ [监视和优化性能](../../relational-databases/performance/monitor-and-tune-for-performance.md)

+ [资源调控器](../../relational-databases/resource-governor/resource-governor.md)

+ [Resource Governor 简介](https://technet.microsoft.com/library/bb895232.aspx)

+ [配置 Resource Governor 的示例](https://blog.sqlauthority.com/2012/06/04/sql-server-simple-example-to-configure-resource-governor-introduction-to-resource-governor/)

### <a name="tools"></a>工具

+ [DISKSPD 存储负载生成器/性能测试工具](https://github.com/microsoft/diskspd)

+ [FSUtil 实用工具参考](https://technet.microsoft.com/library/cc753059.aspx)


## <a name="other-articles-in-this-series"></a>本系列中的其他文章

[R 的性能优化 - 简介](sql-server-r-services-performance-tuning.md)

[R 的性能优化 - SQL Server 配置](sql-server-configuration-r-services.md)

[R 的性能优化 - R 代码和数据优化](r-and-data-optimization-r-services.md)

[性能优化 - 案例研究结果](performance-case-study-r-services.md)
