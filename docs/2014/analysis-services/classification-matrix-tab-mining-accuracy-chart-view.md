---
title: 分类矩阵选项卡 （挖掘准确性图表视图） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.accuracychart.confusionmatrix.f1
ms.assetid: 85d5a047-d656-41e0-8a31-400271c2a620
caps.latest.revision: 22
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 58df3c6d14edb8bfddbd53db0c110475d2a983bd
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37251509"
---
# <a name="classification-matrix-tab-mining-accuracy-chart-view"></a>“分类矩阵”选项卡（“挖掘准确性图表”视图）
  **“分类矩阵”** 选项卡为在 **“列映射”** 选项卡的模型网格中选择的每个模型显示分类矩阵。只有当在 **“列映射”** 选项卡中选择的可预测列不连续时，分类矩阵才可用。 有关更详细的说明**分类矩阵**选项卡上，请参阅[测试和验证&#40;数据挖掘&#41;](data-mining/testing-and-validation-data-mining.md)。  
  
## <a name="options"></a>“常规”  
 **复制**  
 将每个分类矩阵的内容复制到剪贴板。  
  
 **计数\<模型 > 上\<可预测列 >**  
 显示挖掘结构中每个挖掘模型的分类矩阵。 该矩阵包含以下列：  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|**预测**|对于可预测列的每一个状态包含一行。|  
|**\<状态 > （实际）**|可预测列中与每个状态对应的列。 如果行的状态与列的状态相对应，则单元显示数据库中该状态发生的实际次数。 如果行的状态与列的状态不对应，则单元显示预测错误。|  
  
## <a name="see-also"></a>请参阅  
 [挖掘准确性图表设计器&#40;数据挖掘&#41;](mining-accuracy-chart-designer-data-mining.md)   
 [测试和验证任务和操作指南&#40;数据挖掘&#41;](data-mining/testing-and-validation-tasks-and-how-tos-data-mining.md)   
 [测试和验证&#40;数据挖掘&#41;](data-mining/testing-and-validation-data-mining.md)  
  
  
