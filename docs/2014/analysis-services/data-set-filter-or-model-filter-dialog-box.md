---
title: 数据集筛选器或模型筛选器对话框 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: a9602174-b7e2-4e16-8ded-dfd8eb9264d7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 89ba538c3ac3dfd7a262e4ae17cb9ddd6cf7265c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66082613"
---
# <a name="data-set-filter-or-model-filter-dialog-box"></a>“数据集筛选器或模型筛选器”对话框
  此对话框帮助您生成可应用于数据集的筛选器。  数据集可以是用于测试的外部数据集，也可以是挖掘模型的事例数据。 根据筛选器是用于外部数据集还是用于挖掘模型，对话框的名称会发生更改。  
  
 如果将筛选器应用于新数据集，则仅使用满足条件的数据集中的事例来评估数据挖掘模型。 如果将筛选器应用于挖掘模型本身，则仅使用满足筛选条件的现有测试数据集中的事例来为该模型定型并对其进行测试。  
  
-   可以从 **“挖掘准确性图表”** 设计器的 **“输入选择”** 选项卡中访问 **“数据集筛选器”** 对话框。  
  
-   可从数据挖掘设计器的“挖掘模型”选项卡中访问“模型筛选器”对话框。  
  
-   **“条件”** 网格包含可指定表或列名称、运算符和目标值的列。 使用此网格时，实质上是创建 WHERE 子句。  
  
> [!TIP]  
>  若要根据原始定型数据的子集测试准确性，可以添加用于将定型集定义为外部测试数据的数据源视图，然后在“数据集筛选器”网格中添加条件。  
  
 **详细信息：**[测试和验证（数据挖掘）](data-mining/testing-and-validation-data-mining.md)  
  
## <a name="options"></a>选项  
 **条件**  
 显示表名，后跟带有条件的列名。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**和/或**|选择运算符以联接多个条件。|  
|**挖掘结构列**|单击此项可选择数据源，然后单击网格中的连续行可添加数据源中的列。<br /><br /> 网格中的第一行指定数据源视图。 选择数据源视图后， **“挖掘结构列”** 会显示一个表图标， **“值”** 字段显示为此数据源定义的所有条件的组合。<br /><br /> 选择数据源后， **“挖掘结构列”** 框提供一个显示该数据源中各个列的下拉列表。|  
|**“运算符”**|从列表中选择运算符。|  
|**ReplTest1**|对于表， **“值”** 字段显示应用于数据源的所有筛选器的组合。 您也可以单击生成 **（...）** 按钮右侧的文本框中，打开**筛选器**对话框并生成条件。|  
  
 **表达式**  
 显示使用网格生成的条件组。  
  
 **编辑查询**  
 更改筛选器编辑模式，以便可以在“表达式”文本框中直接键入筛选表达式。  
  
> [!NOTE]  
>  手动更改筛选表达式后，即使已在 **“输入选择”** 选项卡上的 **“筛选表达式”** 框中保存了该表达式，也不能返回网格编辑模式。如果希望使用网格生成表达式，则必须删除现有的筛选表达式，然后重新开始。  
  
 **恢复查询编辑**  
 使网格还原为先前的状态，并取消对筛选表达式所做的任何更改。  
  
## <a name="see-also"></a>请参阅  
 [测试和验证任务和操作指南&#40;数据挖掘&#41;](data-mining/testing-and-validation-tasks-and-how-tos-data-mining.md)   
 [挖掘准确性图表设计器&#40;数据挖掘&#41;](mining-accuracy-chart-designer-data-mining.md)  
  
  
