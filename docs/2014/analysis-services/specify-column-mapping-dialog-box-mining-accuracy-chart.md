---
title: 指定列映射对话框 （挖掘准确性图表） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.miningmodeleditor.accuracychart.coltotablecolmapping.f1
ms.assetid: 68e9e2d2-173f-4363-a515-fc60bfee3af0
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4416a51ea32500d56c209d745065da20bf8010c9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66068423"
---
# <a name="specify-column-mapping-dialog-box-mining-accuracy-chart"></a>“指定列映射”对话框（挖掘准确性图表）
  可以使用 **“指定列映射”** 选项卡，从外部数据源中选择表以及将列映射到数据挖掘模型。 随后即可使用外部数据测试挖掘模型的准确性并在准确性图表中显示结果。  
  
 **详细信息：** [测试和验证（数据挖掘）](data-mining/testing-and-validation-data-mining.md)  
  
## <a name="options"></a>选项  
 **挖掘结构**  
 显示包含要测试的模型的所选挖掘结构。  
  
 **选择结构**  
 单击此项将打开“选择挖掘结构”  对话框，在其中可选择不同的挖掘结构。  
  
 **选择输入的表**  
 显示用于生成提升图的所选输入表。 选择包含将用于测试模型准确性的测试数据的表。  
  
> [!NOTE]  
>  如果该窗格中未包含任何表，请单击“选择事例表”  以从数据源视图中添加表。  
  
 **删除表**  
 删除所选表。 如果未选择表或者 **“选择输入表”** 列表中未显示表，则禁用此按钮。  
  
 **选择事例表**  
 单击此项将打开“选择表”  对话框，在其中可选择数据源视图。  
  
 **注意** 只有在尚未选择事例表时，才会显示此按钮。 若要启用该按钮以便可以选择其他事例表，请选择所有现有表并单击 **“删除表”** ，以清除该列表。  
  
 **选择嵌套的表**  
 打开“选择表”  对话框。 只有在已选择事例表的情况下，才会显示此按钮。 如果关联的挖掘结构不包含嵌套表，则禁用此按钮。  
  
 **修改联接**  
 打开“指定嵌套联接”  对话框。 只有在已选择嵌套表的情况下，此按钮才处于活动状态。  
  
## <a name="see-also"></a>请参阅  
 [测试和验证任务和操作指南&#40;数据挖掘&#41;](data-mining/testing-and-validation-tasks-and-how-tos-data-mining.md)   
 [挖掘准确性图表设计器&#40;数据挖掘&#41;](mining-accuracy-chart-designer-data-mining.md)  
  
  
