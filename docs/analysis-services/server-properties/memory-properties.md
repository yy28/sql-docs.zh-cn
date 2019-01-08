---
title: Analysis Services 内存属性 |Microsoft Docs
ms.date: 10/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 763c085e9a4dbc6ecb459ffcd17f5185531b98fb
ms.sourcegitcommit: 8a64c59c5d84150659a015e54f8937673cab87a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2018
ms.locfileid: "53071994"
---
# <a name="memory-properties"></a>内存属性
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  Analysis Services 预分配适度的在启动时的内存，因此可以立即处理请求。 可随着查询和处理工作负荷增加而分配更多内存。 
  
  通过指定配置设置，可以控制释放内存时的阈值。 例如， **HardMemoryLimit** 设置指定自行强制实施的内存不足条件（默认情况下，此阈值未启用），在此条件下会彻底拒绝新请求，直到有更多资源可用。

若要了解有关每个 SQL Server Analysis Services 实例使用的版本的最大内存的详细信息，请参阅[各版本和支持的 SQL Server 功能](../../sql-server/editions-and-components-of-sql-server-2017.md#Cross-BoxScaleLimits)。
  
 除非另有说明，以下设置将适用于表格和多维服务器。  
 
## <a name="default-memory-configuration"></a>默认内存配置

在默认配置下，每个 Analysis Services 实例分配的少量内存 (40 MB 到 50 MB) 在启动时，即使实例处于空闲状态。 

请记住，配置设置是基于每个实例的。 如果在相同硬件上运行 Analysis Services 的多个实例（如表格和多维实例），则每个实例都独立于其他实例来分配自己的内存。

下表简要介绍使用频率较高的内存设置（在参考部分中提供了详细信息）。 仅当 Analysis Services 争夺内存与其他应用程序在同一服务器上配置这些设置：

设置 | Description
--------|------------
LowMemoryLimit | 对于多维实例，这是阈值下限，达到该阈值时，服务器首先开始释放分配给不常使用的对象的内存。
VertiPaqMemoryLimit | 对于表格实例，这是阈值下限，达到该阈值时，服务器首先开始释放分配给不常使用的对象的内存。
TotalMemoryLimit | 这是阈值上限，达到该阈值时，Analysis Services 开始更积极地释放内存以便为正在执行的请求以及新的高优先级请求腾出空间。 
HardMemoryLimit | 这是另一个阈值，达到该阈值时，由于内存压力，Analysis Services 开始彻底拒绝请求。 
 
## <a name="property-reference"></a>属性参考

除非另行指定，否则以下属性同时适用于表格和多维模式。

 介于 1 和 100 之间的值表示 **“物理总内存”** 或 **“虚拟地址空间”** 的百分比（以二者中少者计）。 超过 100 的值表示内存限制（以字节为单位）。
  
 **LowMemoryLimit**  
 一个有符号的 64 位双精度浮点数属性，用于定义 Analysis Services 开始释放对于低优先级的对象，如不常使用的缓存内存的第一个阈值。 一旦分配了内存，服务器便不会释放低于此限制的内存。 默认值为 65；这指示最低内存限制为物理内存或虚拟地址空间的 65%（以二者中少者计）。  
  
 **TotalMemoryLimit**  
 定义一个阈值，达到该阈值时，服务器会释放内存以便为其他请求腾出空间。 达到此限制时，实例将通过关闭过期会话以及卸载未使用的计算从缓存中缓慢清除内存。 默认值为物理内存或虚拟地址空间的 80%（以二者中少者计）。 **TotalMemoryLimit**必须始终小于**HardMemoryLimit**  
  
 **HardMemoryLimit**  
 指定一个内存阈值，达到该阈值后实例会主动终止活动用户会话以减少内存的使用量。 所有终止的会话将收到关于内存压力被取消的错误。 默认值为零 (0)，这意味着 **HardMemoryLimit** 将设置为 **TotalMemoryLimit** 和系统的物理总内存之间的中间值；如果系统的物理内存大于进程的虚拟地址空间，则改用虚拟地址空间来计算 **HardMemoryLimit**。  

**QueryMemoryLimit**   
仅 azure Analysis Services 中。 高级的属性来控制在查询期间的临时结果可以使用的内存量。 仅适用于 DAX 度量值和查询。 针对多维模式服务器的 MDX 查询不使用此限制。 它不考虑查询所使用的常规内存分配。 中的指定百分比。 默认值为 0 时表示指定没有限制。

 **VirtualMemoryLimit**  
  这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **VertiPaqPagingPolicy**  
  仅针对表格实例，指定服务器内存不足时的分页行为。 以下是有效值：  
  
设置  |Description  
---------|---------
**0**     |  （默认值为 Azure Analysis Services）禁用分页。 如果内存不足，处理将失败，同时显示内存不足错误。 如果禁用分页，必须向服务帐户授予 Windows 特权。 有关说明，请参阅[配置服务帐户 (Analysis Services)](../../analysis-services/instances/configure-service-accounts-analysis-services.md)。 
**1**     |  （SQL Server Analysis Services 的默认值）该属性允许使用操作系统页文件 (pagefile.sys) 分页到磁盘。   
  
设置为 1 时，处理不大可能由于内存限制而失败，因为服务器将尝试使用指定的方法对磁盘进行分页。 设置 **VertiPaqPagingPolicy** 属性并不会确保内存错误永远不会发生。 在下列条件下仍然可能会发生内存不足错误：  
  
-   没有足够的内存来用于所有字典。 在处理期间，服务器将锁定每一列的字典在内存中，并且所有这些不能为多个指定的值**VertiPaqMemoryLimit**。  
  
-   没有足够的虚拟地址空间来容纳这个过程。  
  
 为了解决永久性的内存不足错误，您可以尝试重新设计模型以便减少需要处理的数据量，或者可以向计算机添加更多的物理内存。  
  
 **VertiPaqMemoryLimit**  
 仅针对表格实例，如果允许对磁盘进行分页，此属性指定内存占用达到何种程度（表示为内存总量的百分比）才开始分页。 默认值为 60。 如果内存占用不超过 60%，则服务器不会分页到磁盘。 此属性依赖于 **VertiPaqPagingPolicyProperty**，该属性必须设置为 1 才能进行分页。  
  
 **HighMemoryPrice**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **MemoryHeapType**  
  这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。 SQL Server 2016 SP1 及更高版本的 Analysis Services 中的有效值如下所示：
  
  设置 | Description
--------|------------
**-1** | （默认）Automatic。 该引擎将决定具体使用哪一个。
**1** | Analysis Services HEAP。
**2** | Windows LFH。
**5** | 混合分配器。 此分配器将使用为 Windows LFH \<= 16 KB 的分配和 AS 堆 > 16 KB 的分配。 
**6** | Intel TBB 分配器。 在 SQL Server 2016 SP1（及更高版本）的 Analysis Services 中可用。
  
  
 **HeapTypeForObjects**  
  这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。 以下是有效值：
  
   设置 | Description
--------|------------
**-1** | （默认）Automatic。 该引擎将决定具体使用哪一个。
**0** | Windows LFH 堆。
**1** | Analysis Services 槽分配器。
**3** | 每个对象都有其自己的 Analysis Services 堆。

 
 **DefaultPagesCountToReuse**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **HandleIA64AlignmentFaults**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **MidMemoryPrice**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **MinimumAllocatedMemory**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **PreAllocate**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **SessionMemoryLimit**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **WaitCountIfHighMemory**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 中的服务器属性](../../analysis-services/server-properties/server-properties-in-analysis-services.md)   
 [确定 Analysis Services 实例的服务器模式](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
