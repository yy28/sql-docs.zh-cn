---
title: 筛选对话框 （挖掘准确性图表） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 71e884a9-7ec4-4459-a4c4-87f6c796d478
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 87d3273367196d2c0c60780a3f1fa125c0b3bf8e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62731332"
---
# <a name="filter-dialog-box-mining-accuracy-chart"></a>“筛选器”对话框（挖掘准确性图表）
  **“筛选器”** 对话框有助于生成可应用于数据集的条件。 数据集可以是用于测试的外部数据集，也可以是定型挖掘模型所使用的事例数据。 此对话框有助于生成可在 **“数据集筛选器”** 对话框或 **“模型筛选器”** 对话框中作为较复杂筛选条件的一部分进行保存的条件。  
  
-   可以从 **“挖掘准确性图表”** 设计器的 **“输入选择”** 选项卡中访问 **“数据集筛选器”** 对话框。  
  
-   可以从数据挖掘设计器的 **“挖掘模型”** 选项卡中访问 **“模型筛选器”** 对话框。  
  
 如果要将筛选器应用于挖掘模型，则首先使用 **“模型筛选器”** 对话框选择一个表。 然后，可以使用 **“筛选器”** 对话框生成仅应用于该表的条件。  
  
 如果要创建应用于外部测试数据集的筛选器，则首先使用 **“数据集筛选器”** 对话框从数据源视图的表列表中选择一个表。 然后，使用 **“筛选器”** 对话框生成仅应用于该表的条件。  
  
 创建一组应用于单个表的条件后， [!INCLUDE[clickOK](../includes/clickok-md.md)]。 在 **“筛选器”** 对话框中所做的更改会自动添加到父对话框 **“数据集筛选器”** 或 **“模型筛选器”** 中的筛选表达式。  
  
 如果将筛选器应用于新数据集，则现有数据挖掘模型将仅用于评估数据集中满足条件的事例。 但如果将筛选器应用于挖掘模型本身，则仅针对挖掘模型中满足这些条件的事例评估模型的准确性。  
  
 **详细信息：**[测试和验证（数据挖掘）](data-mining/testing-and-validation-data-mining.md)  
  
## <a name="options"></a>选项  
 **条件**  
 一个网格，其中包含为在“数据集筛选器”对话框中选择的表中的列指定条件的列。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**和/或**|单击此项可指定是将 AND 运算符还是 OR 运算符应用于此行中的条件。 仅在从 **“挖掘结构列”** 列表中选择一列后，这些值才可用。|  
|**挖掘结构列**|单击此项可从表中包含的列的列表中选择一列，该表是从 **“数据集筛选器”** 对话框的数据源中选择的。|  
|**“运算符”**|从列表中选择运算符。 可用的运算符取决于列的数据类型。<br /><br /> 如果列包含离散值，则只有以下运算符可用：<br /><br /> =（等于）、<>（不等于）、IS NOT NULL、IS NULL。<br /><br /> 如果列包含连续值，则还支持进行大于和小于运算的运算符。|  
|**ReplTest1**|键入要用作条件的值。|  
  
## <a name="see-also"></a>请参阅  
 [测试和验证任务和操作指南&#40;数据挖掘&#41;](data-mining/testing-and-validation-tasks-and-how-tos-data-mining.md)   
 [挖掘准确性图表设计器&#40;数据挖掘&#41;](mining-accuracy-chart-designer-data-mining.md)  
  
  
