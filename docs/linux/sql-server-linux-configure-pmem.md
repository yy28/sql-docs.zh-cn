---
title: 如何为 Linux 上的 SQL Server 配置永久性内存 (PMEM) |Microsoft Docs
description: 本文提供用于在 Linux 上配置 PMEM 演练。
author: DBArgenis
ms.author: argenisf
manager: craigg
ms.date: 09/24/2018
ms.topic: conceptual
ms.prod: sql
ms.custom: sql-linux
ms.technology: linux
monikerRange: '>= sql-server-ver15 || = sqlallproducts-allversions'
ms.openlocfilehash: 71c4af08573f54b5a33a95f0c821dfdb81b4f0a0
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47765583"
---
# <a name="how-to-configure-persistent-memory-pmem-for-sql-server-on-linux"></a>如何为 Linux 上的 SQL Server 配置永久性内存 (PMEM)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

本文介绍如何为 Linux 上的 SQL Server 配置永久性内存 (PMEM)。 在 SQL Server 2019 CTP 2.0 中引入了在 Linux 上的 PMEM 支持。

## <a name="overview"></a>概述

SQL Server 2016 引入了对非易失性的 Dimm、 支持和一种优化称为[NVDIMM 上写入的尾部的日志缓存]( https://blogs.msdn.microsoft.com/bobsql/2016/11/08/how-it-works-it-just-runs-faster-non-volatile-memory-sql-server-tail-of-log-caching-on-nvdimm/)缩短强制日志缓冲区写入到持久存储所需的操作数量。 这利用了直接访问 DAX 模式中的永久性内存设备的 Windows Server 的功能。

SQL Server 2019 预览扩展永久性内存的支持 linux，(PMEM) 设备提供完整一种启发式的数据和事务日志文件放置在 PMEM 上。 一种启发式是指存储设备使用有效的用户空间 memcpy 操作的访问权限的方法。 而不是通过文件系统和存储堆栈，SQL Server 正在利用直接将数据放入到最少的延迟会产生的设备在 Linux 上的 DAX 支持。

## <a name="enable-enlightenment-of-database-files"></a>启用数据库文件的一种启发式
若要启用一种启发式的 SQL Server 中在 Linux 上的数据库文件，请执行以下步骤：

1. 配置设备在 Linux、 执行此操作使用`ndctl`实用程序。

  - 安装安装`ndctl`pmem 设备进行配置。 你可以找到它[此处](https://docs.pmem.io/getting-started-guide/installing-ndctl)。
  - 使用 [ndctl] 若要创建的命名空间。

  ```bash 
  ndctl create-namespace -f -e namespace0.0 --mode=fsdax* –map=mem
  ```

  >[!NOTE]
  >如果使用的`ndctl`版本低于 59，使用`--mode=memory`。

  使用`ndctl`验证命名空间。 示例输出如下所示：

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

  - 创建并装载 pmem 设备

    例如，使用 XFS

    ```bash
    mkfs.xfs -f /dev/pmem0
    mount –o dax,noatime /dev/pmem0 /mnt/dax
    xfs_io -c "extsize 2m" /mnt/dax
    ```

    例如，对于 EXT4

    ```bash
    mkfs.ext4 -b 4096 -E stride=512 -F /dev/pmem0
    mount –o dax,noatime /dev/pmem0 /mnt/dax
    ```

  一旦已配置了 ndctl、 格式化和装入了设备，可以将数据库文件放入其中。 此外可以创建一个新的数据库 

1. 使用跟踪标志 3979 启用 SQL Server 数据库文件一种启发式。 此跟踪标志是一个启动跟踪标志，并且这种情况下需要使用 mssql-conf 实用工具启用。

1. 请重新启动 SQL Server。

## <a name="next-steps"></a>后续步骤

Linux 上 SQL Server 的详细信息，请参阅[Linux 上的 SQL Server](sql-server-linux-overview.md)。
