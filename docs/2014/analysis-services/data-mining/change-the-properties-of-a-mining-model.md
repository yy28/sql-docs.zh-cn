---
title: 更改挖掘模型的属性 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining models [Analysis Services], properties
- properties [data mining]
ms.assetid: aefaeb7f-d174-48d1-a188-0987a3b1196b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4c34cbfd2ea88d863239c068300c65531fd19f5f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66085880"
---
# <a name="change-the-properties-of-a-mining-model"></a>更改挖掘模型的属性
  某些挖掘模型属性应用于整个模型，而其他一些模型属性应用于单独的列。 例如，`Drillthrough` 属性就应用于整个模型，它指定事例数据是否应该可用于查询；`Description` 属性也是此类属性。 应用于列的属性包括 `Usage` 和 `ModelingFlags`；它们控制列中的数据在模型内的使用方式。  
  
 下面的模型属性具有可用于创建表达式或配置复杂模型属性的高级编辑器。 以下属性提供：  
  
-   `Filter`属性：打开 "[数据集筛选器" 或 "模型筛选器" 对话框](../data-set-filter-or-model-filter-dialog-box.md)。  
  
-   `AlgorithmParameters`属性：打开 "[算法参数" 对话框 &#40;挖掘模型 "视图&#41;](../algorithm-parameters-dialog-box-mining-models-view.md)。  
  
 有关如何在挖掘模型中设置属性的信息，请参阅[挖掘模型列](mining-model-columns.md)。  
  
### <a name="to-change-the-properties-of-a-mining-model"></a>更改挖掘模型的属性  
  
1.  在数据挖掘设计器的“挖掘模型”选项卡中，右键单击包含挖掘模型名称的列标题，或者网格中包含挖掘算法名称的行，然后选择“属性”********。  
  
2.  在屏幕右侧的 **“属性”** 窗口中，突出显示与要更改的属性对应的值，然后输入新的值。  
  
     在设计器中选择一个不同的元素后，新值即生效。  
  
### <a name="to-change-the-properties-of-a-mining-model-column"></a>更改挖掘模型列的属性  
  
1.  在数据挖掘设计器的“挖掘模型”选项卡中，右键单击网格中位于挖掘结构列与挖掘模型的交叉点处的单元格，然后选择“属性”********。  
  
2.  在屏幕右侧的 **“属性”** 窗口中，突出显示与要更改的属性对应的值，然后输入新的值。  
  
    > [!NOTE]  
    >  如果列用法设置为`Ignore`，则列的 "**属性**" 窗口为空。  
  
     在设计器中选择一个不同的元素后，新值即生效。  
  
## <a name="see-also"></a>另请参阅  
 [挖掘模型任务和操作指南](mining-model-tasks-and-how-tos.md)  
  
  
