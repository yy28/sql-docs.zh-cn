---
title: 创建预测 （数据挖掘基础教程） |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a8410ed2-bb98-4d51-a9eb-b239be1201c2
caps.latest.revision: 42
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: a7544951cd66db857d89187f4db65b4661395c0d
ms.sourcegitcommit: 8c040e5b4e8c7d37ca295679410770a1af4d2e1f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/21/2018
ms.locfileid: "36312335"
---
# <a name="creating-predictions-basic-data-mining-tutorial"></a>创建预测（数据挖掘基础教程）
  在测试挖掘模型的准确性并决定你感到满意结果后，然后可以通过使用预测查询生成器上生成预测**挖掘模型预测**对数据挖掘模型中的选项卡设计器。  
  
 预测查询生成器有三个视图。 与**设计**和**查询**视图，您可以生成并检查你的查询。 然后可以运行查询，并查看中的结果**结果**视图。  
  
 所有预测查询均使用 DMX，DMX 是数据挖掘扩展 (DMX) 语言的简称。 DMX 的语法与 T-SQL 的语法相似，但用于对数据挖掘对象的查询。 虽然 DMX 语法不是复杂的使用类似此一个或中的一个查询生成器[SQL Server 数据挖掘外接 for Office](../../2014/analysis-services/data-mining/sql-server-data-mining-add-ins-for-office.md)，使得更易于选择输入并生成表达式，因此，我们强烈建议你了解基础知识。  
  
## <a name="creating-the-query"></a>创建查询  
 创建预测查询的第一步是选择挖掘模型和输入表。  
  
#### <a name="to-select-a-model-and-input-table"></a>选择模型和输入表  
  
1.  上**挖掘模型预测**数据挖掘设计器选项卡，请在**挖掘模型**框中，单击**选择模型**。  
  
2.  在**选择挖掘模型**对话框框中，浏览到树**目标邮递**结构，展开相应的结构，选择`TM_Decision_Tree`，然后单击**确定**.  
  
3.  在**选择输入表**框中，单击**选择事例表**。  
  
4.  在**选择表**对话框中，在**数据源**列表中，选择数据源视图[!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]。  
  
5.  在**表/视图名称**，选择**ProspectiveBuyer (dbo)** 表，并依次**确定**。  
  
     `ProspectiveBuyer`表与最严格相似**vTargetMail**事例表。  
  
## <a name="mapping-the-columns"></a>映射列  
 选择输入表之后，预测查询生成器便会根据各列的名称在挖掘模型和输入表之间创建默认映射。 结构中至少有一列必须与外部数据中的某列相匹配。  
  
> [!IMPORTANT]  
>  用于确定模型准确性的数据必须包含一个可以映射到可预测列的列。 如果不存在这种列，您可以使用空值创建一列，但该列的数据类型必须与可预测列相同。  
  
#### <a name="to-map-the-inputs-to-the-model"></a>将输入内容映射到模型  
  
1.  右键单击连接的线条**挖掘模型**窗口**选择输入表**窗口中，然后选择**修改连接**。  
  
     请注意，并非每个列都映射。 我们会将映射添加若干个**表列**。 我们还将基于当前的日期列生成新的出生日期列，以便更好地匹配列。  
  
2.  下**表列**，单击`Bike Buyer`单元格，再从下拉列表中选择 ProspectiveBuyer.Unknown。  
  
     这样便将可预测列 [Bike Buyer] 映射到一个输入表列。  
  
3.  单击“确定” 。  
  
4.  在**解决方案资源管理器**，右键单击**目标邮递**数据源视图，并选择**视图设计器**。  
  
5.  右键单击表，ProspectiveBuyer，然后选择**新命名的计算**。  
  
6.  在**创建命名计算**对话框中，为**列名**，类型`calcAge`。  
  
7.  有关**说明**，类型**计算基于出生日期的年龄**。  
  
8.  在**表达式**框中，键入`DATEDIFF(YYYY,[BirthDate],getdate())`，然后单击**确定**。  
  
     因为输入的表中没有**年龄**列对应一个在模型中，你可以使用此表达式来计算客户年龄字段从输入表中的出生日期列。 由于**年龄**被标识为最多有影响力的预测自行车购买列中，它必须存在两个模型中和输入表中。  
  
9. 在数据挖掘设计器中，选择**挖掘模型预测**选项卡并重新打开**修改连接**窗口。  
  
10. 下**表列**，单击**年龄**单元格，再从下拉列表中选择 ProspectiveBuyer.calcAge。  
  
    > [!WARNING]  
    >  如果看不到列表中的列，你可能需要刷新设计器中加载的数据源视图的定义。 为此，请从**文件**菜单上，选择**保存所有**，然后关闭并重新打开设计器中的项目。  
  
11. 单击“确定” 。  
  
## <a name="designing-the-prediction-query"></a>设计预测查询  
  
1.  第一个按钮的工具栏上**挖掘模型预测**选项卡**切换到设计查看 / 切换到结果视图切换到查询视图 /** 按钮。 单击此按钮上的向下箭头，然后选择**设计**。  
  
2.  上的网格中**挖掘模型预测**选项卡上，单击在第一个空行中的单元格**源**列，，然后选择**预测函数**。  
  
3.  在**预测函数**行，在**字段**列中，选择`PredictProbability`。  
  
     在**别名**的同一行中，类型的列**结果的概率**。  
  
4.  从**挖掘模型**窗口更高版本，选择并将 [Bike Buyer] 拖到**条件/参数**单元格。  
  
     当你让转，[TM_Decision_Tree]。[Bike Buyer] 将出现在**条件/参数**单元格。  
  
     这将指定 `PredictProbability` 函数的目标列。 有关函数的详细信息，请参阅[数据挖掘扩展插件&#40;DMX&#41;函数引用](/sql/dmx/data-mining-extensions-dmx-function-reference)。  
  
5.  单击下一步中的空行**源**列，，然后选择 TM_Decision_Tree 挖掘模型 **。**  
  
6.  在`TM_Decision_Tree`行，在**字段**列中，选择`Bike Buyer`。  
  
7.  在`TM_Decision_Tree`行，在**条件/参数**列中，键入`=1`。  
  
8.  单击下一步中的空行**源**列，，然后选择**ProspectiveBuyer 表**。  
  
9. 在`ProspectiveBuyer`行，在**字段**列中，选择**ProspectiveBuyerKey**。  
  
     这会将唯一标识符添加到预测查询中，以便您可以标识谁可能购买自行车，以及谁不可能购买自行车。  
  
10. 向网格中添加五个以上的行。 对于每个行中，选择**ProspectiveBuyer 表**作为**源**，然后添加以下各列在**字段**单元格：  
  
    -   calcAge  
  
    -   LastName  
  
    -   FirstName  
  
    -   AddressLine1  
  
    -   AddressLine2  
  
 最后，运行查询并浏览结果。  
  
 **预测查询生成器**还包括这些控件：  
  
-   **显示**复选框  
  
     可以允许您从查询中移除子句而不从设计器中删除它们。 当您使用复杂查询并想要保留语法而不必将 DMX 复制和粘贴到窗口时，这很有用。  
  
-   **分组**  
  
     在所选行的开头插入一个左括号，或在当前行的结尾插入一个右括号。  
  
-   **和/或**  
  
     在紧挨当前函数或列后面插入 `AND` 或 `OR` 运算符。  
  
#### <a name="to-run-the-query-and-view-results"></a>运行查询并查看结果  
  
1.  在**挖掘模型预测**选项卡上，选择**结果**按钮。  
  
2.  运行查询并显示结果后，您可以查看结果。  
  
     **挖掘模型预测**选项卡显示很可能是自行车购买者的潜在客户的联系信息。 **结果的概率**列指示正确预测的概率。 您可以使用这些结果来确定向哪些潜在客户发送电子邮件。  
  
3.  此时您可以保存结果。 您有三种选择：  
  
    -   右键单击在结果中，数据行，然后选择**复制**将只是该值 （和列标题） 保存到剪贴板。  
  
    -   右键单击任何行在结果中，然后选择**复制所有**要复制整个结果集，包括列标题，到剪贴板。  
  
    -   单击**保存查询结果**，如下所示将结果保存到数据库的直接：  
  
        1.  在**保存数据挖掘查询结果**对话框中，选择数据源，或定义新的数据源。  
  
        2.  键入将包含查询结果的表的名称。   
  
        3.  使用选项，**将添加到 DSV**，若要创建表，然后将其添加到现有的数据源视图。 如果您想在同一数据源视图中保留模型的所有相关表（如定型数据、预测源数据和查询结果），此选项很有用。  
  
        4.  使用选项，**覆盖如果存在**，以使用最新结果更新现有表。  
  
             如果您将任何列添加到了预测查询、更改了预测查询中任何列的名称或数据类型，或者对目标表运行了任何 ALTER 语句，必须使用此选项来覆盖表。  
  
             此外，如果多个列具有相同的名称 (例如，默认列名**表达式**) 必须具有相同名称创建为列别名或设计器将尝试将结果保存到 SQL 时，将引发错误服务器。 原因是 SQL Server 不允许多个列具有相同的名称。  
  
             有关详细信息，请参阅[保存数据挖掘查询结果对话框&#40;挖掘模型预测视图&#41;](../../2014/analysis-services/save-data-mining-query-result-dialog-box-mining-model-prediction-view.md)。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [在数据结构上使用钻取&#40;数据挖掘基础教程&#41;](../../2014/tutorials/using-drillthrough-on-structure-data-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>请参阅  
 [使用预测查询生成器创建预测查询](../../2014/analysis-services/data-mining/create-a-prediction-query-using-the-prediction-query-builder.md)  
  
  
