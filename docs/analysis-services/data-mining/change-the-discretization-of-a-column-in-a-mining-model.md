---
title: 更改挖掘模型中的列的离散化 |Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8a85b645562ce39f19c15191b6b1d3ba4a7fb332
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62670430"
---
# <a name="change-the-discretization-of-a-column-in-a-mining-model"></a>更改挖掘模型中列的离散化
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 会自动离散化值-也就是说，它会在数字列在某些情况。 例如，如果数据包含连续数值数据，并且创建了决策树模型，则将依据数据的分布，自动将连续数据的所有列都存入 bin 目录中。 如果要控制数据的离散化方式，则必须更改挖掘结构列的属性，这些属性可控制数据在模型中的使用方式。  
  
 有关如何在挖掘模型中设置属性的常规信息，请参阅 [挖掘模型列](../../analysis-services/data-mining/mining-model-columns.md)。  
  
### <a name="to-display-the-properties-for-a-mining-model-column"></a>显示挖掘模型列的属性  
  
1.  在数据挖掘设计器的“挖掘模型”选项卡中，右键单击包含挖掘模型名称的列标题，或者网格中包含挖掘算法名称的行，然后选择“属性”。    
  
     **“属性”** 窗口将显示与挖掘模型相关联的所有属性。  
  
2.  在靠近屏幕左侧的 **“结构”** 列中，单击包含要离散化的连续数值数据的列。  
  
     **“属性”** 窗口更改为只显示与该列相关联的属性。  
  
### <a name="to-change-the-discretization-method"></a>更改离散化方法  
  
1.  在 **“挖掘属性”** 窗口中，单击 **“内容”** 旁的文本框，然后从下拉列表中选择 **Discretized** 。  
  
     <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationBucketCount%2A> 和 <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationMethod%2A> 属性均处于启用状态。  
  
2.  在中**属性**窗口中，单击文本框旁边的<xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationMethod%2A>，然后选择以下值之一：**自动**， **EqualAreas**，或**群集**。  
  
    > [!NOTE]  
    >  如果列的用法设置为 **Ignore**，则列的“属性”  窗口将为空白。  
  
     在设计器中选择一个不同的元素后，新值即生效。  
  
3.  在中**属性**窗口中，单击文本框旁边的<xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn.DiscretizationBucketCount%2A>并键入一个数字值。  
  
    > [!NOTE]  
    >  如果更改这些属性，则必须重新处理该结构以及要对其使用新设置的所有模型。  
  
## <a name="see-also"></a>请参阅  
 [挖掘模型任务和操作指南](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)  
  
  
