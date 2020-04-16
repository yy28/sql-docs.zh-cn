---
title: 更新单元格 （XMLA） |微软文档
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
ms.openlocfilehash: f0eab50aa7e70aedee93eef2cefee648e6ceb5c9
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/15/2020
ms.locfileid: "81387887"
---
# <a name="updating-cells-xmla"></a>更新单元 (XMLA)
  可以使用[UpdateCells](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/updatecells-element-xmla)命令更改多维数据集中启用的多维数据集中一个或多个单元格的值，以便多维数据集回写。 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]将更新的信息存储在包含要更新的单元格的每个分区的单独回写[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]表中。  
  
> [!NOTE]  
>  在多维数据集写回期间，`UpdateCells` 命令不支持分配。 要使用分配的写回，应使用[语句](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/statement-element-xmla)命令发送多维表达式 （MDX） 更新语句。 有关详细信息，请参阅[更新多维数据集语句&#40;MDX&#41;](/sql/mdx/mdx-data-manipulation-update-cube)。  
  
## <a name="specifying-cells"></a>指定单元  
 命令[Cell](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/cell-element-xmla)的`UpdateCells`Cell 属性包含要更新的单元格。 可使用单元的序号标识 `Cell` 属性中的每个单元。 从概念[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]上讲，对多维数据集中的单元格进行数字，就像多维数据集是*p-* 维数组一样，其中*p*是坐标轴数。 单元按行优先的顺序排列。 下图显示了用于计算单元序号的公式。  
  
 ![用于计算单元序号位置的公式](../../analysis-services/dev-guide/media/cellordinalformula.gif "用于计算单元序号位置的公式")  
  
 知道单元格的元数后，可以在[Cell](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/cell-element-xmla)属性[的 Value](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/value-element-xmla)属性中指示单元格的预期值。  
  
## <a name="see-also"></a>另请参阅  
 [更新元素&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/update-element-xmla)   
 [在 Analysis Services 中使用 XMLA 开发](../multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
