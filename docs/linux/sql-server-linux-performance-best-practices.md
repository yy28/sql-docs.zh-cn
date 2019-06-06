---
title: Linux 上的 SQL Server 的性能最佳做法 |Microsoft 文档
description: 本文提供在 Linux 上运行 SQL Server 性能最佳实践和准则。
author: rgward
ms.author: bobward
manager: craigg
ms.date: 09/14/2017
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 8dc3cafb54fe91709bd3ee078dfeeb1dc5e3d649
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66705171"
---
# <a name="performance-best-practices-and-configuration-guidelines-for-sql-server-on-linux"></a>性能最佳实践和 Linux 上的 SQL Server 配置准则

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文提供了最佳实践和建议，以最大限度地连接到 Linux 上的 SQL Server 的数据库应用程序的性能。 这些建议是特定于 Linux 平台上运行。 所有正常的 SQL Server 建议，如索引设计仍然适用。

以下指南包含有关配置 SQL Server 和 Linux 操作系统的建议。

## <a name="sql-server-configuration"></a>SQL Server 配置

建议以获得最佳性能应用程序在 Linux 上安装 SQL Server 之后执行以下配置任务。

### <a name="best-practices"></a>最佳做法

- **使用节点和/或 Cpu 的进程关联**

   建议使用`ALTER SERVER CONFIGURATION`若要设置`PROCESS AFFINITY`所有**NUMANODEs**和/或 Cpu 您使用 SQL Server （这通常是为所有节点和 Cpu） 的 Linux 操作系统上。 处理器关联可帮助保持高效的 Linux 和 SQL 调度行为。 使用**NUMANODE**选项是最简单方法。 请注意，应使用**进程关联**即使您的计算机上具有单个 NUMA 节点。  请参阅[ALTER SERVER CONFIGURATION](../t-sql/statements/alter-server-configuration-transact-sql.md)文档了解如何设置的详细信息**进程关联**。

- **配置多个 tempdb 数据文件**

   由于 Linux 安装上的 SQL Server 不提供一个选项以配置多个 tempdb 文件，我们建议您考虑在安装后创建多个 tempdb 数据文件。 有关详细信息，请参阅文章中的指导[建议，以减少 SQL Server tempdb 数据库中的分配争用](https://support.microsoft.com/help/2154845/recommendations-to-reduce-allocation-contention-in-sql-server-tempdb-d)。

### <a name="advanced-configuration"></a>高级的配置

以下建议是您可以选择在 Linux 上的 SQL Server 安装之后要执行的可选的配置设置。 这些选项基于工作负荷和配置 Linux 操作系统的要求。

- **设置使用 mssql conf 的内存限制**

   为了确保没有足够的可用物理内存的 Linux 操作系统系统中，SQL Server 进程使用默认情况下只有 80%的物理 RAM。 对于某些系统中的大量物理内存的 20%可能会有相当多。 例如，在系统上使用 1 TB 的 RAM，默认设置会让约为 200 GB 的 RAM 未使用。 在此情况下，你可能想要配置的内存限制到更高的值。 在查看文档**mssql conf**工具并[memory.memorylimitmb](sql-server-linux-configure-mssql-conf.md#memorylimit)设置，则可控制的内存 （单位为 MB） 到 SQL Server 可见。

   在更改此设置，注意不要设置此值过高。 如果未将足够的内存，可能会遇到与 Linux 操作系统和其他 Linux 应用程序的问题。

## <a name="linux-os-configuration"></a>Linux OS 配置

请考虑使用以下 Linux 操作系统配置设置以 SQL Server 安装的最佳性能体验该产品。

### <a name="kernel-settings-for-high-performance"></a>高性能的内核设置
这些是建议的 Linux 操作系统设置与高性能和吞吐量的 SQL Server 安装。 请参阅过程以配置这些设置在 Linux 操作系统文档。



> [!Note]
> 对于 Red Hat Enterprise Linux (RHEL) 的用户，吞吐量性能配置文件将配置这些设置自动 （除了 C 状态）。

下表提供了有关 CPU 设置的建议：

| 设置 | ReplTest1 | 详细信息 |
|---|---|---|
| CPU 频率调控器 | 性能 | 请参阅**cpupower**命令 |
| ENERGY_PERF_BIAS | 性能 | 请参阅**x86_energy_perf_policy**命令 |
| min_perf_pct | 100 | 请参阅 intel p 状态的文档 |
| C-States | 仅 C1 | 请参阅有关如何确保只能 C 状态设置为 C1 的 Linux 或系统文档 |

下表提供了建议的磁盘设置：

| 设置 | ReplTest1 | 详细信息 |
|---|---|---|
| 磁盘预读 | 4096 | 请参阅**blockdev**命令 |
| sysctl 设置 | kernel.sched_min_granularity_ns = 10000000<br/>kernel.sched_wakeup_granularity_ns = 15000000<br/>vm.dirty_ratio = 40<br/>vm.dirty_background_ratio = 10<br/>vm.swappiness=10 | 请参阅**sysctl**命令 |

### <a name="kernel-setting-auto-numa-balancing-for-multi-node-numa-systems"></a>平衡的多节点 NUMA 系统的内核设置自动 numa

如果在多节点上安装 SQL Server **NUMA**系统时，以下**kernel.numa_balancing**内核设置在默认情况下启用状态。 若要允许 SQL Server 上运行最大效率**NUMA**系统中，禁用自动 numa 平衡的多节点 NUMA 系统上：

```bash
sysctl -w kernel.numa_balancing=0
```

### <a name="kernel-settings-for-virtual-address-space"></a>虚拟地址空间的内核设置

默认设置**vm.max_map_count** （这是 65536） 可能不是足够高的 SQL Server 安装。 将此值 （即数上限） 更改为 256k。

```bash
sysctl -w vm.max_map_count=262144
```

### <a name="disable-last-accessed-datetime-on-file-systems-for-sql-server-data-and-log-files"></a>禁用上次访问日期/时间的文件系统上的 SQL Server 数据和日志文件

使用**noatime**与任何用来存储 SQL Server 数据和日志文件的文件系统属性。 请参阅有关如何将此属性设置 Linux 文档。

### <a name="leave-transparent-huge-pages-thp-enabled"></a>将保留透明巨大页 (THP) 已启用

默认情况下，大多数 Linux 安装应该对具有此选项。 我们建议最一致的性能体验，要启用此配置选项。

### <a name="swapfile"></a>交换文件

请确保已正确配置交换文件，以避免任何内存不足问题。 请参阅在 Linux 文档以了解如何创建并正确设置交换文件的大小。

### <a name="virtual-machines-and-dynamic-memory"></a>虚拟机和动态内存

如果您运行 SQL Server Linux 上的虚拟机中，请确保你选择选项以修复虚拟机保留的内存量。 不要使用 HYPER-V 动态内存等功能。

## <a name="next-steps"></a>后续步骤

若要了解有关 SQL Server 功能，可提高性能的详细信息，请参阅[开始使用性能功能](sql-server-linux-performance-get-started.md)。

Linux 上 SQL Server 的详细信息，请参阅[概述的 SQL Server Linux 上](sql-server-linux-overview.md)。
