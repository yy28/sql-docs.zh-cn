---
title: "正在更新单元格 (XMLA) |Microsoft 文档"
ms.custom: 
ms.date: 02/14/2018
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- modifying cells
- XMLA, cells
- updating cells
- cells [Analysis Services]
- XML for Analysis, cells
ms.assetid: a1c61496-36ee-4bce-98d9-d13440d349aa
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 4349868e9e9656a5bbd735c9fa6c6741c95d6e57
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/15/2018
---
# <a name="updating-cells-xmla"></a>更新单元 (XMLA)
  你可以使用[UpdateCells](../../analysis-services/xmla/xml-elements-commands/updatecells-element-xmla.md)命令以更改为多维数据集写回启用多维数据集中的一个或多个单元格的值。 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 将更新的信息存储在单独的写回表包含单元格要更新的每个分区。  
  
> [!NOTE]  
>  **UpdateCells**命令不支持多维数据集写回过程中分配。 若要使用已分配的写回，应使用[语句](../../analysis-services/xmla/xml-elements-commands/statement-element-xmla.md)要发送的多维表达式 (MDX) 更新语句命令。 有关详细信息，请参阅[UPDATE CUBE 语句 &#40;MDX &#41;](../../mdx/mdx-data-manipulation-update-cube.md).  
  
## <a name="specifying-cells"></a>指定单元  
 [单元格](../../analysis-services/xmla/xml-elements-properties/cell-element-xmla.md)属性**UpdateCells**命令包含要更新的单元格。 标识每个单元格中**单元格**属性使用该单元格的序号。 从概念上讲，[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]数字中多维数据集的单元格，就像该多维数据集是*p*-维数组，其中*p*是的轴数。 单元按行优先的顺序排列。 下图显示了用于计算单元序号的公式。  
  
 ![公式来计算的单元格序号位置](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/media/cellordinalformula.gif "公式来计算的单元格序号位置")  
  
 一旦您知道单元格的序号，你可以指示中的单元格的预期的值[值](../../analysis-services/xmla/xml-elements-properties/value-element-xmla.md)属性[单元格](../../analysis-services/xmla/xml-elements-properties/cell-element-xmla.md)属性。  
  
## <a name="see-also"></a>另请参阅  
 [更新元素 &#40;XMLA &#41;](../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)   
 [使用 Analysis Services 中的 XMLA 进行开发](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
