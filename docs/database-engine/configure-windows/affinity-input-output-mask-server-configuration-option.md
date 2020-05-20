---
title: affinity I/O mask 服务器配置选项 | Microsoft Docs
ms.custom: ''
ms.date: 07/06/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- affinity I/O mask option
- processor affinity [SQL Server]
- binding processors [SQL Server]
- CPU affinity mask option
ms.assetid: 9950a8c9-9fe0-4003-95df-6f0d1becb0e7
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 0f7af8a254bea06745c85cfdd0442b28eef876de
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2020
ms.locfileid: "68013226"
---
# <a name="affinity-input-output-mask-server-configuration-option"></a>affinity I/O mask 服务器配置选项
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  为了执行多任务， [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 有时会在不同的处理器之间移动进程线程。 虽然从操作系统方面而言，此活动是高效的，但是在高系统负荷的情况下，该活动会降低 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的性能，因为每个处理器缓存都会不断地重新加载数据。 如果将各个处理器分配给特定线程，则通过消除处理器的重新加载需要，可以提高在这些条件下的性能；线程与处理器之间的这种关联称为“处理器关联”。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 通过以下两个关联掩码选项来支持处理器关联： **关联掩码** （也称为 **CPU 关联掩码**）和 **关联 I/O 掩码**。 有关 **关联掩码** 选项的详细信息，请参阅 [关联掩码服务器配置选项](../../database-engine/configure-windows/affinity-mask-server-configuration-option.md)。 对于具有 33 至 64 个处理器的服务器，CPU 和 I/O 关联支持还要求分别使用 [affinity64 掩码服务器配置选项](../../database-engine/configure-windows/affinity64-mask-server-configuration-option.md) 和 [affinity64 I/O 掩码服务器配置选项](../../database-engine/configure-windows/affinity64-input-output-mask-server-configuration-option.md) 。  
  
> [!NOTE]  
>  对具有 33 到 64 个处理器的服务器的关联支持仅在 64 位操作系统上可用。  
  
 **关联 I/O 掩码** 选项将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 磁盘 I/O 绑定到指定的 CPU 子集。 在高端 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 联机事务处理 (OLTP) 环境中，此扩展可以提高 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 线程执行 I/O 的性能。 此增强功能不支持对各个磁盘或磁盘控制器的硬件关联。  
  
 **关联 I/O 掩码** 的值指定了在多处理器计算机中有哪些 CPU 可用于处理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 磁盘 I/O 操作。 该掩码是一个位图，其中最右边的位指定顺序最低的 CPU(0)，该位左边的位指定顺序次低的 CPU(1)，依此类推。 若要配置超过 32 个处理器，请同时设置 **关联 I/O 掩码** 和 **affinity64 I/O 掩码**。  
  
 **关联 I/O 掩码** 值如下所示：  
  
-   在多处理器计算机中，1 字节 **关联 I/O 掩码** 最多可以涵盖 8 个 CPU。  
  
-   在多处理器计算机中，2 字节 **关联 I/O 掩码** 最多可以涵盖 16 个 CPU。  
  
-   在多处理器计算机中，3 字节 **关联 I/O 掩码** 最多可以涵盖 24 个 CPU。  
  
-   在多处理器计算机中，4 字节 **关联 I/O 掩码** 最多可以涵盖 32 个 CPU。  
  
-   若要包括超过 32 个 CPU，请为前 32 个 CPU 配置一个 4 字节 **关联 I/O 掩码** ，并为余下的 CPU 配置最多 4 字节的 **affinity64 I/O** 掩码。  
  
 关联 I/O 模式中某一位的值为 1，则指定相应的 CPU 可执行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 磁盘 I/O 操作；值为 0，则指定相应的 CPU 未安排任何 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 磁盘 I/O 操作。 如果将所有位设置为零或不指定**关联 I/O 掩码**，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 磁盘 I/O 将由任何可处理 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 线程的 CPU 执行。  
  
 因为设置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]“关联 I/O 掩码”  选项是一项专用操作，所以建议只在需要时使用。 大多数情况下，Windows 2000 或 Windows Server 2003 的默认关联就可以提供最佳性能。  
  
 指定**关联 I/O 掩码**选项后，必须将其与**关联掩码**配置选项一起使用。 请勿在“关联 I/O 掩码”  开关和“关联掩码”  选项中启用相同的 CPU。 每个 CPU 对应的位必须处于下列三种状态之一：  
  
-   在“关联 I/O 掩码”  选项和“关联掩码”  选项中均为 0。  
  
-   在“关联 I/O 掩码”  选项中为 1，在“关联掩码”  选项中为 0。  
  
-   在“关联 I/O 掩码”  选项中为 0，在“关联掩码”  选项中为 1。  
  
 “关联 I/O 掩码”  选项是一个高级选项。 如果使用 **sp_configure** 系统存储过程来更改该设置，则仅当“显示高级选项”设置为 1 时，才可以更改**关联 I/O 掩码**。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中，重新配置“关联 I/O 掩码”  选项要求重启 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。  
  
> [!CAUTION]  
>  请不要在 Windows 操作系统中配置 CPU 关联后，还在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中配置关联掩码。 这些设置实现的效果相同，如果配置不一致，则可能会得到意外的结果。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 最好使用 **中的** sp_configure [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]选项配置 CPU 关联。  
  
## <a name="see-also"></a>另请参阅  
 [监视资源使用情况（系统监视器）](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [RECONFIGURE (Transact-SQL)](../../t-sql/language-elements/reconfigure-transact-sql.md)   
 [服务器配置选项 (SQL Server)](../../database-engine/configure-windows/server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
