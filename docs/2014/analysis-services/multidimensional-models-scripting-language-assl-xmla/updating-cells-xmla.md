---
title: 更新单元 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- modifying cells
- XMLA, cells
- updating cells
- cells [Analysis Services]
- XML for Analysis, cells
ms.assetid: a1c61496-36ee-4bce-98d9-d13440d349aa
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 56c4313ea77fc342c2d7ac4fb142d922038948ca
ms.sourcegitcommit: b87c384e10d6621cf3a95ffc79d6f6fad34d420f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "60155547"
---
# <a name="updating-cells-xmla"></a>更新单元 (XMLA)
  可以使用[UpdateCells](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/updatecells-element-xmla)命令更改启用了多维数据集写回的多维数据集中的一个或多个单元格的值。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将更新的信息存储在单独的写回表以获取每个分区，其中包含要更新的单元格。  
  
> [!NOTE]  
>  在多维数据集写回期间，`UpdateCells` 命令不支持分配。 若要使用已分配的写回，应使用[语句](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/statement-element-xmla)命令发送多维表达式 (MDX) UPDATE 语句。 有关详细信息，请参阅[UPDATE CUBE 语句&#40;MDX&#41;](/sql/mdx/mdx-data-manipulation-update-cube)。  
  
## <a name="specifying-cells"></a>指定单元  
 [单元格](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/cell-element-xmla)属性的`UpdateCells`命令包含要更新的单元格。 可使用单元的序号标识 `Cell` 属性中的每个单元。 从概念上讲，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]多维数据集中的单元进行编号，像是该多维数据集一样*p*-维数组，其中*p*是轴的数目。 单元按行优先的顺序排列。 下图显示了用于计算单元序号的公式。  
  
 ![若要计算的单元格的序号位置的公式](../../../2014/analysis-services/dev-guide/media/cellordinalformula.gif "公式来计算单元序号位置")  
  
 一旦您知道单元的序号，您可以指示的单元格的预期的值[值](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/value-element-xmla)的属性[单元格](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/cell-element-xmla)属性。  
  
## <a name="see-also"></a>请参阅  
 [Update 元素&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/update-element-xmla)   
 [在 Analysis Services 中使用 XMLA 开发](../multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
