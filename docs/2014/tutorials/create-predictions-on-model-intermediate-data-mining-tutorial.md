---
title: 创建预测针对顺序聚类分析模型 （数据挖掘中级教程） |Microsoft Docs
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
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63217745"
---
# <a name="creating-predictions-on-a-sequence-clustering-model-intermediate-data-mining-tutorial"></a>针对顺序分析和聚类分析模型创建预测（数据挖掘中级教程）
  了解群集通过在查看器中浏览模型以获得进一步的序列后，您可以在使用预测查询生成器创建预测查询**挖掘模型预测**数据挖掘设计器中的选项卡。 若要创建预测，首先要选择顺序分析和聚类分析模型，然后选择输入数据。 对于输入，可以使用外部数据源，也可以生成单独查询并在对话框中提供值。  
  
 本课程假定您已经熟悉如何使用预测查询生成器，同时希望了解如何针对顺序分析和聚类分析模型生成查询。 有关如何使用预测查询生成器的常规信息，请参阅[数据挖掘查询接口](../../2014/analysis-services/data-mining/data-mining-query-tools.md)或数据挖掘基础教程中，一部分[创建预测&#40;数据挖掘基础教程&#41;](../../2014/tutorials/creating-predictions-basic-data-mining-tutorial.md).  
  
## <a name="creating-predictions-on-the-regional-model"></a>针对 Regional 模型创建预测  
 对此方案，您首先需要创建一些单独预测查询，以了解预测结果如何因区域不同而不同。  
  
#### <a name="to-create-a-singleton-query-on-a-sequence-clustering-model"></a>针对顺序分析和聚类分析模型创建单独查询  
  
1.  单击**挖掘模型预测**数据挖掘设计器选项卡。  
  
2.  在中**挖掘模型**列菜单中，选择**单独查询**。  
  
     **挖掘模型**窗格和**单独查询输入**窗格中显示。  
  
3.  在中**挖掘模型**窗格中，单击**选择模型**。 （如果已选择顺序分析和聚类分析模型，则可跳过此步骤。）  
  
     **选择挖掘模型**对话框随即打开。  
  
4.  展开表示挖掘结构的节点**Sequence Clustering with Region**，然后选择模型**Sequence Clustering with Region**。 单击“确定”  。 现在，请忽略“输入”窗格；您将在设置预测函数之后指定输入。  
  
5.  在网格中，单击下的空单元格**源**，然后选择**预测函数。** 在下的单元格**字段**，选择**PredictSequence**。  
  
    > [!NOTE]  
    >  此外可以使用**Predict**函数。 如果执行操作，请确保选择的版本**Predict**采用表列作为参数的函数...  
  
6.  在中**挖掘模型**窗格中，选择嵌套的表`v Assoc Seq Line Items`，并为将其拖到网格中**条件/参数**框**PredictSequence**函数。  
  
     拖动和删除表和列的名称，可生成没有语法错误的复杂语句。 但是，它将替换该单元格，其中包括其他可选参数的当前内容**PredictSequence**函数。 为了查看其他参数，可以将函数的另一个实例临时添加到网格供参考。  
  
7.  单击**结果**在预测查询生成器上角的按钮。  
  
 预期的结果包含单个列标题**表达式**。 **表达式**列包含具有三列的嵌套的表，如下所示：  
  
|$SEQUENCE|Line Number|“模型”|  
|---------------|-----------------|-----------|  
|1||Mountain-200|  
  
 这些结果是什么意思？ 请记住，您没有指定任何输入。 因此，该预测针对整个事例，Analysis Services 会返回最可能的总预测。  
  
### <a name="adding-inputs-to-a-singleton-prediction-query"></a>向单独预测查询添加输入  
 到现在为止，您还没有指定任何输入。 在下一个任务，您将使用**单独查询输入**窗格来指定查询的输入。 首先，使用 [Region] 作为区域顺序分析和聚类分析模型的输入，以确定所有区域的预测序列是否都相同。 然后将了解如何修改查询以添加每项查询的概率，并简化结果以便易于查看。  
  
##### <a name="to-generate-predictions-for-a-specific-customer-group"></a>针对特定客户组生成预测  
  
1.  单击**设计**在预测查询生成器，若要切换回查询生成网格的左上角的按钮。  
  
2.  在中**单独查询输入**对话框中，单击**值**框`Region`，然后选择**欧洲**。  
  
3.  单击**结果**按钮，以查看在欧洲客户的预测。  
  
4.  单击**设计**在预测查询生成器，若要切换回查询生成网格的左上角的按钮。  
  
5.  在中**单独查询输入**对话框中，单击**值**框`Region`，然后选择**北美**。  
  
6.  单击**结果**按钮，以查看在北美的客户的预测。  
  
### <a name="adding-probabilities-by-using-a-custom-expression"></a>使用自定义表达式添加概率  
 由于概率是预测的特性并且是作为嵌套表输出，所以输出每个预测的概率要稍微复杂一些。 如果您熟悉数据挖掘扩展插件 (DMX)，就可以轻松地更改查询，在嵌套表上添加嵌套 select 语句。 也可以通过添加自定义表达式的方法在预测查询生成器中创建嵌套 select 语句。  
  
##### <a name="to-output-probabilities-for-a-predicted-sequence-by-using-a-custom-expression"></a>使用自定义表达式输出预测序列的概率  
  
1.  单击**设计**在预测查询生成器，若要切换回查询生成网格的左上角的按钮。  
  
2.  在网格中下,**源**，单击一个新行，然后选择**自定义表达式**。  
  
3.  下的框保留**字段**保留为空。  
  
4.  有关**别名**，类型`t`。  
  
5.  在中**条件/参数**框中，键入完整的嵌套 select 语句，如下面的代码示例中所示。 请确保包括开始括号和结束括号。  
  
    ```  
    (SELECT PredictProbability([Model]) FROM PredictSequence([Sequence Clustering with Region].[v Assoc Seq Line Items]))  
    ```  
  
6.  单击**结果**按钮，以查看在欧洲客户的预测。  
  
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
  
1.  单击**查询**预测查询生成器角的按钮。  
  
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
  
3.  单击**结果**在预测查询生成器上角的按钮。  
  
 手动编辑查询之后，将无法切换回设计视图而不丢失更改。 不过，您可以将创建的 DMX 语句手动保存到文本文件，然后更改回设计视图。 这时，查询会恢复到在设计视图中有效的上一版本。  
  
## <a name="creating-predictions-on-the-related-model"></a>根据相关模型创建预测  
 由于您希望了解模型在区域之间是否发现任何差别，所以前面的示例使用了一个事例表列 Region 作为单独预测查询的输入。 但是，浏览了模型之后，您发现差别不足以证明按区域可以生成自定义产品的建议。 您真正感兴趣的是预测客户选择的产品。 因此，在下面的查询中，您将使用不包括 Region 的顺序分析和聚类分析模型来生成对所有客户的建议。  
  
### <a name="using-nested-table-columns-as-input"></a>使用嵌套表列作为输入  
 首先要创建一个单独预测查询，采用单个产品作为输入并返回下一个最可能的产品。 若要获取此类预测，您需要使用嵌套表列作为输入值。 这是因为正在预测的属性 Model 是嵌套表的一部分。 Analysis Services 提供**嵌套表输入**对话框可以帮助您轻松地创建预测查询与嵌套表属性，使用预测查询生成器。  
  
##### <a name="to-use-a-nested-table-as-input-to-a-prediction"></a>使用嵌套表作为预测输入  
  
1.  单击**设计**在预测查询生成器，若要切换回查询生成网格的左上角的按钮。  
  
2.  在中**单独查询输入**对话框中，单击**值**框`Region`，并选择空行以清除此字段的输入。  
  
3.  在中**单独查询输入**对话框中，单击**值**框`vAssocSeqLineItems`，然后单击 （...） 按钮。  
  
4.  在中**嵌套表输入**对话框中，单击**添加**。  
  
5.  在新行中，单击下的框`Model`，并从列表中选择 Touring Tire。 单击“确定”  。  
  
6.  单击**结果**按钮以查看预测。  
  
 该模型为选择 Touring Tire 作为第一件商品的所有客户推荐了其他商品。 您已经通过浏览模型了解到，客户经常同时购买 Touring Tire 和 Touring Tire Tube，因此这些建议看来不错。  
  
|$SEQUENCE|Line Number|“模型”|  
|---------------|-----------------|-----------|  
|1||Touring Tire Tube|  
|2||Sport-100|  
|3||Long-Sleeve Logo Jersey|  
  
### <a name="creating-a-bulk-prediction-query-using-nested-table-inputs"></a>使用嵌套表输入创建大量预测查询  
 现在，对于模型创建的预测可用来进行营销建议您感到很满意，您将创建一个映射到外部数据源的预测查询。 该数据源将提供表示当前产品的值。 您希望创建一个预测查询，以将客户 ID 和产品列表作为输入，因此需要将客户表添加为事例表，将采购表添加为嵌套表。 然后像前面那样，您将添加预测函数创建建议。  
  
 这与您在第 3 课的市场篮方案中创建预测使用的是同一过程；不过，在顺序分析和聚类分析模型预测中还需要将顺序作为输入。  
  
##### <a name="to-create-a-prediction-query-using-nested-table-inputs"></a>使用嵌套表输入创建预测查询  
  
1.  在中**挖掘模型**窗格中，选择序列聚类分析模型，如果未选中。  
  
2.  在中**选择输入表**对话框中，单击**选择事例表**。  
  
3.  在中**选择表**对话框中，为数据源选择订单。 在中**表/视图名称**列表中，选择 vAssocSeqOrders，，然后单击**确定**。  
  
4.  在中**选择输入表**对话框中，单击**选择嵌套表**。  
  
5.  在中**选择表**对话框中，对于**数据源**，选择订单。 在中**表/视图名称**列表中，选择 vAssocSeqLineItems，然后单击**确定**。  
  
     Analysis Services 将尝试检测关系，如果数据类型匹配并且列名称相近，将自动创建关系。 如果它创建的关系是错误的可右键单击联接线并选择**修改连接**来编辑列映射，或者您可以右键单击联接线并选择**删除**到完全删除关系。 在此方案中，由于表已经在数据源视图中联接，因此，将在“设计”窗格中自动添加这些关系。  
  
6.  在网格中添加一个新行。 有关**源**，选择 vAssocSeqOrders，并为**字段**，选择 CustomerKey。  
  
7.  在网格中添加一个新行。 有关**源**，选择**预测函数**，并为**字段**，选择**PredictSequence**。  
  
8.  将 vAssocSeqLineItems 拖到**条件/参数**框。 单击的末尾**条件/参数**框，然后键入下列参数： `2`。  
  
     中的完整文本**条件/参数**框应为： `[Sequence Clustering].[v Assoc Seq Line Items],2`  
  
9. 单击**结果**按钮，以查看每个客户的预测。  
  
 您已经完成关于顺序分析和聚类分析模型的教程。  
  
## <a name="next-steps"></a>后续步骤  
 如果您已经完成中的所有部分[数据挖掘中级教程&#40;Analysis Services-数据挖掘&#41;](../../2014/tutorials/intermediate-data-mining-tutorial-analysis-services-data-mining.md)下, 一步可能是了解如何使用数据挖掘扩展插件 (DMX) 语句来生成模型和生成预测。 有关详细信息，请参阅[创建和查询数据挖掘模型使用 DMX:教程&#40;Analysis Services-数据挖掘&#41;](../../2014/tutorials/create-query-data-mining-models-dmx-tutorials.md)。  
  
 如果您熟悉编程概念，您还可以使用分析管理对象 (AMO) 以编程方式处理数据挖掘对象。 有关详细信息，请参阅 [AMO 数据挖掘类](https://docs.microsoft.com/bi-reference/amo/amo-data-mining-classes)。  
  
## <a name="see-also"></a>请参阅  
 [顺序分析和聚类分析模型查询示例](../../2014/analysis-services/data-mining/sequence-clustering-model-query-examples.md)   
 [顺序分析和聚类分析模型的挖掘模型内容（Analysis Services - 数据挖掘）](../../2014/analysis-services/data-mining/mining-model-content-for-sequence-clustering-models.md)  
  
  
