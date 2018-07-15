---
title: 自动定义新属性 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- automatic attribute creation
- attributes [Analysis Services], creating
ms.assetid: 208a050a-5e2f-470c-b645-8d835e123db7
caps.latest.revision: 33
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 74b4e1950e6a31675994b7cae1562ff92a56de4a
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37299187"
---
# <a name="define-a-new-attribute-automatically"></a>自动定义新属性
  可以在维度设计器中使用拖放编辑功能，在某个维度中创建新属性。  
  
### <a name="to-create-a-new-attribute-automatically"></a>自动创建新的属性  
  
1.  在维度设计器中，打开要在其中创建属性的维度。  
  
2.  在 **“维度结构”** 选项卡上，从 **“数据源视图”** 窗格内要将属性绑定到的表中，选择相应的列，然后将该列拖至 **“属性”** 窗格。  
  
     [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将创建新属性，其名称与其绑定到的列的名称相同。 如果多个属性使用相同的列，则 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 在属性名称后面加一个数字。  
  
## <a name="see-also"></a>请参阅  
 [多维模型中的维度](dimensions-in-multidimensional-models.md)   
 [维度特性属性参考](dimension-attribute-properties-reference.md)  
  
  
