---
title: SQL Server 配置 (R Services)
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/29/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: feb59ac529b0a66603d9e8b901e9755588ac0379
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/19/2019
ms.locfileid: "68344847"
---
# <a name="sql-server-configuration-for-use-with-r"></a>用于 R 的 SQL Server 配置
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文是一系列文章中的第二个, 描述基于两例研究的 R Services 的性能优化。  本文提供了有关用于运行 SQL Server R Services 的计算机的硬件和网络配置的指导。 它还包含有关配置解决方案中使用的 SQL Server 实例、数据库或表的方式的信息。 由于在 SQL Server 中使用 NUMA 会在硬件和数据库优化之间进行区分, 因此, 第三部分将详细讨论 CPU affinitization 和资源调控。

> [!TIP]
> 如果你不熟悉 SQL Server, 我们强烈建议你同时查看 SQL Server 性能优化指南:[监视和优化性能](https://docs.microsoft.com/sql/relational-databases/performance/monitor-and-tune-for-performance)。

## <a name="hardware-optimization"></a>硬件优化

优化服务器计算机对于确保拥有运行外部脚本的资源非常重要。 当资源有限时, 可能会看到以下症状:

- 作业执行被延迟或取消, 以确定其他数据库操作的优先级
- 错误 "超过了配额" 导致 R 脚本终止, 无需完成
- 加载到 R 内存中的数据已截断, 导致结果不完整

### <a name="memory"></a>内存

计算机上的可用内存量可能会对高级分析算法的性能造成很大的影响。 使用 SQL 计算上下文时, 内存不足可能会影响并行度。 此外，还会影响可处理的区块大小（每个读取操作使用的行数），以及可支持的并发会话数。

强烈建议使用至少 32 GB。 如果有超过 32 GB 的可用空间, 则可以将 SQL 数据源配置为在每个读取操作中使用更多的行, 从而提高性能。

你还可以管理实例使用的内存。 默认情况下, 在分配内存时, SQL Server 优先于外部脚本进程。 在 R 服务的默认安装中, 只有 20% 的可用内存分配给 R。

这对于数据科学任务通常是不够的, 但您不希望枯竭 SQL server 的内存。 您应在数据库引擎、相关服务和外部脚本之间试验和微调内存分配, 并理解最佳配置因情况而异。

对于恢复匹配模式, 外部脚本使用非常繁重, 没有其他数据库引擎服务运行;因此, 分配给外部脚本的资源增加了 70%, 这是用于脚本性能的最佳配置。

### <a name="power-options"></a>电源选项

在 Windows 操作系统上, 应使用 "**高性能**" 电源选项。 使用不同的电源设置会导致使用 SQL Server 时性能下降或不一致。

### <a name="disk-io"></a>磁盘 IO

使用 R Services 的培训和预测作业本质上是 IO 绑定的, 取决于存储数据库的磁盘的速度。 驱动器 (如固态硬盘 (SSD)) 可能会有所帮助。

磁盘 IO 还会受到访问磁盘的其他应用程序的影响：例如，其他客户端对数据库执行的读取操作。 磁盘 IO 性能还会受到使用的文件系统中的设置（例如，文件系统使用的块大小）影响。

如果有多个驱动器可用, 则将数据库存储在与 SQL Server 不同的驱动器上, 以便数据库引擎的请求与数据库中存储的数据的请求不在同一磁盘上。

在训练期间运行使用多个迭代的 RevoScaleR 分析函数时，磁盘 IO 也可能会对性能造成很大的影响。 例如`rxLogit` ,、、`rxDTree`和`rxBTrees`都使用多个迭代。 `rxDForest` SQL Server 数据源时, 这些算法使用经过优化的临时文件来捕获数据。 会话完成后，会自动清理这些文件。 使用高性能磁盘进行读/写操作可以显著提高这些算法的总运行时间。

> [!NOTE]
> 早期版本的 R Services 要求在 Windows 操作系统上支持8.3 文件名。 Service Pack 1 后, 此限制已提升。 但是, 你可以使用 fsutil 来确定驱动器是否支持8.3 文件名, 或者如果不支持, 则启用支持。

### <a name="paging-file"></a>页面文件

Windows 操作系统使用分页文件来管理故障转储和存储虚拟内存页面。 如果你发现分页过度，请考虑增大计算机上的物理内存。 尽管分配更多的物理内存不会消除分页，但确实可以减少分页的需要。

存储页面文件的磁盘的速度也会影响性能。 将页面文件存储在 SSD 中或者在多个 SSD 上使用多个页面文件可以提高性能。

有关调整页面文件大小的信息, 请参阅[如何确定适用于64位版本 Windows 的合适页面文件大小](https://support.microsoft.com/kb/2860880)。

## <a name="optimizations-at-instance-or-database-level"></a>实例或数据库级别的优化

优化 SQL Server 实例是有效执行外部脚本的关键所在。

> [!NOTE]
> 最佳设置会因数据的大小和类型、用于计分或定型模型的列数而异。
> 
> 您可以查看最终文章中特定优化的结果:[性能优化-案例研究结果](../../advanced-analytics/r/performance-case-study-r-services.md)
> 
> 有关示例脚本, 请参阅单独的[GitHub 存储库](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning)。

### <a name="table-compression"></a>表压缩

通常可以使用压缩或列式数据存储来改进 IO 性能。 通常, 数据在表中的多个列中都是重复的, 因此, 在压缩数据时, 使用列存储可充分利用这些重复项。

如果表中有很多插入内容, 则列存储可能效率不高, 但如果数据是静态的或只是不常更改的, 则这是一个不错的选择。 如果纵栏表存储不适用，对主表中的行启用压缩可以改善 IO。

有关详细信息，请参阅以下文档：

+ [数据压缩](../../relational-databases/data-compression/data-compression.md)

+ [对表或索引启用压缩功能](../../relational-databases/data-compression/enable-compression-on-a-table-or-index.md)

+ [列存储索引指南](../../relational-databases/indexes/columnstore-indexes-overview.md)

### <a name="memory-optimized-tables"></a>内存优化表

如今, 对于新式计算机, 内存不再是问题。 随着硬件规格不断提高, 使 RAM 获得良好的价值相对容易。 但同时, 数据的生成速度比以往任何时候都要快, 并且必须以低延迟处理数据。

内存优化表表示一个解决方案, 因为它们利用高级计算机中提供的大内存来处理大数据的问题。 内存优化表主要驻留在内存中, 以便从内存中读取和写入数据。 对于持久性, 将在磁盘上维护表的第二个副本, 并且仅在数据库恢复期间从磁盘读取数据。

如果需要频繁读取和写入表, 内存优化表可帮助实现高可伸缩性和低延迟。  在恢复匹配方案中, 使用内存优化表时, 可以从数据库中读取所有的恢复功能, 并将其存储在主内存中, 以便与新的作业空缺相匹配。 这大大减少了磁盘 IO。

通过使用内存优化表, 在将预测从多个并发批处理写回数据库的过程中, 可实现更高的性能提升。 对 SQL Server 上的内存优化表的使用对表读取和写入启用了低延迟。

在开发过程中, 体验也是无缝的。 持久的内存优化表是在创建数据库的同时创建的。 因此, 无论数据存储在何处, 开发都使用相同的工作流。

### <a name="processor"></a>处理器

SQL Server 可以通过使用计算机上的可用内核并行执行任务;可用的内核越多, 性能越好。 虽然增加核心数可能不适用于 IO 绑定操作, 但 CPU 绑定算法从具有多个内核的更快的 Cpu 受益。

由于服务器通常同时由多个用户使用, 因此数据库管理员必须确定支持高峰工作负荷计算所需的理想内核数。

### <a name="resource-governance"></a>资源调控

在支持 Resource Governor 的版本中, 你可以使用资源池来指定为某些工作负荷分配一定数量的 Cpu。 你还可以管理分配给特定工作负荷的内存量。

SQL Server 中的资源调控允许您集中监视和控制由 R SQL Server 使用的各种资源。例如, 你可能会为数据库引擎分配一半可用内存, 以确保核心服务始终可以运行, 而不管是暂时性更繁重的工作负荷。

外部脚本的内存消耗默认值限制为可用于 SQL Server 自身的总内存的 20%。 默认情况下, 此限制适用于确保依赖于数据库服务器的所有任务不会受到长时间运行 R 作业的严重影响。 但是，数据库管理员可以更改这些限制。 在许多情况下, 20% 的限制不足以支持严重的机器学习工作负荷。

支持的配置选项包括**MAX_CPU_PERCENT**、 **MAX_MEMORY_PERCENT**和**MAX_PROCESSES**。 若要查看当前设置, 请使用以下语句:`SELECT * FROM sys.resource_governor_external_resource_pools`

-  如果服务器主要用于 R Services, 则将 MAX_CPU_PERCENT 增加到 40% 或 60% 可能会有所帮助。

-  如果多个 R 会话必须同时使用同一服务器, 则应增加三个设置。

若要更改已分配的资源值, 请使用 T-sql 语句。

+ 此语句将内存使用率设置为 40%:`ALTER EXTERNAL RESOURCE POOL [default] WITH (MAX_MEMORY_PERCENT = 40)`

+ 此语句设置所有三个可配置值:`ALTER EXTERNAL RESOURCE POOL [default] WITH (MAX_CPU_PERCENT = 40, MAX_MEMORY_PERCENT = 50, MAX_PROCESSES = 20)`

+ 如果更改了内存、CPU 或 max 进程设置, 然后希望立即应用这些设置, 请运行以下语句:`ALTER RESOURCE GOVERNOR RECONFIGURE`

## <a name="soft-numa-hardware-numa-and-cpu-affinity"></a>软件 NUMA、硬件 NUMA 和 CPU 关联

使用 SQL Server 作为计算上下文时, 有时可以通过优化与 NUMA 和处理器相关性相关的设置来获得更好的性能。 

具有_硬件 NUMA_的系统具有多个系统总线, 每个系统总线为一小组处理器提供服务。 每个 CPU 都可以通过一致的方式访问与其他组关联的内存。 每个组称为一个“NUMA 节点”。 如果具有硬件 NUMA，则它可能会配置为使用交错内存而不使用 NUMA。 在这种情况下, Windows 因此 SQL Server 不会将其识别为 NUMA。 

您可以运行以下查询来查找可用于 SQL Server 的内存节点数:

```sql
SELECT DISTINCT memory_node_id
FROM sys.dm_os_memory_clerks
```

如果查询返回单个内存节点 (节点 0), 则要么没有硬件 NUMA, 要么将硬件配置为交错 (非 NUMA)。 如果有4个或更少的 Cpu, 或者至少一个节点只有一个 CPU, 则 SQL Server 也会忽略硬件 NUMA。

如果计算机有多个处理器, 但没有硬件 NUMA, 则还可以使用[软件 numa](https://docs.microsoft.com/sql/database-engine/configure-windows/soft-numa-sql-server)将 cpu 细分为较小的组。  在 SQL Server 2016 和 SQL Server 2017 中, 启动 SQL Server 服务时, 将自动启用软 NUMA 功能。

启用软 NUMA 后, SQL Server 会自动为你管理节点;但是, 若要针对特定工作负荷进行优化, 可以禁用软 NUMA 节点的_软关联_并手动配置 CPU 关联。 这样, 就可以更好地控制分配给哪些节点的工作负荷, 尤其是在使用支持资源调控的 SQL Server 版本的情况下。 通过指定 CPU 关联并使资源池与 Cpu 组对齐, 你可以减少延迟, 并确保在相同的 NUMA 节点中执行相关的进程。

配置软 NUMA 和 CPU 关联以支持 R 工作负荷的整个过程如下所示:

1. 启用软 NUMA (如果可用)
2. 定义处理器关联
3. 使用[Resource Governor](../r/resource-governance-for-r-services.md)为外部进程创建资源池
4. 将[工作负荷组](../../relational-databases/resource-governor/resource-governor-workload-group.md)分配给特定的地缘组

有关详细信息 (包括示例代码), 请参阅本教程:[SQL 优化提示和技巧 (Ke Huang)](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

**其他资源:**

+ [SQL Server 中的软件 NUMA](https://docs.microsoft.com/sql/database-engine/configure-windows/soft-numa-sql-server)
    
    如何将软件 NUMA 节点映射到 Cpu

## <a name="task-specific-optimizations"></a>特定于任务的优化

本部分汇总了在这些案例研究和其他测试中采用的用于优化特定机器学习工作负荷的方法。 常见的工作负荷包括模型定型、功能提取和特征工程以及用于计分的各种方案: 单行、小型批处理和大型批。

### <a name="feature-engineering"></a>特征工程

R 的一个难点是它通常在单个 CPU 上进行处理。 这是许多任务的主要性能瓶颈, 尤其是特征工程。 在恢复匹配解决方案中, 功能设计任务单独创建了2500叉积功能, 这些功能必须与原始100功能组合在一起。 如果所有内容都在单个 CPU 上完成, 则此任务将需要很长时间。

有多种方法可以提高功能工程的性能。 您可以优化 R 代码, 并在建模过程中保持功能提取, 或将特征工程过程移到 SQL 中。

- 使用 R。定义函数后, 在定型期间将它作为参数传递给[rxTransform](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxtransform) 。 如果模型支持并行处理, 则可以使用多个 Cpu 处理功能工程任务。 使用此方法, 数据科学团队在评分时间方面发现了 16% 的性能改进。 但是, 此方法需要支持并行化的模型和可使用并行计划执行的查询。

- 将 R 与 SQL 计算上下文配合使用。 在具有独立资源可用于执行单独批处理的多处理器环境中, 可以通过隔离用于每个批处理的 SQL 查询, 从表中提取数据并在同一工作负荷组中约束数据, 从而实现更高的效率。 用于隔离批处理的方法包括分区, 并使用 PowerShell 并行执行单独的查询。

- 即席并行执行:在 SQL Server 计算上下文中, 你可以依赖 SQL 数据库引擎来强制执行并行执行 (如果可能), 并且如果发现该选项更有效。

- 在单独的特征化进程中使用 T-sql。 使用 SQL Precomputing 功能数据的速度通常更快。

### <a name="prediction-scoring-in-parallel"></a>并行预测 (评分)

SQL Server 的优点之一是能够并行处理大量的行。 这里的优势在于评分。 通常, 模型不需要访问所有数据以进行评分, 因此你可以对输入数据进行分区, 每个工作负荷组处理一项任务。

您还可以将输入数据作为单个查询发送, 然后 SQL Server 分析查询。 如果可以为输入数据创建并行查询计划, 则它会自动将分配给节点的数据分区, 并同时执行所需的联接和聚合。

如果对如何定义用于计分的存储过程感兴趣, 请参阅[GitHub](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/SQLOptimizationTips/SQLR)上的示例项目, 并查找文件 "step5_score_for_matching"。 示例脚本还跟踪查询的开始和结束时间, 并将时间写入 SQL 控制台, 以便您可以评估性能。

### <a name="concurrent-scoring-using-resource-groups"></a>使用资源组的并发评分

为了增加评分问题, 一种很好的做法是采用地图缩减方法, 其中数百万项分为多个批处理。 然后, 同时执行多个评分作业。 在此框架中, 将在不同的 CPU 集上处理批处理, 并收集结果并将结果写回到数据库。

这是在恢复匹配方案中使用的方法;但是, SQL Server 中的资源调控对于实现此方法是必不可少的。 通过为外部脚本作业设置工作负荷组, 可以将 R 计分作业路由到不同的处理器组并实现更快的吞吐量。

资源调控还有助于分配服务器上的可用资源 (CPU 和内存), 以最大程度地降低工作负荷争用。 你可以设置分类器函数来区分不同类型的 R 作业: 例如, 你可能会决定从应用程序调用的计分始终优先, 而重新训练作业的优先级较低。 此资源隔离可能会缩短执行时间, 并提供更可预测的性能。

### <a name="concurrent-scoring-using-powershell"></a>使用 PowerShell 的并发评分

如果你决定自行对数据进行分区, 则可以使用 PowerShell 脚本来执行多个并发计分任务。 为此, 请使用 Invoke-SqlCmd cmdlet, 并并行启动计分任务。

在恢复匹配方案中, 并发设计如下:

- 20个处理器分为四组, 每组五个 Cpu。 每组 Cpu 都位于同一 NUMA 节点上。

- 并发批处理的最大数目设置为8。

- 每个工作负荷组都必须处理两个计分任务。 一旦一项任务读取完数据并开始评分, 另一个任务就可以开始从数据库中读取数据。

若要查看此方案的 PowerShell 脚本, 请打开[Github 项目](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/SQLOptimizationTips)中的文件试验。

### <a name="storing-models-for-prediction"></a>存储预测模型

当训练和评估完成并且您选择了最佳模型后, 我们建议在数据库中存储该模型, 使其可用于预测。 从用于预测的数据库加载预计算模型是高效的, 因为 SQL Server 机器学习在 R 和数据库之间移动时使用特殊的序列化算法来存储和加载模型。

> [!TIP]
> 在 SQL Server 2017 中, 即使服务器上未安装 R, 也可以使用 PREDICT 函数执行评分。 支持有限的模型类型, 从 RevoScaleR 包。

但是, 根据所使用的算法, 某些模型可能很大, 尤其是在对大型数据集进行训练时。 例如, 诸如**lm**或**glm**等算法会生成大量汇总数据和规则。 由于可以存储在 varbinary 列中的模型大小有限制, 因此, 我们建议您在将模型存储到生产数据库中之前, 从模型中消除不必要的项目。

## <a name="articles-in-this-series"></a>本系列文章

[R 的性能优化-简介](../r/sql-server-r-services-performance-tuning.md)

[R SQL Server 配置的性能优化](../r/sql-server-configuration-r-services.md)

[R-R 代码和数据优化的性能优化](../r/r-and-data-optimization-r-services.md)

[性能优化-案例研究结果](../r/performance-case-study-r-services.md)
