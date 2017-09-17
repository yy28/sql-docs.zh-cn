---
title: "删除列 (SSAS 表格) |Microsoft 文档"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 703db83b-e554-450e-813e-23ad08c1cdad
caps.latest.revision: 5
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: fa8c3945f37f19c8ca14039084907bb8eb693f90
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="delete-a-column-ssas-tabular"></a>删除列（SSAS 表格）
  本主题说明如何从表格模型表中删除列。  
  
## <a name="delete-a-model-table-column"></a>删除模型表列  
  
> [!NOTE]  
>  从模型表中删除列不会删除分区查询定义中的列。 如果要删除的列是分区的一部分，则您必须手动从分区查询定义中删除该列。 从分区查询定义中删除该列失败将导致查询该列并返回数据，但在处理操作期间，不会将这些数据填入模型表。 有关详细信息，请参阅 [分区（SSAS 表格）](../../analysis-services/tabular-models/partitions-ssas-tabular.md)。  
  
#### <a name="to-delete-a-model-table-column"></a>删除模型表列  
  
-   在模型设计器中，在包含要删除的列的表中，右键单击该列，然后单击“删除”。  
  
#### <a name="to-delete-a-model-table-column-by-using-the-table-properties-dialog-box"></a>使用“表属性”对话框删除模型表列  
  
1.  在模型设计器中，依次单击包含要删除的列的表、 **“表”** 菜单和  **“表属性”**。  
  
2.  在“列名来自”中，选择“模型”（如果与源不同，则使用模型表列名）。  
  
3.  在 **“编辑表属性”** 对话框的表预览窗口中，取消选中要删除的列，然后单击 **“确定”**。  
  
## <a name="see-also"></a>另请参阅  
 [将列添加到表（SSAS 表格）](../../analysis-services/tabular-models/add-columns-to-a-table-ssas-tabular.md)   
 [分区（SSAS 表格）](../../analysis-services/tabular-models/partitions-ssas-tabular.md)  
  
  
