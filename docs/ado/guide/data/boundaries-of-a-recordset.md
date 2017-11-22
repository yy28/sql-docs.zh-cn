---
title: "记录集边界 |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- EOF property [ADO], boundaries of a Recordset
- Recordset object [ADO], boundaries of a Recordset
- BOF property [ADO], boundaries of a Recordset
ms.assetid: c0dd4a0f-478d-4c5e-b5d5-7535f211d064
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 67a300e30522a5f02bb6c33409a062a3c2434643
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="boundaries-of-a-recordset"></a>记录集的边界
**记录集**支持**BOF**和**EOF**属性来描述的开头和结尾，分别，数据集。 你可以将**BOF**和**EOF**为位于开头和末尾的"影子"记录**记录集**。 计数**BOF**和**EOF**，我们的示例**记录集**现在如下所示：  
  
|ProductID|ProductName|UnitPrice|  
|---------------|-----------------|---------------|  
|BOF|||  
|7|位置 Bob 环保干的梨|30.0000|  
|14|豆腐|23.2500|  
|28|Rssle 泡菜口味|45.6000|  
|51|猪肉干|53.0000|  
|74|Longlife 豆腐|10.0000|  
|EOF|||  
  
 当光标移过最后一条记录， **EOF**设置为**True**; 否则为其值是**False**。 同样，当光标将移动第一个记录之前, **BOF**设置为**True**; 否则为其值是**False**。 这些属性通常用于枚举在数据集中，如以下 JScript 代码段中所示。  
  
```  
while (objRecordset.EOF != true)   
{  
   // Work on the current record.  
   ...  
   // Advance the cursor forward to the next record.  
   objRecordset.MoveNext();  
}  
or  
while (objRecordset.BOF != true)   
{  
   // Work on the current record.  
   ...  
   // Move the cursor to the previous record.  
   objRecordset.MovePrevious();  
}  
```  
  
 如果这两个**BOF**和**EOF**是**True**、**记录集**对象为空。 这两个属性将**False**为到新打开的非空**记录集**对象。 你可以使用**BOF**和**EOF**属性一起用来确定如果**记录集**对象为空或不，如以下 JScript 代码段中所示。  
  
```  
if (objRecordset.EOF == true && objRecordset.BOF == true)  
{  
   WScript.Echo("we got an empty dataset.");  
}  
else  
{  
   WScript.Echo("we got a full dataset.");  
}  
```  
  
 此方案适用于所有类型的游标，并独立于基础提供程序。 如果你尝试确定的空**记录集**对象通过检查其**RecordCount**属性值为零 (0)，或不，您必须采取预防措施，要使用相应的光标和提供程序，支持返回的结果中的记录数。  
  
 如果你删除中的最后一个剩余记录**记录集**对象时，游标仍处于不确定状态。 **BOF**和**EOF**属性可能会一直保留**False**之前尝试重新定位的当前记录，具体情况取决于提供程序。 有关详细信息，请参阅[使用 Delete 方法删除记录](../../../ado/guide/data/deleting-records-using-the-delete-method.md)。
