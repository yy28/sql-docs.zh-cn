---
title: 从示例 （Excel 表分析工具） 填充 |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Table Analysis tools
- fill from example
ms.assetid: dac57d8f-1c65-4878-8ea0-9c680df5e4fb
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d1e09e439469f23412c84ea7bab65c0aa748f286
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66081321"
---
# <a name="fill-from-example-table-analysis-tools-for-excel"></a>从示例填充（Excel 表分析工具）
  ![从示例填充表分析工具中的按钮](media/tat-fillex.gif "从示例填充表分析工具中的按钮")  
  
 **从示例填充**工具可帮助您生成新的基于现有值的数据列。  
  
 例如，假设你的数据包含**采购金额**列中，**订单数量**列中，和一个**顶级客户**根据一些公式使用的列其他列。 如果**顶级客户**列包含很多空行，则可以使用**购买金额**并**订单数量**列作为输入来推断缺失值。 该工具分析数据中的现有模式和所输入的示例，预测分配给每个客户的类别。  
  
 如果您对结果不满意，可以通过提供更多的示例来改进结果。  
  
## <a name="using-the-fill-from-example-tool"></a>使用从示例填充工具  
  
1.  在中**分析**功能区中，单击**从示例填充**。  
  
2.  该工具将基于对数据的分析，自动挑选一列进行填充，您可接受也可覆盖建议的值。  
  
3.  为新数据创建一列，并键入要预测的数据的示例。 请确保要预测的每个值都至少有一个示例。 如果要在现有列中填充数据，请选择那个包含缺失值的列。  
  
4.  （可选） 单击**选择要用于分析列**。 在中**高级列选择**对话框框中，指定最有可能在缺少数据填写时很有用的列。  
  
     例如，如果根据经验，您知道一列和包含缺失值的列之间存在因果关系，您可以取消选择其他列，以获得更佳结果。  
  
     单击“确定” 。  
  
5.  单击 **“运行”**。  
  
     分析完成后，该工具创建一个新**模式**包含分析结果的工作表。 报表列出找到的规则或关键影响因素，并显示每个规则的概率。  
  
     此工具还自动向原始数据表添加包含新值的列。 您可查看这些值，并将它们与原始值进行比较。  
  
### <a name="requirements"></a>要求  
 您只能处理列中的数据。 如果要填充的序列存储在行中，可使用 Excel 中的粘贴、转置功能，将这些数据更改为列格式。  
  
## <a name="understanding-the-pattern-report"></a>理解模式报表  
 在运行时**从示例填充**工具，会创建一个报表提供有关检测到的模式的详细信息。 这些模式用于推断新数据值。  
  
 该模式报表显示每个预测值的关键影响因素。 每个影响因素或规则都被描述为列、列中的值以及规则对预测的相对影响的组合。  
  
 例如，如果您尝试填写一张显示订单发货距离的工作表，您可能会很自然地想到目的地对发货距离有重要影响。 在这种情况下，报表可能包含以下行：  
  
|“列”|ReplTest1|倾向于|相对影响|  
|------------|-----------|------------|---------------------|  
|StateProvinceCode|AB|> 500 公里|80%|  
  
 这意味着，中的值 AB **StateProvinceCode**列强预测发货距离 > 500 公里为单位。  
  
 通常预测所基于的模式远比此示例复杂，对于每个预测，该报表可能会包含许多行规则。 预测值是所有规则综合作用的结果。  
  
> [!NOTE]  
>  **相对影响**显示为阴影条。 该条越长，此规则对所填充的值的预测概率就越大。  
  
 此工具还将新列添加到原始数据表中，名为\<列名称 > 扩展。  
  
 如果原始数据列中包含值，则该值将被复制到新列中。 但是，如果原始列包含空白单元，则在新列的相应位置将包含该向导预测的值。  
  
## <a name="related-tools-and-information"></a>相关工具和信息  
 此外可以使用[浏览数据](explore-data-sql-server-data-mining-add-ins.md)向导，可在数据挖掘客户端 for Excel 来检查 Excel 列中值的分布。 有关详细信息，请参阅[研究和清理数据](exploring-and-cleaning-data.md)。  
  
## <a name="see-also"></a>请参阅  
 [Excel 表分析工具](table-analysis-tools-for-excel.md)  
  
  
