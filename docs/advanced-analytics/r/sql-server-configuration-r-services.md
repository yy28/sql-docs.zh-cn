---
title: "SQL Server 配置 (R Services) | Microsoft Docs"
ms.custom: 
ms.date: 07/26/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4b08969f-b90b-46b3-98e7-0bf7734833fc
caps.latest.revision: "13"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b65eb600060a5d7e12d3095d145a23f5b8b3290b
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/20/2017
---
# <a name="sql-server-configuration-for-use-with-r"></a>与 R 一起使用的 SQL Server 配置

本文是介绍 R 服务基于两个案例研究的性能优化的一系列中第二个。  本文提供了有关用于运行 SQL Server R Services 的计算机的硬件和网络配置的指导。 它还包含有关如何配置 SQL Server 实例、 数据库或表的解决方案中使用的信息。 因为使用的 SQL Server 中的 NUMA 模糊硬件和数据库优化之间的行，第三个部分将讨论详细的 CPU 关联和资源管理。

> [!TIP]
> 如果你不熟悉 SQL Server，我们强烈建议你也查看 SQL Server 性能优化指南：[监视器和性能的优化](https://docs.microsoft.com/sql/relational-databases/performance/monitor-and-tune-for-performance)。

## <a name="hardware-optimization"></a>硬件优化

优化的服务器计算机对于确保你具有资源来运行外部脚本至关重要。 有限资源时，可能会看到这些症状：

- 作业执行已延迟或已取消为优先处理其他数据库操作
- 已超出的错误"配额"导致 R 脚本终止而未完成
- 数据加载到 R 内存截断，为不完整的结果

### <a name="memory"></a>内存

计算机上的可用内存量可能会对高级分析算法的性能造成很大的影响。 使用 SQL 计算上下文时，内存不足可能会影响并行的度。 此外，还会影响可处理的区块大小（每个读取操作使用的行数），以及可支持的并发会话数。

强烈建议至少为 32 GB。 如果你有多个 32 gb 可用空间，你可以配置要在每个读取操作中使用更多的行来提高性能的 SQL 数据源。

你还可以管理的实例使用的内存。 默认情况下，SQL Server 是它们优先于外部脚本进程分配内存时。 在默认安装的 R Services 中，仅有 20%的可用内存分配给。

通常这是不够的数据科学任务，但要在两者都不需要 SQL server 的内存。 应进行试验，以及优化数据库引擎、 相关的服务和外部脚本，并了解的最佳的配置而异情况之间的内存分配。

对于恢复匹配模型中，外部脚本使用是大量，没有任何其他数据库引擎服务运行;因此，分配给外部脚本的资源已增加到 70%，这是脚本性能的最佳配置。

### <a name="power-options"></a>电源选项

在 Windows 操作系统，**高性能**应使用电源选项。 使用不同的电源设置将降低或不一致的性能，使用 SQL Server 时。

### <a name="disk-io"></a>磁盘 IO

训练和预测使用 R Services 作业本质上是 IO 绑定，并依赖于磁盘上存储数据库的速度。 可帮助更快的驱动器，例如固态硬盘 (SSD)。

磁盘 IO 还会受到访问磁盘的其他应用程序的影响：例如，其他客户端对数据库执行的读取操作。 磁盘 IO 性能还会受到使用的文件系统中的设置（例如，文件系统使用的块大小）影响。

如果多个驱动器可用，因此，请求为数据库引擎的 SQL Server 与不同的驱动器上的数据库不命中所在磁盘的存储请求存储在数据库中的数据。

在训练期间运行使用多个迭代的 RevoScaleR 分析函数时，磁盘 IO 也可能会对性能造成很大的影响。 例如， `rxLogit`， `rxDTree`， `rxDForest`，和`rxBTrees`所有使用多个迭代。 SQL Server 数据源时，这些算法使用进行优化以捕获数据的临时文件。 会话完成后，会自动清理这些文件。 具有读/写操作的高性能磁盘可以显著提高这些算法总体经历的时间。

> [!NOTE]
> 早期版本的 R Services 要求在 Windows 操作系统上的 8.3 文件名支持。 在 Service Pack 1 后已解除此限制。 但是，你可以使用 fsutil.exe 来确定驱动器是否支持 8.3 文件名，或如果不启用支持。

### <a name="paging-file"></a>页面文件

Windows 操作系统使用分页文件来管理故障转储和存储虚拟内存页面。 如果你发现分页过度，请考虑增大计算机上的物理内存。 尽管分配更多的物理内存不会消除分页，但确实可以减少分页的需要。

存储页面文件的磁盘的速度也会影响性能。 将页面文件存储在 SSD 中或者在多个 SSD 上使用多个页面文件可以提高性能。

有关大小调整页面文件的信息，请参阅[如何确定合适的页面文件大小为 64 位版本的 Windows](https://support.microsoft.com/kb/2860880)。

## <a name="optimizations-at-instance-or-database-level"></a>在实例或数据库级别的优化

SQL Server 实例的优化是高效地执行外部脚本的关键。

> [!NOTE]
> 最佳的设置而异的大小和类型的数据，你将用于评分或定型模型的列数。
> 
> 你可以查看的最终的文章中的特定优化结果：[性能优化的案例研究结果](../../advanced-analytics/r/performance-case-study-r-services.md)
> 
> 示例脚本，请参阅单独[GitHub 存储库](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/PerfTuning)。

### <a name="table-compression"></a>表压缩

使用压缩或纵栏表数据存储区，通常可以提高 IO 性能。 通常情况下，在表中的多个列中以便通过使用列存储压缩数据时可以采取的这些重复的优点通常重复数据。

列存储可能不会尽可能高效，如果有大量插入到表中，但如果数据是静态的或只有很少更改是一个不错的选择。 如果纵栏表存储不适用，对主表中的行启用压缩可以改善 IO。

有关详细信息，请参阅以下文档：

+ [数据压缩](../../relational-databases/data-compression/data-compression.md)

+ [对表或索引启用压缩功能](../../relational-databases/data-compression/enable-compression-on-a-table-or-index.md)

+ [列存储索引指南](../../relational-databases/indexes/columnstore-indexes-overview.md)

### <a name="memory-optimized-tables"></a>内存优化表

现今，内存不再是现代的计算机的问题。 随着硬件规格不断改进，它是相对较容易到达的正确值的 RAM。 但是，在相同的时间，比以往，更快地生成数据并且必须处理数据较低的延迟。

内存优化表表示一种解决方案，他们会利用较大的内存的高级计算机来处理大数据的问题。 内存优化表主要驻留在内存中，以便从读取数据并将其写入到内存中。 为持久性，在磁盘上维护表的第二个副本和数据仅从磁盘中读取在数据库恢复期间。

如果你需要从读取和频繁写入到的表，内存优化表可帮助高可伸缩性和低延迟。  在恢复匹配方案中，内存优化表允许使用我们要从数据库读取所有恢复功能，并将其存储在主内存中，以便与新职位空缺进行匹配。 这显著减少磁盘 IO。

通过使用内存优化表添加到数据库重新编写预测，多个并发批次中的过程中来实现更多的性能提升。 SQL Server 上的内存优化表使用上表读取和写入启用低延迟。

在开发过程中还是无缝体验。 创建该数据库的同时创建持久内存优化表。 因此，开发使用同一工作流，而不考虑数据存储位置。

### <a name="processor"></a>处理器

SQL Server 可以通过使用计算机; 上的可用内核数在并行执行任务更多内核可用，性能就越高。 有关绑定的 IO 操作可能无法帮助增加的内核数，而 CPU 从具有许多内核更快的 Cpu 绑定算法权益。

因为将使用的服务器通常由多个用户同时，数据库管理员必须确定理想的支持高峰工作负荷计算所需的内核数。

### <a name="resource-governance"></a>资源调控

在支持资源调控器的版本，你可以使用资源池指定某些工作负荷分配一定数量的 Cpu。 你还可以管理分配给特定的工作负荷的内存量。

SQL Server 中的资源调控允许您集中监视和控制 SQL Server 以及。 使用的各种资源例如，你可能会分配对于数据库引擎，以确保该服务可以始终运行而不考虑暂时性较重的工作负荷的核心一半的可用内存。

限制为 20%的适用于 SQL Server 本身的总内存的内存使用情况外部脚本的默认值。 默认情况下，以确保依赖于数据库服务器的所有任务不会严重都影响通过长时间运行的 R 作业才应用此限制。 但是，数据库管理员可以更改这些限制。 在许多情况下，20%限制不足够用来支持严重机器学习工作负荷。

支持的配置选项是**MAX_CPU_PERCENT**， **MAX_MEMORY_PERCENT**，和**MAX_PROCESSES**。 若要查看当前设置，请使用以下语句：`SELECT * FROM sys.resource_governor_external_resource_pools`

-  如果服务器主要用于 R Services，它可能会很有用，以将 MAX_CPU_PERCENT 增加到 40%或 60%。

-  如果多个 R 会话必须在同一时间使用同一台服务器，则应增加所有三个设置。

若要更改已分配的资源值，请使用 T-SQL 的语句。

+ 此语句设置为 40%的内存使用率：`ALTER EXTERNAL RESOURCE POOL [default] WITH (MAX_MEMORY_PERCENT = 40)`

+ 此语句将设置所有三个可配置值：`ALTER EXTERNAL RESOURCE POOL [default] WITH (MAX_CPU_PERCENT = 40, MAX_MEMORY_PERCENT = 50, MAX_PROCESSES = 20)`

+ 如果你改变内存、 CPU 或最大进程设置，然后想要立即应用设置，运行此语句：`ALTER RESOURCE GOVERNOR RECONFIGURE`

## <a name="soft-numa-hardware-numa-and-cpu-affinity"></a>软件 NUMA、 硬件 NUMA 和 CPU 相关性

当使用 SQL Server 作为计算上下文，你有时可以通过优化与 NUMA 和处理器关联相关的设置能获得更好的性能。 

具有系统_硬件 NUMA_有多个系统总线，每个为提供服务的一小部分的处理器。 每个 CPU 可以访问的一致的方式与其他组相关联的内存。 每个组称为一个“NUMA 节点”。 如果具有硬件 NUMA，则它可能会配置为使用交错内存而不使用 NUMA。 在这种情况下，Windows，因此 SQL Server 将不识别为 NUMA。 

你可以运行以下查询以找到可供 SQL Server 的内存节点的数目：

```SQL
SELECT DISTINCT memory_node_id
FROM sys.dm_os_memory_clerks
```

如果查询返回单个内存节点 （节点 0），则你还没有硬件 NUMA，或硬件配置为交错 (非 NUMA)。 SQL Server 还会忽略硬件 NUMA 时有四个或更少的 Cpu，或者如果至少一个节点拥有，只有一个 CPU。

如果你的计算机有多个处理器，但没有硬件 NUMA，也可以使用[SOFT-NUMA](https://docs.microsoft.com/sql/database-engine/configure-windows/soft-numa-sql-server)若要将 Cpu 细分为较小的组。  在 SQL Server 2016 和 SQL Server 自 2017 年中，启动 SQL Server 服务时，将自动启用软件 NUMA 功能。

SQL Server 启用 SOFT-NUMA 后，为你; 的节点自动管理但是，若要针对特定工作负荷进行优化，可以禁用_软关联_和手动配置 CPU 相关性，软的 NUMA 节点。 尤其是当你使用的版本的支持资源调控的 SQL Server，这可以为你提供更好地控制对其工作负荷分配到的节点。 通过指定 CPU 关联并对齐具有的 Cpu 的组的资源池，你可以减少延迟，并确保相关的进程在同一个 NUMA 节点内执行。

配置 SOFT-NUMA 和 CPU 相关性以支持 R 工作负荷的整个过程如下所示：

1. 如果可用，请启用软件 NUMA
2. 定义处理器关联
3. 创建外部进程，使用的资源池[资源调控器](../r/resource-governance-for-r-services.md)
4. 分配[工作负荷组](../../relational-databases/resource-governor/resource-governor-workload-group.md)到特定的地缘组

有关详细信息，包括示例代码，请参阅本教程： [SQL 优化提示和技巧 (Ke Huang)](https://gallery.cortanaintelligence.com/Tutorial/SQL-Server-Optimization-Tips-and-Tricks-for-Analytics-Services)

**其他资源：**

+ [SQL Server 中的软件 NUMA](https://docs.microsoft.com/sql/database-engine/configure-windows/soft-numa-sql-server)
    
    如何将软件 NUMA 节点映射到 Cpu

+ [自动 SOFT-NUMA： 它仅运行更快 （Bob 选区）](https://blogs.msdn.microsoft.com/bobsql/2016/06/03/sql-2016-it-just-runs-faster-automatic-soft-numa/)

   描述历史记录以及实现详细信息，使用较新的多核服务器上的性能。

## <a name="task-specific-optimizations"></a>特定于任务的优化

此部分总结了采用在这些案例研究，以及其他测试，以优化特定机器学习工作负荷中的方法。 常见的工作负荷包括模型定型、 提取特征和功能工程和评分的各种方案： 单行更行、 小批处理和大的批处理。

### <a name="feature-engineering"></a>特征工程

使用 R 的一个难点是，通常处理在单个 CPU 上。 这是主要性能瓶颈许多任务，尤其是功能工程部门。 在恢复匹配解决方案中，必须与原始 100 功能结合使用的 2,500 跨产品功能创建单独的功能工程任务。 当所有内容已在单个 CPU 上完成，此任务将花费很长时间。

有多种方法来提高的性能特征工程。 您可以优化 R 代码和保留功能提取在建模过程中，或将功能工程过程移入 SQL。

- 使用。定义一个函数，然后将其作为自变量传递[rxTransform](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxtransform)在培训期间。 如果模型支持并行处理，可以使用多个 Cpu 处理功能工程任务。 使用此方法，数据科学团队观察到 16%的性能改进在以下方面评分时间。 但是，此方法要求支持并行化和一个可以使用的并行计划执行的查询的模型。

- 使用 R 使用 SQL 计算上下文。 在多处理器环境与独立资源可用于执行单独的批处理文件中，你可以隔离每个批处理，用于从表中提取数据并约束上相同的工作负荷组的数据的 SQL 查询来实现更高的效率。 用于隔离所批次的方法包括分区，并使用 PowerShell 的并行执行单独的查询。

- 即席并行执行： SQL Server 计算上下文，你可以依赖于 SQL 数据库引擎，以强制执行尽可能并行执行和如果找到该选项使其更高效。

- 在单独的特征化的进程中使用 T-SQL。 Precomputing 使用 SQL 功能数据通常是更快。

### <a name="prediction-scoring-in-parallel"></a>（评分） 并行的预测

SQL 服务器的优势之一是它能够处理大量并行中的行。 无，这种优势因此标记如下所示评分。 通常模型不需要对所有数据的访问评分，因此你可以输入的数据中，分区与一个任务处理每个工作负荷组。

你还可以作为单个查询中，发送的输入的数据和 SQL Server 然后对查询进行分析。 如果输入数据，可以创建的并行查询计划，它会自动分配给节点的数据分区和并行以及执行所需的联接和聚合。

如果你有兴趣如何定义使用的存储的过程中评分的详细信息，请参阅示例项目上[GitHub](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/SQLOptimizationTips/SQLR)查找文件"step5_score_for_matching.sql"。 此示例脚本还跟踪查询开始和结束时间以及写入到 SQL 控制台的时间，以便您可以评估性能。

### <a name="concurrent-scoring-using-resource-groups"></a>使用资源组的并发评分

若要扩大评分的问题，很好的做法是采用在其中数以百万计的项划分为多个批的 map-reduce 方法。 然后，同时执行多个评分的作业。 在此框架中，批次不会处理对不同的 CPU 集，以及结果的收集和写回数据库。

这是方案中使用的恢复匹配; 方法但是，SQL Server 中的资源调控至关重要用于实现此方法。 通过设置外部脚本作业的工作负荷组，可以将路由到不同的处理器组计分作业的 R 并实现更快的生产率。

资源调控还可以帮助分配划分 （CPU 和内存），以最大程度减少工作负荷竞争的服务器上的可用资源。 你可以对分类器函数来区分不同类型的 R 作业设置，以便： 例如，你可能决定，评分从应用程序始终调用所需的优先级，时间再培训作业具有较低的优先级。 此资源隔离可能可以缩短执行时间，并提供更可预测的性能。

### <a name="concurrent-scoring-using-powershell"></a>使用 PowerShell 并发评分

如果你决定自行分区数据，你可以使用 PowerShell 脚本执行多个并发的评分任务。 若要执行此操作，使用 Invoke-sqlcmd cmdlet，并启动并行中的评分任务。

在恢复匹配方案中，并发设计，如下所示：

- 20 处理器划分为四个组的五个 Cpu。 Cpu 的每个组位于同一个 NUMA 节点上。

- 并发批处理的最大数目设置为 8。

- 每个工作负荷组必须处理两个评分任务。 只要一个任务完成读取数据和启动评分，在另一任务可以开始从数据库读取数据。

若要查看此方案中的 PowerShell 脚本，请打开在文件 experiment.ps1 [Github 项目](https://github.com/Microsoft/SQL-Server-R-Services-Samples/tree/master/SQLOptimizationTips)。

### <a name="storing-models-for-prediction"></a>存储用于预测的模型

当训练和评估完成和你已选择最佳的模型时，我们建议将该模型存储在数据库中，以便它不用于预测。 从预测数据库加载预先计算的模型是高效，因为 SQL Server 机器学习使用特殊的序列化算法来存储和加载模型时 R 和数据库之间移动。

> [!TIP]
> 在 SQL Server 自 2017 年，你可以使用预测函数来执行评分即使在服务器上未安装 R。 支持有限的模型类型，从 RevoScaleR 包。

但是，具体取决于你使用的算法，某些模型可能会很大，尤其是在大型数据集所涉及的培训。 例如，如算法**lm**或**glm**生成大量的以及规则的摘要数据。 由于上一种模型，可以存储在 varbinary 列的大小没有限制，我们建议你存储在该模型存储在数据库中为生产之前消除不必要的项目，从模型。

## <a name="articles-in-this-series"></a>本系列文章

[性能优化 R – 简介](../r/sql-server-r-services-performance-tuning.md)

[性能优化 R-SQL Server 配置](../r/sql-server-configuration-r-services.md)

[性能优化 R-R 代码和数据优化](../r/r-and-data-optimization-r-services.md)

[性能优化的案例研究结果](../r/performance-case-study-r-services.md)
