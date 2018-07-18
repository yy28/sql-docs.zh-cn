---
title: 按 SQL Server 版本划分的计算能力限制 | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- processors [SQL Server], supported
- number of processors supported
- maximum number of processors supported
ms.assetid: cd308bc9-9468-40cc-ad6e-1a8a69aca6c8
caps.latest.revision: 56
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 2893a0fdb04e834e2eeab0343b23888c244fd036
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37157538"
---
# <a name="compute-capacity-limits-by-edition-of-sql-server"></a>Compute Capacity Limits by Edition of SQL Server
  本主题讨论不同 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] 版本的计算能力限制，以及在具有超线程处理器的物理和虚拟化环境中计算能力限制有何不同。  
  
 ![符合计算机能力限制](../../2014/getting-started/media/compute-capacity-limits.gif "符合计算机能力限制")  
  
 下表描述了上图中所用的符号：  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|0..1|零个或 1 个|  
|@shouldalert|恰好一个|  
|1..*|一个或更多|  
|0..*|零个或更多|  
|1..2|1 个或 2 个|  
  
> [!IMPORTANT]  
>  进一步详细阐述：  
>   
>  1.  虚拟机分配有一个或多个虚拟处理器。  
> 2.  一个或多个虚拟处理器被分配给恰好一个虚拟机。  
> 3.  零个或一个虚拟处理器映射到零个或多个逻辑处理器。 当虚拟处理器到逻辑处理器的映射为：  
>   
>      -   一对零，则表示来宾操作系统未使用未绑定逻辑处理器。  
>     -   一对多，则表示过度提交。  
>     -   零对多，则表示主机系统上没有虚拟机，所以虚拟机没有使用逻辑处理器。  
> 4.  插槽映射到零个或多个内核。 当插槽到内核的映射为：  
>   
>      -   一对零，则表示一个空插槽（未安装芯片）。  
>     -   一对一，则表示在插槽中安装了单核芯片（如今非常罕见)。  
>     -   一对多，则表示插槽中安装了多核芯片（典型值为 2、4、8）。  
> 5.  内核映射到一个或两个逻辑处理器。 当内核到逻辑处理器的映射为：  
>   
>      -   一对一，超线程处于关闭状态。  
>     -   一对二，超线程处于打开状态。  
  
 下列定义适用于在本主题中使用的术语：  
  
-   从 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]、操作系统、应用程序或驱动程序的角度理解，线程或逻辑处理器是一种逻辑计算引擎。  
  
-   内核是一个处理器单元，可由一个或多个逻辑处理器组成。  
  
-   物理处理器可包含一个或多个内核。 物理处理器等同于处理器包或插槽。  
  
 具有多个物理处理器的系统或是具有含多个内核和/或超线程的物理处理器的系统，可支持操作系统同时执行多项任务。 每个执行线程都显示为一个逻辑处理器。 例如，如果计算机具有启用超线程的两个四核处理器，且每个内核两个线程，则您有 16 个逻辑处理器：2 个处理器 x 每个处理器 4 个内核 x 每个内核 2 个线程。 值得注意的是：  
  
-   来自超线程内核的单线程的逻辑处理器计算能力不及来自禁用超线程的同一内核的逻辑处理器计算能力。  
  
-   但是超线程内核中两个逻辑处理器的计算能力则超过了禁用超线程的同一内核的计算能力。  
  
 每个 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本都有以下两种计算能力限制：  
  
1.  插槽最大值（与物理处理器/插槽/处理器包相同）。  
  
2.  操作系统报告的内核最大数量。  
  
 这些限制适用于单个 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]实例。 它们代表单个实例将使用的最大计算能力。 它们不会限制可能部署该实例的服务器。 实际上，在同一物理服务器上部署多个 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 实例可以有效使用物理服务器的计算能力，因为更多插槽和/或内核的计算能力超出了下表中的计算能力限制。  
  
 下表指定每个版本的 [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]的单个实例的计算能力限制：  
  
|[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 版本|单个实例使用的最大计算能力 ([!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)][!INCLUDE[ssDE](../includes/ssde-md.md)])|单个实例使用的最大计算能力（AS、RS）1|  
|---------------------------------------|--------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------|  
|Enterprise Edition： 基于内核的许可<sup>1</sup>|操作系统支持的最大值|操作系统支持的最大值|  
|开发人员|操作系统支持的最大值|操作系统支持的最大值|  
|Evaluation|操作系统支持的最大值|操作系统支持的最大值|  
|Business Intelligence|限制为 4 个插槽或 16 核，取二者中的较小值|操作系统支持的最大值|  
|Standard|限制为 4 个插槽或 16 核，取二者中的较小值|限制为 4 个插槽或 16 核，取二者中的较小值|  
|Web|限制为 4 个插槽或 16 核，取二者中的较小值|限制为 4 个插槽或 16 核，取二者中的较小值|  
|Express|限制为 1 个插槽或 4 核，取二者中的较小值|限制为 1 个插槽或 4 核，取二者中的较小值|  
|Express with Tools|限制为 1 个插槽或 4 核，取二者中的较小值|限制为 1 个插槽或 4 核，取二者中的较小值|  
|Express with Advanced Services|限制为 1 个插槽或 4 核，取二者中的较小值|限制为 1 个插槽或 4 核，取二者中的较小值|  
  
 <sup>1</sup> Enterprise Edition 配合服务器 + 客户端访问许可证 (CAL) 基于许可 （对新协议不可用），限制为最多 20 个内核，每个[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]实例。 基于内核的服务器许可模型没有限制。  
  
 在虚拟化环境中，计算能力限制基于逻辑处理器的数目，而不是内核数目，这是因为处理器体系结构对来宾应用程序不可见。  例如，如果服务器的四个插槽中插入了四核处理器，同时该服务器每个内核可支持两个超线程，这样在启用超线程时就有 32 个逻辑处理器，在禁用超线程时只有 16 个逻辑处理器。 这些逻辑处理器可映射到服务器上的虚拟机，而这些虚拟机在该逻辑处理器上的计算负载映射到主机服务器中物理处理器上的执行线程。  
  
 如果每个虚拟处理器的性能很重要，则最好禁用超线程。 用户可以在 BIOS 设置过程中使用 BIOS 的处理器设置启用或禁用超线程，但这通常是服务器范围内的操作，该操作将影响运行在该服务器上的所有工作负荷。 这就可能要求将要运行在虚拟化环境中的工作负荷与会受益于物理操作系统环境中的超线程性能提升的工作负荷分隔开。  
  
## <a name="see-also"></a>请参阅  
 [SQL Server 2014 的版本和组件](../sql-server/editions-and-components-of-sql-server-2016.md)   
 [SQL Server 2014 的版本支持的功能](../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)   
 [SQL Server 的最大容量规范](../sql-server/maximum-capacity-specifications-for-sql-server.md)   
 [SQL Server 2014 安装快速入门](../../2014/getting-started/quick-start-installation-of-sql-server-2014.md)  
  
  
