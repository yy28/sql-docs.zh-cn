---
title: "创建和管理度量值 (SSAS 表格) |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: edc1a4b2-96d3-4f34-bb70-6cacec79e819
caps.latest.revision: "18"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 3314afb5a5351b541e29d403ac4a41d98ec27263
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="create-and-manage-measures-ssas-tabular"></a>创建和管理度量值（SSAS 表格）
  度量值是为用于报表或 Excel 数据透视表（或数据透视图）而创建的公式。 度量值可以基于标准聚合函数，如 COUNT 或 SUM；或者，您可以通过使用 DAX 定义自己的公式。 本主题中的任务说明如何使用表的度量值网格创建和管理度量值。  
  
 本主题包括以下任务：  
  
-   [使用标准聚合公式创建度量值](#bkmk_create_stand)  
  
-   [使用自定义公式创建度量值](#bkmk_create_custom)  
  
-   [编辑度量值属性](#bkmk_edit)  
  
-   [重命名度量值](#bkmk_rename)  
  
-   [删除度量值](#bkmk_delete)  
  
## <a name="tasks"></a>“任务”  
 为了创建和管理度量值，您将使用表的度量值网格。 您只能在模型设计器的“数据视图”中查看表的度量值网格。 您不能在处于关系图视图中时创建度量值或查看度量值网格；不过，您可以在关系图视图中查看现有的度量值。 要为表显示度量值网格，请单击 **“表”** 菜单，然后单击 **“显示度量值网格”**。  
  
###  <a name="bkmk_create_stand"></a> 使用标准聚合公式创建度量值  
  
-   单击要为其创建度量值的列，然后单击 **“列”** 菜单，指向 **“自动求和”**，再单击某一聚合类型。  
  
     度量值将用默认名称自动创建，后随列正下方的度量值网格中的第一个单元中的公式。  
  
###  <a name="bkmk_create_custom"></a> 使用自定义公式创建度量值  
  
-   在度量值网格中，在要为其创建度量值的列的下方，单击某一单元，然后在公式栏中键入名称，后面依次跟一个冒号 (:)、一个等号 (=) 和公式。 按 Enter 以接受该公式。  
  
###  <a name="bkmk_edit"></a> 编辑度量值属性  
  
-   在度量值网格中，单击某一度量值，然后在 **“属性”** 窗口中，键入或选择不同的属性值。  
  
###  <a name="bkmk_rename"></a> 重命名度量值  
  
-   在度量值网格中，单击某一度量值，然后在 **“属性”** 窗口的 **“度量值名称”**中，键入新名称，再单击 ENTER。  
  
     您也可以在编辑栏中重命名度量值。 度量值名称将位于公式前并且后随一个冒号。  
  
###  <a name="bkmk_delete"></a> 删除度量值  
  
-   在度量值网格中，右键单击某一度量值，然后单击“删除”。  
  
## <a name="see-also"></a>另请参阅  
 [度量值（SSAS 表格）](../../analysis-services/tabular-models/measures-ssas-tabular.md)   
 [KPI（SSAS 表格）](../../analysis-services/tabular-models/kpis-ssas-tabular.md)   
 [计算列（SSAS 表格）](../../analysis-services/tabular-models/ssas-calculated-columns.md)  
  
  
