---
title: 服务器属性（“处理器”页）| Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql13.swb.serverproperties.processor.f1
ms.assetid: cc1581a2-492b-41f0-bda5-17909b65c4f7
author: MikeRayMSFT
ms.author: mikeray
manager: jroth
ms.openlocfilehash: 82e3792b2c92565921f189b4c843e2bacd6e4b49
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66783139"
---
# <a name="server-properties---processors-page"></a>服务器属性 -“处理器”页
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  使用此页可以查看或修改处理器选项。 只有在安装了多个处理器时，才可以启用处理器关联设置。  
  
## <a name="options"></a>选项  
 **处理器关联**  
 将处理器分配给特定的线程，以消除处理器重新加载和减少处理器之间的线程迁移。 有关详细信息，请参阅 [关联掩码服务器配置选项](../../database-engine/configure-windows/affinity-mask-server-configuration-option.md)。  
  
 **I/O 关联**  
 将 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 磁盘 I/O 绑定到指定的 CPU 子集。 有关详细信息，请参阅 [关联 I/O 掩码服务器配置选项](../../database-engine/configure-windows/affinity-input-output-mask-server-configuration-option.md)。  
  
 **自动设置所有处理器的处理器关联掩码**  
 允许 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 设置处理器关联。  
  
 **自动设置所有处理器的 I/O 关联掩码**  
 允许 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 设置 I/O 关联。  
  
 **最大工作线程数**  
 如果为 0，则允许 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 动态设置工作线程数。 对于大多数系统而言，此为最佳设置。 但是，根据您的系统配置，将此选项设置为特定值有时可以提高性能。 有关详细信息，请参阅 [配置 max worker threads 服务器配置选项](../../database-engine/configure-windows/configure-the-max-worker-threads-server-configuration-option.md)。  
  
 **提升 SQL Server 的优先级**  
 指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 是否应当以比同一计算机上的其他进程更高的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 计划优先级运行。 有关详细信息，请参阅 [配置 priority boost 服务器配置选项](../../database-engine/configure-windows/configure-the-priority-boost-server-configuration-option.md)。  
  
 **使用 Windows 纤程(轻型池)**  
 使用 Windows 纤程代替 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务的线程。 请注意，此选项仅适用于 Windows 2003 Server Edition。 有关详细信息，请参阅 [lightweight pooling 服务器配置选项](../../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md)。  
  
 **配置值**  
 显示此窗格上选项的配置值。 如果更改了这些值，请单击 **“运行值”** 以查看更改是否已生效。 如果尚未生效，则必须首先重新启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例。  
  
 **“运行值”**  
 查看此窗格上选项的当前运行值。 这些值是只读的。  
  
## <a name="see-also"></a>另请参阅  
 [服务器配置选项 (SQL Server)](../../database-engine/configure-windows/server-configuration-options-sql-server.md)  
  
  
