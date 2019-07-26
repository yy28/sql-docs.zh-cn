---
title: SQL Server R Services 结果和资源的性能
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/29/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: 8d7f046e961efb6129f807a7626e498062c415b6
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470161"
---
# <a name="performance-for-r-services-results-and-resources"></a>R Services 的性能: 结果和资源
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文是一系列介绍 R Services 的性能优化的第四项和最后一篇文章。 本文总结了测试各种优化方法的两种案例研究的方法、结果和结论。

这两种案例研究的目标不同:

+ 第一案例研究由 R 服务开发团队, 旨在衡量特定优化技术的影响
+ 第二种案例研究是由数据科研团队 vspackage 的, 它具有多个方法来确定针对特定大容量计分方案的最佳优化。

本主题列出了第一次案例研究的详细结果。 对于第二种案例研究, 摘要介绍了总体发现。 本主题末尾的链接指向所有脚本和示例数据, 以及原始作者使用的资源。

## <a name="performance-case-study-airline-dataset"></a>性能案例研究:航空数据集

SQL Server R Services 开发团队分析了各种优化的影响。 已创建单个 rxLogit 模型并对航空公司数据集执行评分。 优化是在训练和评分过程中应用的, 用于评估各个影响。

- GithubSQL Server 优化研究的[示例数据和脚本](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning)

### <a name="test-methods"></a>测试方法

1. 航空公司数据集包含单个表的10M 行。 它已下载并大容量加载到 SQL Server 中。
2. 表中包含六个副本。
3. 对表的副本应用了各种修改, 以测试 SQL Server 功能, 如页压缩、行压缩、索引栏数据存储等。
4. 在应用每个优化之前和之后测量性能。

| 表名| 描述|
|------|------|
| *airline* | 使用 `rxDataStep` 从原始 xdf 文件转换的数据|                          |
| *airlineWithIntCol*   | *DayOfWeek* 已转换为整数而不是字符串。 另外，添加了 *rowNum* 列。|
| *airlineWithIndex*    | 数据与 *airlineWithIntCol* 表相同，但使用 *rowNum* 列添加了单个聚集索引。|
| *airlineWithPageComp* | 数据与 *airlineWithIndex* 表相同，但已启用页压缩。 另外，添加了基于 *CRSDepTime* 和 *ArrDelay* 计算得出的两个列：*CRSDepHour* 和 *Late*。 |
| *airlineWithRowComp*  | 数据与 *airlineWithIndex* 表相同，但已启用行压缩。 另外，添加了基于 *CRSDepTime* 和 *ArrDelay* 计算得出的两个列：*CRSDepHour* 和 *Late*。 |
| *airlineColumnar*     | 包含单个聚集索引的纵栏表存储。 此表中填充了来自已清理的 csv 文件中的数据。|

每个测试包括以下步骤:

1. 运行每项测试之前已引发 R 垃圾回收。
2. 逻辑回归模型是基于表数据创建的。 每项测试的 *rowsPerRead* 值设置为 500000。
3. 使用训练的模型生成分数
4. 每个测试运行了六次。 首次运行的时间 ("冷运行") 已删除。 若要允许偶尔离群值, 还将删除剩余5次运行中的**最长**时间。 已使用四次剩余运行的平均值来计算每项测试的平均消耗运行时。
5. 使用值为3的*reportProgress*参数 (= 报告计时和进度) 运行测试。 每个输出文件都包含有关 IO、转换时间和计算时间所用时间的信息。 这些时间可用于故障排除和诊断。
6. 控制台输出也定向到输出目录中的文件。
7. 测试脚本处理这些文件中的时间来计算运行的平均时间。

例如, 下面的结果是来自单个测试的时间。 主要关注的时间是“总读取时间”（IO 时间）和“转换时间”（设置计算进程所产生的开销）。

**采样计时**

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

建议你下载和修改测试脚本, 以帮助你排查 R Services 或 with RevoScaleR 函数的问题。

### <a name="test-results-all"></a>测试结果 (全部)

本节比较每个测试的前后结果。

#### <a name="data-size-with-compression-and-a-columnar-table-store"></a>使用压缩和纵栏表存储的数据大小

第一次测试是使用压缩和纵栏表来减小数据大小。

| 表名            | “行”     | 保留   | Data       | index_size | 未使用  | 节省率（保留） |
|-----------------------|----------|------------|------------|------------|---------|---------------------|
| *airlineWithIndex*    | 10000000 | 2978816 KB | 2972160 KB | 6128 KB    | 528 KB  | 0                   |
| *airlineWithPageComp* | 10000000 | 625784 KB  | 623744 KB  | 1352 KB    | 688 KB  | 79%                 |
| *airlineWithRowComp*  | 10000000 | 1262520 KB | 1258880 KB | 2552 KB    | 1088 KB | 58%                 |
| *airlineColumnar*     | 9999999  | 201992 KB  | 201624 KB  | 不适用        | 368 KB  | 93%                 |

**总结**

数据大小的最大缩减是通过应用列存储索引来实现的, 然后是页压缩。

#### <a name="effects-of-compression"></a>压缩效果

此测试比较了行压缩、页面压缩和无压缩的优点。 已使用`rxLinMod`三个不同数据表的数据对模型进行定型。 对所有表使用了相同的公式和查询。

| 表名            | 测试名称       | numTasks | 平均时间 |
|-----------------------|-----------------|----------|--------------|
| *airlineWithIndex*    | NoCompression   | 1        | 5.6775       |
|                       | NoCompression-并行| 4        | 5.1775       |
| *airlineWithPageComp* | PageCompression | 1        | 6.7875       |
|                       | PageCompression-并行 | 4        | 5.3225       |
| *airlineWithRowComp*  | RowCompression  | 1        | 6.1325       |
|                       | RowCompression-并行  | 4        | 5.2375       |

**总结**

仅压缩不会有帮助。 在此示例中, 用于处理压缩的 CPU 增加会降低 IO 时间的减少量。

但是，如果将 *numTasks* 设置为 4 以便并行运行测试，则平均时间将会减少。

对于较大的数据集，压缩效果可能更明显。 压缩取决于数据集和值，因此可能需要进行试验，确定压缩对数据集产生的影响。

### <a name="effect-of-windows-power-plan-options"></a>Windows 电源计划选项的影响

在此试验中，已将 `rxLinMod` 用于 *airlineWithIntCol* 表。 Windows 电源计划设置为**均衡**或**高性能**。 在所有测试轮次中，*numTasks* 设置为 1。 测试运行了六次, 并在两个电源选项下执行了两次, 以调查结果的可变性。

**高性能**电源选项:

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

**总结**

使用 Windows**高性能**电源计划时, 执行时间更一致, 速度更快。

#### <a name="using-integer-vs-strings-in-formulas"></a>在公式中使用整数与字符串

此测试评估了修改 R 代码以避免常见的字符串因素问题的影响。 具体而言, 模型是使用`rxLinMod`两个表定型的: 在第一种情况下, 因数存储为字符串; 在第二个表中, 系数存储为整数。

+ 对于*航空公司*表, [DayOfWeek] 列包含字符串。 _ColInfo_参数用于指定系数级别 (星期一、星期二、...)

+  对于*airlineWithIndex*表, [DayOfWeek] 是整数。 未指定_colInfo_参数。

+ 在这两种情况下，都使用了同一个公式：`ArrDelay ~ CRSDepTime + DayOfWeek`。

| 表名          | 测试名称   | 平均时间 |
|---------------------|-------------|--------------|
| *航班*           | *FactorCol* | 10.72        |
| *airlineWithIntCol* | *IntCol*    | 3.4475       |

**总结**

对于系数使用整数而不是字符串时, 有一个明显的优点。

### <a name="avoiding-transformation-functions"></a>避免转换函数

在此测试中, 已使用`rxLinMod`训练模型, 但在两次运行之间更改了代码:

+ 在第一次运行中, 转换函数作为模型生成的一部分应用。 
+ 在第二次运行中, 功能值为预计算且可用, 因此不需要任何转换函数。

| 测试名称             | 平均时间 |
|-----------------------|--------------|
| WithTransformation    | 5.1675       |
| WithoutTransformation | 4.7          |

**总结**

当**不**使用转换函数时, 训练时间较短。 换言之, 当使用预先计算并保存在表中的列时, 模型的定型速度更快。

如果有更多的转换, 并且数据集较大 (\> 100M), 则估计的节省量会更高。

### <a name="using-columnar-store"></a>使用纵栏存储

此测试评估了使用纵栏式数据存储和索引的性能优势。 使用`rxLinMod`对相同的模型进行了定型, 但没有数据转换。

+ 在第一次运行中, 数据表使用了标准行存储区。
+ 在第二次运行中, 使用了列存储。

| 表名         | 测试名称 | 平均时间 |
|--------------------|-----------|--------------|
| *airlineWithIndex* | RowStore  | 4.67         |
| *airlineColumnar*  | ColStore  | 4.555        |

**总结**

纵栏存储比标准行存储区的性能更好。 在较大的数据集 (\> 100 M) 上, 性能可能会有很大差异。

### <a name="effect-of-using-the-cube-parameter"></a>使用 cube 参数的效果

此测试的目的是确定 RevoScaleR 中用于使用预计算**多维数据集**参数的选项是否可以提高性能。 使用以下公式训练`rxLinMod`了模型:

```R
ArrDelay ~ Origin:DayOfWeek + Month + DayofMonth + CRSDepTime
```

在表中, *DayOfWeek*的系数存储为字符串。

| 测试名称     | 多维数据集参数 | numTasks | 平均时间 | 单行预测 (ArrDelay_Pred) |
|---------------|----------------|----------|--------------|---------------------------------|
| CubeArgEffect | `cube = F`     | 1        | 91.0725      | 9.959204                        |
|               |                | 4        | 44.09        | 9.959204                        |
|               | `cube = T`     | 1        | 21.1125      | 9.959204                        |
|               |                | 4        | 8.08         | 9.959204                        |

**总结**

使用 cube 参数参数可以清楚地提高性能。

### <a name="effect-of-changing-maxdepth-for-rxdtree-models"></a>更改 rxDTree 模型的 maxDepth 的效果

在此试验中, `rxDTree`使用算法在*airlineColumnar*表上创建模型。 在此项测试中，*numTasks* 设置为 4。 *MaxDepth*的多个不同值用于演示更改树深度如何影响运行时。

| 测试名称       | maxDepth | 平均时间 |
|-----------------|----------|--------------|
| TreeDepthEffect | 1        | 10.1975      |
|                 | 2        | 13.2575      |
|                 | 4        | 19.27        |
|                 | 8        | 45.5775      |
|                 | 16       | 339.54       |

**总结**

随着树深度的增加, 节点总数以指数方式增加。 创建模型所用的时间也会显著增加。

### <a name="prediction-on-a-stored-model"></a>预测存储模型

此测试的目的是确定将训练的模型保存到 SQL Server 表而不是作为当前正在执行的代码的一部分生成时对评分产生的性能影响。 为评分, 将从数据库加载存储的模型, 并使用内存中的单行数据帧 (本地计算上下文) 创建预测。

测试结果显示了保存模型的时间, 以及加载模型和预测所花费的时间。

| 表名 | 测试名称 | 平均时间（训练模型） | 保存/加载模型花费的时间|
|------------|------------|------------|------------|
| airline    | SaveModel| 21.59| 2.08|
| airline    | LoadModelAndPredict | | 2.09（包括预测花费的时间） |

**总结**

从表中加载定型模型, 显然是执行预测的更快方法。 建议你避免创建模型, 并在同一脚本中执行全部评分。

## <a name="case-study-optimization-for-the-resume-matching-task"></a>案例研究:恢复匹配任务的优化

恢复匹配模型是由 Microsoft 数据科学家 Ke Huang 开发的, 用于测试 SQL Server 中 R 代码的性能, 并通过此操作帮助数据科学家创建可缩放的企业级解决方案。

### <a name="methods"></a>方法

RevoScaleR 和 MicrosoftML 包都用于在包含大型数据集的复杂 R 解决方案中训练预测模型。 所有测试中的 SQL 查询和 R 代码都相同。 测试是在安装了 SQL Server 的单个 Azure VM 上进行的。 然后, 作者将评分时间与和进行比较, 而不是由 SQL Server 提供的以下优化:

- 内存中表
- ssNoVersion
- Resource Governor

为了评估软件 NUMA 对 R 脚本执行的影响, 数据科学团队在具有20个物理内核的 Azure 虚拟机上测试了解决方案。 在这些物理内核上, 自动创建了四个软件 NUMA 节点, 使每个节点包含五个核心。

CPU affinitization 是在恢复匹配方案中强制执行的, 用于评估对 R 作业的影响。 创建了四个**SQL 资源池**和四个**外部资源池**, 并指定了 CPU 关联, 以确保每个节点中都使用同一组 cpu。

每个资源池都已分配给不同的工作负荷组, 以优化硬件利用率。 原因在于, 软 NUMA 和 CPU 关联不能在物理 NUMA 节点中划分物理内存;因此, 根据定义, 基于同一物理 NUMA 节点的所有软 NUMA 节点必须在同一 OS 内存块中使用内存。 换句话说, 没有内存到处理器的关联。

以下过程用于创建此配置:

1. 将默认分配的内存量减少到 SQL Server。

2. 创建四个新池以并行运行 R 作业。

3. 创建四个工作负荷组, 使每个工作负荷组与一个资源池相关联。

4. 重新启动 Resource Governor 新的工作负荷组和分配。

5. 创建用户定义的分类器函数 (UDF), 以便为不同的工作负荷组分配不同的任务。

6. 更新 Resource Governor 配置, 以将函数用于适当的工作负荷组。

### <a name="results"></a>结果

在恢复匹配研究中具有最佳性能的配置如下所示:

-   四个内部资源池 (用于 SQL Server)

-   四个外部资源池 (适用于外部脚本作业)

-   每个资源池都与特定的工作负荷组关联

-   每个资源池分配给不同的 Cpu

-   最大内部内存使用量 (用于 SQL Server) = 30%

-   R 会话使用的最大内存 = 70%

对于恢复匹配模式, 外部脚本使用非常繁重, 没有其他数据库引擎服务正在运行。 因此, 分配给外部脚本的资源增加了 70%, 这为脚本性能提供了最佳配置。

此配置是通过试验不同的值到达的。 如果使用不同的硬件或不同的解决方案, 则最佳配置可能会有所不同。 始终试验以找到适合你的情况的最佳配置!

在优化的解决方案中, 1100000 行数据 (包含100功能) 在20核计算机上的8.5 秒内评分。 优化在评分时间方面大大提高了性能。

结果还建议**特征数量**对评分时间有重大影响。 当在预测模型中使用更多功能时, 改进更突出。

建议阅读此博客文章和随附的教程, 详细讨论。

-   [SQL Server 中的机器学习的优化提示和技巧](https://azure.microsoft.com/blog/optimization-tips-and-tricks-on-azure-sql-server-for-machine-learning-services/)

许多用户已注意到, 第一次加载 R (或 Python) 运行时时有一小的暂停。 出于此原因, 如这些测试中所述, 通常会度量首次运行的时间, 但以后会将其丢弃。 后续的缓存可能会导致第一次和第二次运行之间出现明显的性能差异。 在 SQL Server 和外部运行时之间移动数据时, 尤其是当数据通过网络传递而不是直接从 SQL Server 中加载时, 还会有一些开销。

出于上述所有原因, 不存在用于缓解此初始加载时间的单一解决方案, 因为性能影响因任务的不同而异。 例如, 为批处理中的单行计分执行缓存;因此, 连续计分操作的速度要快得多, 模型和 R 运行时都不会重新加载。 你还可以使用[本机计分](../sql-native-scoring.md)来避免完全加载 R 运行时。

对于大型模型或较大批处理的评分, 与避免数据移动或流式处理和并行处理的收益相比, 开销可能会降至最低。 请参阅此博客文章, 了解更多性能指导:

+ [使用 R 检测每秒1000000个事务的欺诈](https://blog.revolutionanalytics.com/2016/09/fraud-detection.html/)

## <a name="resources"></a>资源

下面是用于开发这些测试的信息、工具和脚本的链接。

+ 性能测试脚本和数据链接:[SQL Server 优化研究的示例数据和脚本](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning)

+ 介绍恢复匹配解决方案的文章:[SQL Server R Services 的优化提示和技巧](https://azure.microsoft.com/blog/optimization-tips-and-tricks-on-azure-sql-server-for-machine-learning-services/)

+ SQL 优化中用于恢复匹配解决方案的脚本:[GitHub 存储库](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/SQLOptimizationTips)

### <a name="learn-about-windows-server-management"></a>了解 Windows server 管理

+ [如何确定 64 位版本 Windows 的合适页面文件大小](https://support.microsoft.com/kb/2860880)

+ [了解 NUMA](https://technet.microsoft.com/library/ms178144.aspx)

+ [SQL Server 如何支持 NUMA](https://technet.microsoft.com/library/ms180954.aspx)

+ [Soft NUMA](https://docs.microsoft.com/sql/database-engine/configure-windows/soft-numa-sql-server)

### <a name="learn-about-sql-server-optimizations"></a>了解 SQL Server 优化

+ [重新组织和重新生成索引](../../relational-databases/indexes/reorganize-and-rebuild-indexes.md)

+ [内存优化表简介](https://docs.microsoft.com/sql/relational-databases/in-memory-oltp/introduction-to-memory-optimized-tables)

+ [演示：内存中 OLTP 的性能改进](https://docs.microsoft.com/sql/relational-databases/in-memory-oltp/demonstration-performance-improvement-of-in-memory-oltp)

+ [数据压缩](../../relational-databases/data-compression/data-compression.md)

+ [对表或索引启用压缩](../../relational-databases/data-compression/enable-compression-on-a-table-or-index.md)

+ [对表或索引禁用压缩](../../relational-databases/data-compression/disable-compression-on-a-table-or-index.md)

### <a name="learn-about-managing-sql-server"></a>了解如何管理 SQL Server

+ [监视和优化性能](../../relational-databases/performance/monitor-and-tune-for-performance.md)

+ [资源调控器](../../relational-databases/resource-governor/resource-governor.md)

+ [简介 Resource Governor](https://technet.microsoft.com/library/bb895232.aspx)

+ [R Services 的资源调控](resource-governance-for-r-services.md)

+ [如何为 R 创建资源池](how-to-create-a-resource-pool-for-r.md)

+ [配置 Resource Governor 的示例](https://blog.sqlauthority.com/2012/06/04/sql-server-simple-example-to-configure-resource-governor-introduction-to-resource-governor/)

### <a name="tools"></a>工具

+ [DISKSPD 存储负载生成器/性能测试工具](https://github.com/microsoft/diskspd)

+ [FSUtil 实用工具参考](https://technet.microsoft.com/library/cc753059.aspx)


## <a name="other-articles-in-this-series"></a>本系列中的其他文章

[R 的性能优化-简介](sql-server-r-services-performance-tuning.md)

[R SQL Server 配置的性能优化](sql-server-configuration-r-services.md)

[R-R 代码和数据优化的性能优化](r-and-data-optimization-r-services.md)

[性能优化-案例研究结果](performance-case-study-r-services.md)
