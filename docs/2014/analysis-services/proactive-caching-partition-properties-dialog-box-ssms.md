---
title: 主动缓存（"分区属性" 对话框）（SSMS） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.sqlserverstudio.partitionproperties.proactivecaching.f1
ms.assetid: ecba72a3-703f-4ede-9d85-9a3318a749e5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: cb486ec383ab6fa1684bd9d0e9b8f6bc67631eee
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66070706"
---
# <a name="proactive-caching-partition-properties-dialog-box-ssms"></a>主动缓存（“分区属性”对话框）(SSMS)
  对于 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据库中的多维数据集，可以在 SQL Server Management Studio 中使用“分区属性”对话框的“主动缓存”页，为其度量值组中的分区设置存储和主动缓存属性。********  
  
## <a name="options"></a>选项  
 **标准设置**  
 选择此选项可启用 **“标准设置滑块”** ，并使用存储模式和主动缓存功能的预定义设置。  
  
 **“标准设置滑块”**  
 设置为下表所列的预定义设置之一：  
  
|设置|说明|  
|-------------|-----------------|  
|**实时 ROLAP**|选择此设置可以使用以下的存储和主动缓存设置：<br /><br /> ROLAP 存储模式。<br /><br /> 启用主动缓存。<br /><br /> 放弃过时缓存，滞后期为 0 秒。<br /><br /> 使对象立即联机。|  
|**实时 HOLAP**|选择此设置可以使用以下的存储和主动缓存设置：<br /><br /> HOLAP 存储模式。<br /><br /> 启用主动缓存。<br /><br /> 放弃过时缓存，滞后期为 0 秒。<br /><br /> 当数据更改时更新缓存，静默间隔为 0 秒，没有静默覆盖间隔。<br /><br /> 使对象立即联机。|  
|**低滞后时间 MOLAP**|选择此设置可以使用以下的存储和主动缓存设置：<br /><br /> MOLAP 存储模式。<br /><br /> 启用主动缓存。<br /><br /> 放弃过时缓存，滞后期为 30 分钟。<br /><br /> 当数据更改时更新缓存，静默间隔为 10 秒，静默覆盖间隔为 10 分钟。<br /><br /> 当数据更改时更新缓存，静默间隔为 10 秒，静默覆盖间隔为 10 分钟。<br /><br /> 使对象立即联机。|  
|**中等滞后时间 MOLAP**|选择此 useBrings 将对象立即联机。<br /><br /> 以下存储和主动缓存设置：<br /><br /> MOLAP 存储模式。<br /><br /> 启用主动缓存。<br /><br /> 放弃过时缓存，滞后期为 4 小时。<br /><br /> 当数据更改时更新缓存，静默间隔为 10 秒，静默覆盖间隔为 10 分钟。<br /><br /> 使对象立即联机。|  
|**自动 MOLAP**|选择此设置可以使用以下的存储和主动缓存设置：<br /><br /> MOLAP 存储模式。<br /><br /> 启用主动缓存。<br /><br /> 当数据更改时更新缓存，静默间隔为 0 秒，没有静默覆盖间隔。|  
|**预定的 MOLAP**|选择此设置可以使用以下的存储和主动缓存设置：<br /><br /> MOLAP 存储模式<br /><br /> 启用主动缓存<br /><br /> 定期更新缓存，重新生成间隔为 1 天|  
|**MOLAP**|选择此设置可以使用以下的存储和主动缓存设置：<br /><br /> MOLAP 存储模式。|  
  
 **自定义设置**  
 选择此项可以显式地设置存储模式、主动缓存和通知选项。  
  
 **选项**  
 单击此项可显示 **“存储选项”** 对话框，以显式地设置存储模式、主动缓存和通知选项。 有关****“存储选项”对话框的详细信息，请参阅[“存储选项”对话框（Analysis Services - 多维数据）](storage-options-dialog-box-analysis-services-multidimensional-data.md)。  
  
## <a name="see-also"></a>另请参阅  
 [主动缓存 &#40;分区&#41;](multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md)   
 ["分区属性" 对话框 &#40;SSMS&#41;](partition-properties-dialog-box-ssms.md)   
 [选择 &#40;分区属性 "对话框&#41; &#40;SSMS&#41;](selection-partition-properties-dialog-box-ssms.md)   
 ["常规 &#40;分区属性" 对话框&#41; &#40;SSMS&#41;](general-partition-properties-dialog-box-ssms.md)   
 [&#40;SSAS 的多维数据集、分区和维度处理的错误配置-多维&#41;](multidimensional-models/error-configuration-for-cube-partition-and-dimension-processing.md)  
  
  
