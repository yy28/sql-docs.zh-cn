---
title: 更改挖掘模型的属性 |Microsoft 文档
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: data-mining
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 00e7019ccf57b3206ee1e8c42270f8d9916ea81d
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="change-the-properties-of-a-mining-model"></a>更改挖掘模型的属性
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  某些挖掘模型属性应用于整个模型，而其他一些模型属性应用于单独的列。 例如， **Drillthrough** 属性就应用于整个模型，它指定事例数据是否应该可用于查询； **Description** 属性也是此类属性。 应用于列的属性包括 **Usage** 和 **ModelingFlags**；它们控制列中的数据在模型内的使用方式。  
  
 下面的模型属性具有可用于创建表达式或配置复杂模型属性的高级编辑器。 以下属性提供：  
  
-   **Filter** 属性：打开[“数据集筛选器或模型筛选器”对话框](http://msdn.microsoft.com/library/a9602174-b7e2-4e16-8ded-dfd8eb9264d7)。  
  
-   **AlgorithmParameters** 属性：打开[“算法参数”对话框（“挖掘模型”视图）](http://msdn.microsoft.com/library/57f9f6f8-8ca4-4a6e-8f18-85f0571b7060)。  
  
 有关如何在挖掘模型中设置属性的信息，请参阅[挖掘模型列](../../analysis-services/data-mining/mining-model-columns.md)。  
  
### <a name="to-change-the-properties-of-a-mining-model"></a>更改挖掘模型的属性  
  
1.  在数据挖掘设计器的“挖掘模型”选项卡中，右键单击包含挖掘模型名称的列标题，或者网格中包含挖掘算法名称的行，然后选择“属性”。  
  
2.  在屏幕右侧的 **“属性”** 窗口中，突出显示与要更改的属性对应的值，然后输入新的值。  
  
     在设计器中选择一个不同的元素后，新值即生效。  
  
### <a name="to-change-the-properties-of-a-mining-model-column"></a>更改挖掘模型列的属性  
  
1.  在数据挖掘设计器的“挖掘模型”选项卡中，右键单击网格中位于挖掘结构列与挖掘模型的交叉点处的单元格，然后选择“属性”。  
  
2.  在屏幕右侧的 **“属性”** 窗口中，突出显示与要更改的属性对应的值，然后输入新的值。  
  
    > [!NOTE]  
    >  如果列的用法设置为 **Ignore**，则列的“属性”窗口将为空白。  
  
     在设计器中选择一个不同的元素后，新值即生效。  
  
## <a name="see-also"></a>另请参阅  
 [挖掘模型任务和操作指南](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)  
  
  
