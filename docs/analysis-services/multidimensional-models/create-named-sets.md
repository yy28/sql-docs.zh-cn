---
title: "创建命名的集 |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- calculations [Analysis Services], named sets
- named sets [Analysis Services]
- members [Analysis Services], named sets
ms.assetid: 03cf97a4-1a18-45f3-acb0-35123bd619be
caps.latest.revision: "31"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 0d8cc48ae6de8ffefb66960c2ecfed89dd2bc825
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2017
---
# <a name="create-named-sets"></a>创建命名集
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]命名的集是一组维度成员或以供重复使用，例如在多维表达式 (MDX) 查询中创建一个集表达式。 可以通过组合多维数据集数据、算数运算符、数字和函数来创建命名集。 例如，可以创建一个名为“前十位工厂”的命名集，它包含“工厂”维度中具有最高的“产量”度量值的十个成员。 然后最终用户可以在查询中使用“前十位工厂”。 例如，最终用户可以将“前十位工厂”放置在一个坐标轴上，将包含“产量”的“度量值”维度放置在另一个坐标轴上。 有关详细信息，请参阅[多维模型中的计算](../../analysis-services/multidimensional-models/calculations-in-multidimensional-models.md)和[在 MDX 中生成命名集 (MDX)](../../analysis-services/multidimensional-models/mdx/mdx-named-sets-building-named-sets.md)。  
  
 若要创建命名集，请使用多维数据集设计器的 **“计算”** 选项卡上的 **“新建命名集”** 命令。 可以在 **“计算”** 选项卡工具栏上的 **“多维数据集”** 菜单中调用该命令。 该命令显示了一个窗体，可指定下列命名集选项：  
  
 **名称**  
 选择命名集的名称。 最终用户浏览多维数据集时将看到该名称。  
  
 **表达式**  
 指定生成命名集的表达式。 该表达式可以用 MDX 编写。 该表达式可以包含下列任何内容：  
  
-   表示多维数据集的维度、级别、度量值等组件的数据表达式。  
  
-   算术运算符。  
  
-   数字。  
  
-   函数。  
  
 您可以将多维数据集组件从 **“计算工具”** 窗格的 **“元数据”** 选项卡中拖动或复制到 **“命名集窗体编辑器”** 窗格的 **“表达式”** 框中。 您可以将函数从 **“计算工具”** 窗格的 **“函数”** 选项卡中拖动或复制到 **“命名集窗体编辑器”** 窗格的 **“表达式”** 框中。  
  
> [!IMPORTANT]  
>  若要通过显式命名集成员的方式来创建集表达式，请用大括号 ({}) 将成员列表括起来。  
  
## <a name="see-also"></a>另请参阅  
 [多维模型中的计算](../../analysis-services/multidimensional-models/calculations-in-multidimensional-models.md)  
  
  
