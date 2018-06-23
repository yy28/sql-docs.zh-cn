---
title: 对挖掘模型应用筛选器 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- model filter [data mining]
- filters [data mining]
- filtering input rows [Analysis Services]
- filtering data [Analysis Services]
ms.assetid: 4d0abeb5-e939-46d3-9097-6e0358244300
caps.latest.revision: 16
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: cb6cdfdf92e5cec0da4e27a78474037e2bd7d70e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36129089"
---
# <a name="apply-a-filter-to-a-mining-model"></a>对挖掘模型应用筛选器
  如果挖掘结构包含嵌套表，则可以对事例表、嵌套表或两者同时应用筛选器。  
  
 以下过程说明了如何创建两种筛选器：事例筛选器和嵌套表行筛选器。  
  
 事例表的条件将客户限制为收入在 30000 到 40000 之间的客户。 嵌套表的条件将客户限制为未购买特定项目的客户。  
  
 本示例中创建的完整筛选条件如下所示：  
  
```  
[Income] > '30000'   
AND  [Income] < '40000'   
AND EXISTS (SELECT * FROM [<nested table name>]   
WHERE [Model] <> 'Water Bottle' )   
```  
  
### <a name="to-create-a-case-filter-on-a-mining-model"></a>创建挖掘模型的事例筛选器  
  
1.  在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]的解决方案资源管理器中，单击包含要筛选的挖掘模型的挖掘结构。  
  
2.  单击 **“挖掘模型”** 选项卡。  
  
3.  选择模型，然后右键单击打开快捷菜单。  
  
     - 或 -  
  
     选择该模型。 然后，在 **“挖掘模型”** 菜单上，选择 **“设置模型筛选器”**。  
  
4.  在 **“模型筛选器”** 对话框的 **“挖掘结构列”** 文本框中，单击网格中的第一行。  
  
5.  如果数据源包含一个平面表，则下拉列表只显示该表中列的名称。  
  
     如果挖掘结构包含多个表，则下拉列表显示源表的名称。 只有选中某个表后，才会显示列名。  
  
     如果挖掘结构包含一个事例表和一个嵌套表，则下拉列表显示事例表中的列和嵌套表的名称。  
  
6.  从下拉列表中选择一列。  
  
     文本框左侧的图标会发生改变，以指示所选项是表还是列。  
  
7.  单击 **“运算符”** 文本框并从列表中选择一个运算符。 有效的运算符会根据所选列的数据类型而不同。  
  
8.  单击 **“值”** 文本框，然后在此框中键入一个值。  
  
     例如，选择`Income`为列中，选择的大于运算符 (>)，然后键入比`30000`。  
  
9. 单击网格中的下一行。  
  
     您所创建的筛选条件自动添加到“表达式”文本框中。 例如，使用 IPv4 地址 `[Income] > '30000'`  
  
10. 单击网格下一行中的“AND/OR”文本框，以添加条件。  
  
     例如，若要创建 BETWEEN 条件，请选择`AND`从下拉列表中的逻辑操作数。  
  
11. 按步骤 7 和 8 中所述选择一个运算符并键入一个值。  
  
     例如，选择`Income`为再次列中，选择的小于运算符 (<)，然后键入`40000`。  
  
12. 单击网格中的下一行。  
  
13. “表达式”文本框中的筛选条件自动更新以包含新的条件。 完成的表达式如下： `[Income] > '30000'AND [Income] < '40000'`  
  
### <a name="to-add-a-filter-on-the-nested-table-in-a-mining-model"></a>向挖掘模型中的嵌套表添加筛选器  
  
1.  在**\<名称 > 模型筛选器**对话框框中，单击下的网格中的空行**挖掘结构列**。  
  
2.  从下拉列表中选择嵌套表的名称。  
  
     文本框左侧的图标会发生改变，以指示所选项是表名称。  
  
3.  单击 **“运算符”** 文本框，然后选择 **“包含”** 或 **“不包含”**。  
  
     在 **“模型筛选器”** 对话框中，只有这些条件可用于嵌套表，因为您要将事例表限定为包含嵌套表中某一特定值的那些事例。 在下一步中，您将设置嵌套表条件的值。  
  
4.  单击“值”框，然后单击 **(…)** 按钮以生成一个表达式。  
  
     **\<名称 > 筛选器**对话框随即打开。 此对话框只能设置当前表的条件，本例中当前表是嵌套表。  
  
5.  单击 **“挖掘结构列”** 框并从嵌套表列下拉列表中选择一个列名。  
  
6.  单击 **“运算符”** 并从该列的有效运算符列表中选择一个运算符。  
  
7.  单击 **“值”** 并键入一个值。  
  
     例如，对于**挖掘结构列，** 选择`Model`。 有关**运算符**，选择`<>`，然后键入值`Water Bottle`。 此条件将创建如下的筛选表达式：  
  
```  
EXISTS (SELECT * FROM [<nested table name>] WHERE [Model] <> 'Water Bottle' )   
```  
  
> [!NOTE]  
>  由于嵌套表数属性的数量不受限制，因此， [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 不提供可供选择的可能值的列表。 必须键入一个确切的值。 此外，不能在嵌套表中使用 LIKE 运算符。  
  
1.  根据需要，通过选择来组合条件添加更多条件`AND`或`OR`中**和/或**框的左侧**条件**网格。 [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
2.  在 **“模型筛选器”** 对话框中，使用 **“筛选器”** 对话框检查创建的条件。 嵌套表的条件表将附加到事例表条件中，并在 **“表达式”** 文本框中显示一组完整的筛选条件。  
  
3.  （可选）单击 **“编辑查询”** 以手动更改筛选表达式。  
  
    > [!NOTE]  
    >  如果手动更改筛选表达式的任意部分，则会禁用该网格，以后只能在文本编辑模式下编辑筛选表达式。 若要恢复网格编辑模式，必须清除筛选表达式并重新开始。  
  
  
## <a name="see-also"></a>请参阅  
 [挖掘模型的筛选器&#40;Analysis Services-数据挖掘&#41;](mining-models-analysis-services-data-mining.md)   
 [挖掘模型任务和操作指南](mining-model-tasks-and-how-tos.md)   
 [从挖掘模型中删除筛选器](delete-a-filter-from-a-mining-model.md)  
  
  