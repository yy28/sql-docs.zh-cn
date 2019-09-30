---
title: 混合缓冲池 | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
ms.assetid: ''
author: briancarrig
ms.author: brcarrig
ms.openlocfilehash: 8bbc7670f3a4d6d8a017e7284c5a661d38594f08
ms.sourcegitcommit: 1c3f56deaa4c1ffbe5d7f75752ebe10447c3e7af
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/25/2019
ms.locfileid: "71251060"
---
# <a name="hybrid-buffer-pool"></a>混合缓冲池
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

混合缓冲池使数据库引擎能够直接访问存储在持久内存 (PMEM) 设备上的数据库文件中的数据页。 [!INCLUDE[sqlv15](../../includes/sssqlv15-md.md)] 中引入了此功能。

在没有 PMEM 的传统系统中，SQL Server 将数据页缓存在缓冲池中。 使用混合缓冲池，SQL Server 会跳过将页面副本执行到缓冲池的基于 DRAM 的部分，直接在 PMEM 设备上的数据库文件上访问该页面。 对混合缓冲池的 PMEM 设备上的数据文件的读取访问直接通过追随指向 PMEM 设备上数据页的指针来执行。  

只能在 PMEM 设备上直接访问干净页。 当页面被标记为脏时，它会先被复制到 DRAM 缓冲池，最后被写回 PMEM 设备并再次标记为干净。 这将在常规检查点操作期间发生。 用于将文件从 PMEM 设备复制到 DRAM 的机制是直接内存映射 I/O (MMIO)，也称为 SQL Server 中的数据文件的 enlightenment  。


混合缓冲池功能同时适用于 Windows 和 Linux。 必须使用支持 DAX (DirectAccess) 的文件系统来格式化 PMEM 设备。 XFS、EXT4、NTFS 文件系统都支持 DAX。 SQL Server 将自动检测数据文件是否驻留在格式正确的 PMEM 设备上，并在用户空间中执行内存映射。 当连接、还原、创建新数据库或为数据库启用混合缓冲池功能时，将在启动时发生此映射。

有关 Windows Server 对 PMEM 的支持的更多信息，请参阅[在 Windows Server 上部署持久内存](/windows-server/storage/storage-spaces/deploy-pmem/)。

有关在 Linux 上为 PMEM 设备配置 SQL Server 的更多信息，请参阅[部署持久性内存](../../linux/sql-server-linux-configure-pmem.md)。

## <a name="enable-hybrid-buffer-pool"></a>启用混合缓冲池

[!INCLUDE[sqlv15](../../includes/sssqlv15-md.md)] 引入了动态数据语言 (DDL) 来控制混合缓冲池。

以下示例为 SQL Server 实例启用混合缓冲池：

```sql
ALTER SERVER CONFIGURATION SET MEMORY_OPTIMIZED HYBRID_BUFFER_POOL = ON;
```

默认情况下，混合缓冲池在实例范围内设置为禁用。 请注意，要使设置更改生效，必须重启 SQL Server 实例。 必须重启以帮助分配足够的哈希页，以计算服务器上的总 PMEM 容量。

以下示例为特定数据库启用混合缓冲池。

```sql
ALTER DATABASE <databaseName> SET MEMORY_OPTIMIZED = ON;
```

默认情况下，混合缓冲池设置为在数据库范围启用。

## <a name="disable-hybrid-buffer-pool"></a>启用混合缓冲池

以下示例为 SQL Server 实例禁用混合缓冲池：

```sql
ALTER SERVER CONFIGURATION SET MEMORY_OPTIMIZED HYBRID_BUFFER_POOL = OFF;
```

默认情况下，混合缓冲池在实例范围内设置为禁用。 请注意，要使设置更改生效，必须重启 SQL Server 实例。 必须重启以防止过度分配哈希页，因为无需计算服务器上的 PMEM 容量。

以下示例为特定数据库禁用混合缓冲池。

```sql
ALTER DATABASE <databaseName> SET MEMORY_OPTIMIZED = OFF;
```

默认情况下，混合缓冲池设置为在数据库范围启用。

## <a name="view-hybrid-buffer-pool-configuration"></a>查看混合缓冲池配置

以下示例返回 SQL Server 实例的混合缓冲池系统配置的当前状态。

```sql
SELECT *
FROM sys.configurations
WHERE
    name = 'hybrid_buffer_pool';
```

以下示例返回两个表：

- 第一个显示 SQL Server 实例的混合缓冲池系统配置的当前状态。
- 第二个列出混合缓冲池 (`is_memory_optimized_enabled`) 的数据库和数据库级别设置。

```sql
SELECT * FROM sys.configurations WHERE name = 'hybrid_buffer_pool';

SELECT name, is_memory_optimized_enabled FROM sys.databases;
```

## <a name="best-practices-for-hybrid-buffer-pool"></a>混合缓冲池的最佳做法

建议在 RAM 小于 16 GB 的实例上禁用混合缓冲池。

在 Windows 上格式化 PMEM 设备时，使用可用于 NTFS 的最大分配单元大小（Windows Server 2019 中为 2 MB）并确保已为 DAX（直接访问）格式化该设备。

文件大小应为 2 MB 的倍数（模数 2 MB 应等于零）。

如果将混合缓冲池的服务器范围的设置设为禁用，则任何用户数据库都不会使用混合缓冲池。

如果启用了“混合缓冲区”的服务器范围的设置，则可通过以下步骤为各用户数据库在数据库作用域级别禁用混合缓冲池，从而禁止这些用户数据库使用混合缓冲池。
