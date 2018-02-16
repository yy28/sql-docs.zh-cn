---
title: "自动定义新属性 |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- automatic attribute creation
- attributes [Analysis Services], creating
ms.assetid: 208a050a-5e2f-470c-b645-8d835e123db7
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: f56c70ce3d75de8f7be924941df227d1213902c0
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/15/2018
---
# <a name="attribute-properties---define-a-new-attribute-automatically"></a>特性属性-自动定义新属性
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
可以在维度设计器中使用拖放编辑功能，在某个维度中创建新属性。  
  
### <a name="to-create-a-new-attribute-automatically"></a>自动创建新的属性  
  
1.  在维度设计器中，打开要在其中创建属性的维度。  
  
2.  在 **“维度结构”** 选项卡上，从 **“数据源视图”** 窗格内要将属性绑定到的表中，选择相应的列，然后将该列拖至 **“属性”** 窗格。  
  
     [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将创建新属性，其名称与其绑定到的列的名称相同。 如果多个属性使用相同的列，则 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 在属性名称后面加一个数字。  
  
## <a name="see-also"></a>另请参阅  
 [多维模型中的维度](../../analysis-services/multidimensional-models/dimensions-in-multidimensional-models.md)   
 [维度特性属性参考](../../analysis-services/multidimensional-models/dimension-attribute-properties-reference.md)  
  
  
