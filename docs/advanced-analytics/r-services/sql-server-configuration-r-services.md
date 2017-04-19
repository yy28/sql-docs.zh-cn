---
title: "SQL Server 配置 (R Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/10/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 4b08969f-b90b-46b3-98e7-0bf7734833fc
caps.latest.revision: 13
author: jeannt
ms.author: jeannt
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: ac5e1483a75fb29c7c50ab834727bf185b7f3c98
ms.lasthandoff: 04/11/2017

---
# <a name="sql-server-configuration-r-services"></a>SQL Server 配置 (R Services)
本部分中的信息提供有关用于托管 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 的计算机的硬件和网络配置的一般指导。 应该将这些内容视为[SQL Server 数据库引擎和 Azure SQL 数据库的性能中心](../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)所述的一般 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 性能优化信息的补充。

## <a name="processor"></a>处理器

[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 可以使用计算机上的可用核心并行执行任务；可用的核心越多，性能就越好。 由于 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 通常由多个用户同时使用，数据库管理员应确定支持峰值工作负荷计算所需的理想核心数。 尽管核心数可能对 IO 约束操作不会带来帮助，但如果 CPU 速度越快且核心越多，则可以让 CPU 约束算法受益。

## <a name="memory"></a>内存

计算机上的可用内存量可能会对高级分析算法的性能造成很大的影响。 使用 SQL 计算上下文时，内存不足可能会影响并行度。 此外，还会影响可处理的区块大小（每个读取操作使用的行数），以及可支持的并发会话数。

强烈建议至少配置 32GB 内存。 如果可用内存超过 32GB，你可以将 SQL 数据源配置为在每个读取操作中使用更多的行，以提高性能。

## <a name="power-options"></a>电源选项

在 Windows 操作系统中，应使用“高性能”电源选项。 使用不同的电源设置会导致在使用 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 时性能下降或不一致。

## <a name="disk-io"></a>磁盘 IO

使用 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 的训练和预测作业原生受到 IO 约束，依赖于存储数据库的磁盘的速度。 更快的驱动器（例如固态硬盘 (SSD)）可能会有所帮助。 

磁盘 IO 还会受到访问磁盘的其他应用程序的影响：例如，其他客户端对数据库执行的读取操作。 磁盘 IO 性能还会受到使用的文件系统中的设置（例如，文件系统使用的块大小）影响。 如果有多个可用的驱动器，请将数据库存在在除 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 以外的驱动器上，使得针对 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 发出的请求不会传入针对数据库中存储的数据发出的请求所在的同一磁盘。

在训练期间运行使用多个迭代的 RevoScaleR 分析函数时，磁盘 IO 也可能会对性能造成很大的影响。 例如，`rxLogit`、`rxDTree`、`rxDForest` 和 `rxBTrees` 都使用多个迭代。 如果数据源为 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，这些算法将使用优化的临时文件来捕获数据。 会话完成后，会自动清理这些文件。 使用高性能磁盘进行读/写操作可以大幅改善这些算法所消耗的总体时间。

> [!NOTE]
> 在 Windows 操作系统中，[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 需要 8.3 文件名支持。 可以使用 fsutil.exe 确定驱动器是否支持 8.3 文件名，如果不支持，还可以启用这种支持。 有关使用 fsutil.exe 验证 8.3 文件名的详细信息，请参阅 [Fsutil 8dot3name](https://technet.microsoft.com/library/ff621566(v=ws.11).aspx)。

### <a name="table-compression"></a>表压缩

通常可以使用压缩或列存储索引提高 IO 性能。 一般情况下，数据往往在表中的多个列内重复，因此，使用列存储索引可以在压缩数据时利用这种重复。

如果在表中执行大量的插入，列存储索引的效率可能不高；但是，如果数据是静态的或者不经常更改，则列存储索引是不错的选择。 如果纵栏表存储不适用，对主表中的行启用压缩可以改善 IO。

有关详细信息，请参阅以下文档：

* [数据压缩](../../relational-databases/data-compression/data-compression.md)

* [对表或索引启用压缩](../../relational-databases/data-compression/enable-compression-on-a-table-or-index.md)

* [列存储索引指南](https://msdn.microsoft.com/library/gg492088.aspx)

## <a name="paging-file"></a>分页文件

Windows 操作系统使用分页文件来管理故障转储和存储虚拟内存页面。 如果你发现分页过度，请考虑增大计算机上的物理内存。 尽管分配更多的物理内存不会消除分页，但确实可以减少分页的需要。

存储页面文件的磁盘的速度也会影响性能。 将页面文件存储在 SSD 中或者在多个 SSD 上使用多个页面文件可以提高性能。

有关调整页面文件大小的信息，请参阅 [How to determine the appropriate page file size for 64-bit versions of Windows](https://support.microsoft.com/en-us/kb/2860880)（如何确定 64 位版本 Windows 的合适页面文件大小）。

## <a name="resource-governance"></a>资源调控

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 支持使用资源调控来控制 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 使用的各种资源。 例如，R 的默认内存消耗值限制为 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 总可用内存的 20%。 这是为了确保 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 工作流不会受到长时间运行的 R 作业的严重影响。 但是，数据库管理员可以更改这些限制。 

限制的资源包括 __MAX_CPU_PERCENT__、__MAX_MEMORY_PERCENT__ 和 __MAX_PROCESSES__。 若要查看当前设置，请使用以下 [!INCLUDE[tsql_md](../../includes/tsql-md.md)] 语句：

```T-SQL
SELECT * FROM sys.resource_governor_external_resource_pools
``` 

如果 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 主要用于 R Services，将 MAX_CPU_PERCENT 增大到 40% 或 60% 可能会有帮助。 如果许多 R 会话同时使用同一个 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]，所有三个值都会增大。 若要更改分配的资源值，请使用 [!INCLUDE[tsql_md](../../includes/tsql-md.md)] 语句。 

此示例将内存用量设置为 40%：

```T-SQL
ALTER EXTERNAL RESOURCE POOL [default] WITH (MAX_MEMORY_PERCENT = 40)
```
以下示例设置所有三个可配置值：
```T-SQL
ALTER EXTERNAL RESOURCE POOL [default] WITH (MAX_CPU_PERCENT = 40, MAX_MEMORY_PERCENT = 50, MAX_PROCESSES = 20)`
``` 

> [!NOTE]
> 若要立即使这些设置的更改生效，请在更改内存、CPU 或最大进程设置后运行 `ALTER RESOURCE GOVERNOR RECONFIGURE` 语句。 

## <a name="see-also"></a>另请参阅
[资源调控器](../../relational-databases/resource-governor/resource-governor.md)

[CREATE EXTERNAL RESOURCE POOL](../../t-sql/statements/create-external-resource-pool-transact-sql.md)

 [SQL Server R Services 性能优化指南](../../advanced-analytics/r-services/sql-server-r-services-performance-tuning.md)
 
 
 [性能案例研究](../../advanced-analytics/r-services/performance-case-study-r-services.md)
 
 [R 和数据优化](../../advanced-analytics/r-services/r-and-data-optimization-r-services.md)

