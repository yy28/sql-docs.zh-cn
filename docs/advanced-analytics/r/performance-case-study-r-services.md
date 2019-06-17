---
title: SQL Server R Services 的结果和资源的 SQL Server 机器学习服务的性能
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/29/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 392a6da09827355e6bc9a901b0e4580e5eb72bf5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62642675"
---
# <a name="performance-for-r-services-results-and-resources"></a>R Services 的性能： 结果和资源
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文是第四个和最后一个序列中的值，它描述 R services 性能优化。 本文汇总了方法、 的发现和结论的测试各种优化方法的两个案例研究。

两个案例研究小组提出不同的目标：

+ 第一个案例研究，R Services 开发团队查找以衡量特定的优化技术的影响
+ 第二个案例研究，由数据科学家团队，试验了多个方法来确定特定的大批量评分方案的最佳优化。

本主题列出了第一个案例研究的详细的结果。 对于第二个案例研究，摘要描述整体结果。 本主题末尾处是所有脚本和示例数据和所使用的原始作者资源的链接。

## <a name="performance-case-study-airline-dataset"></a>性能案例研究：航班数据集

本案例研究由 SQL Server R Services 开发团队进行测试各种优化的效果。 创建单个 rxLogit 模型和评分航班数据集上执行。 在训练和评分来评估单个影响的进程中应用了优化。

- Github:[示例数据和脚本](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning)有关 SQL Server 优化研究

### <a name="test-methods"></a>测试方法

1. 航班数据集包含 10 亿行的单个表。 它下载和大容量加载到 SQL Server。
2. 进行了表的六个副本。
3. 各种修改已应用到表，若要测试 SQL Server 功能，如页压缩，行压缩、 索引、 纵栏表数据存储区等的副本。
4. 之前和之后应用了每个优化测量性能。

| 表名| Description|
|------|------|
| *airline* | 使用 `rxDataStep` 从原始 xdf 文件转换的数据|                          |
| *airlineWithIntCol*   | *DayOfWeek* 已转换为整数而不是字符串。 另外，添加了 *rowNum* 列。|
| *airlineWithIndex*    | 数据与 *airlineWithIntCol* 表相同，但使用 *rowNum* 列添加了单个聚集索引。|
| *airlineWithPageComp* | 数据与 *airlineWithIndex* 表相同，但已启用页压缩。 另外，添加了基于 *CRSDepTime* 和 *ArrDelay* 计算得出的两个列：*CRSDepHour* 和 *Late*。 |
| *airlineWithRowComp*  | 数据与 *airlineWithIndex* 表相同，但已启用行压缩。 另外，添加了基于 *CRSDepTime* 和 *ArrDelay* 计算得出的两个列：*CRSDepHour* 和 *Late*。 |
| *airlineColumnar*     | 包含单个聚集索引的纵栏表存储。 此表中填充了来自已清理的 csv 文件中的数据。|

每个测试都包括以下步骤：

1. 运行每项测试之前已引发 R 垃圾回收。
2. 创建逻辑回归模型基于的表数据。 每项测试的 *rowsPerRead* 值设置为 500000。
3. 使用经过训练的模型生成分数
4. 每个测试运行六次。 已删除的第一次运行 （"冷运行"） 的时间。 若要允许偶发离群值，**最大**在剩余的五个运行之间的时间也已丢弃。 已使用四次剩余运行的平均值来计算每项测试的平均消耗运行时。
5. 使用运行了测试*reportProgress*参数与值 3 （为报表执行时间和进度）。 每个输出文件包含有关 IO、 转换时间和计算时间中所用的时间信息。 这些时间可用于故障排除和诊断。
6. 控制台输出也被定向到输出目录中的文件。
7. 测试脚本将在这些文件，以运行计算的平均时间处理时间。

例如，以下结果是从单个测试的时间。 主要关注的时间是“总读取时间”（IO 时间）和“转换时间”（设置计算进程所产生的开销）。  

**示例计时**

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

我们建议您下载并修改测试脚本，以帮助你解决使用 R Services 或 RevoScaleR 函数的问题。

### <a name="test-results-all"></a>测试结果 （全部）

本部分比较为每个测试之前和之后的结果。

#### <a name="data-size-with-compression-and-a-columnar-table-store"></a>通过压缩和纵栏表存储的数据大小

第一个测试与比较使用压缩和纵栏表来减小数据大小。

| 表名            | “行”     | 保留   | 数据       | index_size | 未使用  | 节省率（保留） |
|-----------------------|----------|------------|------------|------------|---------|---------------------|
| *airlineWithIndex*    | 10000000 | 2978816 KB | 2972160 KB | 6128 KB    | 528 KB  | 0                   |
| *airlineWithPageComp* | 10000000 | 625784 KB  | 623744 KB  | 1352 KB    | 688 KB  | 79%                 |
| *airlineWithRowComp*  | 10000000 | 1262520 KB | 1258880 KB | 2552 KB    | 1088 KB | 58%                 |
| *airlineColumnar*     | 9999999  | 201992 KB  | 201624 KB  | 不适用        | 368 KB  | 93%                 |

**结论**

数据大小的最大减少是通过应用列存储索引，跟页压缩来实现的。

#### <a name="effects-of-compression"></a>压缩的影响

此测试比较行压缩、 页压缩和未压缩的好处。 使用已训练模型`rxLinMod`上三个不同的数据的表中的数据。 对所有表使用了相同的公式和查询。

| 表名            | 测试名称       | numTasks | 平均时间 |
|-----------------------|-----------------|----------|--------------|
| *airlineWithIndex*    | NoCompression   | 1        | 5.6775       |
|                       | NoCompression-并行| 4        | 5.1775       |
| *airlineWithPageComp* | PageCompression | 1        | 6.7875       |
|                       | PageCompression - parallel | 4        | 5.3225       |
| *airlineWithRowComp*  | RowCompression  | 1        | 6.1325       |
|                       | RowCompression - parallel  | 4        | 5.2375       |

**结论**

单纯使用压缩似乎帮助。 在此示例中，用于处理压缩的 CPU 中增加抵消 IO 时间的减少。

但是，如果将 *numTasks* 设置为 4 以便并行运行测试，则平均时间将会减少。

对于较大的数据集，压缩效果可能更明显。 压缩取决于数据集和值，因此可能需要进行试验，确定压缩对数据集产生的影响。

### <a name="effect-of-windows-power-plan-options"></a>Windows 电源计划选项的效果

在此试验中，已将 `rxLinMod` 用于 *airlineWithIntCol* 表。 Windows 电源计划设置为**平衡**或**高性能**。 在所有测试轮次中，*numTasks* 设置为 1。 测试运行六次，且已执行两次下这两个电源选项以调查结果的可变性。

**高性能**电源选项：

| 测试名称 | 运行 \# | 占用时间 | 平均时间 |
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

| 测试名称 | 运行 \# | 占用时间 | 平均时间 |
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

使用 Windows 时，执行时间将是更加一致和更快**高性能**电源计划。

#### <a name="using-integer-vs-strings-in-formulas"></a>在公式中使用整数与字符串

此测试评估修改 R 代码以避免常见问题与字符串因素的影响。 具体而言，模型进行训练使用`rxLinMod`使用两个表： 在第一个，以字符串形式存储因素; 在第二个表中，因素都作为整数存储。

+ 有关*航班*表中，[DayOfWeek] 列包含字符串。 _ColInfo_参数用于指定因子级别 （星期一、 星期二、...）

+  有关*airlineWithIndex*表中，[DayOfWeek] 是一个整数。 _ColInfo_未指定参数。

+ 在这两种情况下，都使用了同一个公式：`ArrDelay ~ CRSDepTime + DayOfWeek`。

| 表名          | 测试名称   | 平均时间 |
|---------------------|-------------|--------------|
| *Airline*           | *FactorCol* | 10.72        |
| *airlineWithIntCol* | *IntCol*    | 3.4475       |

**结论**

使用整数而不是字符串的因素时的一个明显优势。

### <a name="avoiding-transformation-functions"></a>避免转换函数

在此测试中，模型进行训练使用`rxLinMod`，但两个运行之间已更改了代码：

+ 在首次运行，转换函数应用模型构建的一部分。 
+ 在第二个运行中，功能值已被预计算并可用，以便不转换函数时所需。

| 测试名称             | 平均时间 |
|-----------------------|--------------|
| WithTransformation    | 5.1675       |
| WithoutTransformation | 4.7          |

**结论**

定型时间是较短时**不**使用转换函数。 换而言之，对模型进行训练速度更快时使用的是预先计算并保存在表中的列。

节省的空间应为更高版本，如果没有更多的许多转换和数据集是更大 (\> 1 亿)。

### <a name="using-columnar-store"></a>使用纵栏表存储

此测试评估使用列式数据存储和索引的性能优势。 使用相同的模型时训练`rxLinMod`和无需数据进行转换。

+ 在首次运行，使用标准行存储数据表。
+ 在第二个运行中，使用列存储。

| 表名         | 测试名称 | 平均时间 |
|--------------------|-----------|--------------|
| *airlineWithIndex* | RowStore  | 4.67         |
| *airlineColumnar*  | ColStore  | 4.555        |

**结论**

性能是更好地使用纵栏表存储比使用标准行存储。 性能显著差异可能会更大数据集 (\> 1 亿)。

### <a name="effect-of-using-the-cube-parameter"></a>使用多维数据集参数的效果

此测试的目的是为了确定是否使用预计算 RevoScaleR 中的选项**多维数据集**参数可以提高性能。 使用已训练模型`rxLinMod`，使用以下公式：

```R
ArrDelay ~ Origin:DayOfWeek + Month + DayofMonth + CRSDepTime
```

在表中，因素*DayOfWeek*存储为字符串。

| 测试名称     | 多维数据集参数 | numTasks | 平均时间 | 单行预测 (ArrDelay_Pred) |
|---------------|----------------|----------|--------------|---------------------------------|
| CubeArgEffect | `cube = F`     | 1        | 91.0725      | 9.959204                        |
|               |                | 4        | 44.09        | 9.959204                        |
|               | `cube = T`     | 1        | 21.1125      | 9.959204                        |
|               |                | 4        | 8.08         | 9.959204                        |

**结论**

使用多维数据集参数自变量显然可以提高性能。

### <a name="effect-of-changing-maxdepth-for-rxdtree-models"></a>更改模型 rxDTree 的 maxDepth 的效果

在此实验中，`rxDTree`算法用于在创建模型*airlineColumnar*表。 在此项测试中，*numTasks* 设置为 4。 多个不同的值*maxDepth*用于演示如何更改树深度影响运行的时。

| 测试名称       | maxDepth | 平均时间 |
|-----------------|----------|--------------|
| TreeDepthEffect | 1        | 10.1975      |
|                 | 2        | 13.2575      |
|                 | 4        | 19.27        |
|                 | 8        | 45.5775      |
|                 | 16       | 339.54       |

**结论**

随着树深度的增加，以指数方式增加的节点总数。 用于创建模型经过的时间也显著增加。

### <a name="prediction-on-a-stored-model"></a>在存储模型的预测

此测试的目的是为了确定对计分训练的模型保存到 SQL Server 表时的性能影响而不是当前正在执行代码的一部分生成。 评分，从数据库加载存储的模型以及使用内存 （本地计算上下文） 中的一行数据帧创建预测。

测试结果显示的时间来保存模型，以及加载模型和预测所需的时间。

| 表名 | 测试名称 | 平均时间（训练模型） | 保存/加载模型花费的时间|
|------------|------------|------------|------------|
| airline    | SaveModel| 21.59| 2.08|
| airline    | LoadModelAndPredict | | 2.09（包括预测花费的时间） |

**结论**

从表加载训练的模型是清楚地更快地执行预测。 我们建议避免创建模型，并执行评分全部放在同一个脚本。

## <a name="case-study-optimization-for-the-resume-matching-task"></a>案例研究：优化用于 resume 匹配任务

继续匹配模型开发的 Microsoft 数据科学家 Ke Huang 来测试 SQL Server 中 R 代码的性能，通过执行操作，帮助数据科学家创建可缩放的企业级解决方案。

### <a name="methods"></a>方法

RevoScaleR 和 MicrosoftML 包用于定型涉及大型数据集的复杂 R 解决方案中的预测模型。 SQL 查询和 R 代码是在所有测试中完全相同。 安装 SQL server 的单个 Azure VM 上执行测试的条件。 然后，作者进行比较评分时间使用和不使用 SQL Server 提供的以下优化：

- 内存中表
- ssNoVersion
- Resource Governor

若要评估 R 脚本执行对软件 NUMA 的影响，数据科学团队测试解决方案在 20 个物理核心 Azure 虚拟机上。 在这些物理核心、 四个软件 NUMA 节点自动创建，以便每个节点包含五个核心。

CPU 关联已强制执行在 resume 匹配方案中，若要评估对 R 作业的影响。 四个**SQL 的资源池**和四**外部资源池**而创建，并指定了 CPU 关联，以确保将每个节点中使用一组相同的 Cpu。

每个资源池已分配到不同工作负荷组，以优化硬件利用率。 原因是该软件 NUMA 和 CPU 关联不能将划分的物理 NUMA 节点; 中的物理内存因此，根据定义基于同一个物理 NUMA 节点的所有软 NUMA 节点必须使用内存中同一个操作系统内存块。 换而言之，没有任何内存到处理器的关联。

以下过程用于创建此配置：

1. 减少默认情况下分配给 SQL Server 的内存量。

2. 创建四个并行运行 R 作业的新池。

3. 创建四个工作负荷组，以便在每个工作负荷组都与资源池相关联。

4. 使用新的工作负荷组和分配，重新启动资源调控器。

5. 创建用户定义的分类器函数 (UDF) 分配不同的工作负荷组上的不同任务。

6. 更新资源调控器配置以使用相应的工作负荷组的函数。

### <a name="results"></a>结果

必须研究继续匹配中的获得最佳性能的配置如下所示：

-   四个内部资源池 （适用于 SQL Server)

-   （对于外部脚本作业） 的四个外部资源池

-   每个资源池是与特定工作负荷组相关联

-   每个资源池分配给不同的 Cpu

-   最大内部内存使用情况 （适用于 SQL Server) = 30%

-   使用 R 会话的最大内存为 70%

用于 resume 匹配模型外部脚本使用了大量，并且没有其他数据库引擎服务运行。 因此，分配给外部脚本的资源已增加到了 70%，这被证明脚本性能的最佳配置。

此配置被到达通过试验不同的值。 如果使用不同的硬件或另一种解决方案，最佳的配置可能会有所不同。 始终通过试验来找到最适合您的案例配置 ！

在优化的解决方案中，1.1 一百万行数据 （包括 100 功能） 的已评分 20 核计算机上在 8.5 秒内。 优化显著改进了性能根据评分的时间。

结果还建议**的功能数**评分的时间很大的影响。 更多的功能用于预测模型中时，改进了甚至更显著。

我们建议您阅读此博客文章，并详细讨论的随附教程。

-   [SQL Server 中机器学习的优化提示和技巧](https://azure.microsoft.com/blog/optimization-tips-and-tricks-on-azure-sql-server-for-machine-learning-services/)

多个用户已记下 R （或 Python） 运行时加载第一次没有小暂停。 出于此原因，这些测试中所述的第一次运行时间是通常单位但更高版本被丢弃。 后续缓存可能会导致显著的性能差异第一个和第二个运行。 此外还有一些系统开销外部运行时，SQL Server 之间移动数据时尤其是通过网络而不是直接从 SQL Server 加载传递数据。

出于这些原因，没有单一解决方案来缓解此初始加载期间，如变化较大的性能影响取决于任务。 例如，执行缓存的单行批处理; 中的计分因此，后续评分操作都要快得多，并且模型和 R 运行时都不重新加载。 此外可以使用[本机计分](../sql-native-scoring.md)以避免完全加载 R 运行时。

对于训练大型模型或大型批处理中的计分，开销可能会与从避免数据移动或流式处理和并行处理的提升相比最小。 请参阅此博客文章的更多的性能指南：

+ [使用 R 检测欺诈行为在 1 百万个事务 / 秒](https://blog.revolutionanalytics.com/2016/09/fraud-detection.html/)

## <a name="resources"></a>资源

以下是信息、 工具和脚本在这些测试的开发中使用的链接。

+ 性能测试脚本和数据的链接：[示例数据和 SQL Server 优化研究的脚本](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning)

+ 描述恢复匹配解决方案的文章：[优化提示和技巧的 SQL Server R Services](https://azure.microsoft.com/blog/optimization-tips-and-tricks-on-azure-sql-server-for-machine-learning-services/)

+ 在 SQL 优化用于 resume 匹配解决方案脚本：[GitHub 存储库](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/SQLOptimizationTips)

### <a name="learn-about-windows-server-management"></a>了解 Windows server 管理

+ [如何确定 64 位版本 Windows 的合适页面文件大小](https://support.microsoft.com/kb/2860880)

+ [了解 NUMA](https://technet.microsoft.com/library/ms178144.aspx)

+ [SQL Server 如何支持 NUMA](https://technet.microsoft.com/library/ms180954.aspx)

+ [Soft NUMA](https://docs.microsoft.com/sql/database-engine/configure-windows/soft-numa-sql-server)

### <a name="learn-about-sql-server-optimizations"></a>了解有关 SQL Server 优化

+ [重新组织和重新生成索引](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)

+ [内存优化表简介](https://docs.microsoft.com/sql/relational-databases/in-memory-oltp/introduction-to-memory-optimized-tables)

+ [演示：内存中 OLTP 的性能改进](https://docs.microsoft.com/sql/relational-databases/in-memory-oltp/demonstration-performance-improvement-of-in-memory-oltp)

+ [数据压缩](../../relational-databases/data-compression/data-compression.md)

+ [对表或索引启用压缩](../../relational-databases/data-compression/enable-compression-on-a-table-or-index.md)

+ [对表或索引禁用压缩](../../relational-databases/data-compression/disable-compression-on-a-table-or-index.md)

### <a name="learn-about-managing-sql-server"></a>了解如何管理 SQL Server

+ [监视和优化性能](../../relational-databases/performance/monitor-and-tune-for-performance.md)

+ [资源调控器](../../relational-databases/resource-governor/resource-governor.md)

+ [资源调控器简介](https://technet.microsoft.com/library/bb895232.aspx)

+ [R Services 的资源调控](resource-governance-for-r-services.md)

+ [如何为 R 创建资源池](how-to-create-a-resource-pool-for-r.md)

+ [配置资源调控器的示例](https://blog.sqlauthority.com/2012/06/04/sql-server-simple-example-to-configure-resource-governor-introduction-to-resource-governor/)

### <a name="tools"></a>工具

+ [DISKSPD 存储负载生成器/性能测试工具](https://github.com/microsoft/diskspd)

+ [FSUtil 实用工具参考](https://technet.microsoft.com/library/cc753059.aspx)


## <a name="other-articles-in-this-series"></a>本系列中的其他文章

[性能优化适用于 R 的简介](sql-server-r-services-performance-tuning.md)

[R 的 SQL Server 配置的性能优化](sql-server-configuration-r-services.md)

[R-R 的性能优化的代码和数据优化](r-and-data-optimization-r-services.md)

[性能优化-案例研究结果](performance-case-study-r-services.md)
