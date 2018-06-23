---
title: 目标查找方案 （Excel 表分析工具） |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Table Analysis tools
- scenario analysis
- goal seek scenario
ms.assetid: efe50306-cf7c-46b3-9cc4-e7f0b6968b0c
caps.latest.revision: 22
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: ecf3d569cdee1bf2e0ea58e8d582f6b2d3829fca
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36124443"
---
# <a name="goal-seek-scenario-table-analysis-tools-for-excel"></a>目标查找应用场景（Excel 表分析工具）
  ![表分析工具中的目标定位按钮](media/tat-goalseek.gif "表分析工具中的目标查找按钮")  
  
 **目标查找**方案工具是互补到[如果](what-if-scenario-table-analysis-tools-for-excel.md)方案工具。 **假设**工具告诉你进行更改的影响而**目标查找**工具告诉你必须更改以实现所需的结果的基础因素。  
  
 例如，假定您的目标是增加客户满意度。 你可以使用**目标查找**分析，以确定哪些因素会最有可能增加客户满意度，并决定是否经济高效这些更改。  
  
 该工具完成分析后，它会在源数据表中创建两个新列。 这些列显示*可能性*可以实现的目标的结果，和建议的更改，如果有的话。  
  
 该工具可分析一组数据并对整个数据集进行预测，或者可以创建分析，再每次测试一个应用场景。  
  
## <a name="using-the-goal-seek-scenario-tool"></a>使用目标查找应用场景工具  
  
1.  打开 Excel 表。  
  
2.  单击**方案**，然后选择**目标查找**。  
  
3.  在**应用场景分析： 目标查找**对话框中，选择包含目标的列的值从列表中。  
  
4.  指定要达到的值。  
  
     如果列目标包含连续数值，则还可以指定希望采用的值的增减幅度。 例如，你可以选择**销售**作为列并指定目标是 120%的增加。  
  
     或者，可以通过键入上限和下限将目标指定为某一范围的值。  
  
5.  指定包含将要更改的值的列。 也就是说，选取将对其进行操作以产生所需结果的列。  
  
6.  （可选） 单击**选择要用于分析列**，并选择包含有用信息的列。 取消选择对分析无用的列。  
  
    > [!NOTE]  
    >  不要取消选择将用于目标或更改的列。 这些列是必需的。  
  
7.  指定是要针对整个表进行预测，还是仅针对所选行进行预测。  
  
8.  如果你选择**整个表**选项，该工具将预测添加到两个新列中的源表。  
  
9. 如果你选择了选项**在此行上**，分析的结果是查看的对话框中的输出。 该对话框保持打开状态，以便您可以继续尝试不同的值和目标。  
  
### <a name="requirements"></a>要求  
 此工具使用 Microsoft 逻辑回归算法，该算法可处理数值或离散值。  
  
 您可多次运行预测，并选择不同的列，但是每个目标和更改的组合都必须单独计算。  
  
 如果选择了包含有用信息的分析列，则可获得更好的结果。 但是，如果您选择的列太少，则可能很难获得结果。  
  
 一次创建一个预测时，请确保不要选择已包含所需结果的行，否则可能出现错误。 也就是说，当目标查找的目的为确定鼓励购买自行车的因素时，您应该仅包含没有购买自行车的客户。  
  
## <a name="understanding-the-results-of-goal-seek-analysis"></a>理解目标查找分析的结果  
 在创建目标查找应用场景时，该工具执行以下三个操作：  
  
-   创建存储有关表中数据关键事实的数据挖掘结构。  
  
-   基于数据创建逻辑回归挖掘模型。  
  
-   创建所指定的每个值的预测。  
  
 如果一次测试一个目标查找应用场景，则可以交互方式查看结果。 这是创建相同*单独预测查询*。  
  
 该工具中的报表**结果**窗格中的对话框框中是否成功找到来实现所需的目标的方案。 如果找到了成功的解决方案，则该工具还会生成告知所需更改的建议。 例如，**目标查找**工具可能会告诉您该 commuting 距离应小于 5 英里。  
  
 示例结果：  
  
 **购买感兴趣的目标查找找到了解决方案。**  
  
 **最接近匹配通过为"2-5 英里的更改下班路程获得。**  
  
 由于此结果基于数据表中的现有行，因此这意味着，对于特定的客户，如果保持所有其他条件不变，而将该客户的上下班路程减少到 2-5 英里，则该客户将在某种程度上更有可能购买自行车。  
  
 如果在 Excel 表中指定创建的所有行的目标查找预测**整个表**，thetool 原始数据表中创建两个新列。 添加到表中的第一列包含两种标记之一：一种是外带绿圈的复选标记，说明可实现目标，另一种是外带红圈的 X 标记，说明任何更改都不能实现目标。  
  
 第二列包含建议的更改。  
  
> [!NOTE]  
>  建议更改及其成功可能性的置信度级别由算法预先确定，不能更改。  
  
## <a name="related-tools"></a>相关工具  
 Excel 数据挖掘客户端是一个独立的外接程序，它提供更高级的数据挖掘功能，还包含用于创建可预测行为的数据挖掘模型的向导。 有关详细信息，请参阅[创建数据挖掘模型](creating-a-data-mining-model.md)。  
  
 有关使用的算法的详细信息**目标查找**方案工具，请参阅中的主题"Microsoft 逻辑回归算法"[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]联机丛书。  
  
## <a name="see-also"></a>请参阅  
 [Excel 表分析工具](table-analysis-tools-for-excel.md)  
  
  