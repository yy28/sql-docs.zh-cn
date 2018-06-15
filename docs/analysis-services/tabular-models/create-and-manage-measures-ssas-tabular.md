---
title: 创建和管理度量值 |Microsoft 文档
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f6547cca48cbb846901e12cd1ab38822de9133d3
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
ms.locfileid: "34040611"
---
# <a name="create-and-manage-measures"></a>创建和管理度量值 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  度量值是为用于报表或 Excel 数据透视表（或数据透视图）而创建的公式。 度量值可以基于标准聚合函数，如 COUNT 或 SUM；或者，您可以通过使用 DAX 定义自己的公式。 本主题中的任务说明如何使用表的度量值网格创建和管理度量值。  
  
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
  
-   在度量值网格中，单击某一度量值，然后在 **“属性”** 窗口的 **“度量值名称”** 中，键入新名称，再单击 ENTER。  
  
     您也可以在编辑栏中重命名度量值。 度量值名称将位于公式前并且后随一个冒号。  
  
###  <a name="bkmk_delete"></a> 删除度量值  
  
-   在度量值网格中，右键单击某一度量值，然后单击“删除”。  
  
## <a name="see-also"></a>另请参阅  
 [度量值](../../analysis-services/tabular-models/measures-ssas-tabular.md)   
 [Kpi](../../analysis-services/tabular-models/kpis-ssas-tabular.md)   
 [计算的列](../../analysis-services/tabular-models/ssas-calculated-columns.md)  
  
  
