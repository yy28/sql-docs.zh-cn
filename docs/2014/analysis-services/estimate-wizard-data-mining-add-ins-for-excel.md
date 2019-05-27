---
title: 估计向导 （Excel 数据挖掘外接程序） |Microsoft Docs
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
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66081247"
---
# <a name="estimate-wizard-data-mining-add-ins-for-excel"></a>估计向导（Excel 数据挖掘外接程序）
  ![数据挖掘功能区中的估计向导](media/dmc-estimate.gif "数据挖掘功能区中的估计向导")  
  
 **估计**向导帮助您创建估计模型。 估计模型从数据中提取模式，并使用这些模式预测将影响结果的因素。  
  
 估计用于预测数字结果。 例如，如果目标列包含学校的升学率（升学率以百分比表示），则可分析有可能提高或降低升学率的因素，如每个学校的学生数量、学生与教师的比例以及教师数量。  
  
## <a name="using-the-estimate-data-wizard"></a>使用估计数据向导  
  
1.  上**数据挖掘**功能区中，单击**估计**。  
  
2.  在中**选择源数据**对话框框中，选择要使用的源数据。 可以在 Excel 中使用数据**表**，Excel**数据范围**，或从**外部数据源**。  
  
     如果使用外部数据源，您可以创建自定义视图或查询并将其另存为 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据源。  
  
3.  在中**估算**对话框中，选择**要分析的列**。  
  
     目标列必须包含连续的数值数据。  
  
4.  选择要使用作为输入通过检查列**输入列**复选框。  
  
     这些列将用于创建模式。 您应当从分析中删除那些不可能有用的列（如 ID 号）或包含无关数据的列。  
  
5.  **估计**向导选择最佳算法为您的数据集。 但是，您可以单击**参数**以打开**算法参数**对话框并设置高级选项。  
  
6.  如果你的数据是数值，并且可以使用 Microsoft 线性回归方法，可以检查**回归量**框知道 （或强烈怀疑） 的任何数值列与可预测值相关。  
  
     然后，此算法将对该列中的值进行测试以确定它们是否会影响结果。 如果您不确定，请单击**建议**算法将测试所有列并自动检测要用作回归量的最佳值。  
  
    > [!NOTE]  
    >  回归量是创建估计所必需的。 向导总是基于最初传递的数据来推荐最佳回归量。 因此，如果您不能确定，最好接受向导所推荐的选择。  
  
7.  上**将数据拆分为定型集和测试集**页上，指定是否想要创建用于测试数据的一小部分。  
  
8.  上**完成**页上，为新的挖掘结构和挖掘模式下，提供名称或接受提供的默认名称。  
  
9. 设置模型使用选项。  
  
    -   选择**浏览**立即在查看器中打开模型。  
  
         此图形查看器会显示一个依赖关系网络图形以及由该算法生成的决策树。 通过研究这些信息，您可以更好地理解影响估计值的因素。  
  
    -   选择**启用钻取**若要允许的用户您的分析，请查看基础数据。  
  
         此选项仅在您使用决策树或线性回归算法时可用。  
  
    -   **使用临时模型**。 如果您选择此选项，模型将不会被保存到服务器。 在您关闭 Excel 时，临时模型将被删除。  
  
## <a name="more-about-estimation-models"></a>有关估计模型的详细信息  
 **估计**向导支持使用任何以下算法：  
  
-   Microsoft 决策树算法  
  
-   Microsoft 线性回归算法  
  
-   Microsoft 逻辑回归算法  
  
-   Microsoft Neural 网络算法  
  
 在中**算法参数**对话框中，可以设置其他高级的选项，具体取决于哪种算法选择。 有关每种算法的选项的信息，请参阅 SQL Server 联机丛书中的下列主题：  
  
 [Microsoft 决策树算法技术参考](data-mining/microsoft-decision-trees-algorithm-technical-reference.md)  
  
 [Microsoft 线性回归算法技术参考](data-mining/microsoft-linear-regression-algorithm-technical-reference.md)  
  
 [Microsoft 逻辑回归算法技术参考](data-mining/microsoft-logistic-regression-algorithm-technical-reference.md)  
  
 [Microsoft 神经网络算法技术参考](data-mining/microsoft-neural-network-algorithm-technical-reference.md)  
  
### <a name="requirements"></a>要求  
 若要使用估计数据向导，您必须连接到 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 数据库。  
  
 有关如何创建连接的信息，请参阅[连接到源数据&#40;Excel 数据挖掘客户端&#41;](connect-to-source-data-data-mining-client-for-excel.md)。  
  
 若要使用估计算法，尝试预测的结果必须表示为数值，如货币、销售额、日期或时间。  
  
## <a name="see-also"></a>请参阅  
 [创建数据挖掘模型](creating-a-data-mining-model.md)   
 [决策树关系图演练&#40;数据挖掘外接程序&#41;](decision-tree-diagram-walkthrough-data-mining-add-ins.md)  
  
  
