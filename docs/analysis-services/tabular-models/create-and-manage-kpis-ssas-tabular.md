---
title: 创建和管理 Kpi |Microsoft 文档
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8740cfbcf8448a0344d68e182a7cbf379c458a68
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="create-and-manage-kpis"></a>创建和管理 Kpi 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  本文介绍如何创建、 编辑或删除 KPI （关键绩效指标） 表格模型中。 若要创建一个 KPI，请选择计算结果为该 KPI 的基础值的度量值。 然后使用“关键绩效指标”对话框选择计算结果为某一目标值的第二个度量值或绝对值。 之后可以定义状态阈值，这些状态阈值度量基础度量值和目标度量值之间的性能。  
  
## <a name="tasks"></a>“任务”  
  
> [!IMPORTANT]  
>  在创建 KPI 前，您必须首先创建一个求值的基础度量值。 然后，您将该基础度量值扩展到 KPI。 如何创建度量值另一个主题中所述[创建和管理度量值](../../analysis-services/tabular-models/create-and-manage-measures-ssas-tabular.md)。 KPI 也要求目标值。 该值可来自另一个预定义的度量值或绝对值。 一旦您将基础度量值扩展到 KPI 后，可以选择目标值并且在“关键绩效指标”对话框中定义状态阈值。  
  
###  <a name="bkmk_create_KPI"></a> 创建 KPI  
  
1.  在度量值网格中，右键单击将充当基础度量值（值）的度量值，然后单击“创建 KPI”。  
  
2.  在 **“关键绩效指标”** 对话框的 **“定义目标值”**中，选择以下选项之一：  
  
     选择 **“度量值”**，然后从列表框中选择一个目标度量值。  
  
     选择 **“绝对值”**，然后键入一个数值。  
  
3.  在 **“定义状态阈值”**中，单击并滑动阈值下限和上限。  
  
4.  在 **“选择图标样式”**中，单击某一图像类型。  
  
5.  单击 **“说明”**，然后为“KPI”、“值”、“状态”和“目标”键入说明。  
  
> [!TIP]  
>  您可以使用“在 Excel 中分析”功能测试您的 KPI。 有关详细信息，请参阅[在 Excel 中的分析](../../analysis-services/tabular-models/analyze-in-excel-ssas-tabular.md)。  
  
###  <a name="bkmk_edit_KPI"></a> 编辑 KPI  
  
-   在度量值网格中，右键单击充当 KPI 的基础度量值（值）的度量值，然后单击“编辑 KPI 设置”。  
  
###  <a name="bkmk_delete"></a> 删除 KPI 和基础度量值  
  
-   在度量值网格中，右键单击充当 KPI 的基础度量值（值）的度量值，然后单击“删除”。  
  
###  <a name="bkmk_delete_KPI"></a> 删除 KPI 但保留基础度量值  
  
-   在度量值网格中，右键单击充当 KPI 的基础度量值（值）的度量值，然后单击“删除 KPI”。  
  
## <a name="alt-shortcuts"></a>ALT 快捷键  
  
|用户界面部分|键命令|  
|----------------|-----------------|  
|KPI 基础度量值|ALT+B|  
|KPI 状态|Alt+S|  
|“度量值”|Alt+M|  
|“绝对值”|ALT+A|  
|“定义状态阈值”|ALT+U|  
|“选择图标样式”|Alt+I|  
|走向|ALT+T|  
|“说明”|ALT+D|  
|走向|ALT+T|  
  
## <a name="see-also"></a>另请参阅  
 [Kpi](../../analysis-services/tabular-models/kpis-ssas-tabular.md)   
 [度量值](../../analysis-services/tabular-models/measures-ssas-tabular.md)   
 [创建和 managemeasures](../../analysis-services/tabular-models/create-and-manage-measures-ssas-tabular.md)  
  
  
