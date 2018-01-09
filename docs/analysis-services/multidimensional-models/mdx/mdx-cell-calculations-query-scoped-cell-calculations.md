---
title: "创建查询作用域的单元计算 (MDX) |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- WITH keyword
- query-scoped cell calculations [MDX]
ms.assetid: 45987daa-4400-41e9-add7-2428fd75709b
caps.latest.revision: "30"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 34ef680e855c0a6b29363923ba6984189a4e9119
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="mdx-cell-calculations---query-scoped-cell-calculations"></a>MDX 单元计算的查询作用域的单元计算
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]你使用**WITH**关键字中多维表达式 (MDX) 来描述查询的上下文中的计算的单元。 **WITH** 关键字的语法如下：  
  
```  
WITH CELL CALCULATION Cube_Name.CellCalc_Identifier  String_Expression  
```  
  
 `CellCalc_Identifier` 值是计算单元的名称。 `String_Expression` 值包含一个一维正交 MDX 集表达式列表。 这些集表达式中的每个表达式都必须解析为下表中列出的一个类别。  
  
|类别|Description|  
|--------------|-----------------|  
|空集|解析为空集的 MDX 集表达式。 在这种情况下，计算单元的作用域是整个多维数据集。|  
|单个成员集|解析为单个成员的 MDX 集表达式。|  
|级别成员集|解析为单个级别的成员的 MDX 集表达式。 此类集表达式的一个示例是 Level_Expression.**Members** MDX 函数。 若要包括计算成员，请使用 Level_Expression **AllMembers** MDX 函数。 有关详细信息，请参阅 [AllMembers (MDX)](../../../mdx/allmembers-mdx.md)。|  
|后代集|解析为指定成员的后代的 MDX 集表达式。 此类集表达式的一个示例是 **Descendants**(Member_Expression, Level_Expresion, Desc_Flag) MDX 函数。 有关详细信息，请参阅 [Descendants (MDX)](../../../mdx/descendants-mdx.md)。|  
  
 如果 `String_Expression` 参数不描述维度，出于构造计算子多维数据集的目的，MDX 将假设包含所有成员。 因此，如果 `String_Expression` 参数为 NULL，计算单元的定义将应用于整个多维数据集。  
  
 `MDX_Expression` 参数包含一个 MDX 表达式，该表达式的计算结果对于 `String_Expression` 参数中定义的所有单元均为某个单元值。  
  
## <a name="additional-considerations"></a>其他注意事项  
 MDX 只处理一次 **CONDITION** 属性指定的计算条件。 这种只处理一次的做法提高了计算多个计算单元定义的性能，尤其是计算在多维数据集传递间重叠的计算单元时的性能。  
  
 何时发生这唯一的一次处理取决于计算单元定义的创建作用域：  
  
-   如果在全局作用域内作为多维数据集的一部分创建，MDX 将在处理多维数据集时处理计算条件。 如果以任何方式在多维数据集中修改了单元，而且单元包括在计算单元定义的计算子多维数据集中，则在重新处理该多维数据集前，该计算条件可能不准确。 例如，写回中可能发生单元修改。 在重新处理该多维数据集时重新处理计算条件。  
  
-   如果在会话作用域内创建，MDX 将在会话期间发出该语句时处理计算条件。 与在全局作用域内创建的计算单元定义一样，如果修改了单元，计算条件对于计算单元定义可能不准确。  
  
-   如果在查询作用域内创建，MDX 将在运行查询时处理计算条件。 尽管数据滞后问题微不足道，因为 MDX 查询执行的处理时间较短，但这里仍然存在单元修改问题。  
  
 另一方面，只要对多维数据集发出的 MDX 查询涉及计算单元定义中包含的单元，MDX 将就会处理计算公式。 此处理的发生不受创建作用域的限制。  
  
## <a name="see-also"></a>另请参阅  
 [CREATE CELL CALCULATION 语句 (MDX)](../../../mdx/mdx-data-definition-create-cell-calculation.md)  
  
  
