---
title: 筛选挖掘模型 （数据挖掘中级教程） 中的嵌套的表 |Microsoft Docs
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
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63267481"
---
# <a name="filtering-a-nested-table-in-a-mining-model-intermediate-data-mining-tutorial"></a>筛选挖掘模型中的嵌套表（数据挖掘中级教程）
  创建并浏览模型后，您决定将精力集中在客户数据的某个子集上。 例如，您可能希望仅分析包含特定项的购物篮，或者可能希望仅分析在某个时间段内没有购买任何物品的客户的人口统计信息。  
  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 提供了筛选挖掘模型中所使用数据的功能。 此功能很有用，因为不需要设置新的数据源视图，以使用不同的数据。 在数据挖掘基础教程中，您学习了如何通过对事例表应用条件来筛选平面表中的数据。 在此任务中，您将创建一个应用于嵌套表的筛选器。  
  
## <a name="filters-on-nested-vs-case-tables"></a>针对嵌套表和筛选器。事例表  
 如果您的数据源视图包含一个事例表和一个嵌套表，如 Association 模型中使用的数据源视图，则可以筛选事例表中的值、筛选嵌套表中是否存在某个值，或者这两者的组合。  
  
 在本任务中，您将首选制作 Association 模型的副本，然后将 IncomeGroup 和 Region 属性添加到新的相关模型中，以便您能够筛选事例表中的这些属性。  
  
#### <a name="to-create-and-modify-a-copy-of-the-association-model"></a>创建和修改 Association 模型的副本  
  
1.  在中**挖掘模型**选项卡[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]，右键单击`Association`模型并选择**新建挖掘模型**。  
  
2.  有关**模型名称**，类型`Association Filtered`。 有关**算法名称**，选择**Microsoft 关联规则**。 单击“确定” 。  
  
3.  在 Association Filtered 模型的列，单击 IncomeGroup 行并将值从**忽略**到**输入**。  
  
 接下来，将在新的关联模型中创建一个针对事例表的筛选器。 仅当客户在目标区域中时或者仅当客户达到目标收入水平时，该筛选器才传递给模型。 然后，将添加第二个筛选条件集，以指定模型仅使用其购物篮已至少包含一项的客户。  
  
#### <a name="to-add-a-filter-to-a-mining-model"></a>将筛选器添加到挖掘模型中  
  
1.  在中**挖掘模型**选项卡上，右键单击 Association Filtered 模型并选择**设置模型筛选器**。  
  
2.  在 **“模型筛选器”** 对话框的 **“挖掘结构列”** 文本框中，单击网格中的第一行。  
  
3.  在中**挖掘结构列**文本框中，选择 IncomeGroup。  
  
     该文本框左侧的图标会发生改变，以指示所选项是列。  
  
4.  单击**运算符**文本框中，然后选择**=** 运算符从列表中。  
  
5.  单击**值**文本框中，并键入`High`在框中。  
  
6.  单击网格中的下一行。  
  
7.  单击**和/或**文本框中，在下一行中的网格并选择**或**。  
  
8.  在中**挖掘结构列**文本框中，选择 IncomeGroup。 在中**值**文本框中，键入`Moderate`。  
  
     您创建的筛选器条件自动添加到**表达式**文本框中，并应显示，如下所示：  
  
     `[IncomeGroup] = 'High' OR [IncomeGroup] = 'Moderate'`  
  
9. 单击在网格中，保留为默认值，运算符的下一行**AND**。  
  
10. 有关**运算符**，保留默认值**Contains**。 单击**值**文本框。  
  
11. 在中**筛选器**对话框中，在下方的第一行**挖掘结构列**，选择`Model`。  
  
12. 有关**运算符**，选择**IS NOT NULL**。 将保留**值**文本框保留为空。 单击“确定” 。  
  
     中的筛选条件**表达式**的文本框中**模型筛选器**对话框的自动更新以包含嵌套表的新条件。 完成的表达式如下：  
  
     `[IncomeGroup] = 'High' OR [IncomeGroup] = 'Moderate' AND EXISTS SELECT * FROM [vAssocSeqLineItems] WHERE [Model] <> NULL).`  
  
13. [!INCLUDE[clickOK](../includes/clickok-md.md)] ``  
  
#### <a name="to-enable-drillthrough-and-to-process-the-filtered-model"></a>启用钻取并处理筛选后的模型  
  
1.  在中**挖掘模型**选项卡上，右键单击`Association Filtered`模型并选择**属性**。  
  
2.  更改**AllowDrillThrough**属性设置为**True**。  
  
3.  右键单击`Association Filtered`挖掘模型，然后选择**进程模型**。  
  
4.  单击**是**错误消息，若要部署到新的模型中[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]数据库。  
  
5.  在中**处理挖掘结构**对话框中，单击**运行**。  
  
6.  处理完成后单击**关闭**退出**处理进度**对话框中，然后单击**关闭**再次以退出**处理挖掘结构**对话框。  
  
 您可以通过下面的方法进行验证：使用 Microsoft 一般内容树查看器并查看 NODE_SUPPORT 的值，看筛选模型所包含事例的数目是否小于原始模型中事例的数目。  
  
## <a name="remarks"></a>备注  
 您刚才创建的嵌套表筛选器仅检查嵌套表中是否至少存在一个行；然而，您还可以创建用来检查特定产品是否存在的筛选条件。  例如，可以创建下面的筛选器：  
  
```  
[IncomeGroup] = 'High' AND  
 EXISTS (SELECT * FROM [<nested table name>] WHERE [Model] = 'Water Bottle' )   
```  
  
 此语句表示您正在将事例表中的客户限制为仅为那些已购买水壶的客户。 但是，由于嵌套表属性的数量不受限制，因此，[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 不提供可供选择的可能值的列表。 从而，您必须键入确切的值。  
  
 可以单击**编辑查询**以手动更改筛选器表达式。 但是，如果手动更改筛选表达式的任意部分，网格都将被禁用，并且此后只能在文本编辑模式下编辑筛选表达式。 若要恢复网格编辑模式，必须清除筛选表达式并重新开始。  
  
> [!WARNING]  
>  不能在嵌套表筛选器中使用 LIKE 运算符。  
  
## <a name="next-task-in-lesson"></a>课程中的下一个任务  
 [预测关联&#40;数据挖掘中级教程&#41;](../../2014/tutorials/predicting-associations-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>请参阅  
 [模型筛选器语法和示例（Analysis Services – 数据挖掘）](../../2014/analysis-services/data-mining/model-filter-syntax-and-examples-analysis-services-data-mining.md)   
 [挖掘模型的筛选器（Analysis Services - 数据挖掘）](../../2014/analysis-services/data-mining/filters-for-mining-models-analysis-services-data-mining.md)  
  
  
