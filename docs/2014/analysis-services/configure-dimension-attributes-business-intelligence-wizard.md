---
title: 配置维度属性 （商业智能向导） |Microsoft 文档
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
- sql12.asvs.biwizard.acctintelligence.selectattributes.f1
ms.assetid: 3d046e63-bcb1-4ab1-9c37-652463fa68c3
caps.latest.revision: 22
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: e9ce0f7535f111d5c9152304a4e27315f73e5087
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36029137"
---
# <a name="configure-dimension-attributes-business-intelligence-wizard"></a>配置维度属性（商业智能向导）
  可以使用 **“配置维度属性”** 页，将维度属性映射到 [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 用于标识帐户维度属性的属性类型。  
  
## <a name="options"></a>“常规”  
 **维度类型**  
 显示所选维度类型。  
  
> [!NOTE]  
>  此选项将不可用因为`Type`维度属性不能更改为值以外*帐户*帐户维度。  
  
 **维度属性**  
 显示可以映射到维度中现有维度属性的有效属性类型。  
  
 **包括**  
 选中复选框，将维度中相应的属性类型包括在内。  
  
 **特性类型**  
 列出可以映射到维度中现有维度属性的属性类型。  
  
 **维度属性**  
 选择应该映射到相应属性类型的维度属性。  
  
 **将度量值设置为半累加性基于帐户类型**  
 选中此选项，可以将与此维度相关联的每个度量值更改为按帐户类型聚合。  
  
> [!NOTE]  
>  如果从维度设计器或者通过在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]的解决方案资源管理器中右键单击维度启动了商业智能向导，则将不会显示此选项。  
  
## <a name="see-also"></a>请参阅  
 [商业智能向导的 F1 帮助](business-intelligence-wizard-f1-help.md)   
 [多维数据集设计器&#40;Analysis Services-多维数据&#41;](cube-designer-analysis-services-multidimensional-data.md)   
 [维度设计器&#40;Analysis Services-多维数据&#41;](dimension-designer-analysis-services-multidimensional-data.md)  
  
  