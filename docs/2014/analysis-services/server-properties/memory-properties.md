---
title: 内存属性 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- LowMemoryLimit property
- MinimumAllocatedMemory property
- MidMemoryPrice property
- MemoryHeapType property
- memory [Analysis Services]
- DefaultPagesCountToReuse property
- TotalMemoryLimit property
- SessionMemoryLimit property
- VirtualMemoryLimit property
- WaitCountIfHighMemory property
- HighMemoryPrice property
- HeapTypeForObjects property
ms.assetid: 085f5195-7b2c-411a-9813-0ff5c6066d13
author: minewiskan
ms.author: owend
ms.openlocfilehash: 4f1ffd3bd5a41b141e81fcb37b064e5cc4f35f84
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84940633"
---
# <a name="memory-properties"></a>内存属性
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 支持下表中列出的服务器内存属性。 有关设置这些属性的指南，请参阅 [SQL Server 2008 R2 Analysis Services 操作指南](https://go.microsoft.com/fwlink/?LinkID=225539)。  
  
 介于 1 和 100 之间的值表示 **“物理总内存”** 或 **“虚拟地址空间”** 的百分比（以二者中少者计）。 超过 100 的值表示内存限制（以字节为单位）。  
  
 **适用于：** 多维和表格服务器模式，除非另外说明。  
  
## <a name="properties"></a>“属性”  
 `LowMemoryLimit`  
 一个有符号的 64 位双精度浮点数属性，可定义服务器内存不足所在的点，以总物理内存的百分比表示。 达到此限制时，实例将通过关闭过期会话以及卸载未使用的计算从缓存中缓慢清除内存。 服务器不会在未超过此限制的情况下释放内存。 默认值为 65；这指示最低内存限制为物理内存或虚拟地址空间的 65%（以二者中少者计）。  
  
 `TotalMemoryLimit`  
 定义一个阈值，当达到此阈值时，服务器会更主动地释放内存。 默认值为物理内存或虚拟地址空间的 80%（以二者中少者计）。  
  
 请注意，`TotalMemoryLimit` 必须始终小于 `HardMemoryLimit`。  
  
 `HardMemoryLimit`  
 指定一个内存阈值，达到该阈值后实例会主动终止活动用户会话以减少内存的使用量。 所有终止的会话都将收到关于因内存压力而被取消的错误。 默认值为零 (0)，这意味着 `HardMemoryLimit` 将设置为 `TotalMemoryLimit` 和系统的物理总内存之间的中间值；如果系统的物理内存大于进程的虚拟地址空间，则改用虚拟地址空间来计算 `HardMemoryLimit`。  
  
 `VirtualMemoryLimit`  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 `VertiPaqPagingPolicy`  
 指定服务器内存不足时的分页行为。 以下是有效值：  
  
 零（**0**）禁用分页。 如果内存不足，处理将失败，同时显示内存不足错误。 如果禁用分页，必须向服务帐户授予 Windows 特权。 有关说明，请参阅[配置服务帐户 (Analysis Services)](../instances/configure-service-accounts-analysis-services.md)。  
  
 **1** 为默认值。 该属性支持使用操作系统页文件 (pagefile.sys) 分页到磁盘。  
  
 在 `VertiPaqPagingPolicy` 设置为 1 时，处理不大可能由于内存限制而失败，因为服务器将尝试使用您指定的方法对磁盘进行分页。 设置 `VertiPaqPagingPolicy` 属性并不会确保内存错误永远不会发生。 在下列条件下仍然可能会发生内存不足错误：  
  
-   没有足够的内存来用于所有字典。 在处理过程中，Analysis Services 会在内存中锁定每一列的字典，并且所有这些列所占用的内存不能超过为 `VertiPaqMemoryLimit` 指定的值。  
  
-   没有足够的虚拟地址空间来容纳这个过程。  
  
 为了解决永久性的内存不足错误，您可以尝试重新设计模型以便减少需要处理的数据量，或者可以向计算机添加更多的物理内存。  
  
 仅适用于表格服务器模式。  
  
 `VertiPaqMemoryLimit`  
 如果允许分页到磁盘，此属性指定内存占用达到何种程度（表示为内存总量的百分比）才开始分页。 默认值为 60。 如果内存占用不超过 60%，则服务器不会分页到磁盘。  
  
 此属性依赖于 `VertiPaqPagingPolicyProperty`，该属性必须设置为 1 才能进行分页。  
  
 仅适用于表格服务器模式。  
  
 `HighMemoryPrice`  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 `MemoryHeapType`  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 仅适用于多维服务器模式。  
  
 `HeapTypeForObjects`  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 仅适用于多维服务器模式。  
  
 `DefaultPagesCountToReuse`  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 `HandleIA64AlignmentFaults`  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 `MidMemoryPrice`  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 `MinimumAllocatedMemory`  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 `PreAllocate`  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 `SessionMemoryLimit`  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 `WaitCountIfHighMemory`  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
## <a name="see-also"></a>另请参阅  
 [在 Analysis Services 中配置服务器属性](server-properties-in-analysis-services.md)   
 [确定 Analysis Services 实例的服务器模式](../instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  
