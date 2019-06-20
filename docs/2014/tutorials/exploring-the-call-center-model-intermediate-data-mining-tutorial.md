---
title: 探索呼叫中心模型 （数据挖掘中级教程） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 9095212c-9068-4dd8-85ce-17a467adeabb
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: a6aa4074aa04af86e478b57b1870fd0dd855bea8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63315080"
---
# <a name="exploring-the-call-center-model-intermediate-data-mining-tutorial"></a>探索呼叫中心模型（数据挖掘中级教程）
  您已生成了探索模型，现在可以使用 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 提供的以下工具来了解有关数据的更多信息。  
  
-   [Microsoft 神经网络查看器](#bkmk_NNviewer) **:** 此查看器现已推出**挖掘模型查看器**选项卡上的数据挖掘设计器，它旨在帮助您试验数据中的交互性。  
  
-   [Microsoft 一般内容树查看器](#bkmk_genviewer) **:** 该标准查看器提供了有关模式和生成模型时算法发现的统计信息的深入详细信息。  
  
##  <a name="bkmk_NNviewer"></a> Microsoft 神经网络查看器  
 在查看器有三个窗格-**输入**，**输出**，并**变量**。  
  
 通过使用**输出**窗格中，可以选择不同的可预测属性或因变量的值。 如果您的模型包含多个可预测属性，则可以选择从特性**输出属性**列表。  
  
 **变量**窗格将根据相关属性或变量选择的两个结果进行比较。 彩色条直观的表示变量对目标结果的影响程度。 您还可以查看变量的提升分数。 提升分数的计算方法不同，具体取决于使用的挖掘模型类型，但通常会告诉您使用此属性进行预测时在模型中的提高程度。  
  
 **输入**窗格，您可以将影响因素添加到要尝试各种假设方案的模型。  
  
### <a name="using-the-output-pane"></a>使用“输出”窗格  
 在此初始模型中，您会希望看到各种因素是如何影响服务等级的。 若要执行此操作，可以从输出属性的列表中选择服务等级，然后通过从下拉列表中选择范围来比较不同级别的服务**值 1**并**值 2**。  
  
##### <a name="to-compare-lowest-and-highest-service-grades"></a>比较最低服务等级和最高服务等级  
  
1.  有关**值 1**，选择具有最小值的范围。 例如，范围 0-0-0.7 表示最低的挂断率，因此为最佳服务级别。  
  
    > [!NOTE]  
    >  根据模型的配置方式，此范围内的确切值可能会有所不同。  
  
2.  有关**值 2**，选择具有最高值的范围。 例如，值范围 > = 0.12 表示最高的挂断率，因此最差服务等级。 换句话说，在此班次期间，打电话的客户有 12% 在与代表通话之前就挂断了电话。  
  
     内容**变量**窗格会更新，以比较导致的结果值的属性。 因此，左列显示与最佳服务等级关联的属性，右列显示与最差服务等级关联的属性。  
  
### <a name="using-the-variables-pane"></a>使用“变量”窗格  
 在此模型中，显示，`Average Time Per Issue`是一个重要因素。 此变量指示在不考虑呼叫类型的情况下应答一个呼叫所花费的平均时间。  
  
##### <a name="to-view-and-copy-probability-and-lift-scores-for-an-attribute"></a>查看和复制属性的概率和提升分数  
  
1.  在中**变量**窗格中，将鼠标悬停的第一行中的彩色条。  
  
     该彩色的条显示程度`Average Time Per Issue`影响服务等级。 工具提示显示每个变量和目标结果的组合的总分数、概率和提升分数。  
  
2.  在中**变量**窗格中，右键单击任意彩色条并选择**副本**。  
  
3.  在 Excel 工作表，右键单击任意单元格并选择**粘贴**。  
  
     报表以 HTML 表格式粘贴，仅显示每个条的分数。  
  
4.  在不同的 Excel 工作表中，右键单击任意单元格，然后选择**选择性粘贴**。  
  
     报表以文本格式粘贴，并包括相关统计信息（如下节所述）。  
  
### <a name="using-the-input-pane"></a>使用“输入”窗格  
 假设您希望看到特定因素所产生的影响，例如班次或操作员数。 您可以通过选择一个特定的变量**输入**窗格中，并**变量**窗格将自动更新，以比较两个以前给定了指定的变量的所选组。  
  
##### <a name="to-review-the-effect-on-service-grade-by-changing-input-attributes"></a>通过更改输入属性查看对服务等级产生的影响  
  
1.  在中**输入**窗格中，对于**属性**，选择 Shift。  
  
2.  有关**值**，选择**AM**。  
  
     **变量**窗格将进行更新以显示模型的影响时 shift **AM**。 所有其他选项保持不变-您将仍然比较最低和最高服务等级。  
  
3.  有关**值**，选择**PM1**。  
  
     **变量**窗格以显示班次更改时影响对模型进行更新。  
  
4.  在中**输入**窗格中，单击下的下一个空白行**属性**，然后选择 Calls。 有关**值**，选择指示最大呼叫数量的范围。  
  
     一个新的输入条件会添加到列表中。 **变量**要显示的某一班次对模型产生的影响，当呼叫量是最高的窗格中更新。  
  
5.  继续更改 Shift 和 Calls 的值可以发现班次、呼叫数量和服务等级之间所有值得注意的相关性。  
  
    > [!NOTE]  
    >  若要清除**输入**窗格中，以便可以使用不同的属性，单击**刷新查看器内容**。  
  
### <a name="interpreting-the-statistics-provided-in-the-viewer"></a>解释查看器中提供的统计信息  
 较长的等待时间是高挂断率的强预测因子，这意味着较差的服务等级。 这似乎是一个明显的结论；但挖掘模型为您提供了一些其他统计数据，以帮助您解释这些趋势。  
  
-   **分数**:指示此变量用于区分结果的整体重要性的值。 分数越高，变量对结果产生的影响就越大。  
  
-   **值 1 的概率**:表示该值对该结果的概率的百分比。  
  
-   **Value 2 的概率**:表示该值对该结果的概率的百分比。  
  
-   **值为 1 的提升**并**值为 2 的提升**:表示用于此特定变量预测 Value 1 和 Value 2 结果的影响的分数。 分数越高，使用该变量预测结果时就越准确。  
  
 下表包含首要影响因素的一些示例值。 例如， **value 1 的概率**为 60.6%并**value 2 的概率**为 8.30%，这意味着，当 Average Time Per Issue 位于 44-70 分钟数的范围中时，60.6%的事例发生在具有最高服务等级 (Value 1) 和 8.30%的情况下是在具有最差服务等级 (Value 2)。  
  
 通过此信息，可以得出一些结论。 较短的呼叫响应时间（范围为 44-70）会严重影响较好的服务等级（范围为 0.00-0.07）。 分数 (92.35) 告诉您此变量非常重要。  
  
 但是，当您向下查看相关因素的列表时，会发现一些其他因素产生的影响更微妙、更难于解释。 例如，班次似乎影响服务，但提升分数和相关概率指示班次不是主要因素。  
  
|特性|ReplTest1|倾向于\<0.07|Favors >= 0.12|  
|---------------|-----------|--------------------|----------------------|  
|Average Time Per Issue|89.087 - 120.000||分数：100<br /><br /> Value1 的概率：4.45 %<br /><br /> Value2 的概率：51.94 %<br /><br /> Value1 的提升：0.19<br /><br /> Value2 的提升：1.94|  
|Average Time Per Issue|44.000 - 70.597|分数：92.35<br /><br /> Value1 的概率：60.06 %<br /><br /> Value2 的概率：8.30 %<br /><br /> Value1 的提升：2.61<br /><br /> Value2 的提升：0.31||  
  
 [返回页首](#bkmk_NNviewer)  
  
##  <a name="bkmk_genviewer"></a> Microsoft 一般内容树查看器  
 通过使用该查看器，您可以查看在处理模型时算法创建的更多详细信息。 **MicrosoftGeneric 内容树查看器**挖掘模型表示为一系列节点，其中每个节点表示有关定型数据已知的知识。 该查看器可用于所有模型，但节点内容根据模型类型而不同。  
  
 对于神经网络模型或逻辑回归模型，您会发现 `marginal statistics node` 特别有用。 该节点包含有关数据中值分布的派生统计信息。 如果希望获取数据摘要而无需编写许多 T-SQL 查询，该信息会很有用。 前一主题中装箱值的图表派生自边际统计信息节点。  
  
#### <a name="to-obtain-a-summary-of-data-values-from-the-mining-model"></a>从挖掘模型中获取数据摘要  
  
1.  在数据挖掘设计器中**挖掘模型查看器**选项卡上，选择\<挖掘模型名称 >。  
  
2.  从**查看器**列表中，选择**Microsoft 一般内容树查看器**。  
  
     刷新挖掘模型的视图会在左侧窗格中显示节点层次结构，并在右侧窗格中显示 HTML 表。  
  
3.  在中**节点标题**窗格中，单击名为 10000000000000000 的节点。  
  
     任何模型中的最顶部节点都始终是模型根节点。 在神经网络模型或逻辑回归模型中，紧位于该节点下方的节点是边际统计信息节点。  
  
4.  在中**节点的详细信息**窗格中，向下滚动直至找到 NODE_DISTRIBUTION 行。  
  
5.  向下滚动 NODE_DISTRIBUTION 表可以查看按照神经网络算法计算的值的分布。  
  
 若要在报表中使用该数据，可以选择并复制特定行的信息，也可以使用下列数据挖掘扩展插件 (DMX) 查询来提取节点的完整内容。  
  
```  
SELECT *   
FROM [Call Center EQ4].CONTENT  
WHERE NODE_NAME = '10000000000000000'  
```  
  
 还可以使用节点层次结构和 NODE_DISTRIBUTION 表中的详细信息来遍历神经网络中的各个路径，并查看来自隐藏层的统计信息。 有关详细信息，请参阅[神经网络模型查询示例](../../2014/analysis-services/data-mining/neural-network-model-query-examples.md)。  
  
 [返回页首](#bkmk_NNviewer)  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [向呼叫中心结构中添加逻辑回归模型&#40;数据挖掘中级教程&#41;](../../2014/tutorials/add-logistic-regression-model-to-call-center-intermediate-data-mining.md)  
  
## <a name="see-also"></a>请参阅  
 [神经网络模型的挖掘模型内容（Analysis Services - 数据挖掘）](../../2014/analysis-services/data-mining/mining-model-content-for-neural-network-models-analysis-services-data-mining.md)   
 [神经网络模型查询示例](../../2014/analysis-services/data-mining/neural-network-model-query-examples.md)   
 [Microsoft 神经网络算法技术参考](../../2014/analysis-services/data-mining/microsoft-neural-network-algorithm-technical-reference.md)   
 [更改挖掘模型中列的离散化](../../2014/analysis-services/data-mining/change-the-discretization-of-a-column-in-a-mining-model.md)  
  
  
