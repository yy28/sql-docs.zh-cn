---
title: 创建预测的呼叫中心模型 （数据挖掘中级教程） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 5be0cec7-f639-4eeb-835e-e3204ae619e9
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 30f24ab457669f572189d2eb13deca3f672f5e18
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63217868"
---
# <a name="creating-predictions-for-the-call-center-models-intermediate-data-mining-tutorial"></a>为呼叫中心模型创建预测（数据挖掘中级教程）
  现在您已经了解了关于班次、操作员人数、呼叫和服务等级之间的交互，您将准备创建一些可用于业务分析和规划的预测查询。 首先您将在探索模型上创建一些预测来测试某些假设。 接下来，您将通过使用逻辑回归模型创建大容量预测。  
  
 本课假定您已经熟悉预测查询的概念。  
  
## <a name="creating-predictions-using-the-neural-network-model"></a>使用神经网络模型创建预测  
 下面的示例演示如何使用为探索阶段创建的神经网络模型进行单独预测。 单独预测是试用不同的值以在模型中查看效果的好办法。 在此方案中，如果六个经验丰富的操作员值夜班，您将预测该夜班的服务等级（未指定星期几）。  
  
#### <a name="to-create-a-singleton-query-by-using-the-neural-network-model"></a>通过使用神经网络模型创建单独查询  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] 中，打开包含要使用的模型的解决方案。  
  
2.  在数据挖掘设计器中，单击**挖掘模型预测**选项卡。  
  
3.  在中**挖掘模型**窗格中，单击**选择模型**。  
  
4.  **选择挖掘模型**对话框显示挖掘结构的列表。 展开挖掘结构可查看与该结构相关联的挖掘模型列表。  
  
5.  展开挖掘结构 Call Center Default，选中神经网络模型 Call Center - LR。  
  
6.  从 **“挖掘模型”** 菜单中选择 **“单独查询”**。  
  
     **单独查询输入**出现对话框，请使用列映射到挖掘模型中的列。  
  
7.  在中**单独查询输入**对话框中，单击 Shift 行，然后选择*午夜*。  
  
8.  单击 Lvl 2 Operators 和类型的行`6`。  
  
9. 在底部的一半**挖掘模型预测**选项卡上，单击网格中的第一行。  
  
10. 在中**源**列中，单击向下箭头，然后选择**预测函数**。 在中**字段**列中，选择**PredictHistogram**。  
  
     可以自动使用此预测函数的参数列表将显示在**条件/参数**框。  
  
11. 将 ServiceGrade 列从列表中的列拖到**挖掘模型**窗格**条件/参数**框。  
  
     列的名称自动作为参数插入。 可以选择任何可预测属性列以便放入此文本框。  
  
12. 单击按钮**切换到查询结果视图**，在预测查询生成器上角。  
  
 预期结果包含对于给定这些输入的每个服务等级可能的预测值，以及对每个预测的支持值和概率值。 您可以随时返回设计视图，更改输入或添加更多输入。  
  
## <a name="creating-predictions-by-using-a-logistic-regression-model"></a>通过使用逻辑回归模型创建预测  
 如果您已经知道与业务问题相关的属性，您就可以使用逻辑回归模型来预测在某些属性中进行更改的效果。 逻辑回归是一种统计方法，常用于基于独立变量中的更改进行预测：例如，它用于财务计分中，以便基于客户人口统计信息来预测客户行为。  
  
 在本任务中，您将学习如何创建将用于预测的数据源，然后进行预测来协助回答一些业务问题。  
  
### <a name="generating-data-used-for-bulk-prediction"></a>生成用于大容量预测的数据  
 有多种方式可提供输入数据：例如，您可以从电子表格中导入人员配备级别，并通过模型运行该数据以预测下个月的服务质量。  
  
 在本课中，您将使用数据源视图设计器创建命名查询。 该命名查询是一个自定义 Transact-SQL 语句，为计划的每个班次计算配备的最多操作员数、接收的最少呼叫数和生成的平均问题数。 然后，您将该数据与一个挖掘模型联接以预测有关未来一系列日期的情况。  
  
##### <a name="to-generate-input-data-for-a-bulk-prediction-query"></a>生成大容量预测查询的输入数据  
  
1.  在解决方案资源管理器中右键单击**数据源视图**，然后选择**新数据源视图**。  
  
2.  在数据源视图向导中，选择[!INCLUDE[ssAWDWsp](../includes/ssawdwsp-md.md)]作为数据源，然后单击**下一步**。  
  
3.  上**选择表和视图**页上，单击**下一步**而不选择任何表。  
  
4.  上**完成向导**页上，键入名称， `Shifts`。  
  
     该名称将作为数据源视图的名称显示在解决方案资源管理器中。  
  
5.  右键单击空设计窗格中，然后选择**新建命名查询**。  
  
6.  在中**创建命名查询**对话框中，对于**名称**，类型`Shifts for Call Center`。  
  
     该名称将仅作为命名查询的名称显示在数据源视图设计器中。  
  
7.  将以下查询语句粘贴到对话框下半部分的 SQL 文本窗格中。  
  
    ```  
    SELECT DISTINCT WageType, Shift,   
    AVG(Orders) as AvgOrders, MIN(Orders) as MinOrders, MAX(Orders) as MaxOrders,  
    AVG(Calls) as AvgCalls, MIN(Calls) as MinCalls, MAX(Calls) as MaxCalls,  
    AVG(LevelTwoOperators) as AvgOperators, MIN(LevelTwoOperators) as MinOperators, MAX(LevelTwoOperators) as MaxOperators,  
    AVG(IssuesRaised) as AvgIssues, MIN(IssuesRaised) as MinIssues, MAX(IssuesRaised) as MaxIssues  
    FROM dbo.FactCallCenter  
    GROUP BY Shift, WageType  
    ```  
  
8.  在设计窗格中，右键单击表 Shifts for Call Center，然后选择**浏览数据**以预览 T-SQL 查询返回的数据。  
  
9. 右键单击选项卡上， **Shifts.dsv (Design)** ，然后单击**保存**以保存新的数据源视图定义。  
  
### <a name="predicting-service-metrics-for-each-shift"></a>预测每个班次的服务标准  
 现在您已经为每个班次生成了一些值，将使用那些值作为您生成的逻辑回归模型的输入，来生成可用于业务规划的一些预测。  
  
##### <a name="to-use-the-new-dsv-as-input-to-a-prediction-query"></a>使用新 DSV 作为预测查询输入  
  
1.  在数据挖掘设计器中，单击**挖掘模型预测**选项卡。  
  
2.  在中**挖掘模型**窗格中，单击**选择模型**中, 选择 Call Center-LR 从可用模型列表。  
  
3.  从**挖掘模型**菜单上，清除选项**单独查询**。 将警告您单独查询输入将丢失。 单击 **“确定”**。  
  
     **单独查询输入**替换为对话框**选择输入表**对话框。  
  
4.  单击“选择事例表” 。  
  
5.  在中**选择表**对话框中，从列表中的数据源的 selectShifts。 在中**表/视图名称**列表中，选择 Shifts for Call Center （它可能会自动选择），并单击**确定。**  
  
     **挖掘模型预测**设计图面上将更新以显示基于列中输入数据和模型的名称和数据类型创建的映射。  
  
6.  右键单击联接线，其中一个，然后选择**修改连接**。  
  
     在此对话框中，您可以确切看到映射了哪些列以及未映射哪些列。 该挖掘模型包含 Calls 列、Orders 列、IssuesRaised 列和 LvlTwoOperators 列，这些列可以映射到您基于源数据中上述列创建的任何聚合中。 在此情况下，您将映射到平均值。  
  
7.  单击 LevelTwoOperators，旁边的空单元格，然后选择**Shifts for Call Center.AvgOperators**。  
  
8.  单击 Calls，选择旁边的空单元格**Shifts for Call Center.AvgCalls**。 然后单击**确定**。  
  
##### <a name="to-create-the-predictions-for-each-shift"></a>创建每个班次的预测  
  
1.  在底部网格中的一半**预测查询生成器**，单击下的空单元格**源，** ，然后选择 Shifts for Call Center。  
  
2.  在下的空单元格**字段**，选择 Shift。  
  
3.  单击网格中的下一个空行并重复实数过程来为 WageType 添加另一行。  
  
4.  单击网格中的下一个空行。 在中**源**列中，选择**预测函数**。 在中**字段**列中，选择**Predict**。  
  
5.  将 ServiceGrade 列从**挖掘模型**窗格到网格中，并进入**条件/参数**单元格。 在中**别名**字段中，键入**Predicted Service Grade**。  
  
6.  单击网格中的下一个空行。 在中**源**列中，选择**预测函数**。 在中**字段**列中，选择**PredictProbability**。  
  
7.  将 ServiceGrade 列从**挖掘模型**窗格到网格中，并进入**条件/参数**单元格。 在中**别名**字段中，键入**概率**。  
  
8.  单击**切换到查询结果视图**可查看预测。  
  
 下表显示了每个班次的示例结果。  
  
|班次|WageType|预测服务等级|概率|  
|-----------|--------------|-----------------------------|-----------------|  
|AM|假日|0.165|0.377520666|  
|午夜|假日|0.105|0.364105573|  
|PM1|假日|0.165|0.40056055|  
|PM2|假日|0.165|0.338532973|  
|AM|weekday|0.165|0.370847617|  
|午夜|weekday|0.08|0.352999173|  
|PM1|weekday|0.165|0.317419177|  
|PM2|weekday|0.105|0.311672027|  
  
### <a name="predicting-the-effect-of-reduced-response-time-on-service-grade"></a>预测缩短响应时间对服务等级的影响  
 您为每个班次生成了一些平均值，并将那些值用作逻辑回归模型的输入。 但是，假定业务目标是将挂断率保持在 0.00-0.05 的范围内，但结果并不令人满意。  
  
 因此，根据原始模型（该模型显示了响应时间对服务等级的巨大影响），业务团队决定运行一些预测，评估缩短响应呼叫的平均时间是否会提高服务质量。 例如，如果您将呼叫响应时间缩短到当前响应时间的 90%，甚至 80%，服务等级值会发生什么变化？  
  
 创建计算每个班次平均响应时间的数据源视图 (DSV)，随后添加计算该平均响应时间的 80% 或 90% 的列，这操作起来很容易。 然后可以将该 DSV 用作模型输入。  
  
 尽管此处未显示确切的步骤，但是下表比较了在您将响应时间缩短到当前响应时间的 80% 或 90% 时对服务等级的影响。  
  
 从这些结果中可以得出结论：对于针对的班次，应将响应时间缩短到当前响应时间的 90% 以提高服务质量。  
  
|班次、工资和日|预测的当前平均响应时间下的服务质量|预测的响应时间缩短为 90％ 时的服务质量|预测减少 80%的响应时间的服务质量|  
|--------------------------|------------------------------------------------------------------|--------------------------------------------------------------------------|--------------------------------------------------------------------------|  
|假日 AM|0.165|0.05|0.05|  
|假日 PM1|0.05|0.05|0.05|  
|假日午夜|0.165|0.05|0.05|  
  
 可以在此模型上创建多种其他预测查询。 例如，您可以预测多少运算符所需满足某些服务级别，或要响应一定数量的传入呼叫。 因为您可以在逻辑回归模型中包括多个输出，所以很容易试用不同的独立变量和结果，而无需创建许多单独的模型。  
  
## <a name="remarks"></a>备注  
 数据挖掘外接 Excel 2007 提供了逻辑回归向导很轻松地回答一些复杂问题，例如多少名二级操作员所需服务等级提高到一个特定班次的目标级别。 数据挖掘外接程序是免费下载的，并包含基于神经网络或逻辑回归算法的向导。 有关更多信息，请参见下列链接：  
  
-   [SQL Server 2005 数据挖掘外接适用于 Office 2007](https://www.microsoft.com/sql/technologies/dm/addins.mspx):目标查找和假设应用场景分析  
  
-   [SQL Server 2008 数据挖掘外接适用于 Office 2007](https://go.microsoft.com/fwlink/?LinkID=117790):目标查找应用场景分析，假设应用场景分析和预测计算器  
  
## <a name="conclusion"></a>结束语  
 您已经学习了创建、自定义和解释基于 Microsoft 神经网络算法和 Microsoft 逻辑回归算法的挖掘模型。 这些模型类型很精细，允许在分析中使用几乎无限种变化，因此会很复杂并难于掌握。  
  
 但是，如果提供模式的统计支持（很难使用 Transact-SQL 或甚至 PowerPivot 通过手动浏览数据来发现），这些算法可以通过因素的很多组合来迭代并自动标识最强的相关性。  
  
## <a name="see-also"></a>请参阅  
 [逻辑回归模型查询示例](../../2014/analysis-services/data-mining/logistic-regression-model-query-examples.md)   
 [Microsoft 逻辑回归算法](../../2014/analysis-services/data-mining/microsoft-logistic-regression-algorithm.md)   
 [Microsoft Neural Network Algorithm](../../2014/analysis-services/data-mining/microsoft-neural-network-algorithm.md)   
 [神经网络模型查询示例](../../2014/analysis-services/data-mining/neural-network-model-query-examples.md)  
  
  
