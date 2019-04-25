---
title: 选择成员 （商业智能向导） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.biwizard.currencyconversion.memberconversion.f1
ms.assetid: 1a147461-d594-41e7-a41d-09d2d003e1e0
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2d15a32302aa5d7a4ee3ca087944effc017ce8c1
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62747510"
---
# <a name="select-members-business-intelligence-wizard"></a>选择成员（商业智能向导）
  可以使用 **“选择成员”** 页，确定商业智能向导应对哪些成员应用 **“设置货币换算选项”** 页上指定的货币换算功能。  
  
> [!NOTE]  
>  如果从维度设计器或者通过在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]的解决方案资源管理器中右键单击维度启动了商业智能向导，则将不会显示此页。  
  
## <a name="options"></a>选项  
 **度量值维度**  
 选择此选项可以对多维数据集中的一个或多个度量值应用货币换算功能。  
  
 如果选择此选项，网格中将显示下表中所列出的选项：  
  
|Option|Description|  
|------------|-----------------|  
|**内置度量值类型**|选择此选项可为指定的度量值包括货币换算功能。|  
|**度量值**|从包含汇率的比率度量值组中，选择在换算从“内置度量值类型”中选择的度量值时要使用的度量值。|  
  
 **帐户层次结构**  
 选择此选项可以对多维数据集中所包括帐户维度的帐户层次结构中的一个或多个成员应用货币换算功能。 帐户层次结构是在维度的帐户中的层次结构`Type`属性设置为*帐户*。  
  
 如果选择此选项，网格中将显示下表中所列出的选项：  
  
|Option|Description|  
|------------|-----------------|  
|**帐户成员**|选择此选项可为帐户层次结构中指定的成员包括货币换算功能。|  
|**度量值**|从包含汇率的比率度量值组中，选择在换算 **“帐户成员”** 中所选成员的度量值时要使用的度量值。|  
  
 **基于类型的帐户层次结构**  
 选择此选项可以向以下成员应用货币换算功能：帐户层次结构中 `Type` 属性设置为指定帐户类型的特性的所有成员。  
  
 如果选择此选项，网格中将显示下表中所列出的选项：  
  
|Option|Description|  
|------------|-----------------|  
|**帐户类型**|选择此选项可为指定的帐户类型包括货币换算功能。|  
|**度量值**|对于使用 **“帐户类型”** 中所选择的帐户类型的属性，从包含汇率的比率度量值组中，选择在换算这些属性的成员的度量值时要使用的度量值。|  
  
## <a name="see-also"></a>请参阅  
 [商业智能向导的 F1 帮助](business-intelligence-wizard-f1-help.md)   
 [多维数据集设计器&#40;Analysis Services-多维数据&#41;](cube-designer-analysis-services-multidimensional-data.md)   
 [维度设计器&#40;Analysis Services-多维数据&#41;](dimension-designer-analysis-services-multidimensional-data.md)  
  
  
