---
title: "计算列 (SSAS 表格) |Microsoft 文档"
ms.custom: 
ms.date: 05/22/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e1011278-556d-4984-b01d-a37f8a33b304
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5155ce65d240db9bec2f01ada5dcba61c9926037
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="calculated-columns"></a>计算列
  计算的列，在表格模型中，使你能够添加新数据与你的模型。 您可以创建用于定义列的行级值的 DAX 公式，而不用在列中粘贴或导入值。 然后，计算列可用于报表、数据透视表或数据透视图中，您可以像使用任何其他数据列一样使用计算列。  
  
> [!NOTE]  
>  在 DirectQuery 模式下，表格模型不支持计算列。 有关详细信息，请参阅[DirectQuery 模式下](../../analysis-services/tabular-models/directquery-mode-ssas-tabular.md)。  
  
  
##  <a name="bkmk_understanding"></a> 优势  
 计算列中的公式非常类似于 Excel 中的公式。 但与 Excel 不同，您不能为表中的不同行创建不同的公式；而是 DAX 公式自动应用于整个列。  
  
 在某个列包含公式时，将为每一行都计算值。 在您输入有效公式时，将立即为列计算结果。 在需要时（例如，在刷新基础数据时），将重新计算列值。  
  
 您可以创建基于度量值和其他计算列的计算列。 例如，您可以创建一个计算列以便从文本字符串中提取一个数字，然后在其他计算列中使用该数字。  
  
 计算列基于您已在现有表中具有的数据，或者通过使用 DAX 公式创建。 例如，您可以选择串联值、执行添加、提取子字符串或比较其他字段中的值。 若要添加某一计算列，您必须在模型中具有至少一个表。  
  
 此示例演示计算列中的一个简单的公式：  
  
```  
=EOMONTH([StartDate],0])  
  
```  
  
 此公式将从 StartDate 列中提取月份。 它然后计算表中每一行的月末值。 第二个参数指定 StartDate 中该月前或该月后的月份数；在这个例子中，0 意味着同一月。 例如，如果 StartDate 列中的值为 6/1/2001，则计算列中的值将是 6/30/2001。  
  
##  <a name="bkmk_naming"></a> Naming a calculated column  
 默认情况下，新的计算列将添加到表中其他列的右侧，并且自动向该列分配默认名称 **CalculatedColumn1**、 **CalculatedColumn2**，依此类推。 您也可以右键单击某一列，然后单击“插入列”以便在两个现有列之间创建一个新列。 您可以通过单击和拖动在同一个表中重新排列列，并且可以在创建列后重命名列；但是，您应该知道针对计算列的更改的以下限制：  
  
-   每个列名称在表中都必须唯一。  
  
-   避免使用已用于同一模型中的度量值的名称。 尽管度量值和计算列可以具有相同的名称，但是如果名称不唯一，可能会导致计算错误。 为了避免无意中调用度量值，在引用列时请始终使用完全限定的列引用。  
  
-   当您重命名计算列时，必须手动更新依赖于该列的所有公式。 如果您没有处于手动更新模式，则更新公式结果将自动发生。 但是，此操作可能要花一些时间。  
  
-   有一些字符不能用于列名中。 有关详细信息，请参阅 [DAX 语法参考](http://msdn.microsoft.com/en-us/098630f4-7d1d-467e-976c-99b2279430d5)中的“命名要求”。  
  
##  <a name="bkmk_perf"></a> Performance of calculated columns  
 与用于度量值的公式相比，用于计算列的公式可能会消耗更多的资源。 原因之一是：计算列的结果始终是为表中的每一行计算的，而度量值仅是为报表、数据透视表或数据透视图中使用的筛选器定义的单元计算的。 例如，某个具有 100 万行的表将始终具有含 100 万个结果的计算列，并且对性能具有相应影响。 但是，数据透视表通常会通过应用行和列标题对数据进行筛选；因此，仅为数据透视表的每个单元中的数据子集计算度量值。  
  
 一个公式对于在公式中引用的对象（例如其他列或计算值的表达式）具有依赖关系。 例如，对于基于其他列的计算列，或对于包含引用列的表达式的计算，只有在计算这些相关列之后，才会计算它们。 默认情况下，在工作簿中启用自动刷新；因此，在更新值和刷新公式时，所有此类依赖项都可能会影响性能。  
  
 为了避免在创建计算列时出现性能问题，请遵循下列指导原则：  
  
-   不要创建包含许多复杂依赖关系的单个公式，而应分步创建多个公式并将结果保存到列中，这样您就能够验证结果并评估性能。  
  
-   修改数据通常要求重新计算计算列。 可以通过将重新计算模式设置为手动来避免上述情况；但是，如果计算列中的任何值不正确，则该列将灰显，直到您刷新并重新计算数据。  
  
-   如果更改或删除表之间的关系，则使用这些表中的列的公式将会失效。  
  
-   如果创建了一个包含循环或自引用依赖关系的公式，将会发生错误。  
  
##  <a name="bkmk_rel_tasks"></a> Related tasks  
  
|主题|Description|  
|-----------|-----------------|  
|[创建计算的列](../../analysis-services/tabular-models/ssas-calculated-columns-create-a-calculated-column.md)|本主题中的任务描述了如何向表中添加新的计算列。|  
  
## <a name="see-also"></a>另请参阅  
 [表和列](../../analysis-services/tabular-models/tables-and-columns-ssas-tabular.md)   
 [度量值](../../analysis-services/tabular-models/measures-ssas-tabular.md)   
 [计算](../../analysis-services/tabular-models/calculations-ssas-tabular.md)  
  
  
