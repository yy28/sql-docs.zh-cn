---
title: 创建神经网络结构和模型 （数据挖掘中级教程） |Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- discretization [Analysis Services]
- DISCRETIZED column
- DiscretizationBuckets property
- DiscretizationMethod property
- EQUAL_AREAS method
ms.assetid: 3f16215c-531e-4ecf-a11f-ee7c6a764463
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 6787db165770f944838a312ecd3e0386d161da38
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2019
ms.locfileid: "56037718"
---
# <a name="creating-a-neural-network-structure-and-model-intermediate-data-mining-tutorial"></a>创建神经网络结构和模型（数据挖掘中级教程）
  若要创建数据挖掘模型，必须先使用数据挖掘向导基于新数据源视图创建一个新的挖掘结构。 在本任务中，您将使用该向导创建一个挖掘结构，同时创建一个基于 [!INCLUDE[msCoName](../includes/msconame-md.md)] 神经网络算法的关联挖掘模型。  
  
 由于神经网络非常灵活且可以分析输入和输出的多个组合，因此应试用多种处理数据的方式以获得最佳结果。 例如，你可能想要自定义服务质量数值目标的方式*装箱*，或分组，以满足特定业务要求。 为此，您将向该挖掘结构中添加一个以不同的方式对数值数据进行分组的新列，然后创建一个使用这个新列的模型。 您将使用这些挖掘模型来进行一些浏览。  
  
 最后，在您从神经网络模型中了解到哪些因素对您的业务问题影响最大之后，您需要生成一个单独的预测和记分模型。 需要使用 [!INCLUDE[msCoName](../includes/msconame-md.md)] 逻辑回归算法，该算法基于神经网络模型，但经过优化可用于基于特定输入查找解决方案。  
  
 **步骤**  
  
 [创建默认挖掘结构和模型](#bkmk_defaul)  
  
 [使用离散化可预测列装箱](#bkmk_ColumnCopy)  
  
 [复制列，并更改不同模型的离散化方法](#bkmk_Alias)  
  
 [创建可预测列的别名，以便您可以比较模型](#bkmk_Alias2)  
  
 [处理所有模型](#bkmk_SeedProcess)  
  
## 创建默认呼叫中心结构  <a name="bkmk_defaul"></a>  
  
1.  在解决方案资源管理器中[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]，右键单击**挖掘结构**，然后选择**新建挖掘结构**。  
  
2.  在 **“欢迎使用数据挖掘向导”** 页上，单击 **“下一步”**。  
  
3.  上**选择定义方法**页上，确认**从现有关系数据库或数据仓库**已选择，然后单击**下一步**。  
  
4.  上**创建数据挖掘结构**页上，确认选项**创建具有挖掘模型的挖掘结构**处于选中状态。  
  
5.  单击该选项的下拉列表**想要使用何种数据挖掘技术？**，然后选择**Microsoft 神经网络**。  
  
     由于逻辑回归模型基于神经网络，因此，您可以重用同一结构，添加新的挖掘模型。  
  
6.  单击“下一步” 。  
  
     **选择数据源视图**页将出现。  
  
7.  下**可用数据源视图**，选择`Call Center`，然后单击**下一步**。  
  
8.  上**指定表类型**页上，选择**用例**旁边的复选框**FactCallCenter**表。 未选择任何内容的**DimDate**。 单击“下一步” 。  
  
9. 上**指定定型数据**页上，选择**密钥**列的旁边**FactCallCenterID。**  
  
10. 选择`Predict`并**输入**复选框。  
  
11. 选择**键**，**输入**，和`Predict`复选框，如下表中所示：  
  
    |表/列|键/输入/预测|  
    |---------------------|-------------------------|  
    |AutomaticResponses|输入|  
    |AverageTimePerIssue|输入/预测|  
    |Calls|输入|  
    |DateKey|请勿使用|  
    |DayOfWeek|输入|  
    |FactCallCenterID|Key|  
    |IssuesRaised|输入|  
    |LevelOneOperators|输入/预测|  
    |LevelTwoOperators|输入|  
    |Orders|输入/预测|  
    |ServiceGrade|输入/预测|  
    |班次|输入|  
    |TotalOperators|请勿使用|  
    |WageType|输入|  
  
     请注意已选定多个可预测列。 神经网络算法的优点之一是：它可以分析输入和输出属性的所有可能组合。 您不希望执行此操作对于大型数据集，因为这会成倍增加处理时间...  
  
12. 上**指定列内容和数据类型**页上，验证网格包含的列、 内容类型和下表中所示的数据类型，然后单击**下一步**。  
  
    |“列”|内容类型|数据类型|  
    |-------------|------------------|----------------|  
    |AutomaticResponses|连续|Long|  
    |AverageTimePerIssue|连续|Long|  
    |Calls|连续|Long|  
    |DayOfWeek|离散|Text|  
    |FactCallCenterID|Key|Long|  
    |IssuesRaised|连续|Long|  
    |LevelOneOperators|连续|Long|  
    |LevelTwoOperators|连续|Long|  
    |Orders|连续|Long|  
    |ServiceGrade|连续|双精度|  
    |班次|离散|Text|  
    |WageType|离散|Text|  
  
13. 上**创建测试设置**页上，清除选项时，文本框**测试数据百分比**。 单击“下一步” 。  
  
14. 上**完成向导**页上，对于**挖掘结构名称**，类型`Call Center`。  
  
15. 有关**挖掘模型名称**，类型`Call Center Default NN`，然后单击**完成**。  
  
     **允许钻取**框处于禁用状态，因为您不能钻取到使用神经网络模型的数据。  
  
16. 在解决方案资源管理器，右键单击您刚数据挖掘结构的名称创建，并选择**进程**。  
  
## <a name="use-discretization-to-bin-the-target-column"></a>使用离散化将目标列装箱  
 默认情况下，创建具有数值型可预测属性的神经网络模型时，Microsoft 神经网络算法将该属性视为连续数值。 例如，ServiceGrade 属性在理论上是介于 0.00（应答所有呼叫）和 1.00（挂断所有呼叫）之间的数值。 在此数据集中的值具有以下分布：  
  
 ![服务级别值的分发](../../2014/tutorials/media/skt-service-grade-valuesc.gif "服务级别值的分布")  
  
 因此，处理模型时，输出的分组方式可能会与预期的不同。 例如，如果使用聚类分析来确定最佳值组，该算法将 ServiceGrade 中的值为这样一个：0.0748051948 - 0.09716216215. 尽管此分组在数学上很准确，但此类范围可能对业务用户并没有太大意义。  
  
 在此步骤中，要使结果更直观，您将组数字值以不同的方式，创建数值数据列的副本。  
  
### <a name="how-discretization-works"></a>如何使用离散化  
 Analysis Services 提供了各种装箱或处理数值数据的方法。 下表说明了以三种不同方式处理输出属性 ServiceGrade 所得到的结果的差异：  
  
-   将其视为连续数值。  
  
-   让算法使用聚类分析来确定最佳值划分方式。  
  
-   指定数值按等面积方法装箱。  
  
 默认模型（连续）  
  
|Value|Support|  
|-----------|-------------|  
|Missing|0|  
|0.09875|120|  
  
 以聚类分析方式装箱  
  
|Value|Support|  
|-----------|-------------|  
|\< 0.0748051948|34|  
|0.0748051948 - 0.09716216215|27|  
|0.09716216215 - 0.13297297295|39|  
|0.13297297295 - 0.167499999975|10|  
|>= 0.167499999975|10|  
  
 按等面积装箱  
  
|Value|Support|  
|-----------|-------------|  
|\< 0.07|26|  
|0.07 - 0.00|22|  
|0.09 - 0.11|36|  
|>= 0.12|36|  
  
> [!NOTE]  
>  可以在处理完所有数据后，从模型的边际统计信息节点获取这些统计信息。 有关边际统计信息节点的详细信息，请参阅[神经网络模型的挖掘模型内容&#40;Analysis Services-数据挖掘&#41;](../../2014/analysis-services/data-mining/mining-model-content-for-neural-network-models-analysis-services-data-mining.md)。  
  
 此表中，VALUE 列为您显示了 ServiceGrade 的数值的处理方式。 SUPPORT 列为您显示有多少事例具有此值或属于该范围。  
  
-   **使用连续数字 （默认值）**  
  
     如果使用了默认方法，算法将计算 120 个非重复值的结果，这些值的均值为 0.09875。 您还可以查看缺失值的数目。  
  
-   **装箱的聚类分析**  
  
     如果让 Microsoft 聚类分析算法来确定值的可选分组时，该算法会将 ServiceGrade 的值划分为五个 (5) 范围。 每个范围内的事例数目不是均匀分布的，正如您从 support 列看到的那样。  
  
-   **按等面积装箱**  
  
     如果选择此方法，该算法会强制将值划分到大小相等的 Bucket 中，而这又会更改每个范围的上下限。 您可以指定 Bucket 的数目，但要避免任何 Bucket 中的值少于两个。  
  
 有关装箱选项的详细信息，请参阅[离散化方法&#40;数据挖掘&#41;](../../2014/analysis-services/data-mining/discretization-methods-data-mining.md)。  
  
 或者，而不是使用数字值，可以添加一个单独派生列，该列将服务等级划分为预定义的目标范围，如**最佳**(ServiceGrade \<= 0.05)， **可接受**(0.10 > ServiceGrade > 0.05)，并**较差**(ServiceGrade > = 0.10)。  
  
###  <a name="bkmk_newColumn"></a> 创建列的副本，并更改离散化方法  
 您将创建包含目标属性 ServiceGrade 的挖掘列的副本并将更改对数字进行分组的方式。 可以创建挖掘结构中任何列（包括可预测属性）的多个副本。  
  
 在本教程中，您将使用离散化的等面积方法并指定四个 Bucket。 此方法所产生的分组与您的业务用户所希望的目标值十分接近。  
  
####  <a name="bkmk_ColumnCopy"></a> 若要创建挖掘结构中的列的自定义的副本  
  
1.  在解决方案资源管理器中，双击刚刚创建的挖掘结构。  
  
2.  在挖掘结构选项卡，单击**添加挖掘结构列**。  
  
3.  在中**Select 列**对话框中，从列表中选择 ServiceGrade**源列**，然后单击**确定**。  
  
     一个新的列添加到挖掘结构列的列表中。 默认情况下，这个新的挖掘列具有与现有列相同的名称，并有一个数值后缀，如 ServiceGrade 1。 您可以更改该列的名称，使其更具描述性。  
  
     您还将指定离散化方法。  
  
4.  右键单击 ServiceGrade 1，然后选择**属性**。  
  
5.  在中**属性**窗口中，找到**名称**属性，并将名称更改为**Service Grade Binned** 。  
  
6.  出现一个对话框，询问您是否要对所有相关的挖掘模型列的名称进行同样的更改。 单击 **“否”**。  
  
7.  在中**属性**窗口中，找到的部分**数据类型**并将其展开，如有必要。  
  
8.  将属性 `Content` 的值从 `Continuous` 更改为 `Discretized`。  
  
     以下属性现在可用。 按下表所示更改属性值：  
  
    |属性|默认值|新值|  
    |--------------|-------------------|---------------|  
    |`DiscretizationMethod`|`Continuous`|`EqualAreas`|  
    |`DiscretizationBucketCount`|无值|4|  
  
    > [!NOTE]  
    >  <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationBucketCount%2A> 的默认值实际为 0，这意味着算法将自动确定 Bucket 的最佳数量。 因此，如果希望将该属性的值重置为其默认值，请键入 0。  
  
9. 在数据挖掘设计器中，单击**挖掘模型**选项卡。  
  
     请注意，在您添加挖掘结构列的副本时，该副本的用法标志将自动设置为 `Ignore`。 通常，当您向挖掘结构中添加列的副本时，您不会将该副本与原始列一起用于分析，否则算法会发现两列之间存在可能掩盖其他关系的密切关联。  
  
##  <a name="bkmk_NewModel"></a> 向挖掘结构添加新的挖掘模型  
 至此您已针对目标属性创建了一个新的分组，现在需要添加一个使用该离散化列的新挖掘模型。 完成后，CallCenter 挖掘结构将有两个挖掘模型：  
  
-   挖掘模型 Call Center Default NN 将 ServiceGrade 值作为连续范围来处理。  
  
-   将创建新的挖掘模型 Call Center Binned NN 将 ServiceGrade 列，分布到四个大小相等的 bucket 的值用作其目标结果。  
  
#### <a name="to-add-a-mining-model-based-on-the-new-discretized-column"></a>添加基于新的离散化列的挖掘模型  
  
1.  在解决方案资源管理器，右键单击您刚在挖掘结构创建，并选择**打开**。  
  
2.  单击 **“挖掘模型”** 选项卡。  
  
3.  单击**创建相关的挖掘模型**。  
  
4.  在中**新建挖掘模型**对话框中，对于**模型名称**，类型`Call Center Binned NN`。 在中**算法名称**下拉列表中选择**Microsoft 神经网络**。  
  
5.  在新挖掘模型中包含的列列表中，找到 ServiceGrade，将用法从 `Predict` 改为 `Ignore`。  
  
6.  同样，找到 ServiceGrade Binned，将用法从 `Ignore` 改为 `Predict`。  
  
##  <a name="bkmk_Alias2"></a> 为目标列创建别名  
 通常，您不能比较使用不同可预测属性的挖掘模型。 但是，您可以为挖掘模型列创建别名。 以便它具有与原始列相同的名称，也就是说，可以重命名的列，ServiceGrade Binned，挖掘模型中。 然后可以在一个准确性图表中直接比较这两个模型，即使数据是以不同的方式离散化的也是如此。  
  
###  <a name="bkmk_Alias"></a> 若要在挖掘模型中添加挖掘结构列的别名  
  
1.  在中**挖掘模型**选项卡上，在**结构**，选择 ServiceGrade Binned。  
  
     请注意，**属性**窗口显示 ScalarMiningStructure 列对象的属性。  
  
2.  在挖掘模型列 ServiceGrade Binned NN 下方单击与 ServiceGrade Binned 列对应的单元格。  
  
     请注意现在**属性**窗口显示对象 MiningModelColumn 的属性。  
  
3.  找到**名称**属性，并将值更改为`ServiceGrade`。  
  
4.  找到**描述**属性，然后键入**临时列别名**。  
  
     **属性**窗口应包含以下信息：  
  
    |属性|ReplTest1|  
    |--------------|-----------|  
    |**说明**|Temporary column alias|  
    |**ID**|ServiceGrade Binned|  
    |**建模标志**||  
    |**名称**|Service Grade|  
    |**SourceColumn ID**|Service Grade 1|  
    |**Usage**|Predict|  
  
5.  在任意位置单击**挖掘模型**选项卡。  
  
     网格进行更新以显示新的临时列别名`ServiceGrade`，在列用法旁边。 包含挖掘结构及两个挖掘模型的网格应如下所示：  
  
    |结构|Call Center Default NN|Call Center Binned NN|  
    |---------------|----------------------------|---------------------------|  
    ||Microsoft 神经网络|Microsoft 神经网络|  
    |AutomaticResponses|输入|输入|  
    |AverageTimePerIssue|Predict|Predict|  
    |Calls|输入|输入|  
    |DayOfWeek|输入|输入|  
    |FactCallCenterID|Key|Key|  
    |IssuesRaised|输入|输入|  
    |LevelOneOperators|输入|输入|  
    |LevelTwoOperators|输入|输入|  
    |Orders|输入|输入|  
    |ServceGrade Binned|Ignore|预测 (ServiceGrade)|  
    |ServiceGrade|Predict|Ignore|  
    |班次|输入|输入|  
    |Total Operators|输入|输入|  
    |WageType|输入|输入|  
  
## <a name="process-all-models"></a>处理所有模型  
 最后，为了确保您创建的模型易于比较，将为默认模型和装箱模型均设置种子参数。 设置种子值可保证每个模型都从同一点开始处理数据。  
  
> [!NOTE]  
>  如果不为种子参数指定一个数值，SQL Server Analysis Services 将基于模型的名称来生成一个种子。 由于这些模型始终具有不同的名称，因此您必须设置一个种子值，以确保这两个模型按相同的顺序来处理数据。  
  
###  <a name="bkmk_SeedProcess"></a> 若要指定的种子并处理模型  
  
1.  在中**挖掘模型**选项卡上，该模型名为 Call Center-LR，右键单击该列并选择**设置算法参数**。  
  
2.  在 HOLDOUT_SEED 参数所在的行，单击下的空单元格**值**，然后键入`1`。 单击“确定” 。 对与此结构关联的每个模型重复此步骤。  
  
    > [!NOTE]  
    >  选择哪个值作为种子无关紧要，关键是您需要对所有相关模型使用同一个种子。  
  
3.  在中**挖掘模型**菜单中，选择**处理挖掘结构和所有模型**。 单击**是**将更新后的数据挖掘项目部署到服务器。  
  
4.  在中**处理挖掘模型**对话框中，单击**运行**。  
  
5.  单击**关闭**以关闭**处理进度**对话框中，然后单击**关闭**中再次**处理挖掘模型**对话框。  
  
 至此您已创建两个相关的挖掘模型，接下来将浏览数据以发现数据中的关系。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [探索呼叫中心模型&#40;数据挖掘中级教程&#41;](../../2014/tutorials/exploring-the-call-center-model-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>请参阅  
 [挖掘结构（Analysis Services - 数据挖掘）](../../2014/analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)  
  
  
