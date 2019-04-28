---
title: 定义货币换算 （商业智能向导） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.biwizard.currencyconversion.existingscriptpage.f1
ms.assetid: 37dd65b7-9d8d-44ad-b316-96a92c622472
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e7cca289615e94cd4ccfbcee038e002c33700be8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62732307"
---
# <a name="define-currency-conversion-business-intelligence-wizard"></a>定义货币换算（商业智能向导）
  可以使用“定义货币换算”页，查看商业智能向导生成的包含货币换算功能的多维表达式 (MDX) 脚本。 然后可以使用此向导生成的 MDX 脚本覆盖或追加到多维数据集的 MDX 脚本中以前定义的货币换算功能。  
  
> [!NOTE]  
>  只有在商业智能向导检测到多维数据集的 MDX 脚本中至少有一处以前定义的货币换算时，才会显示此页。 在多维数据集的 MDX 脚本中，将嵌入以下注释表示货币换算：  
>   
>  `//<Currency conversion>`  
>   
>  `...`  
>   
>  `[MDX statements for the currency conversion]`  
>   
>  `...`  
>   
>  `//</Currency conversion>`  
>   
>  如果更改或删除这些注释，则商业智能向导可能无法检测到以前定义的任意货币换算。  
  
## <a name="options"></a>选项  
 **新建货币换算脚本**  
 显示由当前商业智能向导会话生成的 MDX 脚本。  
  
 **覆盖现有货币换算脚本**  
 选择此项将用“新建货币换算脚本”中显示的 MDX 脚本覆盖“现有货币换算脚本”中显示的 MDX 脚本。  
  
 **此项后追加**  
 选择此项将把“新建货币换算脚本”中显示的 MDX 脚本追加到“现有货币换算脚本”中显示的 MDX 脚本的末尾。 所追加的脚本将显示为新部分。  
  
 **现有货币换算脚本**  
 选择现有 MDX 脚本的一部分，其中包含要覆盖或追加到以前定义的货币换算功能。  
  
## <a name="see-also"></a>请参阅  
 [商业智能向导的 F1 帮助](business-intelligence-wizard-f1-help.md)   
 [多维数据集设计器&#40;Analysis Services-多维数据&#41;](cube-designer-analysis-services-multidimensional-data.md)   
 [维度设计器&#40;Analysis Services-多维数据&#41;](dimension-designer-analysis-services-multidimensional-data.md)  
  
  
