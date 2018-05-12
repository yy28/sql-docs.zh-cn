---
title: 正在更新单元格 (XMLA) |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1e886925621378aa5d01cc77a74edf0e1ea246cc
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="updating-cells-xmla"></a>更新单元 (XMLA)
  你可以使用[UpdateCells](../../analysis-services/xmla/xml-elements-commands/updatecells-element-xmla.md)命令以更改为多维数据集写回启用多维数据集中的一个或多个单元格的值。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将更新的信息存储在单独的写回表包含单元格要更新的每个分区。  
  
> [!NOTE]  
>  **UpdateCells**命令不支持多维数据集写回过程中分配。 若要使用已分配的写回，应使用[语句](../../analysis-services/xmla/xml-elements-commands/statement-element-xmla.md)要发送的多维表达式 (MDX) 更新语句命令。 有关详细信息，请参阅[UPDATE CUBE 语句&#40;MDX&#41;](../../mdx/mdx-data-manipulation-update-cube.md)。  
  
## <a name="specifying-cells"></a>指定单元  
 [单元格](../../analysis-services/xmla/xml-elements-properties/cell-element-xmla.md)属性**UpdateCells**命令包含要更新的单元格。 标识每个单元格中**单元格**属性使用该单元格的序号。 从概念上讲，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]数字中多维数据集的单元格，就像该多维数据集是*p*-维数组，其中*p*是的轴数。 单元按行优先的顺序排列。 下图显示了用于计算单元序号的公式。  
  
 ![公式来计算的单元格序号位置](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/media/cellordinalformula.gif "公式来计算的单元格序号位置")  
  
 一旦您知道单元格的序号，你可以指示中的单元格的预期的值[值](../../analysis-services/xmla/xml-elements-properties/value-element-xmla.md)属性[单元格](../../analysis-services/xmla/xml-elements-properties/cell-element-xmla.md)属性。  
  
## <a name="see-also"></a>另请参阅  
 [更新元素 & #40;XMLA & #41;](../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)   
 [使用 Analysis Services 中的 XMLA 进行开发](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
