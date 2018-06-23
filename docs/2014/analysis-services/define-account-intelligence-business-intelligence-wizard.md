---
title: 定义帐户智能 （商业智能向导） |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.asvs.biwizard.acctintelligence.mapaccounttype.f1
ms.assetid: fe4c204b-1031-4ac4-9916-8052ce2301cc
caps.latest.revision: 20
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 3b55d270b9b7ae2a2094c24e0f71bdcd0f72a0ee
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36125727"
---
# <a name="define-account-intelligence-business-intelligence-wizard"></a>定义帐户智能（商业智能向导）
  可以使用 **“定义帐户智能”** 页，将 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例上定义的帐户类型映射到特定数据源（提供帐户维度数据）中的源表所定义的帐户类型。  
  
> [!NOTE]  
>  如果将维度属性映射到“配置维度属性”页上的“帐户类型”属性时，将显示此页。  
  
## <a name="options"></a>“常规”  
 **源表帐户类型**  
 显示的值包含在分配给“配置维度属性”页上的“帐户类型”属性类型的维度属性中。  
  
 **内置帐户类型**  
 选择在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例中定义的帐户类型，该帐户类型将映射到源表中的帐户类型。  
  
 下表列出了在 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 实例中定义的帐户类型：  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**资产**|在特定时间拥有的物品的价值。|  
|**平衡**|在特定时间某物的计数。|  
|**费用**|所花费的价值。|  
|**流**|事物的增量计数。|  
|**收入**|收到的价值。|  
|**负债**|在特定时间所拖欠的价值。|  
|**统计**|某事物的计算比率，或者未聚合的某事物的计数。|  
  
## <a name="see-also"></a>请参阅  
 [商业智能向导的 F1 帮助](business-intelligence-wizard-f1-help.md)   
 [多维数据集设计器&#40;Analysis Services-多维数据&#41;](cube-designer-analysis-services-multidimensional-data.md)   
 [维度设计器&#40;Analysis Services-多维数据&#41;](dimension-designer-analysis-services-multidimensional-data.md)  
  
  