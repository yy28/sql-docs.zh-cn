---
title: Analysis Services 文件存储属性 |Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0319006e3ca6d69416746d802c20164da309b188
ms.sourcegitcommit: 8a64c59c5d84150659a015e54f8937673cab87a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2018
ms.locfileid: "53071974"
---
# <a name="filestore-properties"></a>FileStore 属性
[!INCLUDE[ssas-appliesto-sqlas-all-aas](../../includes/ssas-appliesto-sqlas-all-aas.md)]

  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 支持`filestore`下表中列出的服务器属性。 这些属性都是高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改这些属性。 有关更多服务器属性以及如何设置这些属性的详细信息，请参阅 [Analysis Services 中的服务器属性](../../analysis-services/server-properties/server-properties-in-analysis-services.md)。  
  
 **适用范围：** 多维和表格服务器模式  
  
## <a name="properties"></a>Properties  
 **MemoryLimit**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **MemoryLimitMin**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **PercentScanPerPrice**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **PerformanceTrace**  
 这是一项高级属性，除非有 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 技术支持的指导，否则不应更改此属性。  
  
 **RandomFileAccessMode**  
 这是一项布尔属性，指示是否在随机文件访问模式下访问数据库文件和缓存文件。 默认情况下禁用此属性。 默认情况下，服务器不设置随机文件访问标志，打开分区数据文件的读取访问权限时。  
  
 在高端系统上，特别是在具有大型内存资源和多个 NUMA 节点的系统上，使用随机文件访问可能会给您带来好处。 在随机访问模式下，Windows 会绕过页映射操作的数据从磁盘读入系统文件缓存，因此可降低对缓存的争用。  
  
 您将需要执行比较测试，以便确定查询性能是否由于更改此属性而得到改善。 有关执行比较测试的最佳做法，包括清除缓存和避免常见错误，请参阅 [SQL Server 2008 R2 Analysis Services 操作指南](http://go.microsoft.com/fwlink/?LinkID=225539)。 有关权衡使用此属性的其他信息，请参阅[ http://support.microsoft.com/kb/2549369 ](http://support.microsoft.com/kb/2549369)。  
  
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
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 中的服务器属性](../../analysis-services/server-properties/server-properties-in-analysis-services.md)   
 [确定 Analysis Services 实例的服务器模式](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  
