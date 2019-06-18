---
title: 更新单元 (XMLA) |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0cfee2adf9d730b458fd482317d16d963f15ebc1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63262178"
---
# <a name="updating-cells-xmla"></a>更新单元 (XMLA)
  可以使用[UpdateCells](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/updatecells-element-xmla)命令更改启用了多维数据集写回的多维数据集中的一个或多个单元格的值。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将更新的信息存储在单独的写回表以获取每个分区，其中包含要更新的单元格。  
  
> [!NOTE]  
>  **UpdateCells**命令不支持多维数据集写回过程中分配。 若要使用已分配的写回，应使用[语句](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/statement-element-xmla)命令发送多维表达式 (MDX) UPDATE 语句。 有关详细信息，请参阅[UPDATE CUBE 语句&#40;MDX&#41;](../../mdx/mdx-data-manipulation-update-cube.md)。  
  
## <a name="specifying-cells"></a>指定单元  
 [单元格](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/cell-element-xmla)的属性**UpdateCells**命令包含要更新的单元格。 标识每个单元格中**单元格**属性使用该单元格的序号。 从概念上讲，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]多维数据集中的单元进行编号，像是该多维数据集一样*p*-维数组，其中*p*是轴的数目。 单元按行优先的顺序排列。 下图显示了用于计算单元序号的公式。  
  
 ![若要计算的单元格的序号位置的公式](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/media/cellordinalformula.gif "公式来计算单元序号位置")  
  
 一旦您知道单元的序号，您可以指示的单元格的预期的值[值](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/value-element-xmla)的属性[单元格](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/cell-element-xmla)属性。  
  
## <a name="see-also"></a>请参阅  
 [Update 元素&#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/update-element-xmla)   
 [在 Analysis Services 中使用 XMLA 开发](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
