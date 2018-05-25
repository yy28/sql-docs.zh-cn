---
title: 在 Linux 上的 SQL Server 的性能最佳实践 |Microsoft 文档
description: 这篇文章提供有关在 Linux 上运行 SQL Server 2017 性能最佳实践和指南。
author: rgward
ms.author: bobward
manager: craigg
ms.date: 09/14/2017
ms.topic: article
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.openlocfilehash: 4725a8043be3aad99f3432f99d00f6279a9d814d
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2018
---
# <a name="performance-best-practices-and-configuration-guidelines-for-sql-server-2017-on-linux"></a>性能最佳实践和 SQL Server 自 2017 年在 Linux 上的配置指南

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文提供了最佳做法和建议以最大化连接到 Linux 上的 SQL Server 的数据库应用程序的性能。 这些建议是特定于 Linux 平台上运行。 所有正常的 SQL Server 建议，如索引设计仍适用。

以下准则包含配置 SQL Server 和 Linux 操作系统的建议。

## <a name="sql-server-configuration"></a>SQL Server 配置

建议在实现应用程序的最佳性能的 linux 操作系统上安装 SQL Server 后，请执行以下配置任务。

### <a name="best-practices"></a>最佳做法

- **使用节点和/或 Cpu 的进程关联**

   建议使用`ALTER SERVER CONFIGURATION`设置`PROCESS AFFINITY`所有**NUMANODEs**和/或 Cpu 你正在使用 SQL 服务器 （这是通常的所有节点和 Cpu） Linux 操作系统上。 处理器关联可帮助维护高效的 Linux 和 SQL 计划行为。 使用**NUMANODE**选项是最简单方法。 请注意，应使用**PROCESS AFFINITY**即使计算机上有单个 NUMA 节点。  请参阅[ALTER SERVER CONFIGURATION](../t-sql/statements/alter-server-configuration-transact-sql.md)有关如何设置的详细信息的文档**PROCESS AFFINITY**。

- **配置多个 tempdb 数据文件**

   因为 Linux 安装上的 SQL 服务器未提供一个选项以配置多个 tempdb 文件，我们建议您考虑安装后创建多个 tempdb 数据文件。 有关详细信息，请参阅本文中的指导[建议，以减少在 SQL Server tempdb 数据库中的分配争用](https://support.microsoft.com/en-us/help/2154845/recommendations-to-reduce-allocation-contention-in-sql-server-tempdb-d)。

### <a name="advanced-configuration"></a>高级的配置

以下建议是你可以选择在 Linux 上的 SQL server 的安装后执行的可选配置设置。 这些选项基于的工作负荷和配置 Linux 操作系统的要求。

- **设置内存限制，mssql conf**

   为了确保没有足够的可用物理内存于 Linux 操作系统中，SQL Server 进程使用默认情况下只有 80%的物理 RAM。 对于哪些大量的物理 RAM，可能是 20%的某些系统很多。 例如，在使用 1 TB 系统的 RAM 中，默认设置将使大约 200 GB 的 RAM 未使用。 在此情况下，你可能想要配置的内存限制到更高的值。 在查看文档**mssql conf**工具和[memory.memorylimitmb](sql-server-linux-configure-mssql-conf.md#memorylimit)设置，则可控制对 SQL Server 上可见 （单位为 MB） 的内存。

   在更改此设置，请注意不要设置此值过高。 如果不保留足够的内存，你可能会遇到与 Linux 操作系统和其他 Linux 应用程序的问题。

## <a name="linux-os-configuration"></a>Linux 操作系统配置

请考虑使用以下 Linux 操作系统配置设置体验安装 SQL Server 的最佳性能。

### <a name="kernel-settings-for-high-performance"></a>为了获得高性能的内核设置
这些是建议的 Linux 操作系统设置为高相关的性能和吞吐量的 SQL Server 安装。 请参阅你的 Linux 操作系统文档，了解过程配置这些设置。



> [!Note]
> 对于 Red Hat Enterprise Linux (RHEL) 用户，吞吐量性能配置文件将配置这些设置自动 （除外 C-state)。

下表提供了建议的 CPU 设置：

| 设置 | “值” | 详细信息 |
|---|---|---|
| CPU 频率调控器 | 性能 | 请参阅**cpupower**命令 |
| ENERGY_PERF_BIAS | 性能 | 请参阅**x86_energy_perf_policy**命令 |
| min_perf_pct | 100 | 请参阅 intel p 状态的文档 |
| C 状态 | 仅 C1 | 请参阅如何确保 C 状态设置为 C1 仅 Linux 或系统文档 |

下表提供了磁盘设置的建议：

| 设置 | “值” | 详细信息 |
|---|---|---|
| 磁盘执行提前读 | 4096 | 请参阅**blockdev**命令 |
| sysctl 设置 | kernel.sched_min_granularity_ns = 10000000<br/>kernel.sched_wakeup_granularity_ns = 15000000<br/>vm.dirty_ratio = 40<br/>vm.dirty_background_ratio = 10<br/>vm.swappiness=10 | 请参阅**sysctl**命令 |

### <a name="kernel-setting-auto-numa-balancing-for-multi-node-numa-systems"></a>平衡的多节点 NUMA 系统的内核设置自动 numa

如果在多节点上安装 SQL Server **NUMA**系统、 以下**kernel.numa_balancing**默认启用内核设置。 若要允许 SQL Server 上运行最大效率**NUMA**系统，禁用自动 numa 平衡的多节点 NUMA 系统上：

```bash
sysctl -w kernel.numa_balancing=0
```

### <a name="kernel-settings-for-virtual-address-space"></a>内核虚拟地址空间设置

默认设置**vm.max_map_count** （这是 65536） 可能不是足够高的 SQL Server 安装。 将此值 （这是一个上限） 更改为 256k。

```bash
sysctl -w vm.max_map_count=262144
```

### <a name="disable-last-accessed-datetime-on-file-systems-for-sql-server-data-and-log-files"></a>禁用上次访问的日期/时间的文件系统上的 SQL Server 数据和日志文件

使用**noatime**具有用于存储 SQL Server 数据和日志文件的任何文件系统属性。 请参阅 Linux 文档如何设置此属性。

### <a name="leave-transparent-huge-pages-thp-enabled"></a>将透明巨大页 (THP) 启用

默认情况下，大多数 Linux 安装应该对具有此选项。 我们建议用于最一致的性能体验，要启用此配置选项。

### <a name="swapfile"></a>交换文件

确保已正确配置的交换文件，以避免任何内存不足问题。 请查阅你的 Linux 文档，了解如何创建和正确的大小交换文件。

### <a name="virtual-machines-and-dynamic-memory"></a>虚拟机和动态内存

如果正在虚拟机在 Linux 上运行 SQL Server，请确保您选择选项来修复虚拟机保留的内存量。 不要使用 HYPER-V 动态内存等功能。

## <a name="next-steps"></a>后续步骤

若要了解有关提高性能的 SQL Server 功能的详细信息，请参阅[入门性能功能](sql-server-linux-performance-get-started.md)。

在 Linux 上 SQL Server 的详细信息，请参阅[概述的 SQL Server on Linux](sql-server-linux-overview.md)。
