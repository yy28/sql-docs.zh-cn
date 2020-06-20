---
title: 创建和管理 Kpi （SSAS 表格） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.kpi.f1
ms.assetid: c96026c2-4394-4c3c-986b-4c95a4421900
author: minewiskan
ms.author: owend
ms.openlocfilehash: 4b64c5014f6f32d2e6e702937a739b66f38362e0
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84939818"
---
# <a name="create-and-manage-kpis-ssas-tabular"></a>创建和管理 KPI（SSAS 表格）
  本主题介绍如何在表格模型中创建、编辑或删除 KPI（关键绩效指标）。 若要创建 KPI，请选择计算结果为 KPI 的基础值的度量值。 然后使用“关键绩效指标”对话框选择计算结果为某一目标值的第二个度量值或绝对值。 之后可以定义状态阈值，这些状态阈值度量基础度量值和目标度量值之间的性能。  
  
 本主题包括以下任务：  
  
-   [创建 KPI](#bkmk_create_KPI)  
  
-   [编辑 KPI](#bkmk_edit_KPI)  
  
-   [删除 KPI 和基础度量值](#bkmk_delete)  
  
-   [删除 KPI 但保留基础度量值](#bkmk_delete_KPI)  
  
## <a name="tasks"></a>任务  
  
> [!IMPORTANT]  
>  在创建 KPI 前，您必须首先创建一个求值的基础度量值。 然后，您将该基础度量值扩展到 KPI。 另一主题 [创建和管理度量值（SSAS 表格）](measures-ssas-tabular.md)中有描述如何创建度量值。 KPI 也要求目标值。 该值可来自另一个预定义的度量值或绝对值。 一旦您将基础度量值扩展到 KPI 后，可以选择目标值并且在“关键绩效指标”对话框中定义状态阈值。  
  
###  <a name="to-create-a-kpi"></a><a name="bkmk_create_KPI"></a> 创建 KPI  
  
1.  在度量值网格中，右键单击将充当基础度量值（值）的度量值，然后单击“创建 KPI”****。  
  
2.  在 **“关键绩效指标”** 对话框的 **“定义目标值”** 中，选择以下选项之一：  
  
     选择 **“度量值”**，然后从列表框中选择一个目标度量值。  
  
     选择 **“绝对值”**，然后键入一个数值。  
  
3.  在 **“定义状态阈值”** 中，单击并滑动阈值下限和上限。  
  
4.  在 **“选择图标样式”** 中，单击某一图像类型。  
  
5.  单击 **“说明”**，然后为“KPI”、“值”、“状态”和“目标”键入说明。  
  
> [!TIP]  
>  您可以使用“在 Excel 中分析”功能测试您的 KPI。 有关详细信息，请参阅本主题后面的 [在 Excel 中分析（SSAS 表格）](analyze-in-excel-ssas-tabular.md)中的“角色管理器”对话框定义角色的表格模型作者。  
  
###  <a name="to-edit-a-kpi"></a><a name="bkmk_edit_KPI"></a> 编辑 KPI  
  
-   在度量值网格中，右键单击充当 KPI 的基础度量值（值）的度量值，然后单击“编辑 KPI 设置”****。  
  
###  <a name="to-delete-a-kpi-and-the-base-measure"></a><a name="bkmk_delete"></a> 删除 KPI 和基础度量值  
  
-   在度量值网格中，右键单击充当 KPI 的基础度量值（值）的度量值，然后单击“删除”****。  
  
###  <a name="to-delete-a-kpi-but-keep-the-base-measure"></a><a name="bkmk_delete_KPI"></a>删除 KPI 但保留基础度量值  
  
-   在度量值网格中，右键单击充当 KPI 的基础度量值（值）的度量值，然后单击“删除 KPI”****。  
  
## <a name="alt-shortcuts"></a>ALT 快捷键  
  
|用户界面部分|键命令|  
|----------------|-----------------|  
|KPI 基础度量值|ALT+B|  
|KPI 状态|Alt+S|  
|度量|Alt+M|  
|“绝对值”|ALT+A|  
|“定义状态阈值”|ALT+U|  
|“选择图标样式”|Alt+I|  
|趋势|ALT+T|  
|说明|ALT+D|  
|趋势|ALT+T|  
  
## <a name="see-also"></a>另请参阅  
 [&#40;SSAS 表格&#41;的 Kpi](kpis-ssas-tabular.md)   
 [&#40;SSAS 表格&#41;度量值](measures-ssas-tabular.md)   
 [创建和管理度量值（SSAS 表格）](create-and-manage-measures-ssas-tabular.md)  
  
  
