---
title: Linux 上的 SQL Server 的性能最佳做法
description: 本文提供运行 Linux 上的 SQL Server 的性能最佳做法和指南。
author: tejasaks
ms.author: tejasaks
ms.reviewer: vanto
ms.date: 09/16/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 1b2a4f55908f249d9f574d392dea26932648e58d
ms.sourcegitcommit: c74bb5944994e34b102615b592fdaabe54713047
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/22/2020
ms.locfileid: "90989910"
---
# <a name="performance-best-practices-and-configuration-guidelines-for-sql-server-on-linux"></a>Linux 上的 SQL Server 的性能最佳做法和配置指南

[!INCLUDE [SQL Server - Linux](../includes/applies-to-version/sql-linux.md)]

本文提供了最佳做法和建议，以最大程度地提高连接到 Linux 上的 SQL Server 的数据库应用程序的性能。 这些建议特定在 Linux 平台上运行。 所有正常 SQL Server 建议（例如索引设计）仍适用。

以下指南包含配置 SQL Server 和 Linux 操作系统的建议。

## <a name="sql-server-configuration"></a>SQL Server 配置

建议在安装 Linux 上的 SQL Server 后执行以下配置任务，以实现应用程序的最佳性能。

### <a name="best-practices"></a>最佳做法

- **对节点和/或 Cpu 使用 PROCESS AFFINITY**

   对于所有用于 Linux 操作系统上的 SQL Server 的 NUMANODE`ALTER SERVER CONFIGURATION``PROCESS AFFINITY` 和/或 CPU（通常是所有节点和 CPU），建议使用 **设置**。 处理器关联有助于保持高效的 Linux 和 SQL 计划行为。 使用 NUMANODE  选项是最简单的方法。 请注意，即使你的计算机上只有一个 NUMA 节点，也应该使用 PROCESS AFFINITY  。  有关如何设置 [PROCESS AFFINITY](../t-sql/statements/alter-server-configuration-transact-sql.md) 的详细信息，请参阅**更改服务器配置**文档。

- **配置多个 tempdb 数据文件**

   由于 Linux 上的 SQL Server 安装不提供配置多个 tempdb 文件的选项，因此建议在安装后考虑创建多个 tempdb 数据文件。 有关详细信息，请参阅[建议以减少 SQL Server tempdb 数据库中的分配争用](https://support.microsoft.com/help/2154845/recommendations-to-reduce-allocation-contention-in-sql-server-tempdb-d)一文。

### <a name="advanced-configuration"></a>高级配置

以下建议是可选的配置设置，你可以选择在安装 Linux 上的 SQL Server 之后执行这些设置。 这些选项取决于你的工作负载和 Linux 操作系统配置的要求。

- **使用 mssql-conf 设置内存限制**

   为了确保 Linux 操作系统有足够的可用物理内存，默认情况下 SQL Server 进程只使用 80% 的物理 RAM。 对于某些系统，如果物理 RAM 很大，20% 可能是一个很大的数字。 例如，在具有 1 TB RAM 的系统上，默认设置将保留 200 GB RAM 不使用。 在这种情况下，你可能希望将内存限制配置为较高的值。 请参阅有关 **mssql-conf** 工具的文档和 [memory.memorylimitmb](sql-server-linux-configure-mssql-conf.md#memorylimit) 设置，该设置可控制对 SQL Server 可见的内存（以 MB 为单位）。

   更改此设置时，请注意不要将此值设置得太高。 如果不留出足够的内存，则可能会遇到 Linux 操作系统和其他 Linux 应用程序的问题。

## <a name="linux-os-configuration"></a>Linux OS 配置

请考虑使用以下 Linux 操作系统配置设置，以体验 SQL Server 安装的最佳性能。

### <a name="kernel-settings-for-high-performance"></a>高性能内核设置
这些是与 SQL Server 安装的高性能和吞吐量相关的推荐 Linux 操作系统设置。 请参阅 Linux 操作系统文档，以了解如何配置这些设置。



> [!Note]
> 对于 Red Hat Enterprise Linux (RHEL) 用户，[优化的](https://tuned-project.org)吞吐量-性能配置文件将自动配置这些设置（C 状态除外）。 自 RHEL 8.0 起，/usr/lib/tuned 内置 mssql 配置文件使用 Red Hat 共同开发，可为 SQL Server 工作负载提供与 Linux 性能相关的更好的优化。 此配置文件包含 RHEL 吞吐量-性能配置文件，我们在下面提供了它的定义，供你查看其他 Linux 发行版和不带此配置文件的 RHEL 版本。

下表提供了 CPU 设置的建议：

| 设置 | 值 | 详细信息 |
|---|---|---|
| CPU 频率调控器 | 性能 | 请参阅 **cpupower** 命令 |
| ENERGY_PERF_BIAS | 性能 | 请参阅 **x86_energy_perf_policy** 命令 |
| min_perf_pct | 100 | 查看有关 intel p 状态的文档 |
| C 状态 | 仅限 C1 | 请参阅 Linux 或系统文档，了解如何确保将 C 状态设置为仅限 C1 |

下表提供了磁盘设置的建议：

| 设置 | 值 | 详细信息 |
|---|---|---|
| 磁盘预读 | 4096 | 请参阅 **blockdev** 命令 |
| sysctl 设置 | kernel.sched_min_granularity_ns = 10000000<br/>kernel.sched_wakeup_granularity_ns = 15000000<br/>vm.dirty_ratio = 40<br/>vm.dirty_background_ratio = 10<br/>vm.swappiness = 10 | 请参阅 **sysctl** 命令 |

### <a name="kernel-setting-auto-numa-balancing-for-multi-node-numa-systems"></a>多节点 NUMA 系统的内核设置自动 numa 平衡

如果在多节点 NUMA  系统上安装 SQL Server，则默认会启用以下 kernel.numa_balancing  内核设置。 若要使 SQL Server 在 NUMA  系统上以最高效率运行，请在多节点 NUMA 系统上禁用自动 NUMA 平衡：

```bash
sysctl -w kernel.numa_balancing=0
```

### <a name="kernel-settings-for-virtual-address-space"></a>虚拟地址空间的内核设置

vm.max_map_count  的默认设置 (65536) 对 SQL Server 安装来说可能不够高。 出于此原因，请在 SQL Server 部署中，将 vm.max_map_count 值更改为 262144，并参阅[使用优化的 mssql 配置文件的建议 Linux 设置](#proposed-linux-settings-using-a-tuned-mssql-profile)部分，了解如何进一步优化这些内核参数。 vm.max_map_count 的最大值为 2147483647。

```bash
sysctl -w vm.max_map_count=262144
```

### <a name="proposed-linux-settings-using-a-tuned-mssql-profile"></a>使用优化的 mssql 配置文件的建议 Linux 设置

```bash
#
# A tuned configuration for SQL Server on Linux
#
    
[main]
summary=Optimize for Microsoft SQL Server
include=throughput-performance
    
[cpu]
force_latency=5

[sysctl]
vm.swappiness = 1
vm.dirty_background_ratio = 3
vm.dirty_ratio = 80
vm.dirty_expire_centisecs = 500
vm.dirty_writeback_centisecs = 100
vm.transparent_hugepages=always
# For multi-instance SQL deployments, use
# vm.transparent_hugepages=madvice
vm.max_map_count=1600000
net.core.rmem_default = 262144
net.core.rmem_max = 4194304
net.core.wmem_default = 262144
net.core.wmem_max = 1048576
kernel.numa_balancing=0
kernel.sched_latency_ns = 60000000
kernel.sched_migration_cost_ns = 500000
kernel.sched_min_granularity_ns = 15000000
kernel.sched_wakeup_granularity_ns = 2000000
```

若要启用此优化的配置文件，请将这些定义保存在 /usr/lib/tuned/mssql 文件夹下的 tuned.conf 文件中，并使用以下命令启用配置文件

```bash
chmod +x /usr/lib/tuned/mssql/tuned.conf
tuned-adm profile mssql
```

使用以下命令验证其是否启用

```bash
tuned-adm active
```
或
```bash
tuned-adm list
```

### <a name="disable-last-accessed-datetime-on-file-systems-for-sql-server-data-and-log-files"></a>在文件系统上禁用 SQL Server 数据和日志文件的上次访问日期/时间

对用于存储 SQL Server 数据和日志文件的任何文件系统使用 noatime**** 属性。 有关如何设置此属性的说明，请参阅 Linux 文档。

### <a name="leave-transparent-huge-pages-thp-enabled"></a>启用透明大页 (THP)

大多数 Linux 安装应在默认情况下启用此选项。 建议将此配置选项设置为启用，以获得最一致的性能体验。 但是，如果在具有多个实例的 SQL Server 部署中发生大量内存分页活动，或者在服务器上与其他内存需求较高的应用程序一起执行 SQL Server 的情况下，建议在执行以下命令后测试应用程序的性能 

```bash
echo madvise > /sys/kernel/mm/transparent_hugepage/enabled
```
或者使用以下命令行修改 mssql 优化后的配置文件

```bash
vm.transparent_hugepages=madvise
```
并在修改后使 mssql 配置文件处于活动状态
```bash
tuned-adm off
tuned-adm profile mssql
```

### <a name="swapfile"></a>交换文件

请确保已正确配置交换文件，以免出现内存不足的问题。 有关如何创建交换文件并正确调整其大小的详细说明，请参阅 Linux 文档。

### <a name="virtual-machines-and-dynamic-memory"></a>虚拟机和动态内存

如果在虚拟机中运行 Linux 上的 SQL Server，请确保选择选项来修复为虚拟机预留的内存量。 请勿使用 Hyper-V 动态内存等功能。

## <a name="next-steps"></a>后续步骤

若要详细了解提高性能的 SQL Server 功能，请参阅[性能功能入门](sql-server-linux-performance-get-started.md)。

有关 Linux 上的 SQL Server 的详细信息，请参阅 [Linux 上的 SQL Server 概述](sql-server-linux-overview.md)。
