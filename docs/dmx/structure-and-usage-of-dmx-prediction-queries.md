---
title: 结构和使用情况的 DMX 预测查询 |Microsoft 文档
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- DMX
helpviewer_keywords:
- prediction joins [DMX]
- empty prediction joins [DMX]
- natural prediction joins [DMX]
- DMX [Analysis Services], prediction queries
- prediction queries [DMX]
- queries [DMX], prediction queries
- singleton query predictions [DMX]
- Data Mining Extensions [Analysis Services], prediction queries
ms.assetid: 098bdaa6-9e7d-4e13-a9aa-eb17ce1750e6
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 6f4e5d0f723851776340d3435c05e382c88552ae
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="structure-and-usage-of-dmx-prediction-queries"></a>DMX 预测查询的结构和用法
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  在[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]，你可以使用预测查询中数据挖掘扩展插件 (DMX) 来预测新的数据集，基于挖掘模型的结果中的未知的列值。  
  
 使用何种查询类型取决于您要从模型中获取的具体信息。 如果要实时创建简单预测，例如要知道网站上的一位潜在客户是否符合自行车购买者的特征，则可以使用单独查询。 如果要根据数据源中包含的一组事例创建一批预测，则可使用常规预测查询。  
  
## <a name="prediction-types"></a>预测类型  
 可以使用 DMX 创建下列类型的预测：  
  
 预测联接  
 用于根据挖掘模型中存在的模式创建输入数据的预测。 此查询语句后面必须跟**ON**提供挖掘模型列和输入的列之间的联接条件的子句。  
  
 自然预测联接  
 用于创建基于挖掘模型中的列名的预测，这些列名与您正在执行查询的表中的列名完全匹配。 此查询语句不需要**ON**子句，因为自动生成的联接条件基于挖掘模型列和输入的列之间匹配的名称。  
  
 空预测联接  
 用于发现最可能的预测，无需提供输入数据。 返回的将是仅根据挖掘模型内容创建的预测。  
  
 单独查询  
 用于通过向查询提供数据来创建预测。 由于只需为查询提供一个事例便可快速获得结果，所以该语句非常有用。 例如，可以使用查询来预测某位年龄为 35 岁的已婚女士是否会购买自行车。 该查询不需要外部数据源。  
  
## <a name="query-structure"></a>查询结构  
 若要在 DMX 中生成预测查询，请使用下列元素的组合：  
  
-   **选择 [平展]**  
  
-   **TOP**  
  
-   **从***\<模型 >***PREDICTION JOIN**   
  
-   **ON**  
  
-   **WHERE**  
  
-   **ORDER BY**  
  
 **选择**预测查询的元素定义的列，并且会在结果中显示的表达式设置，并可以包括下列数据：  
  
-   **预测**或**PredictOnly**从挖掘模型的列。  
  
-   来自用于创建预测的输入数据的任何列。  
  
-   可以返回一列数据的函数。  
  
 **FROM** *\<模型 >* **PREDICTION JOIN**元素定义可用于创建该预测的源数据。 对于单独查询，即为分配给列的一系列值。 对于空预测联接，该项将保留为空。  
  
 **ON**元素映射到外部数据集中的列的挖掘模型中定义的列。 如果要创建空预测联接查询或自然预测联接，则不必包括该元素。  
  
 你可以使用**其中**子句来筛选预测查询的结果。 你可以使用**顶部**或**ORDER BY**子句来选择最可能的预测。 有关使用这些子句的详细信息，请参阅[选择&#40;DMX&#41;](../dmx/select-dmx.md)。  
  
 预测语句的语法的详细信息，请参阅[SELECT FROM&#60;模型&#62;PREDICTION JOIN &#40;DMX&#41; ](../dmx/select-from-model-prediction-join-dmx.md)和[SELECT FROM&#60;模型&#62; &#40;DMX&#41;](../dmx/select-from-model-dmx.md).  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘扩展插件 & #40; DMX & #41;引用](../dmx/data-mining-extensions-dmx-reference.md)   
 [数据挖掘扩展插件&#40;DMX&#41;函数引用](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [数据挖掘扩展插件&#40;DMX&#41;运算符参考](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [数据挖掘扩展插件 & #40; DMX & #41;语句引用](../dmx/data-mining-extensions-dmx-statements.md)   
 [数据挖掘扩展插件&#40;DMX&#41;语法约定](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [数据挖掘扩展插件&#40;DMX&#41;语法元素](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [常规预测函数&#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [了解 DMX Select 语句](../dmx/understanding-the-dmx-select-statement.md)  
  
  
