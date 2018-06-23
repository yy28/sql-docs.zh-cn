---
title: 预测关联 （数据挖掘中级教程） |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 9140c5f2-b340-45a6-9c27-d870d15aafea
caps.latest.revision: 21
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: e20e747900d63ae13892b919f45be2f11f5c094b
ms.sourcegitcommit: 8c040e5b4e8c7d37ca295679410770a1af4d2e1f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/21/2018
ms.locfileid: "36313025"
---
# <a name="predicting-associations-intermediate-data-mining-tutorial"></a>预测关联（数据挖掘中级教程）
  在处理模型后，您可以使用模型中存储的关联的相关信息来创建预测。 在本课程的最后一个任务中，您将了解如何针对所创建的关联模型生成预测查询。 本课程假定您已经熟悉了如何使用预测查询生成器，同时希望了解如何生成针对关联模型的预测查询。 有关详细信息如何使用预测查询生成器，请参阅[数据挖掘查询接口](../../2014/analysis-services/data-mining/data-mining-query-tools.md)。  
  
## <a name="creating-a-singleton-prediction-query"></a>创建单独预测查询  
 针对关联模型的预测查询可能非常有用：  
  
-   基于以前或相关的采购，向客户提出物料方面的建议  
  
-   查找相关事件。  
  
-   标识事务集中或事务集之间的关系。  
  
 若要生成预测查询，请先选择要使用的关联模型，然后指定输入数据。 输入可以来自外部数据源（例如值列表），也可以生成单独查询并随时提供值。  
  
 对此方案，您首先需要创建一些单独预测查询，以了解预测是如何运行的。 然后您将创建一个批预测的查询，以便根据客户当前的购买情况提出建议。  
  
#### <a name="to-create-a-prediction-query-on-an-association-model"></a>针对关联模型创建预测查询  
  
1.  单击**挖掘模型预测**数据挖掘设计器选项卡。  
  
2.  在**挖掘模型**窗格中，单击**选择模型**。 （如果已选择正确的模型，则可跳过此步骤和下一步骤。）  
  
3.  在**选择挖掘模型**对话框框中，展开表示挖掘结构节点**关联**，并选择的模型**关联**。 单击“确定” 。  
  
     现在，可以忽略“输入”窗格。  
  
4.  在网格中，单击下的空单元格**源**和选择**预测函数。** 在下面的单元格中**字段**，选择`PredictAssociation`。  
  
     你还可以使用**预测**函数来预测关联。 如果你执行操作，请务必选择的版本**预测**采用表格列作为自变量的函数。  
  
5.  在**挖掘模型**窗格中，选择嵌套的表`vAssocSeqLineItems`，并为将其拖到网格，**条件/参数**框`PredictAssociation`函数。  
  
     通过拖放表和列名称可以生成没有语法错误的复杂语句。 但是，它将替换该单元格，其中包括用于其他可选自变量的当前内容`PredictAssociation`函数。 为了查看其他参数，可以将函数的另一个实例临时添加到网格供参考。  
  
6.  单击**条件/参数**框中和表名称后键入以下文本： `,3`  
  
     中的完整文本**条件/参数**框应处于，如下所示：  
  
     `[Association].[v Assoc Seq Line Items],3`  
  
7.  单击**结果**的预测查询生成器角的按钮。  
  
 预期的结果包含一个具有标题的单个列**表达式**。 **表达式**列包含一个具有单个列和以下三个行的嵌套的表。 由于未指定输入值，因此这些预测表示整个模型最可能的产品关联。  
  
|“模型”|  
|-----------|  
|Women's Mountain Shorts|  
|Water Bottle|  
|Touring-3000|  
  
 接下来，你将使用**单独查询输入**窗格，可以指定作为查询中，输入的产品和查看最有可能的产品与该项相关联。  
  
#### <a name="to-create-a-singleton-prediction-query-with-nested-table-inputs"></a>创建带有嵌套表输入的单独预测查询  
  
1.  单击**设计**右上方的预测查询生成器，若要切换回查询生成网格的按钮。  
  
2.  上**挖掘模型**菜单上，选择**单独查询**。  
  
3.  在**挖掘模型**对话框中，选择**关联**模型。  
  
4.  在网格中，单击下的空单元格**源**和选择**预测函数。** 在下面的单元格中**字段**，选择`PredictAssociation`。  
  
5.  在**挖掘模型**窗格中，选择嵌套的表`vAssocSeqLineItems`，并为将其拖到网格，**条件/参数**框`PredictAssociation`函数。 类型`,3`后的嵌套的表名称前面的过程中一样。  
  
6.  在**单独查询输入**对话框中，单击**值**旁边框**vAssoc Seq 行项**，然后单击 **（...）** 按钮。  
  
7.  在**嵌套表输入**对话框中，选择`Touring Tire`中**键列**窗格中，，然后单击**添加**。  
  
8.  单击**结果**按钮。  
  
 现在结果显示最可能与 Touring Tire 关联的产品的预测。  
  
|“模型”|  
|-----------|  
|Touring Tire Tube|  
|Sport-100|  
|Water Bottle|  
  
 但是，您已经通过浏览模型了解到，客户经常同时购买 Touring Tire 和 Touring Tire Tube；您更愿意了解您能够向同时购买这些商品的客户推荐哪些产品。 您将更改查询以便根据市场篮中的两个项目预测相关产品。 您还将修改查询以添加所有预测产品的概率。  
  
#### <a name="to-add-inputs-and-probabilities-to-the-singleton-prediction-query"></a>向单独预测查询添加输入和概率  
  
1.  单击**设计**右上方的预测查询生成器，若要切换回查询生成网格的按钮。  
  
2.  在**单独查询输入**对话框中，单击**值**旁边框**vAssoc Seq 行项**，然后单击 **（...）** 按钮。  
  
3.  在**键列**窗格中，选择`Touring Tire`，然后单击**添加**。  
  
4.  在网格中，单击下的空单元格**源**和选择**预测函数。** 在下面的单元格中**字段**，选择`PredictAssociation`。  
  
5.  在**挖掘模型**窗格中，选择嵌套的表`vAssocSeqLineItems`，并为将其拖到网格，**条件/参数**框`PredictAssociation`函数。 类型`,3`后的嵌套的表名称前面的过程中一样。  
  
6.  在**嵌套表输入**对话框中，选择`Touring Tire Tube`中**键列**窗格中，，然后单击**添加**。  
  
7.  在网格中的行中`PredictAssociation`函数中，单击**条件/参数**框中，并更改要添加的自变量，INCLUDE_STATISTICS 的参数。  
  
     中的完整文本**条件/参数**框应处于，如下所示：  
  
     `[Association].[v Assoc Seq Line Items], INCLUDE_STATISTICS, 3`  
  
8.  单击**结果**按钮。  
  
 嵌套表中的结果现在更改为同时显示支持率和概率的预测。 有关如何解释这些值的详细信息，请参阅[挖掘模型内容关联模型的&#40;Analysis Services-数据挖掘&#41;](../../2014/analysis-services/data-mining/mining-model-content-for-association-models-analysis-services-data-mining.md)。  
  
|“模型”|$SUPPORT|$PROBABILITY|$ADJUSTEDPROBABILITY|  
|-----------|--------------|------------------|--------------------------|  
|Sport-100|4334|0.291...|0.252...|  
|Water Bottle|2866|0.192...|0.175...|  
|Patch Kit|2113|0.142...|0.132|  
  
## <a name="working-with-results"></a>使用结果  
 如果结果中有很多嵌套表，您可能希望简化结果以便查看。 为此，您可以手动修改查询并添加 `FLATTENED` 关键字。  
  
#### <a name="to-flatten-nested-rowsets-in-a-prediction-query"></a>平展预测查询中的嵌套行集  
  
1.  单击**SQL**右上方的预测查询生成器的按钮。  
  
     网格更改为一个打开的窗格，在此您可以查看和修改由预测查询生成器创建的 DMX 语句。  
  
2.  在 `SELECT` 关键字后键入 `FLATTENED`。  
  
     查询的完整文本应如下所示：  
  
    ```  
    SELECT FLATTENED  
      PredictAssociation([Association].[v Assoc Seq Line Items],INCLUDE_STATISTICS,3)  
    FROM  
      [Association]  
    NATURAL PREDICTION JOIN  
    (SELECT (SELECT 'Touring Tire' AS [Model]  
      UNION SELECT 'Touring Tire Tube' AS [Model]) AS [v Assoc Seq Line Items]) AS t  
    ```  
  
3.  单击**结果**的预测查询生成器角的按钮。  
  
 请注意，手动编辑查询之后，将无法切换回设计视图而不丢失更改。 如果希望保存查询，可以将创建的 DMX 语句手动复制到一个文本文件中。 更改回设计视图后，查询会恢复到设计视图中有效的上一版本。  
  
## <a name="creating-multiple-predictions"></a>创建多个预测  
 假设您希望根据以往的购买情况了解每个客户的最佳预测。 您可以使用外部数据作为预测查询的输入，例如包含客户 ID 和最近产品购买情况的表。 要求是，这些数据表已经定义为 Analysis Services 数据源视图；而且输入数据必须包含事例和类似模型中使用的嵌套表。 不需要相同的名称，但结构必须相似。 为了实现本教程教学目的，您将使用对模型进行定型的原始表。  
  
#### <a name="to-change-the-input-method-for-the-prediction-query"></a>更改预测查询的输入方法  
  
1.  在**挖掘模型**菜单上，选择**单独查询**同样，若要清除的复选标记。  
  
2.  出现一条错误消息警告您单独查询将丢失。 单击 **“是”**。  
  
     输入的对话框中的名称更改为**选择输入表**。  
  
 您希望创建一个预测查询，以将客户 ID 和产品列表作为输入，因此需要将客户表添加为事例表，将采购表添加为嵌套表。 然后您将添加预测函数来创建建议。  
  
#### <a name="to-create-a-prediction-query-using-nested-table-inputs"></a>使用嵌套表输入创建预测查询  
  
1.  在“挖掘模型”窗格中选择 Association Filtered 模型。  
  
2.  在**选择输入表**对话框中，单击**选择事例表**。  
  
3.  在**选择表**对话框中，为**数据源**，选择 AdventureWorksDW2008。 在**表/视图名称**列表，选择 vAssocSeqOrders，，然后单击**确定**。  
  
     将表 vAssocSeqOrders 添加到窗格中。  
  
4.  在**选择输入表**对话框中，单击**选择嵌套表**。  
  
5.  在**选择表**对话框中，为**数据源**，选择 AdventureWorksDW2008。 在**表/视图名称**列表，选择 vAssocSeqLineItems，，然后单击**确定**。  
  
     将表 vAssocSeqLineItems 添加到窗格中。  
  
6.  在**指定嵌套联接**对话框中，拖动 OrderNumber 字段从事例表，并将其放在嵌套表的 OrderNumber 字段。  
  
     您也可以单击**添加关系**，并通过从列表中选择列创建关系。  
  
7.  在**指定关系**对话框框中，验证 OrderNumber 字段会正确映射，然后单击**确定**。  
  
8.  单击**确定**关闭**指定嵌套联接**对话框。  
  
     在“设计”窗格中将更新事例表和嵌套表，显示将外部数据列连接到模型中的列的联接。 如果关系是错误的你可以右键单击联接线并选择**修改连接**编辑列映射，也可以右击联接线并选择**删除**删除关系完全。  
  
9. 在网格中添加一个新行。 有关**源**，选择**vAssocSeqOrders 表**。 有关**字段**，选择 CustomerKey。  
  
10. 在网格中添加一个新行。 有关**源**，选择**vAssocSeqOrders 表**。 有关**字段**，选择区域。  
  
11. 在网格中添加一个新行。 有关**源**，选择**预测函数**，和**字段**，选择`PredictAssociation`。  
  
12. 将 vAssocSeqLineItems，拖到**条件/参数**框`PredictAssociation`行。 单击末尾**条件/参数**框中，然后键入以下文本： `INCLUDE_STATISTICS,3`  
  
     中的完整文本**条件/参数**框应为： `[Association].[v Assoc Seq Line Items], INCLUDE_STATISTICS, 3`  
  
13. 单击**结果**按钮，以查看每个客户的预测。  
  
 您可以尝试针对多个模型创建一个相似的预测查询，来查看筛选是否会更改预测结果。 有关创建预测和其他类型的查询的详细信息，请参阅[关联模型查询示例](../../2014/analysis-services/data-mining/association-model-query-examples.md)。  
  
## <a name="see-also"></a>请参阅  
 [关联模型的挖掘模型内容&#40;Analysis Services-数据挖掘&#41;](../../2014/analysis-services/data-mining/mining-model-content-for-association-models-analysis-services-data-mining.md)   
 [PredictAssociation &#40;DMX&#41;](/sql/dmx/predictassociation-dmx)   
 [使用预测查询生成器创建预测查询](../../2014/analysis-services/data-mining/create-a-prediction-query-using-the-prediction-query-builder.md)  
  
  
