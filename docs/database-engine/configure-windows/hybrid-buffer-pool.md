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
author: DBArgenis
ms.author: argenisf
manager: craigg
ms.openlocfilehash: 5e36363347d9d491f541715dffa3cce731cc1efc
ms.sourcegitcommit: be09f0f3708f2e8eb9f6f44e632162709b4daff6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/21/2019
ms.locfileid: "65993552"
---
# <a name="hybrid-buffer-pool"></a>混合缓冲池
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

混合缓冲池使数据库引擎能够直接访问存储在持久内存 (PMEM) 设备上的数据库文件中的数据页。 [!INCLUDE[sqlv15](../../includes/sssqlv15-md.md)] 中引入了此功能。

在没有 PMEM 的传统系统中，SQL Server 将数据页缓存在缓冲池中。 使用混合缓冲池，SQL Server 会跳过将页面副本执行到缓冲池的基于 DRAM 的部分，直接在 PMEM 设备上的数据库文件上访问该页面。 使用内存映射 I/O (MMIO)（也称为 SQL Server 中数据文件的“启用 (enlightenment)”）来访问 PMEM 设备上用于混合缓冲池的数据文件  。

只能在 PMEM 设备上直接访问干净页。 当页面被标记为脏时，它会先被复制到 DRAM 缓冲池，最后被写回 PMEM 设备并再次标记为干净。 这将在常规检查点操作期间发生。

混合缓冲池功能同时适用于 Windows 和 Linux。 必须使用支持 DAX (DirectAccess) 的文件系统来格式化 PMEM 设备。 XFS、EXT4、NTFS 和 ReFS 文件系统都支持 DAX。 当连接、还原或创建了新数据库或启用了混合缓冲池功能时，SQL Server 会自动检测数据文件是否驻留在格式正确的 PMEM 设备上，并在启动时在用户空间中执行内存映射。

有关 Windows Server 对 PMEM 的支持（也称为存储类内存 (SCM)）的更多信息，请参阅[在 Windows Server 上部署持久内存](/windows-server/storage/storage-spaces/deploy-pmem/)。

有关在 Linux 上为 PMEM 设备配置 SQL Server 的更多信息，请参阅[部署持久性内存](../../linux/sql-server-linux-configure-pmem.md)）。

## <a name="enable-hybrid-buffer-pool"></a>启用混合缓冲池

[!INCLUDE[sqlv15](../../includes/sssqlv15-md.md)] 引入了动态数据语言 (DDL) 来控制混合缓冲池。

以下示例为 SQL Server 实例启用混合缓冲池：

```sql
ALTER SERVER CONFIGURATION SET MEMORY_OPTIMIZED HYBRID_BUFFER_POOL = ON;
```

默认情况下，混合缓冲池在实例范围内设置为禁用。

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

默认情况下，混合缓冲池在实例范围内设置为禁用。

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

在 Windows 上格式化 PMEM 设备时，使用可用于 NTFS 或 ReFS的最大分配单元大小（Windows Server 2019 中为 2MB）并确保已为 DAX（直接访问）格式化该设备。

如果将混合缓冲池的服务器范围的设置设为禁用，则任何用户数据库都不会使用混合缓冲池。

如果启用了“混合缓冲区”的服务器范围的设置，则可通过以下步骤为各用户数据库在数据库作用域级别禁用混合缓冲池，从而禁止这些用户数据库使用混合缓冲池。