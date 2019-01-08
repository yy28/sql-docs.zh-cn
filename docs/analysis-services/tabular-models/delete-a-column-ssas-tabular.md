---
title: 删除 Analysis Services 表格模型中的列 |Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6f61aea9e4751094dafd37fe3b9ca8ed8d6ef0fe
ms.sourcegitcommit: 8a64c59c5d84150659a015e54f8937673cab87a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2018
ms.locfileid: "53072074"
---
# <a name="delete-a-column"></a>删除列 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  本文介绍如何从表格模型表中删除列。  
  
## <a name="delete-a-model-table-column"></a>删除模型表列  
  
> [!NOTE]  
>  从模型表中删除列不会删除分区查询定义中的列。 如果要删除的列是分区的一部分，则您必须手动从分区查询定义中删除该列。 从分区查询定义中删除该列失败将导致查询该列并返回数据，但在处理操作期间，不会将这些数据填入模型表。 有关详细信息，请参阅[分区](../../analysis-services/tabular-models/partitions-ssas-tabular.md)。  
  
#### <a name="to-delete-a-model-table-column"></a>删除模型表列  
  
-   在模型设计器中，在包含要删除的列的表中，右键单击该列，然后单击“删除”。  
  
#### <a name="to-delete-a-model-table-column-by-using-the-table-properties-dialog-box"></a>使用“表属性”对话框删除模型表列  
  
1.  在模型设计器中，依次单击包含要删除的列的表、 **“表”** 菜单和  **“表属性”**。  
  
2.  在“列名来自”中，选择“模型”（如果与源不同，则使用模型表列名）。  
  
3.  在 **“编辑表属性”** 对话框的表预览窗口中，取消选中要删除的列，然后单击 **“确定”**。  
  
## <a name="see-also"></a>请参阅  
 [向表中添加列](../../analysis-services/tabular-models/add-columns-to-a-table-ssas-tabular.md)   
 [分区](../../analysis-services/tabular-models/partitions-ssas-tabular.md)  
  
  
