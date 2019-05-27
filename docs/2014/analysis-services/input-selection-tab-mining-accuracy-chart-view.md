---
title: 输入所选内容选项卡 （挖掘准确性图表视图） |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.accuracychart.columnmapping.f1
ms.assetid: f8b1193c-5c86-4c7e-8e35-158d293184fa
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3fb4771c7345eb270e91a377d2755a25606f9a93
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66080416"
---
# <a name="input-selection-tab-mining-accuracy-chart-view"></a>“输入选择”选项卡（“挖掘准确性图表”视图）
  可以使用 **“挖掘准确性图表”** 设计器的 **“输入选择”** 选项卡，指定用于测试模型和生成准确性图表的数据源。  
  
 **详细信息：**[测试和验证（数据挖掘）](data-mining/testing-and-validation-data-mining.md)  
  
## <a name="options"></a>选项  
 **同步预测**  **列和值**  
 选中此项可以协调网格中的可预测属性，这样在模型定型期间，即使这些属性具有不同名称，也会从相同的可预测挖掘结构列中派生。  
  
 **注意** 默认情况下此选项处于选中状态。 只有在您知道两个挖掘结构列派生自同一基础关系源或多维源并且这两列包含相同的状态或具有相同的离散程度时，才可清除此框。  
  
 **选择要在提升图中显示的可预测的挖掘模型列**  
 包含的列用于控制提升图中包括的模型以及提升图使用这些模型的方式的网格。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**显示**|选中要在图表中显示的挖掘模型中每个可预测列名称旁边的框。<br /><br /> 如果图表因过于复杂而不便查看，请清除一列或多列旁边的框以简化该图表。<br /><br /> 注意：选择至少一个列，否则无法创建准确性图表。|  
|**挖掘模型**|列出挖掘结构中包含的挖掘模型。|  
|**可预测列名称**|选择用于创建提升图的挖掘模型中包含的可预测列。|  
|**预测值**|为可预测列选择值。 如果保留此项为空白，则提升图将预测模型对于可预测列的所有状态的执行性能。|  
  
 **选择要用于准确性图表的数据集**  
 其中包含用于指定准确性测试数据的三个选项的选项组。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**使用挖掘模型测试事例**|使用在对挖掘结构进行分区时创建的测试集，并应用为模型定义的筛选器。 有关模型筛选器的信息，请参阅 [Filters for Mining Models &#40;Analysis Services - Data Mining&#41;](data-mining/mining-models-analysis-services-data-mining.md)|  
|**使用挖掘结构测试事例**|使用在对挖掘结构进行分区时创建的测试集。|  
|**指定其他数据集**|从现有数据源视图中指定要用作测试数据集的表。|  
  
## <a name="filtering-options"></a>筛选选项  
 如果选择选项 **“指定其他数据集”**，则可以定义数据源视图并创建要应用于这些数据的筛选器。 创建筛选器时，您将在从数据源视图返回测试数据的查询中创建 WHERE 子句。  
  
 **注意** 使用 **“输入选择”** 选项卡无法为挖掘模型指定筛选器。若要创建模型筛选器，请单击 **“挖掘模型”** 选项卡，然后编辑模型属性。  
  
 如果创建挖掘模型时未创建用于测试的维持集，则可以选择此选项并将原始数据源视图指定为测试集。 通过使用此解决方法，您还可以设置原始数据集的筛选器。  
  
 **指定列映射**  
 打开“指定列映射”对话框，在其中可以选择数据源、指定事例表和嵌套表以及将外部数据列映射到挖掘结构列。  
  
 有关详细信息，请参阅[“指定列映射”对话框（挖掘准确性图表）](specify-column-mapping-dialog-box-mining-accuracy-chart.md)。  
  
 **筛选表达式**  
 显示使用筛选器编辑器生成的筛选条件。  
  
 **打开筛选器编辑器**  
 打开“数据集筛选器”对话框（使用该对话框可以选择外部表并对事例表列设置条件）和“筛选器”对话框（该对话框可帮助你生成应用于所选表中各个列或应用于嵌套表中的列的条件）。  
  
## <a name="see-also"></a>请参阅  
 [测试和验证任务和操作指南&#40;数据挖掘&#41;](data-mining/testing-and-validation-tasks-and-how-tos-data-mining.md)   
 [挖掘准确性图表设计器&#40;数据挖掘&#41;](mining-accuracy-chart-designer-data-mining.md)   
 [对挖掘模型应用筛选器](data-mining/apply-a-filter-to-a-mining-model.md)   
 [挖掘模型的筛选器（Analysis Services - 数据挖掘）](data-mining/mining-models-analysis-services-data-mining.md)  
  
  
