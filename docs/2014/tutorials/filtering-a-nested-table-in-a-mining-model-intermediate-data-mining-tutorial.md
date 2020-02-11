---
title: 在挖掘模型中筛选嵌套表（数据挖掘中级教程） |Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 0a3ae0e5-897b-4898-a60d-5455eec3d305
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: f57d691587d658e968cd79cf4f4ab4731db29915
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "63267481"
---
# <a name="filtering-a-nested-table-in-a-mining-model-intermediate-data-mining-tutorial"></a>筛选挖掘模型中的嵌套表（数据挖掘中级教程）
  创建并浏览模型后，您决定将精力集中在客户数据的某个子集上。 例如，您可能希望仅分析包含特定项的购物篮，或者可能希望仅分析在某个时间段内没有购买任何物品的客户的人口统计信息。  
  
 
  [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 提供了筛选挖掘模型中所使用数据的功能。 此功能非常有用，因为您无需设置新的数据源视图即可使用不同的数据。 在数据挖掘基础教程中，您学习了如何通过对事例表应用条件来筛选平面表中的数据。 在此任务中，您将创建一个应用于嵌套表的筛选器。  
  
## <a name="filters-on-nested-vs-case-tables"></a>针对嵌套表和针对事例表的筛选器  
 如果您的数据源视图包含一个事例表和一个嵌套表，如 Association 模型中使用的数据源视图，则可以筛选事例表中的值、筛选嵌套表中是否存在某个值，或者这两者的组合。  
  
 在本任务中，您将首选制作 Association 模型的副本，然后将 IncomeGroup 和 Region 属性添加到新的相关模型中，以便您能够筛选事例表中的这些属性。  
  
#### <a name="to-create-and-modify-a-copy-of-the-association-model"></a>创建和修改 Association 模型的副本  
  
1.  在的[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]"**挖掘模型**" 选项卡中，右键`Association`单击该模型，然后选择 "**新建挖掘模型**"。  
  
2.  对于 "**型号名称**" `Association Filtered`，请键入。 对于 "**算法名称**"，请选择 " **Microsoft 关联规则**"。 单击“确定”。   
  
3.  在关联筛选模型的列中，单击 "IncomeGroup" 行，并将值从 "**忽略**" 更改为 "**输入**"。  
  
 接下来，将在新的关联模型中创建一个针对事例表的筛选器。 仅当客户在目标区域中时或者仅当客户达到目标收入水平时，该筛选器才传递给模型。 然后，将添加第二个筛选条件集，以指定模型仅使用其购物篮已至少包含一项的客户。  
  
#### <a name="to-add-a-filter-to-a-mining-model"></a>将筛选器添加到挖掘模型中  
  
1.  在 "**挖掘模型**" 选项卡中，右键单击筛选的模型关联，然后选择 "**设置模型筛选器**"。  
  
2.  在 **“模型筛选器”** 对话框的 **“挖掘结构列”** 文本框中，单击网格中的第一行。  
  
3.  在 "**挖掘结构列**" 文本框中，选择 "IncomeGroup"。  
  
     该文本框左侧的图标会发生改变，以指示所选项是列。  
  
4.  单击 "**运算符**" 文本框，然后从**=** 列表中选择运算符。  
  
5.  单击 "**值**" 文本框，然后在`High`框中键入。  
  
6.  单击网格中的下一行。  
  
7.  单击网格下一行中的 "**和/或**" 文本框，然后选择**或**。  
  
8.  在 "**挖掘结构列**" 文本框中，选择 "IncomeGroup"。 在 "**值**" 文本框中， `Moderate`键入。  
  
     您创建的筛选条件将自动添加到 "**表达式**" 文本框中，并应如下所示：  
  
     `[IncomeGroup] = 'High' OR [IncomeGroup] = 'Moderate'`  
  
9. 单击网格中的下一行，将运算符保留为默认值**和**。  
  
10. 对于 "**运算符**"，保留默认值 "**包含**"。 单击 "**值**" 文本框。  
  
11. 在 "**筛选器**" 对话框中，在 "**挖掘结构列**" 下的`Model`第一行中，选择。  
  
12. 对于 "**运算符**"，选择 "**不为 NULL**"。 将 "**值**" 文本框留空。 单击“确定”。   
  
     "**模型筛选器**" 对话框的 "**表达式**" 文本框中的筛选条件会自动更新，以在嵌套表中包含新的条件。 完成的表达式如下：  
  
     `[IncomeGroup] = 'High' OR [IncomeGroup] = 'Moderate' AND EXISTS SELECT * FROM [vAssocSeqLineItems] WHERE [Model] <> NULL).`  
  
13. [!INCLUDE[clickOK](../includes/clickok-md.md)] ``  
  
#### <a name="to-enable-drillthrough-and-to-process-the-filtered-model"></a>启用钻取并处理筛选后的模型  
  
1.  在 "**挖掘模型**" 选项卡中，右键`Association Filtered`单击该模型，然后选择 "**属性**"。  
  
2.  将**AllowDrillThrough**属性更改为**True**。  
  
3.  右键单击挖掘模型`Association Filtered` ，然后选择 "**处理模型**"。  
  
4.  在错误消息中单击 **"是"** 以将新模型部署[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]到数据库。  
  
5.  在 "**处理挖掘结构**" 对话框中，单击 "**运行**"。  
  
6.  处理完成后，单击 "**关闭**" 退出 "**处理进度**" 对话框，然后再次单击 "**关闭**" 以退出 "**处理挖掘结构**" 对话框。  
  
 您可以通过下面的方法进行验证：使用 Microsoft 一般内容树查看器并查看 NODE_SUPPORT 的值，看筛选模型所包含事例的数目是否小于原始模型中事例的数目。  
  
## <a name="remarks"></a>备注  
 您刚才创建的嵌套表筛选器仅检查嵌套表中是否至少存在一个行；然而，您还可以创建用来检查特定产品是否存在的筛选条件。  例如，可以创建下面的筛选器：  
  
```  
[IncomeGroup] = 'High' AND  
 EXISTS (SELECT * FROM [<nested table name>] WHERE [Model] = 'Water Bottle' )   
```  
  
 此语句表示您正在将事例表中的客户限制为仅为那些已购买水壶的客户。 但是，由于嵌套表属性的数量不受限制，因此，[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 不提供可供选择的可能值的列表。 从而，您必须键入确切的值。  
  
 您可以单击 "**编辑查询**" 以手动更改筛选表达式。 但是，如果手动更改筛选表达式的任意部分，网格都将被禁用，并且此后只能在文本编辑模式下编辑筛选表达式。 若要恢复网格编辑模式，必须清除筛选表达式并重新开始。  
  
> [!WARNING]  
>  不能在嵌套表筛选器中使用 LIKE 运算符。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [预测 &#40;中级数据挖掘教程的关联&#41;](../../2014/tutorials/predicting-associations-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>另请参阅  
 [模型筛选器语法和示例 &#40;Analysis Services 数据挖掘&#41;](../../2014/analysis-services/data-mining/model-filter-syntax-and-examples-analysis-services-data-mining.md)   
 [挖掘模型的筛选器 &#40;Analysis Services 数据挖掘&#41;](../../2014/analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md)  
  
  
