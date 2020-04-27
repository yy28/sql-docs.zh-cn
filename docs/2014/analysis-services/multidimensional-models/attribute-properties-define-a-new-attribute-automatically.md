---
title: 自动定义新属性 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- automatic attribute creation
- attributes [Analysis Services], creating
ms.assetid: 208a050a-5e2f-470c-b645-8d835e123db7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5f77148e039e61c080d0eae4e4ab7cad06ef050d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66077309"
---
# <a name="define-a-new-attribute-automatically"></a>自动定义新属性
  可以在维度设计器中使用拖放编辑功能，在某个维度中创建新属性。  
  
### <a name="to-create-a-new-attribute-automatically"></a>自动创建新的属性  
  
1.  在维度设计器中，打开要在其中创建属性的维度。  
  
2.  在 **“维度结构”** 选项卡上，从 **“数据源视图”** 窗格内要将属性绑定到的表中，选择相应的列，然后将该列拖至 **“属性”** 窗格。  
  
     [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将创建新属性，其名称与其绑定到的列的名称相同。 如果多个属性使用相同的列，则 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 在属性名称后面加一个数字。  
  
## <a name="see-also"></a>另请参阅  
 [多维模型中的维度](dimensions-in-multidimensional-models.md)   
 [维度特性属性参考](dimension-attribute-properties-reference.md)  
  
  
