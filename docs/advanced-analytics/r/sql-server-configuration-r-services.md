---
title: SQL Server 配置 (R Services) 的 SQL Server 机器学习服务
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/29/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: efeb55e9fb3a241978fd31944f662250b0f36d48
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962449"
---
# <a name="sql-server-configuration-for-use-with-r"></a>与 R 一起使用的 SQL Server 配置
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文是第二个序列中的说明基于两个案例研究的 R services 性能优化。  本文提供有关用于运行 SQL Server R Services 的计算机的硬件和网络配置指南。 它还包含有关如何配置 SQL Server 实例、 数据库或在解决方案中使用的表的信息。 使用 SQL Server 中的 NUMA 的界线之间的硬件和数据库优化，因为第三个部分讨论了详细的 CPU 关联和资源调控。

> [!TIP]
> 如果您是刚接触 SQL Server，我们强烈建议您也查看 SQL Server 性能优化指南：[监视和调整适用于性能](https://docs.microsoft.com/sql/relational-databases/performance/monitor-and-tune-for-performance)。

## <a name="hardware-optimization"></a>硬件优化

服务器计算机的优化非常重要的确保您具有资源来运行外部脚本。 当资源有限时，可能会看到以下症状：

- 延迟或取消，以确定其他数据库操作的优先级作业执行
- 已超出错误"配额"导致 R 脚本终止而未完成
- 数据加载到 R 内存被截断为不完整的结果

### <a name="memory"></a>内存

计算机上的可用内存量可能会对高级分析算法的性能造成很大的影响。 使用 SQL 计算上下文时，内存不足可能会影响并行度。 此外，还会影响可处理的区块大小（每个读取操作使用的行数），以及可支持的并发会话数。

强烈建议至少配置 32gb 内存。 如果有多个 32 gb 的可用空间，可以配置 SQL 数据源，可以使用更多的行中每个读取操作来提高性能。

此外可以管理的实例使用的内存。 默认情况下，SQL Server 将优先于外部脚本进程分配内存时。 在 R Services 的默认安装中，仅有 20%的可用内存分配给。

通常这不是足够的数据科学任务，但要在不影响虚拟 SQL server 的内存。 应尝试并优化数据库引擎、 相关的服务和外部脚本，并了解的最佳配置各不相同情况之间的内存分配。

用于 resume 匹配模型中，外部脚本使用了大量，并且没有任何其他数据库引擎服务运行;因此，分配给外部脚本的资源已增加到了 70%，这是脚本性能的最佳配置。

### <a name="power-options"></a>电源选项

在 Windows 操作系统，**高性能**应使用电源选项。 使用不同的电源设置会导致性能下降或不一致时使用的 SQL Server。

### <a name="disk-io"></a>磁盘 IO

训练和预测使用 R Services 作业原生受到 IO 绑定，并依赖于磁盘上存储数据库的速度。 可能有助于更快的驱动器，如固态硬盘 (SSD)。

磁盘 IO 还会受到访问磁盘的其他应用程序的影响：例如，其他客户端对数据库执行的读取操作。 磁盘 IO 性能还会受到使用的文件系统中的设置（例如，文件系统使用的块大小）影响。

如果提供多个驱动器，则 SQL Server 数据库引擎的请求以便不同的驱动器上的数据库没有达到与位于同一磁盘的存储请求存储在数据库中的数据。

在训练期间运行使用多个迭代的 RevoScaleR 分析函数时，磁盘 IO 也可能会对性能造成很大的影响。 例如， `rxLogit`， `rxDTree`， `rxDForest`，和`rxBTrees`所有使用多个迭代。 SQL Server 数据源时，这些算法使用优化来捕获数据的临时文件。 会话完成后，会自动清理这些文件。 具有读/写操作的高性能磁盘可以大幅改善这些算法所经过的总体时间。

> [!NOTE]
> 早期版本的 R Services 要求在 Windows 操作系统上的 8.3 文件名支持。 Service Pack 1 后解除了这一限制。 但是，可以使用 fsutil.exe 确定驱动器是否支持 8.3 文件名，或如果未启用支持。

### <a name="paging-file"></a>页面文件

Windows 操作系统使用分页文件来管理故障转储和存储虚拟内存页面。 如果你发现分页过度，请考虑增大计算机上的物理内存。 尽管分配更多的物理内存不会消除分页，但确实可以减少分页的需要。

存储页面文件的磁盘的速度也会影响性能。 将页面文件存储在 SSD 中或者在多个 SSD 上使用多个页面文件可以提高性能。

有关大小调整页面文件的信息，请参阅[如何确定 64 位版本的 Windows 的合适页面文件大小](https://support.microsoft.com/kb/2860880)。

## <a name="optimizations-at-instance-or-database-level"></a>在实例或数据库级别的优化

SQL Server 实例的优化是高效地执行外部脚本的关键。

> [!NOTE]
> 最佳的设置而异的大小和类型的数据，您将用于评分或训练模型的列数。
> 
> 你可以查看最后一篇文章中的特定优化的结果：[性能优化-案例研究结果](../../advanced-analytics/r/performance-case-study-r-services.md)
> 
> 有关示例脚本，请参阅单独[GitHub 存储库](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning)。

### <a name="table-compression"></a>表压缩

使用压缩或列式数据存储，通常可以提高 IO 性能。 通常情况下，在多个列在表中，以便通过使用列存储压缩数据时可以采取这种重复利用经常重复数据。

列存储可能不会那样高效，如果有大量插入到表中，但如果数据是静态的或不经常更改是一个不错的选择。 如果纵栏表存储不适用，对主表中的行启用压缩可以改善 IO。

有关详细信息，请参阅以下文档：

+ [数据压缩](../../relational-databases/data-compression/data-compression.md)

+ [对表或索引启用压缩功能](../../relational-databases/data-compression/enable-compression-on-a-table-or-index.md)

+ [列存储索引指南](../../relational-databases/indexes/columnstore-indexes-overview.md)

### <a name="memory-optimized-tables"></a>内存优化表

如今，内存不再是现代计算机问题。 在硬件规格继续改进，它是相对较容易地得到正确值 RAM。 但是，在同一时间，比以往，更快地生成数据并且必须较低的延迟处理数据。

内存优化表表示一种解决方案，他们会利用较大的内存可用来解决这个问题的大数据的高级计算机中。 内存优化表主要驻留在内存中，以便从读取数据并将其写入到内存中。 有关持续性，在磁盘上维护表的第二个副本和数据只能从磁盘中读取在数据库恢复期间。

如果需要读取和频繁写入到表，内存优化表可以帮助提供高可伸缩性和低延迟。  在继续匹配方案中，使用的内存优化表允许我们能够从数据库读取所有恢复功能，并将其存储在主内存中，以与新职位空缺相匹配。 这大大减少了磁盘 IO。

使用内存优化表的过程中向数据库返回写入的预测，从多个并发批处理通过进一步提高性能。 SQL Server 上的内存优化表使用启用表读取和写入较低的延迟。

在开发过程中还是无缝体验。 创建数据库时创建持久内存优化表。 因此，开发使用相同的工作流而不考虑数据存储位置。

### <a name="processor"></a>处理器

SQL Server 可以通过使用计算机; 上的可用内核并行执行任务可用的核心越多，性能便越高。 尽管增加内核可能无助于 IO 绑定操作，CPU 绑定算法权益与多个核心更快的 Cpu。

因为服务器通常同时使用多个用户中，数据库管理员必须确定支持峰值工作负荷计算所需的内核的理想数目。

### <a name="resource-governance"></a>资源调控

在支持资源调控器的版本，可以使用资源池来指定某些工作负荷分配一定数量的 Cpu。 此外可以管理分配给特定的工作负荷的内存量。

SQL Server 中的资源调控可让您集中监视和使用 SQL server 和的各种资源的控制例如，可能会分配数据库引擎，以确保服务始终可以忽略暂时性较重的工作负荷而运行该核心一半的可用内存。

限制为适用于 SQL Server 本身的总内存的 20%的内存使用情况外部脚本的默认值。 若要确保依赖于数据库服务器的所有任务不会严重都影响的长时间运行的 R 作业的默认情况下才应用此限制。 但是，数据库管理员可以更改这些限制。 在许多情况下，20%限制不足够用来支持严重机器学习工作负荷。

支持的配置选项都**MAX_CPU_PERCENT**， **MAX_MEMORY_PERCENT**，并**MAX_PROCESSES**。 若要查看当前设置，请使用此语句： `SELECT * FROM sys.resource_governor_external_resource_pools`

-  如果服务器主要用于 R Services，它可能有助于 MAX_CPU_PERCENT 增大到 40%或 60%。

-  如果许多 R 会话必须在同一时间使用同一台服务器，则应增加所有三个设置。

若要更改分配的资源值，请使用 T-SQL 的语句。

+ 此语句将设置为 40%的内存使用情况： `ALTER EXTERNAL RESOURCE POOL [default] WITH (MAX_MEMORY_PERCENT = 40)`

+ 此语句将设置所有三个可配置的值： `ALTER EXTERNAL RESOURCE POOL [default] WITH (MAX_CPU_PERCENT = 40, MAX_MEMORY_PERCENT = 50, MAX_PROCESSES = 20)`

+ 如果更改内存、 CPU 或最大进程设置，然后想要立即应用设置，运行此语句： `ALTER RESOURCE GOVERNOR RECONFIGURE`

## <a name="soft-numa-hardware-numa-and-cpu-affinity"></a>软件 NUMA、 硬件 NUMA 和 CPU 关联

当使用 SQL Server 作为计算上下文，有时可以通过优化与 NUMA 和处理器绑定相关的设置来获得更好的性能。 

具有系统_硬件 NUMA_具有多个系统总线，每个为一小组处理器。 每个 CPU 都可以访问一致的方式与其他组相关联的内存。 每个组称为一个“NUMA 节点”。 如果具有硬件 NUMA，则它可能会配置为使用交错内存而不使用 NUMA。 在这种情况下，Windows，因此 SQL Server 将无法识别它为 NUMA。 

可以运行以下查询以查找 SQL Server 的可用内存节点的数目：

```sql
SELECT DISTINCT memory_node_id
FROM sys.dm_os_memory_clerks
```

如果查询返回一个内存节点 （节点 0），没有硬件 NUMA，或者该硬件配置为交错 (非 NUMA)。 SQL Server 还会忽略的硬件 NUMA 时有四个或更少的 Cpu，或者如果至少有一个节点上只有一个 CPU。

如果你的计算机具有多个处理器，但没有硬件 NUMA，则可以使用[SOFT-NUMA](https://docs.microsoft.com/sql/database-engine/configure-windows/soft-numa-sql-server)若要将 Cpu 细分为更小的组。  在 SQL Server 2016 和 SQL Server 2017 中，启动 SQL Server 服务时，会自动启用软件 NUMA 功能。

当启用软件 NUMA 时，SQL Server 自动节点会为你管理;但是，若要针对特定工作负荷进行优化，可以禁用_软关联_并手动配置的软 NUMA 节点的 CPU 关联。 这可以提供更好地控制哪些工作负荷分配给哪些节点，尤其是当你使用支持资源调控的 SQL Server 的版本。 通过指定 CPU 关联并对齐具有的 Cpu 组的资源池，可以减少延迟，并确保在同一个 NUMA 节点中执行相关的过程。

配置软件 NUMA 和 CPU 关联以支持 R 工作负荷的整体过程如下所示：

1. 如果可用，请启用软件 NUMA
2. 定义处理器关联
3. 创建外部进程，使用的资源池[资源调控器](../r/resource-governance-for-r-services.md)
4. 将分配[工作负荷组](../../relational-databases/resource-governor/resource-governor-workload-group.md)到特定的地缘组

有关详细信息，包括示例代码中，请参阅本教程中：[SQL 优化提示和技巧 (Ke Huang)](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

**其他资源：**

+ [SQL Server 中的软件 NUMA](https://docs.microsoft.com/sql/database-engine/configure-windows/soft-numa-sql-server)
    
    如何将软件 NUMA 节点映射到 Cpu

## <a name="task-specific-optimizations"></a>特定于任务的优化

本部分总结了方法采用了这些案例研究、 中和在其他测试中，有关优化特定机器学习工作负荷。 常见的工作负荷包括模型训练，特征提取和特征工程和评分的各种方案： 的单行、 小型批处理和大型批处理。

### <a name="feature-engineering"></a>特征工程

使用 R 的一个痛点是，通常处理单个 CPU 上。 这是主要的性能瓶颈的许多任务，尤其是特征工程。 在继续匹配解决方案中，特征工程任务单独创建 2,500 必须与原始 100 功能结合使用的跨产品功能。 如果所有内容在单个 CPU 中执行此操作，此任务将花费很长时间。

有多种方法可以改善特征工程的性能。 可以优化 R 代码，并保留特征提取在建模过程中，或将功能工程过程移动到 SQL。

- 使用。定义一个函数，然后将其作为参数传递[rxTransform](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxtransform)在定型期间。 如果模型支持并行处理，可以使用多个 Cpu 处理特征工程任务。 使用此方法时，数据科学团队观察到 16%性能评分时间方面的改进。 但是，此方法要求支持并行化和可以使用并行计划执行的查询的模型。

- 使用 R 使用 SQL 计算上下文。 在多处理器环境中使用单独的批执行的独立资源，可以隔离每个批，用于从表中提取数据并将相同的工作负荷组上的数据限制的 SQL 查询，从而实现更高的效率。 方法用于将隔离到批处理包含分区，并使用 PowerShell 的并行执行单独的查询。

- 即席并行执行：在 SQL Server 计算上下文中，您可以依赖 SQL 数据库引擎，以强制实施并行执行如有可能，如果找到该选项提高工作效率。

- 在单独的特征化的进程中使用 T-SQL。 Precomputing 使用 SQL 功能数据通常是速度更快。

### <a name="prediction-scoring-in-parallel"></a>并行 （评分） 的预测

SQL Server 的优点之一是能够处理大量并行中的行。 这是这种优势因此标记为评分。 通常模型不需要访问所有数据进行评分，因此你可以使用一个任务处理每个工作负荷组分区输入的数据。

您还可以发送的输入的数据作为单个查询和 SQL Server 然后分析该查询。 如果并行查询计划可以创建输入数据，它会自动分配给节点的数据进行分区和并行以及执行所需的联接和聚合。

如果您有兴趣如何定义计分中使用的存储的过程的详细信息，请参阅示例项目上[GitHub](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/SQLOptimizationTips/SQLR)和查找文件"step5_score_for_matching.sql"。 此示例脚本还跟踪查询开始和结束时间以及写入到 SQL 控制台的时间，以便您可以评估性能。

### <a name="concurrent-scoring-using-resource-groups"></a>使用资源组并发评分

若要扩展评分的问题，较好的做法是采用在其中数以百万计的项被划分到多个批次的 map-reduce 方法。 然后，同时执行多个评分作业。 在这种框架，批处理是处理不同的 CPU 集和结果收集，并将其写回到数据库。

这是方案中使用的恢复匹配; 方法但是，在 SQL Server 中的资源调控对于实现这种方法至关重要。 通过设置外部脚本作业的工作负荷组，可以将路由到不同的处理器组评分作业 R 并实现更快的吞吐量。

资源调控还可以帮助分配划分 （CPU 和内存），以最大程度减少工作负荷竞赛的服务器上的可用资源。 可以设置的分类器函数来区分不同类型的 R 作业： 例如，你可能会决定，评分调用从应用程序始终优先，而重新训练作业具有较低的优先级。 此资源隔离可能可以改进执行时间，并提供更可预测的性能。

### <a name="concurrent-scoring-using-powershell"></a>使用 PowerShell 并发评分

如果你决定自行分区数据，可以使用 PowerShell 脚本来执行多个并发的评分任务。 若要执行此操作，使用 Invoke-sqlcmd cmdlet，并启动并行中的评分任务。

在继续匹配方案中，并发设计，如下所示：

- 20 处理器划分为五个 Cpu 的四个组。 Cpu 的每个组位于同一个 NUMA 节点上。

- 并发批处理的最大数目设置为 8。

- 每个工作负荷组必须处理两个评分任务。 只要一个任务完成读取数据并启动评分，可以开始其他任务从数据库读取数据。

若要查看此方案中的 PowerShell 脚本，请打开在文件 experiment.ps1 [Github 项目](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/SQLOptimizationTips)。

### <a name="storing-models-for-prediction"></a>存储模型进行预测

在训练和评估完成和你选择最佳模型，我们建议在数据库中存储模型，以便它可用于预测。 从该预测的数据库中加载预先计算的模型是高效，因为 SQL Server 机器学习使用特殊的序列化的算法来存储和 R 和数据库之间移动时加载模型。

> [!TIP]
> 在 SQL Server 2017 中，您可以使用 PREDICT 函数执行评分即使在服务器上未安装 R。 RevoScaleR 包中支持有限的模型类型。

但是，具体取决于所用的算法，某些模型可能会很大，尤其是在上一个大型数据集进行训练。 例如，如算法**lm**或**glm**生成大量以及规则的摘要数据。 由于模型可以存储在 varbinary 列的大小有限制，我们建议您将模型存储在数据库中为生产环境之前消除不必要的项目，从模型。

## <a name="articles-in-this-series"></a>本系列文章

[性能优化适用于 R 的简介](../r/sql-server-r-services-performance-tuning.md)

[R 的 SQL Server 配置的性能优化](../r/sql-server-configuration-r-services.md)

[R-R 的性能优化的代码和数据优化](../r/r-and-data-optimization-r-services.md)

[性能优化-案例研究结果](../r/performance-case-study-r-services.md)
