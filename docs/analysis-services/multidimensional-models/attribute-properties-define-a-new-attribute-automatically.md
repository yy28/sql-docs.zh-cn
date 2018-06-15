---
title: 自动定义新属性 |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 5368288930526435682723ba8f50d878ff029ce1
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
ms.locfileid: "34021704"
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
  
  
