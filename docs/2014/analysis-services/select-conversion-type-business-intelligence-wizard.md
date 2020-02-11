---
title: 选择转换类型（商业智能向导） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.biwizard.currencyconversion.conversiontype.f1
ms.assetid: 2c664138-e8a1-4c47-8e7d-ee01c57e4692
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ab618eaa2d8d54b08e3d01fa238d19451084eff8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66069621"
---
# <a name="select-conversion-type-business-intelligence-wizard"></a>选择换算类型（商业智能向导）
  可以使用 **“选择换算类型”** 页，为使用多种货币存储的事务定义本地货币和报表货币之间的关系。 本地货币是存储 **“选择度量值”** 页中所选度量值的事务时使用的货币。 报表货币是转换 **“选择度量值”** 页中所选事务时使用的货币。  
  
> [!NOTE]  
>  如果从维度设计器或者通过在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]的解决方案资源管理器中右键单击维度启动了商业智能向导，则将不会显示此页。  
  
## <a name="options"></a>选项  
 **多对多**  
 使用本地货币存储事务。 货币换算功能将此类事务换算成 **“设置货币换算选项”** 页中指定的先导货币，然后换算成一个或多个其他报表货币。  
  
 例如，先导货币可以设置为美元 (USD)，而事实数据表使用欧元 (EUR)、澳大利亚元 (AUD) 和墨西哥比索 (MXN) 来存储交易。 选择此选项可以将这些事务从其指定的本地货币换算成先导货币，然后再次将换算的事务从先导货币换算成指定的报表货币。 结果是可以使用指定的本地货币存储事务，并使用指定的先导货币或 **“指定报表货币”** 页中指定的任一报表货币来查看事务。  
  
 **多对一**  
 使用本地货币存储事务。 货币换算功能将此类事务换算成 **“设置货币换算选项”** 页中指定的先导货币。 该先导货币用作唯一指定的报表货币。  
  
> [!NOTE]  
>  如果选择此选项，则不显示“指定报表货币”**** 页。  
  
 例如，先导货币可以设置为美元 (USD)，而事实数据表使用欧元 (EUR)、澳大利亚元 (AUD) 和墨西哥比索 (MXN) 来存储交易。 选择此选项可以将这些事务从其指定的本地货币换算成先导货币。 结果是可以使用指定的本地货币存储事务，并使用指定的先导货币来查看事务。  
  
 **一对多**  
 使用“设置货币换算选项”**** 页中指定的先导货币存储事务，然后换算成一种或多种其他报表货币。  
  
> [!NOTE]  
>  如果选择此选项，则不显示“定义本地货币引用”**** 页。  
  
 例如，先导货币可以设置为美元 (USD)，而事实数据表使用 USD 来存储事务。 选择此选项可以将这些事务从先导货币换算成指定的报表货币。 结果是可以使用指定的先导货币存储事务，并使用指定的先导货币或 **“指定报表货币”** 页中指定的任一报表货币来查看事务。  
  
## <a name="see-also"></a>另请参阅  
 [商业智能向导的 F1 帮助](business-intelligence-wizard-f1-help.md)   
 [多维数据集设计器 &#40;Analysis Services 多维数据&#41;](cube-designer-analysis-services-multidimensional-data.md)   
 [维度设计器 &#40;Analysis Services 多维数据&#41;](dimension-designer-analysis-services-multidimensional-data.md)  
  
  
