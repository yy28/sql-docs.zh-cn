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
ms.openlocfilehash: 71279981c5fd3879d633e0fdd8cdec74bed6deac
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2019
ms.locfileid: "68887707"
---
# <a name="updating-cells-xmla"></a>更新单元 (XMLA)
  可以使用[UpdateCells](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/updatecells-element-xmla)命令更改为多维数据集写回启用的多维数据集中的一个或多个单元的值。 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 对于包含要更新的单元格的每个分区,将更新的信息存储在单独的[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]写回表中。  
  
> [!NOTE]  
>  在多维数据集写回期间，`UpdateCells` 命令不支持分配。 若要使用已分配的写回, 应使用[语句](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/statement-element-xmla)命令发送多维表达式 (MDX) UPDATE 语句。 有关详细信息, 请参阅[UPDATE CUBE &#40;语句&#41;MDX](/sql/mdx/mdx-data-manipulation-update-cube)。  
  
## <a name="specifying-cells"></a>指定单元  
 `UpdateCells`命令的[Cell](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/cell-element-xmla)属性包含要更新的单元格。 可使用单元的序号标识 `Cell` 属性中的每个单元。 从概念[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]上讲, 将多维数据集中的单元格作为二维数组, 其中*p*是轴的数目。 单元按行优先的顺序排列。 下图显示了用于计算单元序号的公式。  
  
 ![用于计算单元序号位置的公式](https://docs.microsoft.com/analysis-services/analysis-services/dev-guide/media/cellordinalformula.gif "用于计算单元序号位置的公式")  
  
 一旦知道了单元的序号, 就可以在[cell](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/cell-element-xmla)属性的[value](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/value-element-xmla)属性中指示单元格的预期值。  
  
## <a name="see-also"></a>请参阅  
 [Update 元素&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/update-element-xmla)   
 [在 Analysis Services 中使用 XMLA 开发](../multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
