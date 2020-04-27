---
title: 针对顺序分析和聚类分析模型创建预测（数据挖掘中级教程） |Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 94a8d4f9-a76a-49c5-9785-917010359511
author: minewiskan
ms.author: owend
manager: kfilee
ms.openlocfilehash: 893067e234d868ae6dde2f93d93bfd50458bfeb2
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "63217745"
---
# <a name="creating-predictions-on-a-sequence-clustering-model-intermediate-data-mining-tutorial"></a>针对顺序分析和聚类分析模型创建预测（数据挖掘中级教程）
  通过在查看器中浏览顺序来更好地了解顺序分析和聚类分析模型之后，可以使用数据挖掘设计器中 "**挖掘模型预测**" 选项卡上的预测查询生成器来创建预测查询。 若要创建预测，首先要选择顺序分析和聚类分析模型，然后选择输入数据。 对于输入，可以使用外部数据源，也可以生成单独查询并在对话框中提供值。  
  
 本课程假定您已经熟悉如何使用预测查询生成器，同时希望了解如何针对顺序分析和聚类分析模型生成查询。 有关如何使用预测查询生成器的常规信息，请参阅[数据挖掘查询接口](../../2014/analysis-services/data-mining/data-mining-query-tools.md)或基本数据挖掘教程的部分，[创建 &#40;基本数据挖掘教程&#41;的预测](../../2014/tutorials/creating-predictions-basic-data-mining-tutorial.md)。  
  
## <a name="creating-predictions-on-the-regional-model"></a>针对 Regional 模型创建预测  
 对此方案，您首先需要创建一些单独预测查询，以了解预测结果如何因区域不同而不同。  
  
#### <a name="to-create-a-singleton-query-on-a-sequence-clustering-model"></a>针对顺序分析和聚类分析模型创建单独查询  
  
1.  单击数据挖掘设计器的 "**挖掘模型预测**" 选项卡。  
  
2.  在 "**挖掘模型**列" 菜单中，选择 "**单独查询**"。  
  
     随即出现 "**挖掘模型**" 窗格和 "**单独查询输入**" 窗格。  
  
3.  在 "**挖掘模型**" 窗格中单击 "**选择模型**"。 （如果已选择顺序分析和聚类分析模型，则可跳过此步骤。）  
  
     此时将打开 "**选择挖掘模型**" 对话框。  
  
4.  展开表示挖掘结构**顺序群集**的节点，并选择 "**包含区域**的模型序列"。 单击" **确定**"。 现在，请忽略“输入”窗格；您将在设置预测函数之后指定输入。  
  
5.  在网格中，单击 "**源**" 下的空单元格，然后选择 "**预测函数"。** 在 "**字段**" 下的单元中，选择 " **PredictSequence**"。  
  
    > [!NOTE]  
    >  您也可以使用**Predict**函数。 如果执行此操作，请确保选择采用表列作为参数的**Predict**函数的版本。  
  
6.  在 "**挖掘模型**" 窗格中，选择嵌套`v Assoc Seq Line Items`表，并将其拖到网格中的**PredictSequence**函数的 "**条件/参数**" 框。  
  
     拖放表名称和列名称使您能够生成复杂语句，而不会出现语法错误。 但是，它将替换单元的当前内容，其中包括**PredictSequence**函数的其他可选参数。 为了查看其他参数，可以将函数的另一个实例临时添加到网格供参考。  
  
7.  单击预测查询生成器上角的 "**结果**" 按钮。  
  
 预期结果包含带有标题**表达式**的单个列。 **Expression**列包含一个嵌套表，其中包含三列，如下所示：  
  
|$SEQUENCE|Line Number|型号|  
|---------------|-----------------|-----------|  
|1||Mountain-200|  
  
 这些结果是什么意思？ 请记住，您没有指定任何输入。 因此，该预测针对整个事例，Analysis Services 会返回最可能的总预测。  
  
### <a name="adding-inputs-to-a-singleton-prediction-query"></a>向单独预测查询添加输入  
 到现在为止，您还没有指定任何输入。 在下一任务中，您将使用 "**单独查询输入**" 窗格来指定查询的某些输入。 首先，使用 [Region] 作为区域顺序分析和聚类分析模型的输入，以确定所有区域的预测序列是否都相同。 然后将了解如何修改查询以添加每项查询的概率，并简化结果以便易于查看。  
  
##### <a name="to-generate-predictions-for-a-specific-customer-group"></a>针对特定客户组生成预测  
  
1.  单击预测查询生成器左上角的 "**设计**" 按钮，切换回查询生成网格。  
  
2.  在 "**单独查询输入**" 对话框中，单击 "**值**" `Region`框，然后选择 "**欧洲**"。  
  
3.  单击 "**结果**" 按钮，查看欧洲客户的预测。  
  
4.  单击预测查询生成器左上角的 "**设计**" 按钮，切换回查询生成网格。  
  
5.  在 "**单独查询输入**" 对话框中，单击 "**值**" `Region`框，然后选择 "**北美**"。  
  
6.  单击 "**结果**" 按钮可以查看北美中客户的预测。  
  
### <a name="adding-probabilities-by-using-a-custom-expression"></a>使用自定义表达式添加概率  
 由于概率是预测的特性并且是作为嵌套表输出，所以输出每个预测的概率要稍微复杂一些。 如果您熟悉数据挖掘扩展插件 (DMX)，就可以轻松地更改查询，在嵌套表上添加嵌套 select 语句。 也可以通过添加自定义表达式的方法在预测查询生成器中创建嵌套 select 语句。  
  
##### <a name="to-output-probabilities-for-a-predicted-sequence-by-using-a-custom-expression"></a>使用自定义表达式输出预测序列的概率  
  
1.  单击预测查询生成器左上角的 "**设计**" 按钮，切换回查询生成网格。  
  
2.  在网格中的 "**源**" 下，单击新行，然后选择 "**自定义表达式**"。  
  
3.  将 "**字段**" 下的框留空。  
  
4.  对于 "**别名**" `t`，键入。  
  
5.  在 "**条件/参数**" 框中，键入完整的子 select 语句，如下面的代码示例中所示。 请确保包括开始括号和结束括号。  
  
    ```  
    (SELECT PredictProbability([Model]) FROM PredictSequence([Sequence Clustering with Region].[v Assoc Seq Line Items]))  
    ```  
  
6.  单击 "**结果**" 按钮，查看欧洲客户的预测。  
  
 现在结果包含两个嵌套表，一个包含预测，另一个包含预测的概率。 如果查询不能运行，可以切换到查询设计视图查看完整的查询语句，应该如下所示：  
  
```  
SELECT  
  PredictSequence([Sequence Clustering with Region].[v Assoc Seq Line Items]),  
  ( (SELECT PredictProbability([Model]) FROM PredictSequence([Sequence Clustering with Region].[v Assoc Seq Line Items]))) as [t]  
FROM  
  [Sequence Clustering with Region]  
NATURAL PREDICTION JOIN  
(SELECT 'Europe' AS [Region]) AS t  
```  
  
### <a name="working-with-results"></a>使用结果  
 如果结果中有很多嵌套表，您可能希望简化结果以便查看。 为此，您可以手动修改查询并添加 `FLATTENED` 关键字。  
  
##### <a name="to-flatten-nested-rowsets-in-a-prediction-query"></a>平展预测查询中的嵌套行集  
  
1.  单击预测查询生成器角的 "**查询**" 按钮。  
  
     网格更改为一个打开的窗格，在此您可以查看和修改由预测查询生成器创建的 DMX 语句。  
  
2.  在 `SELECT` 关键字后键入 `FLATTENED`。  
  
     完整的查询文本应与以下内容相似：  
  
    ```  
    SELECT FLATTENED  
      PredictSequence([Sequence Clustering with Region].[v Assoc Seq Line Items]),  
      ( (SELECT PredictProbability([Model]) FROM PredictSequence([Sequence Clustering with Region].[v Assoc Seq Line Items]))) as [t]  
    FROM  
      [Sequence Clustering with Region]  
    NATURAL PREDICTION JOIN  
    (SELECT 'Europe' AS [Region]) AS t  
    ```  
  
3.  单击预测查询生成器上角的 "**结果**" 按钮。  
  
 手动编辑查询之后，将无法切换回设计视图而不丢失更改。 不过，您可以将创建的 DMX 语句手动保存到文本文件，然后更改回设计视图。 这时，查询会恢复到在设计视图中有效的上一版本。  
  
## <a name="creating-predictions-on-the-related-model"></a>根据相关模型创建预测  
 由于您希望了解模型在区域之间是否发现任何差别，所以前面的示例使用了一个事例表列 Region 作为单独预测查询的输入。 但是，浏览了模型之后，您发现差别不足以证明按区域可以生成自定义产品的建议。 您真正感兴趣的是预测客户选择的产品。 因此，在下面的查询中，您将使用不包括 Region 的顺序分析和聚类分析模型来生成对所有客户的建议。  
  
### <a name="using-nested-table-columns-as-input"></a>使用嵌套表列作为输入  
 首先要创建一个单独预测查询，采用单个产品作为输入并返回下一个最可能的产品。 若要获取此类预测，您需要使用嵌套表列作为输入值。 这是因为正在预测的属性 Model 是嵌套表的一部分。 Analysis Services 提供了 "**嵌套表输入**" 对话框，通过使用预测查询生成器，可以帮助您轻松地创建对嵌套表属性的预测查询。  
  
##### <a name="to-use-a-nested-table-as-input-to-a-prediction"></a>使用嵌套表作为预测输入  
  
1.  单击预测查询生成器左上角的 "**设计**" 按钮，切换回查询生成网格。  
  
2.  在 "**单独查询输入**" 对话框中，单击 "**值**" `Region`框，然后选择空行以清除此字段的输入。  
  
3.  在 "**单独查询输入**" 对话框中，单击 "**值**" `vAssocSeqLineItems`框，然后单击 "（...）" 按钮。  
  
4.  在 "**嵌套表输入**" 对话框中，单击 "**添加**"。  
  
5.  在新行中，单击下`Model`的框，然后从列表中选择 "旅行轮胎"。 单击" **确定**"。  
  
6.  单击 "**结果**" 按钮查看预测。  
  
 该模型为选择 Touring Tire 作为第一件商品的所有客户推荐了其他商品。 您已经通过浏览模型了解到，客户经常同时购买 Touring Tire 和 Touring Tire Tube，因此这些建议看来不错。  
  
|$SEQUENCE|Line Number|型号|  
|---------------|-----------------|-----------|  
|1||Touring Tire Tube|  
|2||Sport-100|  
|3||Long-Sleeve Logo Jersey|  
  
### <a name="creating-a-bulk-prediction-query-using-nested-table-inputs"></a>使用嵌套表输入创建大量预测查询  
 现在，对于模型创建的预测可用来进行营销建议您感到很满意，您将创建一个映射到外部数据源的预测查询。 该数据源将提供表示当前产品的值。 您希望创建一个预测查询，以将客户 ID 和产品列表作为输入，因此需要将客户表添加为事例表，将采购表添加为嵌套表。 然后像前面那样，您将添加预测函数创建建议。  
  
 这与您在第 3 课的市场篮方案中创建预测使用的是同一过程；不过，在顺序分析和聚类分析模型预测中还需要将顺序作为输入。  
  
##### <a name="to-create-a-prediction-query-using-nested-table-inputs"></a>使用嵌套表输入创建预测查询  
  
1.  在 "**挖掘模型**" 窗格中，选择 "顺序分析和聚类分析模型" （如果尚未选择）。  
  
2.  在 "**选择输入表**" 对话框中，单击 "**选择事例表**"。  
  
3.  在 "**选择表**" 对话框中，为 "数据源" 选择 Orders。 在 "**表/视图名称**" 列表中，选择 "vAssocSeqOrders"，然后单击 **"确定"**。  
  
4.  在 "**选择输入表**" 对话框中，单击 "**选择嵌套表**"。  
  
5.  在 "**选择表**" 对话框中，为 "**数据源**" 选择 Orders。 在 "**表/视图名称**" 列表中，选择 "vAssocSeqLineItems"，然后单击 **"确定"**。  
  
     Analysis Services 将尝试检测关系，如果数据类型匹配并且列名称相近，将自动创建关系。 如果它创建的关系是错误的，则可以右键单击联接线并选择 "**修改连接**" 来编辑列映射，或者右键单击联接线并选择 "**删除**" 以完全删除该关系。 在此方案中，由于表已经在数据源视图中联接，因此，将在“设计”窗格中自动添加这些关系。  
  
6.  在网格中添加一个新行。 对于 "**源**"，请选择 "vAssocSeqOrders"，对于 "**字段**"，请选择 CustomerKey。  
  
7.  在网格中添加一个新行。 对于 "**源**"，选择 "**预测函数**"，为 "**字段**" 选择**PredictSequence**。  
  
8.  将 vAssocSeqLineItems 拖到 "**条件/参数**" 框中。 单击 "**条件/参数**" 框的末尾，然后键入以下参数： `2`。  
  
     "**条件/参数**" 框中的完整文本应为：`[Sequence Clustering].[v Assoc Seq Line Items],2`  
  
9. 单击 "**结果**" 按钮，查看每个客户的预测。  
  
 您已经完成关于顺序分析和聚类分析模型的教程。  
  
## <a name="next-steps"></a>后续步骤  
 如果您已经完成了数据挖掘模型中的所有部分[&#40;Analysis Services 数据挖掘&#41;](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md)，则下一步可能是了解如何使用数据挖掘扩展插件（DMX）语句来生成模型和生成预测。 有关详细信息，请参阅[利用 DMX 创建和查询数据挖掘模型：教程 &#40;Analysis Services 数据挖掘&#41;](../../2014/tutorials/create-query-data-mining-models-dmx-tutorials.md)。  
  
 如果您熟悉编程概念，您还可以使用分析管理对象 (AMO) 以编程方式处理数据挖掘对象。 有关详细信息，请参阅 [AMO 数据挖掘类](https://docs.microsoft.com/bi-reference/amo/amo-data-mining-classes)。  
  
## <a name="see-also"></a>另请参阅  
 [顺序分析和聚类分析模型查询示例](../../2014/analysis-services/data-mining/sequence-clustering-model-query-examples.md)   
 [顺序分析和聚类分析模型的挖掘模型内容（Analysis Services - 数据挖掘）](../../2014/analysis-services/data-mining/mining-model-content-for-sequence-clustering-models.md)  
  
  
