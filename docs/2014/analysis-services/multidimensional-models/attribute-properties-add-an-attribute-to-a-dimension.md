---
title: 向维度中添加属性 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- adding attributes
- automatic attribute creation
- attributes [Analysis Services], creating
- attributes [Analysis Services], adding
- manual attribute creation [Analysis Services]
ms.assetid: 25826ba1-2b38-4b34-bd3a-7eba116093ae
caps.latest.revision: 29
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 7b3f94d20f7f39efffd435793bf3dff808e115df
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36138110"
---
# <a name="add-an--attribute-to-a-dimension"></a>向维度中添加属性
  在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中，可以自动或手动将属性添加到维度中。  
  
 若要自动创建属性，请在 **的维度设计器的** “维度结构” [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]选项卡中，选择要映射到属性的列，然后将该列从 **“数据源视图”** 窗格中拖到 **“属性”** 窗格中。 这样便可创建映射到该列的属性，并为属性分配与该列名称相同的名称。 如果已经存在使用该名称的属性，则 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 会在重复的名称之后添加一个序号后缀，针对第一个重复的名称添加“1”，以此类推。  
  
 若要手动创建属性，请将 **“属性”** 窗格设置为网格视图。 在网格中的最后一行的名称列中，单击**\<新属性 >** 项。 为新属性键入名称。 这样便可创建未映射到列的特性，并且该特性的所有属性都具有默认设置。 在 **的** “属性” [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 窗口中，您可以通过配置新特性的 **KeyColumns** 属性来设置映射。  
  
 有关详细信息，请参阅 [自动定义新属性](attribute-properties-define-a-new-attribute-automatically.md)、 [手动定义新属性](../define-a-new-attribute-manually.md)、 [将属性绑定到名称列](attribute-properties-bind-an-attribute-to-a-name-column.md)和 [修改某个特性的 KeyColumn 属性](attribute-properties-modify-the-keycolumn-property.md)。  
  
## <a name="see-also"></a>请参阅  
 [维度特性属性参考](dimension-attribute-properties-reference.md)  
  
  