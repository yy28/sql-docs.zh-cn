---
title: 如何为 Linux 上的 SQL Server 配置持久性内存 (PMEM)
description: 本文提供在 Linux 上配置 PMEM 的教程。
author: DBArgenis
ms.author: argenisf
ms.reviewer: vanto
ms.date: 11/06/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 4ed705b1b26193585a6278508ac98666d069418a
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/25/2019
ms.locfileid: "68077566"
---
# <a name="how-to-configure-persistent-memory-pmem-for-sql-server-on-linux"></a>如何为 Linux 上的 SQL Server 配置持久性内存 (PMEM)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文介绍如何为 Linux 上的 SQL Server 配置持久性内存 (PMEM)。 SQL Server 2019 预览版引入了对 Linux 的 PMEM 支持。

## <a name="overview"></a>概述

SQL Server 2016 引入了对非易失性 DIMM 的支持，以及称为[日志结尾在 NVDIMM 上缓存]( https://blogs.msdn.microsoft.com/bobsql/2016/11/08/how-it-works-it-just-runs-faster-non-volatile-memory-sql-server-tail-of-log-caching-on-nvdimm/)的优化。 这些优化减少了将日志缓冲区强化为持久性存储所需的操作数量。 这利用了 Windows Server 对 DAX 模式下的持久性内存设备的直接访问权限。

SQL Server 2019 预览版将对持久性内存 (PMEM) 设备的支持扩展到 Linux，对 PMEM 上放置的数据和事务日志文件提供完整 enlightenment。 Enlightenment 是指使用高效用户空间 `memcpy()` 操作访问存储设备的方法。 SQL Server 利用 Linux 上的 DAX 支持将数据直接放入设备中，而不是通过文件系统和存储堆栈，从而减少延迟。

## <a name="enable-enlightenment-of-database-files"></a>对数据库文件启用 enlightenment
若要对 Linux 上的 SQL Server 中的数据库文件启用 enlightenment，请执行以下步骤：

1. 配置设备。

  在 Linux 中，使用 `ndctl` 实用工具。

  - 安装 `ndctl` 以配置 PMEM 设备。 可在[此处](https://docs.pmem.io/getting-started-guide/installing-ndctl)找到。
  - 使用 [ndctl] 创建命名空间。

  ```bash 
  ndctl create-namespace -f -e namespace0.0 --mode=fsdax* --map=mem
  ```

  >[!NOTE]
  >如果正在使用低于 59 的 `ndctl` 版本，请使用 `--mode=memory`。

  使用 `ndctl` 验证命名空间。 示例输出如下：

```bash
ndctl list
[
  {
    "dev":"namespace0.0",
    "mode":"memory",
    "size":1099511627776,
    "blockdev":"pmem0",
    "numa_node":0
  }
]
```

  - 创建和装载 PMEM 设备

    例如，使用 XFS

    ```bash
    mkfs.xfs -f /dev/pmem0
    mount -o dax,noatime /dev/pmem0 /mnt/dax
    xfs_io -c "extsize 2m" /mnt/dax
    ```

    例如，使用 EXT4

    ```bash
    mkfs.ext4 -b 4096 -E stride=512 -F /dev/pmem0
    mount -o dax,noatime /dev/pmem0 /mnt/dax
    ```

  使用 ndctl 配置设备，并将其格式化和装载后，可以将数据库文件放在其中。 还可以创建新的数据库 

1. 由于 PMEM 设备是 O_DIRECT 安全的，因此请启用跟踪标志 3979来禁用强制刷新机制。 此跟踪标志为启动跟踪标志，因此需要使用 mssql-conf 实用工具来启用。 请注意，这是服务器范围的配置更改，如果有任何需要强制刷新机制以确保数据完整性的 O_DIRECT 不兼容设备，则不应使用此跟踪标志。 有关详细信息，请参阅 https://support.microsoft.com/en-us/help/4131496/enable-forced-flush-mechanism-in-sql-server-2017-on-linux

1. 请重新启动 SQL Server。

## <a name="next-steps"></a>后续步骤

有关 Linux 上的 SQL Server 的详细信息，请参阅 [Linux 上的 SQL Server](sql-server-linux-overview.md)。
