---
title: 探索呼叫中心模型（数据挖掘中级教程） |Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "63315080"
---
# <a name="exploring-the-call-center-model-intermediate-data-mining-tutorial"></a>探索呼叫中心模型（数据挖掘中级教程）
  您已生成了探索模型，现在可以使用 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 提供的以下工具来了解有关数据的更多信息。  
  
-   [Microsoft 神经网络查看](#bkmk_NNviewer)器 **：** 该查看器位于数据挖掘设计器的 "**挖掘模型查看器**" 选项卡中，旨在帮助您试验数据中的交互。  
  
-   [Microsoft 一般内容树查看器](#bkmk_genviewer) **：** 此标准查看器提供有关算法在生成模型时所发现的模式和统计信息的详细信息。  
  
##  <a name="bkmk_NNviewer"></a>Microsoft 神经网络查看器  
 查看器有三个窗格-**输入**、**输出**和**变量**。  
  
 通过使用 "**输出**" 窗格，可以为可预测属性或依赖变量选择不同的值。 如果模型包含多个可预测属性，则可以从 "**输出属性**" 列表中选择属性。  
  
 "**变量**" 窗格比较您在参与特性或变量方面所选的两个结果。 彩色条直观的表示变量对目标结果的影响程度。 您还可以查看变量的提升分数。 提升分数的计算方法不同，具体取决于使用的挖掘模型类型，但通常会告诉您使用此属性进行预测时在模型中的提高程度。  
  
 通过 "**输入**" 窗格，您可以向模型添加影响方，以尝试各种假设方案。  
  
### <a name="using-the-output-pane"></a>使用“输出”窗格  
 在此初始模型中，您会希望看到各种因素是如何影响服务等级的。 为此，您可以从输出属性列表中选择 "服务级别"，然后通过从 "**值 1** " 和 "**值 2**" 下拉列表中选择范围来比较不同级别的服务。  
  
##### <a name="to-compare-lowest-and-highest-service-grades"></a>比较最低服务等级和最高服务等级  
  
1.  对于 "**值 1**"，请选择具有最小值的范围。 例如，范围 0-0-0.7 表示最低的挂断率，因此为最佳服务级别。  
  
    > [!NOTE]  
    >  根据模型的配置方式，此范围内的确切值可能会有所不同。  
  
2.  对于 "**值 2**"，请选择具有最高值的范围。 例如，值为 >= 0.12 的范围表示最高的放弃率，因此是最差的服务等级。 换句话说，在此班次期间，打电话的客户有 12% 在与代表通话之前就挂断了电话。  
  
     "**变量**" 窗格的内容会进行更新，以比较影响结果值的属性。 因此，左列显示与最佳服务等级关联的属性，右列显示与最差服务等级关联的属性。  
  
### <a name="using-the-variables-pane"></a>使用“变量”窗格  
 在此模型中，它显示`Average Time Per Issue`为一个重要的因素。 此变量指示在不考虑呼叫类型的情况下应答一个呼叫所花费的平均时间。  
  
##### <a name="to-view-and-copy-probability-and-lift-scores-for-an-attribute"></a>查看和复制属性的概率和提升分数  
  
1.  在 "**变量**" 窗格中，将鼠标悬停在第一行中的彩色条上。  
  
     此彩色条显示了对服务`Average Time Per Issue`级别的贡献程度。 工具提示显示每个变量和目标结果的组合的总分数、概率和提升分数。  
  
2.  在 "**变量**" 窗格中，右键单击任何彩色条，然后选择 "**复制**"。  
  
3.  在 Excel 工作表中，右键单击任意单元格并选择 "**粘贴**"。  
  
     报表以 HTML 表格式粘贴，仅显示每个条的分数。  
  
4.  在其他 Excel 工作表中，右键单击任意单元格并选择 "**选择性粘贴**"。  
  
     报表以文本格式粘贴，并包括相关统计信息（如下节所述）。  
  
### <a name="using-the-input-pane"></a>使用“输入”窗格  
 假设您希望看到特定因素所产生的影响，例如班次或操作员数。 您可以使用 "**输入**" 窗格选择特定变量，并且 "**变量**" 窗格会自动更新，以比较指定了指定变量的两个以前选择的组。  
  
##### <a name="to-review-the-effect-on-service-grade-by-changing-input-attributes"></a>通过更改输入属性查看对服务等级产生的影响  
  
1.  在 "**输入**" 窗格中，为 "**属性**" 选择 Shift。  
  
2.  对于 "**值**"，选择 " **AM**"。  
  
     "**变量**" 窗格将更新以显示班次为**AM**时对模型的影响。 所有其他选择保持不变-仍在比较最低和最高服务等级。  
  
3.  对于 "**值**"，请选择**PM1**。  
  
     "**变量**" 窗格将更新以显示班次更改时对模型的影响。  
  
4.  在 "**输入**" 窗格中，单击 "**属性**" 下的下一个空白行，然后选择 "调用"。 对于 "**值**"，请选择指示最大调用数的范围。  
  
     一个新的输入条件会添加到列表中。 "**变量**" 窗格会进行更新，以显示调用量最大时，特定班次对模型的影响。  
  
5.  继续更改 Shift 和 Calls 的值可以发现班次、呼叫数量和服务等级之间所有值得注意的相关性。  
  
    > [!NOTE]  
    >  若要清除**输入**窗格以便使用不同的属性，请单击 "**刷新查看器内容**"。  
  
### <a name="interpreting-the-statistics-provided-in-the-viewer"></a>解释查看器中提供的统计信息  
 较长的等待时间是高挂断率的强预测因子，这意味着较差的服务等级。 这似乎是一个明显的结论；但挖掘模型为您提供了一些其他统计数据，以帮助您解释这些趋势。  
  
-   **评分**：值，该值指示此变量在结果之间的对比的整体重要性。 分数越高，变量对结果产生的影响就越大。  
  
-   **值1的概率**：表示此结果的此值概率的百分比。  
  
-   **值2的概率**：表示此结果的此值概率的百分比。  
  
-   **提升值 1**并**提升值 2**：表示使用此特定变量预测值1和值2结果的影响的分数。 分数越高，使用该变量预测结果时就越准确。  
  
 下表包含首要影响因素的一些示例值。 例如，**值1的概率**为60.6%，值为**2 的概率**是8.30%，这意味着，每个问题的平均时间都在44-70 分钟的时间范围内60.6，这两个事例的平均时间在最高服务等级（值为1）的移位范围内，而8.30% 的事例中的服务等级为（值2）。  
  
 通过此信息，可以得出一些结论。 较短的呼叫响应时间（范围为 44-70）会严重影响较好的服务等级（范围为 0.00-0.07）。 分数 (92.35) 告诉您此变量非常重要。  
  
 但是，当您向下查看相关因素的列表时，会发现一些其他因素产生的影响更微妙、更难于解释。 例如，班次似乎影响服务，但提升分数和相关概率指示班次不是主要因素。  
  
|Attribute|值|优先\< 0.07|优先 >= 0.12|  
|---------------|-----------|--------------------|----------------------|  
|Average Time Per Issue|89.087-120.000||分数：100<br /><br /> Value1 的概率：4.45%<br /><br /> Value2 的概率：51.94%<br /><br /> 用于 Value1：0.19 的提升<br /><br /> Value2 的提升：1.94|  
|Average Time Per Issue|44.000-70.597|分数：92.35<br /><br /> Value1 的概率：60.06%<br /><br /> Value2 的概率：8.30%<br /><br /> Value1 的提升：2.61<br /><br /> Value2 的提升：0.31||  
  
 [返回页首](#bkmk_NNviewer)  
  
##  <a name="bkmk_genviewer"></a>Microsoft 一般内容树查看器  
 通过使用该查看器，您可以查看在处理模型时算法创建的更多详细信息。 **MicrosoftGeneric 内容树查看器**将挖掘模型表示为一系列节点，其中每个节点表示有关定型数据的已知知识。 该查看器可用于所有模型，但节点内容根据模型类型而不同。  
  
 对于神经网络模型或逻辑回归模型，您会发现 `marginal statistics node` 特别有用。 该节点包含有关数据中值分布的派生统计信息。 如果希望获取数据摘要而无需编写许多 T-SQL 查询，该信息会很有用。 前一主题中装箱值的图表派生自边际统计信息节点。  
  
#### <a name="to-obtain-a-summary-of-data-values-from-the-mining-model"></a>从挖掘模型中获取数据摘要  
  
1.  在数据挖掘设计器的 "**挖掘模型查看**器" 选项\<卡中，选择 "挖掘模型名称">。  
  
2.  从 "**查看器**" 列表中，选择 " **Microsoft 一般内容树查看器**"。  
  
     刷新挖掘模型的视图会在左侧窗格中显示节点层次结构，并在右侧窗格中显示 HTML 表。  
  
3.  在 "**节点标题**" 窗格中，单击名称为10000000000000000的节点。  
  
     任何模型中的最顶部节点都始终是模型根节点。 在神经网络模型或逻辑回归模型中，紧位于该节点下方的节点是边际统计信息节点。  
  
4.  在 "**节点详细信息**" 窗格中，向下滚动，直到找到行 NODE_DISTRIBUTION。  
  
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
 [向呼叫中心结构中添加逻辑回归模型 &#40;中级数据挖掘教程&#41;](../../2014/tutorials/add-logistic-regression-model-to-call-center-intermediate-data-mining.md)  
  
## <a name="see-also"></a>另请参阅  
 [&#40;Analysis Services 数据挖掘的神经网络模型的挖掘模型内容&#41;](../../2014/analysis-services/data-mining/mining-model-content-for-neural-network-models-analysis-services-data-mining.md)   
 [神经网络模型查询示例](../../2014/analysis-services/data-mining/neural-network-model-query-examples.md)   
 [Microsoft 神经网络算法技术参考](../../2014/analysis-services/data-mining/microsoft-neural-network-algorithm-technical-reference.md)   
 [更改挖掘模型中列的离散化](../../2014/analysis-services/data-mining/change-the-discretization-of-a-column-in-a-mining-model.md)  
  
  
