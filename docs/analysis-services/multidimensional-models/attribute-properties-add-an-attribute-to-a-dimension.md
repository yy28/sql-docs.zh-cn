---
title: 向维度中添加属性 |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: multidimensional-models
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e512d61e1417bd5ad794f48289f537777a34f307
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="attribute-properties---add-an--attribute-to-a-dimension"></a>特性属性-向维度中添加属性
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中，可以自动或手动将属性添加到维度中。  
  
 若要自动创建属性，请在 **的维度设计器的** “维度结构” [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]选项卡中，选择要映射到属性的列，然后将该列从 **“数据源视图”** 窗格中拖到 **“属性”** 窗格中。 这样便可创建映射到该列的属性，并为属性分配与该列名称相同的名称。 如果已经存在使用该名称的属性，则 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 会在重复的名称之后添加一个序号后缀，针对第一个重复的名称添加“1”，以此类推。  
  
 若要手动创建属性，请将 **“属性”** 窗格设置为网格视图。 在网格中的最后一行的名称列中，单击**\<新属性 >** 项。 为新属性键入名称。 这样便可创建未映射到列的特性，并且该特性的所有属性都具有默认设置。 在 **的** “属性” [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 窗口中，您可以通过配置新特性的 **KeyColumns** 属性来设置映射。  
  
 有关详细信息，请参阅 [自动定义新属性](../../analysis-services/multidimensional-models/attribute-properties-define-a-new-attribute-automatically.md)、 [将属性绑定到名称列](../../analysis-services/multidimensional-models/attribute-properties-bind-an-attribute-to-a-name-column.md)和 [修改某个特性的 KeyColumn 属性](../../analysis-services/multidimensional-models/attribute-properties-modify-the-keycolumn-property.md)中，可以自动或手动将属性添加到维度中。  
  
## <a name="see-also"></a>另请参阅  
 [维度特性属性参考](../../analysis-services/multidimensional-models/dimension-attribute-properties-reference.md)  
  
  
