---
title: 指定列内容和数据类型（数据挖掘向导） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 0634be64-4c38-4381-9b19-fe9a5889306c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d224a321ed78f89a798966bd28c0ff7f16d55134
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66068471"
---
# <a name="specify-column-content-and-data-type-data-mining-wizard"></a>指定列内容和数据类型（数据挖掘向导）
  可以使用 **“指定列的内容和数据类型”** 页，为在向导的上一页中选择的每一列指定用法和数据类型。 如果希望忽略列，请单击 **“上一步”** 返回到 **“指定定型数据”** 页，并清除所有复选框。  
  
 列的用法指示数据在模型中的使用方式。 列可以用作标识序列的键，用作分析中要使用的输入值，还可以用作要预测的值。 列既可用于预测又可用于输入。  
  
 数据类型指定列中所包含数据的类型的更多详细信息，以及在定型过程中将如何使用数据。 某些内容类型需要某种特定的数据类型，反过来也是这样。 根据创建挖掘模型时所使用的算法，可能还需要指定特定数据类型。 有关挖掘模型和结构中的内容类型和数据类型的信息，请参阅[内容类型（数据挖掘）](data-mining/content-types-data-mining.md)。  
  
 **有关详细信息：** [挖掘结构 &#40;Analysis Services 数据挖掘&#41;](data-mining/mining-structures-analysis-services-data-mining.md)、[挖掘模型列](data-mining/mining-model-columns.md)、[数据挖掘向导 &#40;Analysis Services 数据挖掘&#41;](data-mining/data-mining-wizard-analysis-services-data-mining.md)、[创建关系挖掘结构](data-mining/create-a-relational-mining-structure.md)  
  
## <a name="options"></a>选项  
 **挖掘模型结构**  
 显示您在向导的上一页中所选视图和嵌套表中的列。  
  
 **“列”**  
 列出各列。  
  
 **内容类型**  
 指定列的内容类型。 如果在向导的上一页上指定该列是键，则可用值如下：  
  
|选项|说明|  
|------------|-----------------|  
|密钥|指定该列包含事例序列的唯一标识符。|  
|键序列|指定该列包含序列标识符。|  
|键时间|指定该列包含用于标识日期或时序的日期或其他唯一连续数值。|  
  
 如果选择该列作为非键列，则可用值如下（具体取决于数据类型）：  
  
|选项|说明|  
|------------|-----------------|  
|连续|指定该列包含连续数值。|  
|离散化|指定该列包含已离散化数值或可被视为离散值的数值。|  
|离散|指定该列包含文本或其他非数值。|  
  
 **数据类型**  
 指定列的数据类型。  
  
 可用值如下：  
  
-   `Boolean`  
  
-   `Date`  
  
-   `Double`  
  
-   `Long`  
  
-   `Text`  
  
 **Detect**  
 分析所有数值列中数据的示例。 利用建议的内容类型替换指定的 **“内容类型”** 值。  
  
## <a name="see-also"></a>另请参阅  
 [数据挖掘向导 F1 帮助 &#40;Analysis Services 数据挖掘&#41;](data-mining-wizard-f1-help-analysis-services-data-mining.md)   
 [在数据挖掘向导 &#40;建议相关列&#41;](suggest-related-columns-data-mining-wizard.md)   
 [在数据挖掘向导 &#40;指定表类型&#41;](specify-table-types-data-mining-wizard.md)   
 [指定数据挖掘向导 &#40;列的内容和数据类型&#41;](specify-the-column-s-content-and-data-type-data-mining-wizard.md)  
  
  
