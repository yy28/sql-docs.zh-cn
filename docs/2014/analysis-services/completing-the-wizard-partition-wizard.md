---
title: 完成向导 （分区向导） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.partitionwizard.finish.f1
ms.assetid: 68a4dd5d-94d9-4a02-be31-949a6da0ef51
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 150007626cab59ab7905d369e8e50d7f1b001982
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48102218"
---
# <a name="completing-the-wizard-partition-wizard"></a>完成向导（分区向导）
  可以使用 **“完成向导”** 页，对分区进行命名，为分区定义聚合设计，以及根据需要在完成分区向导后部署并处理分区。  
  
## <a name="options"></a>选项  
 **名称**  
 为新分区键入名称。 如果使用多个表，请输入用于同表名进行组合的前缀以创建各个分区名称。  
  
 **聚合选项**  
 为分区指定聚合选项。  
  
 下表列出了可用的聚合选项：  
  
|选项|Description|  
|------------|-----------------|  
|**现在设计为分区设计聚合**|在分区向导创建新分区之后，为新分区设计聚合。 如果选择此选项，则在分区向导中单击 **“完成”** 后将启动聚合设计向导。 有关聚合设计向导的详细信息，请参阅[聚合设计向导 F1 帮助](aggregation-design-wizard-f1-help.md)。|  
|**稍后设计聚合**|此时只创建分区，而不设计聚合。|  
|**从现有分区复制聚合设计**|将聚合设计从度量值组中的现有分区复制到新分区。 单击此项后， **“复制来源”** 选项即会可用。 使用 **“复制来源”** 选项可以选择要从中复制聚合设计的分区。<br /><br /> 请注意，将来可能要合并的分区必须具有相同的表结构和聚合设计。 若要将新分区与度量值组中的现有分区合并，则应将现有分区的聚合设计复制到新分区中。|  
  
 **立即部署并处理**  
 向“处理位置和存储位置”页上指定的 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例部署分区并对分区进行处理。 在此页上单击 **“完成”** 之后，向导将部署并处理分区。  
  
## <a name="see-also"></a>请参阅  
 [分区&#40;Analysis Services-多维数据&#41;](multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)  
  
  
