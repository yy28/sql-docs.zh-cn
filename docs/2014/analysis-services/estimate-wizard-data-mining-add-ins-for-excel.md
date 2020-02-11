---
title: 估计向导（Excel 数据挖掘外接程序） |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data modeling [data mining]
- estimation
ms.assetid: 7f2b1d5f-c9b3-4939-b35a-34ae099af15f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9b7ffc1b77d90946a119dc462da2057cf3fe4988
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66081247"
---
# <a name="estimate-wizard-data-mining-add-ins-for-excel"></a>估计向导（Excel 数据挖掘外接程序）
  ![“数据挖掘”功能区中的估计向导](media/dmc-estimate.gif "“数据挖掘”功能区中的估计向导")  
  
 **估计**向导帮助您创建估计模型。 估计模型从数据中提取模式，并使用这些模式预测将影响结果的因素。  
  
 估计用于预测数字结果。 例如，如果目标列包含学校的升学率（升学率以百分比表示），则可分析有可能提高或降低升学率的因素，如每个学校的学生数量、学生与教师的比例以及教师数量。  
  
## <a name="using-the-estimate-data-wizard"></a>使用估计数据向导  
  
1.  在 "**数据挖掘**" 功能区上，单击 "**估计**"。  
  
2.  在 "**选择源数据**" 对话框中，选择要使用的源数据。 您可以在 Excel**表**、Excel**数据区域**或**外部数据源**中使用数据。  
  
     如果使用外部数据源，您可以创建自定义视图或查询并将其另存为 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据源。  
  
3.  在 "**估计**" 对话框中，选择**要分析的列**。  
  
     目标列必须包含连续的数值数据。  
  
4.  选中 "**输入列**" 复选框，选择要用作输入的列。  
  
     这些列将用于创建模式。 您应当从分析中删除那些不可能有用的列（如 ID 号）或包含无关数据的列。  
  
5.  **估计**向导为您的数据集选择最佳算法。 不过，可以单击 "**参数**" 打开 "**算法参数**" 对话框并设置高级选项。  
  
6.  如果你的数据是数值，并且你可以使用 Microsoft 线性回归方法，则可以在 "**回归量**" 框中检查你知道（或强烈怀疑）与可预测值相关的任何数值列。  
  
     然后，此算法将对该列中的值进行测试以确定它们是否会影响结果。 如果不确定，请单击 "**建议**"，算法将测试所有列，并自动检测要用作回归量的最佳值。  
  
    > [!NOTE]  
    >  回归量是创建估计所必需的。 向导总是基于最初传递的数据来推荐最佳回归量。 因此，如果您不能确定，最好接受向导所推荐的选择。  
  
7.  在 "将**数据拆分为定型集和测试集**" 页上，指定是否要创建用于测试的一小部分数据。  
  
8.  在 "**完成**" 页上，提供新挖掘结构和挖掘模式的名称，或接受提供的默认名称。  
  
9. 设置模型使用选项。  
  
    -   选择 "**浏览**" 可立即在查看器中打开模型。  
  
         此图形查看器会显示一个依赖关系网络图形以及由该算法生成的决策树。 通过研究这些信息，您可以更好地理解影响估计值的因素。  
  
    -   选择 "**启用钻取**" 可允许分析的用户查看基础数据。  
  
         此选项仅在您使用决策树或线性回归算法时可用。  
  
    -   **使用临时模型**。 如果您选择此选项，模型将不会被保存到服务器。 在您关闭 Excel 时，临时模型将被删除。  
  
## <a name="more-about-estimation-models"></a>有关估计模型的详细信息  
 **估计**向导支持使用以下任何算法：  
  
-   Microsoft 决策树算法  
  
-   Microsoft 线性回归算法  
  
-   Microsoft 逻辑回归算法  
  
-   Microsoft 神经网络算法  
  
 在 "**算法参数**" 对话框中，可以根据所选的算法设置其他高级选项。 有关每种算法的选项的信息，请参阅 SQL Server 联机丛书中的下列主题：  
  
 [Microsoft 决策树算法技术参考](data-mining/microsoft-decision-trees-algorithm-technical-reference.md)  
  
 [Microsoft 线性回归算法技术参考](data-mining/microsoft-linear-regression-algorithm-technical-reference.md)  
  
 [Microsoft 逻辑回归算法技术参考](data-mining/microsoft-logistic-regression-algorithm-technical-reference.md)  
  
 [Microsoft 神经网络算法技术参考](data-mining/microsoft-neural-network-algorithm-technical-reference.md)  
  
### <a name="requirements"></a>要求  
 若要使用估计数据向导，您必须连接到 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据库。  
  
 有关如何创建连接的信息，请参阅[连接到源数据 &#40;Excel 数据挖掘客户端&#41;](connect-to-source-data-data-mining-client-for-excel.md)。  
  
 若要使用估计算法，尝试预测的结果必须表示为数值，如货币、销售额、日期或时间。  
  
## <a name="see-also"></a>另请参阅  
 [创建数据挖掘模型](creating-a-data-mining-model.md)   
 [决策树关系图演练 &#40;数据挖掘外接程序&#41;](decision-tree-diagram-walkthrough-data-mining-add-ins.md)  
  
  
