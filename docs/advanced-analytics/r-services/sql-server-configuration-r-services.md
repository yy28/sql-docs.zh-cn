---
title: "SQL Server 配置 （R 服务） | Microsoft Docs"
ms.custom: ""
ms.date: "03/10/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4b08969f-b90b-46b3-98e7-0bf7734833fc
caps.latest.revision: 13
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 12
---
# SQL Server 配置 （R 服务）
此部分中的信息提供有关使用计算机的硬件和网络配置的常规指导到主机 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]。 它应被视为常规除了 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 性能优化中提供信息 [SQL Server 数据库引擎和 Azure SQL Database 的性能中心](../../relational-databases/security/security-center-for-sql-server-database-engine-and-azure-sql-database.md)。

## 处理器

[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 可以通过使用计算机; 上的可用内核并行执行任务则有更多内核性能越好。 由于 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 通常是由多个用户同时使用，数据库管理员应确定的理想之选为支持峰值工作负荷计算所需的核心数。 有关 IO 绑定操作，可能没有帮助的内核数，而受 CPU 限制算法将受益于更快的 Cpu 具有多个内核。

## 内存

在计算机上的可用内存量会对性能的高级分析算法很大的影响。 使用 SQL 计算上下文时，没有足够的内存可能会影响并行度。 它还会影响块区大小 （每次读取操作的行） 可进行处理，并可以支持的同时会话的数目。

强烈建议至少为 32 GB。 如果您有多个 32 gb 可用空间，您可以配置 SQL 数据源，在每个读取操作中使用更多的行以提高性能。

## 电源选项

在 Windows 操作系统， __高性能__ 应使用电源选项。 使用不同的电源设置将导致性能降低或不一致时使用 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]。

## 磁盘 IO

使用的训练和预测作业 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 天生就 IO 绑定，并依赖于数据库存储在磁盘的速度。 有助于更快的驱动器，例如固态硬盘 (SSD)。 

访问磁盘的其他应用程序也会影响磁盘 IO︰ 例如，读取对其他客户端数据库执行的操作。 磁盘 IO 性能也可能受到中使用，例如文件系统所使用的块大小的文件系统上的设置。 如果提供多个驱动器，则在与不同的驱动器上存储数据库 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 如此，请求为 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 未命中同一个磁盘作为对存储在数据库中的数据的请求。

运行在训练过程中使用多个迭代的 RevoScaleR 分析函数时，磁盘 IO 会还将大大影响性能。 例如， `rxLogit`, ，`rxDTree`, ，`rxDForest` 和 `rxBTrees` 都使用多个迭代。 数据源时 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], ，这些算法使用经过了优化，捕获数据的临时文件。 会话完成后，会自动清除这些文件。 具有读/写操作的高性能磁盘可以显著提高这些算法所经过的总体时间。

> [!NOTE]
> [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 需要在 Windows 操作系统上的 8.3 文件名支持。 若要确定驱动器是否支持 8.3 文件名，或如果不启用支持，您可以使用 fsutil.exe。 8.3 文件名中使用 fsutil.exe 的详细信息，请参阅 [Fsutil 8dot3name](https://technet.microsoft.com/library/ff621566(v=ws.11).aspx)。

### 表压缩

通常可通过使用压缩或 columstore 索引提高 IO 性能。 通常情况下，在多个列在表中，因此使用列存储索引利用这些重复时压缩数据经常重复数据。

列存储索引可能不会尽可能高效，如果有大量的插入行的表，但如果数据是静态的或只有很少更改是一个不错的选择。 如果纵栏式应用商店不合适，对行的主表启用压缩功能可提高 IO。

有关详细信息，请参阅以下文档：

* [数据压缩](../../relational-databases/data-compression/data-compression.md)

* [对表或索引启用压缩功能](../../relational-databases/data-compression/enable-compression-on-a-table-or-index.md)

* [列存储索引指南](Columnstore%20Indexes%20Guide.md)

## 分页文件

Windows 操作系统使用的页面文件来管理故障转储和存储的虚拟内存页面。 如果您注意到出现了过度分页，请考虑增加计算机上的物理内存。 尽管有更多的物理内存不会消除分页，但它确实会降低对分页的需要。

页面文件存储在磁盘的速度也会影响性能。 存储页面文件固态硬盘上的或跨多个 Ssd，使用多个页面文件可以提高性能。

请参阅 [如何确定合适的页面文件大小的 64 位版本的 Windows 最](https://support.microsoft.com/en-us/kb/2860880) 有关大小调整页面文件的信息。

## 资源调控

[!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 用于控制使用的各种资源支持资源调控 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]。 例如的默认值为 R 的内存消耗最多 20%的可用总内存 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)]。 这样做是为了确保 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 长时间运行的 R 作业不会严重影响工作流。 但是，数据库管理员可以更改这些限制。 

有限的资源是 __MAX_CPU_PERCENT__, ，__MAX_MEMORY_PERCENT__, ，和 __MAX_PROCESSES__。 若要查看当前设置，请使用此 [!INCLUDE[tsql_md](../../includes/tsql-md.md)] 语句︰

```T-SQL
SELECT * FROM sys.resource_governor_external_resource_pools
``` 

如果 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 主要是用于 R 服务，它可能会有所帮助增加 MAX_CPU_PERCENT 到 40%或 60%。 如果存在使用相同的多个 R 会话 [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] 一次所有三个将增加。 若要更改分配的资源值，请使用 [!INCLUDE[tsql_md](../../includes/tsql-md.md)] 语句。 

此示例将设置为 40%的内存使用情况︰

```T-SQL
ALTER EXTERNAL RESOURCE POOL [default] WITH (MAX_MEMORY_PERCENT = 40)
```
下面的示例设置所有三个可配置的值︰
```T-SQL
ALTER EXTERNAL RESOURCE POOL [default] WITH (MAX_CPU_PERCENT = 40, MAX_MEMORY_PERCENT = 50, MAX_PROCESSES = 20)`
``` 

> [!NOTE]
> 若要更改这些设置将立即生效，请运行语句 `ALTER RESOURCE GOVERNOR RECONFIGURE` 在更改内存、 CPU 或最大进程设置后运行。 

## 另请参阅
[资源调控器](../../relational-databases/resource-governor/resource-governor.md)

[创建外部的资源池](../../t-sql/statements/create-external-resource-pool-transact-sql.md)

 [SQL Server R 服务性能优化指南](../../advanced-analytics/r-services/sql-server-r-services-performance-tuning.md)
 
 
 [性能案例研究](../../advanced-analytics/r-services/performance-case-study-r-services.md)
 
 [R 和数据优化](../../advanced-analytics/r-services/r-and-data-optimization-r-services.md)