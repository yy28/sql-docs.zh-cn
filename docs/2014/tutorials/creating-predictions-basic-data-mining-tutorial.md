---
title: 创建预测（数据挖掘基础教程） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: a8410ed2-bb98-4d51-a9eb-b239be1201c2
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 456aec6c6b9d0d1a5d0ee1d9949507a37577130c
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "67597534"
---
# <a name="creating-predictions-basic-data-mining-tutorial"></a>创建预测（数据挖掘基础教程）
  在您测试了挖掘模型的准确性并确定您对结果感到满意后，就可以使用数据挖掘设计器中 "**挖掘模型预测**" 选项卡上的预测查询生成器来生成预测。  
  
 预测查询生成器有三个视图。 利用 "**设计**" 和 "**查询**" 视图，您可以生成并检查查询。 然后，您可以运行查询并在 "**结果**" 视图中查看结果。  
  
 所有预测查询均使用 DMX，DMX 是数据挖掘扩展 (DMX) 语言的简称。 DMX 的语法与 T-SQL 的语法相似，但用于对数据挖掘对象的查询。 尽管 DMX 语法不复杂，但使用与此类似的查询生成器，或者使用[SQL Server Office 数据挖掘外接程序](../../2014/analysis-services/data-mining/sql-server-data-mining-add-ins-for-office.md)中的查询生成器，因此，我们强烈建议你了解基础知识。  
  
## <a name="creating-the-query"></a>创建查询  
 创建预测查询的第一步是选择挖掘模型和输入表。  
  
#### <a name="to-select-a-model-and-input-table"></a>选择模型和输入表  
  
1.  在数据挖掘设计器的 "**挖掘模型预测**" 选项卡上的 "**挖掘模型**" 框中，单击 "**选择模型**"。  
  
2.  在 "**选择挖掘模型**" 对话框中，在树中导航到**目标邮件**结构，展开结构，选择`TM_Decision_Tree`，然后单击 **"确定"**。  
  
3.  在 "**选择输入表**" 框中，单击 "**选择事例表**"。  
  
4.  在 "**选择表**" 对话框的 "**数据源**" 列表中，选择数据源视图[!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]。  
  
5.  在 "**表/视图名称**" 中，选择**ProspectiveBuyer （dbo）** 表，然后单击 **"确定"**。  
  
     `ProspectiveBuyer`该表最接近于**vTargetMail**事例表。  
  
## <a name="mapping-the-columns"></a>映射列  
 选择输入表之后，预测查询生成器便会根据各列的名称在挖掘模型和输入表之间创建默认映射。 结构中至少有一列必须与外部数据中的某列相匹配。  
  
> [!IMPORTANT]  
>  用于确定模型准确性的数据必须包含一个可以映射到可预测列的列。 如果不存在这种列，您可以使用空值创建一列，但该列的数据类型必须与可预测列相同。  
  
#### <a name="to-map-the-inputs-to-the-model"></a>将输入内容映射到模型  
  
1.  右键单击将 "**挖掘模型**" 窗口连接到 "**选择输入表**" 窗口的行，然后选择 "**修改连接**"。  
  
     请注意，并非每个列都映射。 我们将为多个**表列**添加映射。 我们还将基于当前的日期列生成新的出生日期列，以便更好地匹配列。  
  
2.  在 "**表列**" 下， `Bike Buyer`单击单元格，然后从下拉列表中选择 "ProspectiveBuyer"。  
  
     这样便将可预测列 [Bike Buyer] 映射到一个输入表列。  
  
3.  单击" **确定**"。  
  
4.  在**解决方案资源管理器**中，右键单击**目标邮件**数据源视图，然后选择 "**视图设计器**"。  
  
5.  右键单击表 ProspectiveBuyer，然后选择 "**新建命名计算**"。  
  
6.  在 "**创建命名计算**" 对话框中，键入`calcAge`"**列名称**"。  
  
7.  对于 "**说明**"，键入**基于生日计算年龄**。  
  
8.  在 "**表达式**" 框中`DATEDIFF(YYYY,[BirthDate],getdate())`键入，然后单击 **"确定"**。  
  
     由于输入表中没有**Age**列对应于模型中的列，因此您可以使用此表达式来计算输入表中 "出生日期" 列的客户年龄。 由于**Age**被标识为预测自行车购买的最具影响力的列，因此它必须同时存在于模型和输入表中。  
  
9. 在数据挖掘设计器中，选择 "**挖掘模型预测**" 选项卡，然后重新打开 "**修改连接**" 窗口。  
  
10. 在 "**表列**" 下，单击 " **Age** " 单元格，然后从下拉列表中选择 "ProspectiveBuyer"。  
  
    > [!WARNING]  
    >  如果看不到列表中的列，则可能必须刷新设计器中加载的数据源视图的定义。 为此，请在 "**文件**" 菜单中选择 "**全部保存**"，然后关闭并重新打开设计器中的项目。  
  
11. 单击" **确定**"。  
  
## <a name="designing-the-prediction-query"></a>设计预测查询  
  
1.  "**挖掘模型预测**" 选项卡的工具栏上的第一个按钮是 "**设计视图"/"切换到结果视图"/"切换到查询视图**" 按钮。 单击此按钮上的向下箭头，然后选择 "**设计**"。  
  
2.  在 "**挖掘模型预测**" 选项卡上的网格中，单击 "**源**" 列中第一个空行中的单元，然后选择 "**预测函数**"。  
  
3.  在**预测函数**行的 "**字段**" 列中，选择`PredictProbability`。  
  
     在同一行的 "**别名**" 列中，键入**result 的概率**。  
  
4.  在上面的 "**挖掘模型**" 窗口中，选择 "[自行车购买者]" 并将其拖到 "**条件/参数**" 单元中。  
  
     当你开始时，[TM_Decision_Tree]。[自行车购买者] 出现在 "**条件/参数**" 单元中。  
  
     这将指定 `PredictProbability` 函数的目标列。 有关函数的详细信息，请参阅[数据挖掘扩展插件 &#40;DMX&#41; 函数引用](/sql/dmx/data-mining-extensions-dmx-function-reference)。  
  
5.  单击 "**源**" 列中的下一个空行，然后选择**TM_Decision_Tree**挖掘模型 "。  
  
6.  在`TM_Decision_Tree`行的 "**字段**" 列中，选择`Bike Buyer`。  
  
7.  在`TM_Decision_Tree`行的 "**条件/参数**" 列中，键入`=1`。  
  
8.  单击 "**源**" 列中的下一个空行，然后选择 " **ProspectiveBuyer 表**"。  
  
9. 在`ProspectiveBuyer`行的 "**字段**" 列中，选择 " **ProspectiveBuyerKey**"。  
  
     这会将唯一标识符添加到预测查询中，以便您可以标识谁可能购买自行车，以及谁不可能购买自行车。  
  
10. 向网格中添加五个以上的行。 对于每一行，选择 " **ProspectiveBuyer 表**" 作为**源**，然后在 "**字段**" 单元格中添加以下列：  
  
    -   calcAge  
  
    -   LastName  
  
    -   FirstName  
  
    -   AddressLine1  
  
    -   AddressLine2  
  
 最后，运行查询并浏览结果。  
  
 **预测查询生成器**还包括以下控件：  
  
-   **显示**复选框  
  
     可以允许您从查询中移除子句而不从设计器中删除它们。 当您使用复杂查询并想要保留语法而不必将 DMX 复制和粘贴到窗口时，这很有用。  
  
-   **组**  
  
     在所选行的开头插入一个左括号，或在当前行的结尾插入一个右括号。  
  
-   **AND/OR**  
  
     在紧挨当前函数或列后面插入 `AND` 或 `OR` 运算符。  
  
#### <a name="to-run-the-query-and-view-results"></a>运行查询并查看结果  
  
1.  在 "**挖掘模型预测**" 选项卡中，选择 "**结果**" 按钮。  
  
2.  运行查询并显示结果后，您可以查看结果。  
  
     "**挖掘模型预测**" 选项卡显示可能为自行车购买者的潜在客户的联系信息。 Result 列的**概率**表示预测正确的概率。 您可以使用这些结果来确定向哪些潜在客户发送电子邮件。  
  
3.  此时您可以保存结果。 您有三种选择：  
  
    -   右键单击结果中的行数据，然后选择 "**复制**"，只将该值（和列标题）保存到剪贴板。  
  
    -   右键单击结果中的任何行，然后选择 "**全部复制**" 以将整个结果集（包括列标题）复制到剪贴板。  
  
    -   单击 "**保存查询结果**" 将结果直接保存到数据库，如下所示：  
  
        1.  在 "**保存数据挖掘查询结果**" 对话框中，选择数据源或定义新的数据源。  
  
        2.  键入将包含查询结果的表的名称。   
  
        3.  使用选项 "**添加到 DSV**" 创建表并将其添加到现有数据源视图。 如果要在同一数据源视图中保留模型的所有相关表（如定型数据、预测源数据和查询结果），此方法很有用。  
  
        4.  使用 "**如果存在，则覆盖**" 选项来更新具有最新结果的现有表。  
  
             如果您将任何列添加到了预测查询、更改了预测查询中任何列的名称或数据类型，或者对目标表运行了任何 ALTER 语句，必须使用此选项来覆盖表。  
  
             此外，如果多个列具有相同的名称（例如，默认的列名**表达式**），则必须为具有重复名称的列创建一个别名，否则当设计器尝试将结果保存到 SQL Server 时，将引发错误。 原因是 SQL Server 不允许多个列具有相同的名称。  
  
             有关详细信息，请参阅 "[将数据挖掘查询结果保存到 &#40;挖掘模型预测" 视图&#41;](../../2014/analysis-services/save-data-mining-query-result-dialog-box-mining-model-prediction-view.md)。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [对结构数据使用钻取 &#40;基本数据挖掘教程&#41;](../../2014/tutorials/using-drillthrough-on-structure-data-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>另请参阅  
 [使用预测查询生成器创建预测查询](../../2014/analysis-services/data-mining/create-a-prediction-query-using-the-prediction-query-builder.md)  
  
  
