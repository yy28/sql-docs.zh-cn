---
title: 选择成员 （商业智能向导） |Microsoft 文档
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
- sql12.asvs.biwizard.currencyconversion.memberconversion.f1
ms.assetid: 1a147461-d594-41e7-a41d-09d2d003e1e0
caps.latest.revision: 25
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 75cd6c2aeca77d55b4ec66baa3dccb4c77f4a66e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36125456"
---
# <a name="select-members-business-intelligence-wizard"></a>选择成员（商业智能向导）
  可以使用 **“选择成员”** 页，确定商业智能向导应对哪些成员应用 **“设置货币换算选项”** 页上指定的货币换算功能。  
  
> [!NOTE]  
>  如果从维度设计器或者通过在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]的解决方案资源管理器中右键单击维度启动了商业智能向导，则将不会显示此页。  
  
## <a name="options"></a>“常规”  
 **度量值维度**  
 选择此选项可以对多维数据集中的一个或多个度量值应用货币换算功能。  
  
 如果选择此选项，网格中将显示下表中所列出的选项：  
  
|选项|Description|  
|------------|-----------------|  
|**内置的度量值类型**|选择此选项可为指定的度量值包括货币换算功能。|  
|**度量值**|从包含汇率的比率度量值组中，选择在换算从“内置度量值类型”中选择的度量值时要使用的度量值。|  
  
 **帐户层次结构**  
 选择此选项可以对多维数据集中所包括帐户维度的帐户层次结构中的一个或多个成员应用货币换算功能。 帐户层次结构是帐户内的层次结构维度其`Type`属性设置为*帐户*。  
  
 如果选择此选项，网格中将显示下表中所列出的选项：  
  
|选项|Description|  
|------------|-----------------|  
|**帐户成员**|选择此选项可为帐户层次结构中指定的成员包括货币换算功能。|  
|**度量值**|从包含汇率的比率度量值组中，选择在换算 **“帐户成员”** 中所选成员的度量值时要使用的度量值。|  
  
 **基于类型的帐户层次结构**  
 选择要应用于的所有成员的货币换算功能属性帐户层次结构中其`Type`属性设置为指定的帐户类型。  
  
 如果选择此选项，网格中将显示下表中所列出的选项：  
  
|选项|Description|  
|------------|-----------------|  
|**帐户类型**|选择此选项可为指定的帐户类型包括货币换算功能。|  
|**度量值**|对于使用 **“帐户类型”** 中所选择的帐户类型的属性，从包含汇率的比率度量值组中，选择在换算这些属性的成员的度量值时要使用的度量值。|  
  
## <a name="see-also"></a>请参阅  
 [商业智能向导的 F1 帮助](business-intelligence-wizard-f1-help.md)   
 [多维数据集设计器&#40;Analysis Services-多维数据&#41;](cube-designer-analysis-services-multidimensional-data.md)   
 [维度设计器&#40;Analysis Services-多维数据&#41;](dimension-designer-analysis-services-multidimensional-data.md)  
  
  