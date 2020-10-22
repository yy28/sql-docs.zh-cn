---
title: 进行配置以供 R 使用
description: 本文提供有关用于运行 SQL Server R Services 的计算机的硬件和网络配置的指导。
ms.prod: sql
ms.technology: machine-learning-services
ms.date: 03/29/2019
ms.topic: how-to
author: dphansen
ms.author: davidph
ms.custom: seo-lt-2019
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: feaa53fa47591ecdb3f1f0bc66ab390def8fbbb1
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/19/2020
ms.locfileid: "92195771"
---
# <a name="sql-server-configuration-for-use-with-r"></a>进行 SQL Server 配置以供 R 使用
[!INCLUDE [SQL Server 2016 and later](../../includes/applies-to-version/sqlserver2016.md)]

本文是基于两个案例研究介绍 R Services 的性能优化的系列文章中的第二篇。  本文提供有关用于运行 SQL Server R Services 的计算机的硬件和网络配置的指导。 它还包含有关配置解决方案中使用的 SQL Server 实例、数据库或表的方式的信息。 由于在 SQL Server 中使用 NUMA 模糊了硬件和数据库优化之间的界限，因此第三部分将详细讨论 CPU 关联和资源调控。

> [!TIP]
> 如果未使用过 SQL Server，则强烈建议你同时查看 SQL Server 性能优化指南：[监视和优化性能](../../relational-databases/performance/monitor-and-tune-for-performance.md)。

## <a name="hardware-optimization"></a>硬件优化

优化服务器计算机对于确保拥有运行外部脚本的资源来说非常重要。 当资源受限时，可能会发现以下问题：

- 延迟或取消作业执行，以优先处理其他数据库操作
- 错误“超出配额”导致 R 脚本未完成即终止
- 截断加载到 R 内存中的数据，从而导致不完整的结果

### <a name="memory"></a>内存

计算机上的可用内存量可能会对高级分析算法的性能造成很大的影响。 使用 SQL 计算上下文时，内存不足可能会影响并行度。 此外，还会影响可处理的区块大小（每个读取操作使用的行数），以及可支持的并发会话数。

强烈建议至少配置 32 GB 内存。 如果可用内存超过 32 GB，则可以将 SQL 数据源配置为在每个读取操作中使用更多的行，从而提高性能。

此外，还可以管理实例使用的内存。 默认情况下，分配内存时，SQL Server 的优先级高于外部脚本进程。 在 R 服务的默认安装中，只有 20% 的可用内存分配给 R。

通常，这对于数据科学任务来说还不够，但你也不希望耗尽 SQL Server 的内存。 应试验和微调数据库引擎、相关服务和外部脚本之间的内存分配，并理解最佳配置因情况而异。

对于恢复匹配模型，外部脚本使用非常多，且没有其他数据库引擎服务运行；因此，分配给外部脚本的资源增加到 70%，这是获取脚本性能的最佳配置。

### <a name="power-options"></a>电源选项

在 Windows 操作系统中，应使用“高性能”电源选项  。 使用不同的电源设置会导致使用 SQL Server 时性能下降或不一致。

### <a name="disk-io"></a>磁盘 IO

使用 R Services 的定型和预测作业原生受到 IO 约束，且依赖于存储数据库的磁盘的速度。 更快的驱动器（例如固态硬盘 (SSD)）可能会有所帮助。

磁盘 IO 还会受到访问磁盘的其他应用程序的影响：例如，其他客户端对数据库执行的读取操作。 磁盘 IO 性能还会受到使用的文件系统中的设置（例如，文件系统使用的块大小）影响。

如果有多个可用的驱动器，请将数据库存储在与 SQL Server 不同的驱动器上，使得针对数据库引擎发出的请求不会传入针对数据库中存储的数据发出的请求所在的同一磁盘。

在训练期间运行使用多个迭代的 RevoScaleR 分析函数时，磁盘 IO 也可能会对性能造成很大的影响。 例如，`rxLogit`、`rxDTree`、`rxDForest` 和 `rxBTrees` 均使用多个迭代。 如果数据源为 SQL Server，则这些算法将使用已优化的临时文件来捕获数据。 会话完成后，会自动清理这些文件。 使用高性能磁盘进行读/写操作可以大幅改善这些算法所消耗的总体时间。

> [!NOTE]
> 早期版本的 R Services 要求 Windows 操作系统具有 8.3 文件名支持。 Service Pack 1 发布后，此限制已解除。 但是，可以使用 fsutil.exe 确定驱动器是否支持 8.3 文件名，如果不支持，还可以启用这种支持。

### <a name="paging-file"></a>页面文件

Windows 操作系统使用分页文件来管理故障转储和存储虚拟内存页面。 如果你发现分页过度，请考虑增大计算机上的物理内存。 尽管分配更多的物理内存不会消除分页，但确实可以减少分页的需要。

存储页面文件的磁盘的速度也会影响性能。 将页面文件存储在 SSD 中或者在多个 SSD 上使用多个页面文件可以提高性能。

有关调整页面文件大小的信息，请参阅[如何确定 64 位版本 Windows 的合适页面文件大小](https://support.microsoft.com/kb/2860880)。

## <a name="optimizations-at-instance-or-database-level"></a>实例或数据库级别的优化

优化 SQL Server 实例是高效执行外部脚本的关键。

> [!NOTE]
> 最佳设置存在差异，具体取决于数据大小和类型，以及用于评分或定型模型的列数。
> 
> 可以在最后一篇文章中查看特定优化的结果：[性能优化 - 案例研究结果](../../machine-learning/r/performance-case-study-r-services.md)
> 
> 有关示例脚本，请参阅单独的 [GitHub 存储库](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning)。

### <a name="table-compression"></a>表压缩

通常，可以使用压缩或分栏式数据存储来提高 IO 性能。 一般情况下，数据往往在表中的多个列内重复，因此，使用列存储可以在压缩数据时利用这种重复。

如果在表中执行大量的插入，列存储的效率可能不高；但是，如果数据是静态的或者不经常更改，则列存储索引是不错的选择。 如果纵栏表存储不适用，对主表中的行启用压缩可以改善 IO。

有关详细信息，请参阅以下文档：

+ [Data compression](../../relational-databases/data-compression/data-compression.md)（数据压缩）

+ [对表或索引启用压缩](../../relational-databases/data-compression/enable-compression-on-a-table-or-index.md)

+ [列存储索引指南](../../relational-databases/indexes/columnstore-indexes-overview.md)

### <a name="memory-optimized-tables"></a>内存优化表

如今，对于新式计算机来说，内存已不再是一个问题。 随着硬件规格的不断提高，获取性价比高的 RAM 也变得相对容易。 但同时，数据的生成比以往更快，且必须以低延迟处理数据。

内存优化表代表了一种解决方案，其中他们利用高级计算机中可用的大内存来处理大数据问题。 内存优化表主要位于内存中，以便在内存中读取和写入数据。 为保证持续性，该表的第二个副本保存在磁盘上，且仅在数据库恢复期间可读取磁盘数据。

如果需要频繁地对表进行读写操作，内存优化表可帮助实现高可伸缩性和低延迟。  在恢复匹配方案中，使用内存优化表时，可以从数据库中读取所有的恢复功能，并将其存储在主内存中，以便与新的作业空缺相匹配。 这大大减少了磁盘 IO。

通过在将预测从多个并发批写回到数据库的过程中使用内存优化表，可实现更高的性能提升。 在 SQL Server 上使用内存优化表可实现对表的读写操作的低延迟。

在开发过程中，体验也是无缝的。 在创建数据库的同时创建了持久的内存优化表。 因此，无论数据存储在何处，开发过程都使用相同的工作流。

### <a name="processor"></a>处理器

SQL Server 可通过使用计算机上的可用核心并行执行任务；可用的核心越多，性能就越好。 尽管增加核心数可能对 IO 约束操作不会带来帮助，但如果 CPU 速度越快且核心越多，则可以让 CPU 约束算法受益。

由于服务器通常由多个用户同时使用，因此数据库管理员必须确定支持峰值工作负载计算所需的理想核心数。

### <a name="resource-governance"></a>资源调控

在支持 Resource Governor 的版本中，可使用资源池来指定为某些工作负载分配一定数量的 CPU。 此外，还可以管理分配给特定工作负载的内存量。

借助 SQL Server 中的资源调控，可以集中监视和控制 SQL Server 和 R 使用的各种资源。例如，可以为数据库引擎分配一半的可用内存，以确保即使工作负载暂时变大，核心服务也始终可以运行。

外部脚本的内存消耗默认值限制为 SQL Server 本身可用的总内存的 20%。 默认情况下应用此限制，以确保长期运行的 R 作业不会严重影响所有依赖数据库服务器的任务。 但是，数据库管理员可以更改这些限制。 在许多情况下，20% 的限制不足以支持大量机器学习工作负载。

支持的配置选项为“MAX_CPU_PERCENT”、“MAX_MEMORY_PERCENT”和“MAX_PROCESSES”    。 若要查看当前设置，请使用以下语句：`SELECT * FROM sys.resource_governor_external_resource_pools`

-  如果服务器主要用于 R Services，则将 MAX_CPU_PERCENT 提高到 40% 或 60% 可能会有所帮助。

-  如果多个 R 会话必须同时使用同一服务器，则这三个设置都应增加。

若要更改已分配的资源值，请使用 T-SQL 语句。

+ 此语句将内存使用量设置为 40%：`ALTER EXTERNAL RESOURCE POOL [default] WITH (MAX_MEMORY_PERCENT = 40)`

+ 此语句设置所有三个可配置值：`ALTER EXTERNAL RESOURCE POOL [default] WITH (MAX_CPU_PERCENT = 40, MAX_MEMORY_PERCENT = 50, MAX_PROCESSES = 20)`

+ 如果更改了内存、CPU 或最大进程设置，且希望立即应用这些设置，请运行以下语句：`ALTER RESOURCE GOVERNOR RECONFIGURE`

## <a name="soft-numa-hardware-numa-and-cpu-affinity"></a>Soft-NUMA、硬件 NUMA 和 CPU 相关性

将 SQL Server 用作计算上下文时，有时可以通过优化与 NUMA 和处理器相关性相关的设置来获得更好的性能。 

具有_硬件 NUMA_ 的系统包含多条系统总线，每条系统总线为一小组处理器提供服务。 每个 CPU 都可以通过一致的方式访问与其他组关联的内存。 每个组称为一个“NUMA 节点”。 如果具有硬件 NUMA，则它可能会配置为使用交错内存而不使用 NUMA。 在这种情况下，Windows 和 SQL Server 都不会将其识别为 NUMA。 

可运行以下查询来查找可用于 SQL Server 的内存节点数：

```sql
SELECT DISTINCT memory_node_id
FROM sys.dm_os_memory_clerks
```

如果查询返回单个内存节点（节点 0），则表示没有硬件 NUMA，或者该硬件已配置为交错硬件（非 NUMA）。 如果仅有 4 个或更少的 CPU，或者至少有一个节点只有一个 CPU，则 SQL Server 也会忽略硬件 NUMA。

如果计算机有多个处理器，但没有硬件 NUMA，则还可以使用 [Soft-NUMA](../../database-engine/configure-windows/soft-numa-sql-server.md) 将 CPU 细分为更小的组。  在 SQL Server 2016 和 SQL Server 2017 中，启动 SQL Server 服务时会自动启用 Soft-NUMA 功能。

启用 Soft-NUMA 后，SQL Server 会自动管理节点；但是，若要针对特定工作负载进行优化，可以禁用软关联并手动配置 soft NUMA 节点的 CPU 相关性  。 这样，就可以更好地控制将哪些工作负载分配给哪些节点，尤其是在使用支持资源调控的 SQL Server 版本时。 通过指定 CPU 相关性并使资源池与 CPU 组对齐，可以减少延迟，并确保相关进程在同一 NUMA 节点内执行。

配置 Soft-NUMA 和 CPU 相关性以支持 R 工作负载的整个过程如下所示：

1. 启用 Soft-NUMA（如果可用）
2. 定义处理器相关性
3. 使用 [Resource Governor](../administration/resource-governor.md) 为外部进程创建资源池
4. 将[工作负载组](../../relational-databases/resource-governor/resource-governor-workload-group.md)分配给特定的地缘组

有关详细信息（包括示例代码），请参阅此教程：[SQL 优化提示和技巧 (Ke Huang)](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

其他资源： 

+ [SQL Server 中的 Soft-NUMA](../../database-engine/configure-windows/soft-numa-sql-server.md)
    
    如何将 Soft-NUMA 节点映射到 CPU

## <a name="task-specific-optimizations"></a>特定于任务的优化

本节总结了在这些案例研究和其他测试中采用的用于优化特定机器学习工作负载的方法。 常见的工作负载包括模型定型、特征提取和特征工程，以及用于评分的各种方案：单行、小型批和大型批。

### <a name="feature-engineering"></a>特性工程

R 的一个难点是它通常在单个 CPU 上进行处理。 这是许多任务（尤其是特征工程）的主要性能瓶颈。 在恢复匹配解决方案中，仅特征工程任务一项就创建了 2,500 个必须与原始的 100 个特征相结合的跨产品特征。 如果所有内容都在单个 CPU 上完成，则此任务将花费大量时间。

有多种方法可以提高特征工程的性能。 可以优化 R 代码并在建模过程中进行特征提取，也可以将特征工程进程移到 SQL 中。

- 使用 R。定义一个函数，然后在定型期间将其作为参数传递给 [rxTransform](/r-server/r-reference/revoscaler/rxtransform)。 如果模型支持并行处理，则可以使用多个 CPU 处理特征工程任务。 使用此方法，数据科学团队发现在评分时间方面性能提高了 16%。 但是，此方法需要支持并行化的模型以及可使用并行计划执行的查询。

- 将 R 与 SQL 计算上下文结合使用。 在具有可用于执行分隔批的隔离资源的多处理器环境中，可通过隔离用于每个批处理的 SQL 查询，从表中提取数据并将数据约束在同一工作负载组上，从而提高效率。 用于隔离批的方法包括分区，以及使用 PowerShell 并行执行单独的查询。

- 临时并行执行：在 SQL Server 计算上下文中，如果可能且如果发现该选项更有效，则可以依靠 SQL 数据库引擎强制执行并行执行。

- 在单独的特征化进程中使用 T-SQL。 使用 SQL 预计算特征数据通常更快。

### <a name="prediction-scoring-in-parallel"></a>并行预测（评分）

SQL Server 的优势之一是它能够并行处理大量的行。 此优势在评分方面最为明显。 通常情况下，模型不需要访问所有数据即可进行评分，因此，可以对输入数据进行分区，每个工作负载组处理一项任务。

此外，还可以将输入数据作为单个查询发送，然后 SQL Server 会分析该查询。 如果可以为输入数据创建并行查询计划，则它会自动将分配给节点的数据分区，并同时执行所需的联接和聚合。

如果有兴趣了解如何定义用于评分的存储过程的详细信息，请参阅 [GitHub](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/SQLOptimizationTips-Resume-Matching/SQLR) 上的示例项目，并查找文件“step5_score_for_matching.sql”。 示例脚本还会跟踪查询的开始和结束时间，并将时间写入 SQL 控制台，以便评估性能。

### <a name="concurrent-scoring-using-resource-groups"></a>使用资源组的并发评分

若要扩大评分问题，一种很好的做法是采用可将数百万项分为多个批的 map-reduce 方法。 然后，同时执行多个评分作业。 在此框架中，这些批在不同的 CPU 集上进行处理，并将结果收集和写回到数据库。

这是在恢复匹配方案中使用的方法；但是，SQL Server 中的资源调控对于实现此方法至关重要。 通过为外部脚本作业设置工作负载组，可以将 R 评分作业路由到不同的处理器组并实现更快的吞吐量。

资源调控还可以帮助分配和划分服务器上的可用资源（CPU 和内存），以最大程度地减少工作负载争用。 可设置分类器函数来区分不同类型的 R 作业：例如，可以决定从应用程序调用的评分始终处于高优先级，而重新定型作业则处于低优先级。 此资源隔离可能会缩短执行时间，并提供更可预测的性能。

### <a name="concurrent-scoring-using-powershell"></a>使用 PowerShell 的并发评分

如果决定自行对数据进行分区，则可以使用 PowerShell 脚本执行多个并发评分任务。 若要执行此操作，请使用 Invoke-SqlCmd cmdlet，并行启动评分任务。

在恢复匹配方案中，并发设计如下：

- 20 个处理器分为四组，每组五个 CPU。 每组 CPU 都位于同一 NUMA 节点上。

- 并发批的最大数量设置为 8。

- 每个工作负载组必须处理两个评分任务。 一旦一项任务完成数据读取并开始评分，另一项任务就可以开始从数据库中读取数据。

若要查看此方案的 PowerShell 脚本，请在 [Github 项目](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/SQLOptimizationTips-Resume-Matching)中打开文件 experiment.ps1。

### <a name="storing-models-for-prediction"></a>存储模型以进行预测

当定型和评估已完成且已选择了最佳模型后，建议将模型存储在数据库中，以便进行预测。 从数据库加载预计算的模型以进行预测是高效的，因为在 R 和数据库之间移动时，SQL Server 机器学习会使用特殊的序列化算法来存储和加载模型。

> [!TIP]
> 在 SQL Server 2017 中，即使服务器上未安装 R，也可以使用 PREDICT 函数执行评分。 RevoScaleR 包支持的模型类型有限。

但是，根据所使用的算法，某些模型可能会非常大，尤其是在对大型数据集进行定型时。 例如，lm 或 glm 等算法会生成大量汇总数据和规则   。 由于可以存储在 varbinary 列中的模型大小受限，因此，建议在将模型存储到数据库中进行生产之前，请删除模型中不必要的项目。

## <a name="articles-in-this-series"></a>本系列文章

[R 的性能优化 - 简介](../r/sql-server-r-services-performance-tuning.md)

[R 的性能优化 - SQL Server 配置](../r/sql-server-configuration-r-services.md)

[R 的性能优化 - R 代码和数据优化](../r/r-and-data-optimization-r-services.md)

[性能优化 - 案例研究结果](../r/performance-case-study-r-services.md)