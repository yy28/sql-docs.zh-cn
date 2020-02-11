---
title: 服务器属性（“处理器”页）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql12.swb.serverproperties.processor.f1
ms.assetid: cc1581a2-492b-41f0-bda5-17909b65c4f7
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: aae800226a585f7a29334887829be2a09277a004
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62809147"
---
# <a name="server-properties-processors-page"></a>服务器属性（“处理器”页）
  使用此页可以查看或修改处理器选项。 只有在安装了多个处理器时，才可以启用处理器关联设置。  
  
## <a name="options"></a>选项  
 **处理器关联**  
 将处理器分配给特定的线程，以消除处理器重新加载和减少处理器之间的线程迁移。 有关详细信息，请参阅 [关联掩码服务器配置选项](affinity-mask-server-configuration-option.md)。  
  
 **I/o 相关性**  
 将[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]磁盘 i/o 绑定到指定的 cpu 子集。 有关详细信息，请参阅 [关联 I/O 掩码服务器配置选项](affinity-input-output-mask-server-configuration-option.md)。  
  
 **自动设置所有处理器的处理器关联掩码**  
 允许 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 设置处理器关联。  
  
 **自动设置所有处理器的 i/o 关联掩码**  
 允许 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 设置 I/O 关联。  
  
 **最大工作线程数**  
 如果为 0，则允许 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 动态设置工作线程数。 对于大多数系统而言，此为最佳设置。 但是，根据您的系统配置，将此选项设置为特定值有时可以提高性能。 有关详细信息，请参阅 [配置 max worker threads 服务器配置选项](configure-the-max-worker-threads-server-configuration-option.md)。  
  
 **提升 SQL Server 优先级**  
 指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 是否应当以比同一计算机上的其他进程更高的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 计划优先级运行。 有关详细信息，请参阅 [配置 priority boost 服务器配置选项](configure-the-priority-boost-server-configuration-option.md)。  
  
 **使用 Windows 纤程（轻型池）**  
 使用 Windows 纤程代替 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务的线程。 请注意，此选项仅适用于 Windows 2003 Server Edition。 有关详细信息，请参阅 [lightweight pooling 服务器配置选项](lightweight-pooling-server-configuration-option.md)。  
  
 **配置值**  
 显示此窗格上选项的配置值。 如果更改了这些值，请单击 **“运行值”** 以查看更改是否已生效。 如果尚未生效，则必须首先重新启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的实例。  
  
 **“运行值”**  
 查看此窗格上选项的当前运行值。 这些值是只读的。  
  
## <a name="see-also"></a>另请参阅  
 [服务器配置选项 (SQL Server)](server-configuration-options-sql-server.md)  
  
  
