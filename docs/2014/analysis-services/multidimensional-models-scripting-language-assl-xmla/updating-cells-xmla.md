---
title: 正在更新单元格 (XMLA) |Microsoft 文档
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- modifying cells
- XMLA, cells
- updating cells
- cells [Analysis Services]
- XML for Analysis, cells
ms.assetid: a1c61496-36ee-4bce-98d9-d13440d349aa
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: f2a4a8976602080f28f736814783397bc6611e64
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36127406"
---
# <a name="updating-cells-xmla"></a>更新单元 (XMLA)
  你可以使用[UpdateCells](../xmla/xml-elements-commands/updatecells-element-xmla.md)命令以更改为多维数据集写回启用多维数据集中的一个或多个单元格的值。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将更新的信息存储在单独的写回表包含单元格要更新的每个分区。  
  
> [!NOTE]  
>  在多维数据集写回期间，`UpdateCells` 命令不支持分配。 若要使用已分配的写回，应使用[语句](../xmla/xml-elements-commands/statement-element-xmla.md)要发送的多维表达式 (MDX) 更新语句命令。 有关详细信息，请参阅[UPDATE CUBE 语句&#40;MDX&#41;](/sql/mdx/mdx-data-manipulation-update-cube)。  
  
## <a name="specifying-cells"></a>指定单元  
 [单元格](../xmla/xml-elements-properties/cell-element-xmla.md)属性`UpdateCells`命令包含要更新的单元格。 可使用单元的序号标识 `Cell` 属性中的每个单元。 从概念上讲，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]数字中多维数据集的单元格，就像该多维数据集是*p*-维数组，其中*p*是的轴数。 单元按行优先的顺序排列。 下图显示了用于计算单元序号的公式。  
  
 ![公式来计算的单元格序号位置](../../../2014/analysis-services/dev-guide/media/cellordinalformula.gif "公式来计算的单元格序号位置")  
  
 一旦您知道单元格的序号，你可以指示中的单元格的预期的值[值](../xmla/xml-elements-properties/value-element-xmla.md)属性[单元格](../xmla/xml-elements-properties/cell-element-xmla.md)属性。  
  
## <a name="see-also"></a>请参阅  
 [更新元素&#40;XMLA&#41;](../xmla/xml-elements-commands/update-element-xmla.md)   
 [在 Analysis Services 中使用 XMLA 开发](../multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
