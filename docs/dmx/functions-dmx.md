---
title: "函数 (DMX) |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- DMX
helpviewer_keywords:
- DMX [Analysis Services], functions
- VBA [DMX]
- stored procedures [DMX]
- functions [DMX]
- Excel [DMX]
- Data Mining Extensions [Analysis Services], functions
ms.assetid: 75ab6346-f4a4-4699-90f3-66d35f930ed7
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: b12a4a948dcb90c43eee52a01436ac0ca0c3f174
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="functions-dmx"></a>函数 (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  当你使用数据挖掘扩展插件 (DMX) 查询对象到[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]，你可以使用函数中的数据挖掘模型或输入数据集列中返回比只是值的详细信息。 例如，使用 DMX 查询不仅可以返回列的预测值，还可以返回预测正确的概率。 您不仅可以使用 DMX 函数，还可以使用 Microsoft Visual Basic for Applications (VBA)、Microsoft Excel 和存储过程中的函数。  
  
## <a name="dmx-functions"></a>DMX 函数  
 使用 DMX 函数可以执行下列任务：  
  
-   返回预测。  
  
-   返回预测的统计信息，如概率和支持率。  
  
-   筛选查询结果。  
  
-   重新排序表表达式。  
  
 大多数 DMX 函数均返回一个标量值（如对预测的支持率），但有些函数则只返回表格结果。 例如，PredictHistogram 函数返回包含的支持和概率指定的可预测列的每个状态的表。 结果将在一个新表格列中显示。  
  
 **有关详细信息：** [常规预测函数 &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)，[数据挖掘扩展插件 &#40; DMX &#41;函数参考](../dmx/data-mining-extensions-dmx-function-reference.md)  
  
## <a name="visual-basic-for-applications-vba-and-excel-functions"></a>Visual Basic for Applications (VBA) 和 Excel 函数  
 除 DMX 函数外，还可以调用 DMX 语句中的各种 VBA 和 Excel 函数。 例如，lCase 函数可用于修改 TM_Decision_Tree 模型内容中的 Attribute_Name 列的显示方式。 如下面的代码示例所示。  
  
```  
SELECT lCase([Attribute_Name])   
FROM [TM_Decision_Tree].CONTENT  
```  
  
 如果 VBA 和 Excel 中存在相同的功能，你必须为函数名称前缀在 DMX 语句中使用**VBA**或**Excel**。 例如，`VBA!Log` 或 `Excel!Log` 两个函数。 如果要使用的 VBA 或 Excel 函数同时存在于 DMX 或多维表达式 (MDX) 中，或者函数中包含美元符号字符 ($)，则必须使用方括号 ([]) 来转义函数。 例如，函数调用将成为 `[VBA!Format]`。  
  
## <a name="stored-procedures"></a>存储过程  
 可以使用公共语言运行时编程语言来创建可以扩展 DMX 功能的存储过程。 例如，回归树挖掘模型返回系数，如 A、 B、 并依此类推，用于描述回归公式中，但模型不返回公式本身，如 A + Bx = y。 但是，可以编写一个存储过程，使用数据挖掘模型对象来导航内容架构，并将回归公式作为输出结果返回。 因此，DMX 语句可以在查询结果中返回一组回归公式。  
  
 **有关详细信息：** [多维模型程序集管理](../analysis-services/multidimensional-models/multidimensional-model-assemblies-management.md)  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘扩展插件 &#40; DMX &#41;引用](../dmx/data-mining-extensions-dmx-reference.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;函数参考](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;运算符参考](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;语句引用](../dmx/data-mining-extensions-dmx-statements.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;语法约定](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [数据挖掘扩展插件 &#40; DMX &#41;语法元素](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [常规预测函数 &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)   
 [结构和使用情况的 DMX 预测查询](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [了解 DMX Select 语句](../dmx/understanding-the-dmx-select-statement.md)  
  
  

