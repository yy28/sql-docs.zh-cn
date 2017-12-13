---
title: "Filestore 属性 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- Income property
- InitialBonus property
- PercentScanPerPrice property
- FileStore properties
- BackgroundTrimCost property
- Tax property
- PerformanceTrace property
- MinimumBalance property
- UnbufferedThreshold property
- BackgroundTrimAmount property
- MaximumBalance property
- MemoryLimitMin property
- MemoryLimit property
ms.assetid: 580cf0aa-7425-4d48-aa8d-128f5b488fcd
caps.latest.revision: "19"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 55928f4471506b5379d2082632999ef4fc4d6f28
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2017
---
# <a name="filestore-properties"></a>FileStore 属性
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)][!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]支持下表中列出的文件存储服务器属性。 这些属性都是高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改这些属性。 有关更多服务器属性以及如何设置这些属性的详细信息，请参阅 [Analysis Services 中的服务器属性](../../analysis-services/server-properties/server-properties-in-analysis-services.md)。  
  
 **适用于：** 多维和表格服务器模式  
  
## <a name="properties"></a>属性  
 **MemoryLimit**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **MemoryLimitMin**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **PercentScanPerPrice**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **PerformanceTrace**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **RandomFileAccessMode**  
 这是一项布尔属性，指示是否在随机文件访问模式下访问数据库文件和缓存文件。 默认情况下禁用此属性。 默认情况下，在打开分区数据文件以便进行读访问时，Analysis Services 不设置随机文件访问标志。  
  
 在高端系统上，特别是在具有大型内存资源和多个 NUMA 节点的系统上，使用随机文件访问可能会给您带来好处。 在随机访问模式中，Windows 会绕过将数据从磁盘读入系统文件缓存的页映射操作，因此会降低对缓存的争用。  
  
 您将需要执行比较测试，以便确定查询性能是否由于更改此属性而得到改善。 有关执行比较测试的最佳做法，包括清除缓存和避免常见错误，请参阅 [SQL Server 2008 R2 Analysis Services 操作指南](http://go.microsoft.com/fwlink/?LinkID=225539)。 有关权衡使用此属性的其他信息，请参阅 [http://support.microsoft.com/kb/2549369](http://support.microsoft.com/kb/2549369)。  
  
 若要在 Management Studio 中查看或修改此属性，请在服务器属性页中启用高级属性列表。 您也可以在 msmdsrv.ini 文件中更改该属性。 建议在设置该属性后重新启动服务器；否则，将会继续在之前的模式下访问已打开的文件。  
  
 **UnbufferedThreshold**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
## <a name="memory-model-category"></a>内存模型类别  
 **MemoryModel\Tax**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **MemoryModel\Income**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **MemoryModel\MaximumBalance**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **MemoryModel\MinimumBalance**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **MemoryModel\InitialBonus**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
## <a name="see-also"></a>另请参阅  
 [Analysis Services 中的服务器属性](../../analysis-services/server-properties/server-properties-in-analysis-services.md)   
 [确定 Analysis Services 实例的服务器模式](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  
