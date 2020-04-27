---
title: 浏览神经网络模型 |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining models, browsing
- mining models, viewing
- mining model, neural network
- neural networks
- dependency network
ms.assetid: e4224cb7-115b-4889-ac07-03f096fb55fc
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b32db07a67e309d304aeb145be59fd79c0af5f49
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "78174196"
---
# <a name="browsing-a-neural-network-model"></a>浏览神经网络模型
  使用“浏览”**** 打开神经网络或逻辑回归模型时，该模型显示在交互式查看器（类似于 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 中的神经网络模型查看器）中。 该查看器有助于您探索相关性并获取有关该模型和基础数据中各种模式的信息。

##  <a name="explore-the-model"></a><a name="BKMK_Tabs"></a>浏览模型
 基于 [!INCLUDE[msCoName](../includes/msconame-md.md)] 神经网络或逻辑回归算法的模型是类似的，它们都是将数据作为已知输入和输出中的一组连接进行分析。 “浏览”**** 查看器可帮助你使用以下控件浏览这些连接：

-   [变量](#BKMK_Variables)

-   [输入](#BKMK_Inputs)

-   [Outputs](#BKMK_Outputs)

 如果要使用此查看器，可以使用[分类向导（Excel 数据挖掘外接程序）](classify-wizard-data-mining-add-ins-for-excel.md)向导创建一个模型，并使用“算法参数”**** 对话框中的“高级”**** 选项将算法更改为 Microsoft 逻辑回归。

###  <a name="variables"></a><a name="BKMK_Variables"></a>变化
 “变量”**** 窗格按输入变量对模型影响大小的顺序显示输入变量的列表。 可以使用“输入”**** 和“输出”**** 控件来筛选模型，从而控制显示的变量及其顺序。

 使用此查看器，您可以探索在确定客户是更有可能属于自行车购买者类别还是更有可能属于非购买者类别时最为重要的因素。

 ![针对所选属性结果的测试效果](media/dm13-neuralnet-agebuyer1.gif "针对所选属性结果的测试效果")

##### <a name="explore-variables"></a>浏览变量

1.  首先，设置当前筛选器，“变量”**** 窗格按最重要属性的顺序进行排序。 条的长度指示因素的强度。

     在本示例中，可以看到收入是最有影响的因素，其次是地区。 另一方面，拥有多辆汽车和很多孩子的客户购买自行车的可能性最低。

2.  在“变量”**** 窗格中，单击“属性”**** 的列标题。

     通过按属性排序，可以看到为每个输入列创建的箱。 具有离散值的列（如“occupation”）按文本值进行装箱**。

3.  请注意“Age”**** 和“Income”**** 的值范围。

     如果任何一个输入列是数字（即，整个数据列是连续数字数据类型），则这些数字会存储或装箱到离散范围内。

     对于“Income”，该列已细分为多个分组，如 78.4-154.06（用于最高收入范围）。

     ![排序以查看变量的装箱方式](media/dm13-nn-bucketing-variables.gif "排序以查看变量的装箱方式")

     如果需要不同的分组，应使用[重新标记（SQL Server 数据挖掘外接程序）](relabel-sql-server-data-mining-add-ins.md)工具或 Excel 函数，在生成模型前创建新收入类别。

4.  单击“倾向于 - 是”**** 将图形恢复到默认视图。

     默认情况下，按第一个结果值的“倾向于”**** 值对视图排序。 通过在“输出”**** 中选择新的“Value 1”**** 和“Value 2”**** 值，可以更改分配给第一列和第二列的结果。

5.  将鼠标指针悬停在图表中最上面的彩色条上。

     出现一个工具提示，其中包含一个“重要性”** 分数、一对“概率”** 分数和一对“提升”** 值。

    -   “重要性”**** 是针对整个数据集计算的，用于标识所有输入中与目标结果最相关的属性。 查看器按重要性分数对图表中的值进行排序。

    -   “概率”**** 是面向整个数据集的目标结果，针对每个属性/值对计算的。

    -   “提升”**** 可显示此特定属性/值对对于提升某个结果的贡献度。

     注意：无论将鼠标指针悬停在哪一列上，工具提示都包含相同的信息。

 [返回页首](#BKMK_Tabs)

###  <a name="inputs"></a><a name="BKMK_Inputs"></a>输入
 通过“输入”**** 窗格，可以选择一组输入作为筛选器应用于模型，这样可以看到这些选项基于定型数据对结果产生的影响

##### <a name="explore-inputs"></a>浏览输入

1.  假设要以特定组为目标，查看组中最影响购买行为的因素。

     在 "**输入**" 窗格中，单击 "**属性**" 下的 " ** \<所有>** " 单元，然后选择 "**年龄**"。

     对于“值”****，请选择最年轻的年龄类别。

2.  请注意，即使对特定年龄组进行筛选，太平洋地区也靠近列表的顶部。 这是因为，与其他地区的客户相比，太平洋地区的客户购买自行车的可能性高很多。

     因为地区不是您能影响的因素，所以，若要不考虑此变量查看其他因素，可以再次更改输入。

     在“输入”**** 窗格中，单击“Age”**** 下面的空单元，选择“Region”****。

     对于“值”****，选择“Europe”****。

3.  继续添加输入筛选器，重点关注特别感兴趣的组。

     例如，对于输入属性，添加“Gender”****，然后选择“Female”**** 作为值。

     ![针对所选属性结果的测试效果](media/dm13-neuralnet-agebuyer2.gif "针对所选属性结果的测试效果")

     注意变量列表是如何变化的。 此时，“Income”**** 是在预测目标结果时最重要的变量。

     应用输入筛选器的顺序不会影响结果。

 [返回页首](#BKMK_Tabs)

###  <a name="outputs"></a><a name="BKMK_Outputs"></a>输出
 在“输出”**** 窗格中，可以选择感兴趣的结果。 通过神经网络，可以指定所需数目的结果列，不过，添加更多输出会增加模型的复杂性，可能需要更长的处理时间。

 若要比较两个输出，这两个输出必须已指定为“预测”**** 或“仅预测”**** 列。

##### <a name="explore-outputs"></a>浏览输出

1.  使用“输出属性”**** 列表选择一个属性。

2.  从“值 1”和“值 2”列表中选择两个结果。 输出属性的这两个状态将在 **“变量”** 窗格中进行比较。

 [返回页首](#BKMK_Tabs)

## <a name="more-about-neural-network-models"></a>有关神经网络模型的详细信息
 查看器中的信息是使用特定于此模型类型的存储过程从服务器检索的：System.Microsoft.AnalysisServices.System.DataMining.NeuralNet.GetAttributeScores。

 如果要使用外接程序创建含有多个可预测属性的模型，请使用“高级”**** 建模选项。

 有关详细信息，请参阅[创建挖掘结构（SQL Server 数据挖掘外接程序）](create-mining-structure-sql-server-data-mining-add-ins.md)和[将模型添加到结构（Excel 数据挖掘外接程序）](add-model-to-structure-data-mining-add-ins-for-excel.md)。

## <a name="see-also"></a>另请参阅
 [在 Excel 中浏览模型 &#40;SQL Server 数据挖掘外接程序&#41;](browsing-models-in-excel-sql-server-data-mining-add-ins.md)


