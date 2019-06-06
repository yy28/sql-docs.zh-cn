---
title: 记录集的边界 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- EOF property [ADO], boundaries of a Recordset
- Recordset object [ADO], boundaries of a Recordset
- BOF property [ADO], boundaries of a Recordset
ms.assetid: c0dd4a0f-478d-4c5e-b5d5-7535f211d064
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 967ccb49cd2bbaa805420e7c982cc11721931022
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66702346"
---
# <a name="boundaries-of-a-recordset"></a>记录集的边界
**记录集**支持**BOF**并**EOF**属性来描述的开头和结尾，分别将数据集。 您可以看作**BOF**并**EOF**作为定位在开头和末尾的"虚拟"记录**记录集**。 计数**BOF**并**EOF**，我们的示例**记录集**现在如下所示：  
  
|ProductID|ProductName|UnitPrice|  
|---------------|-----------------|---------------|  
|BOF|||  
|7|柳贡干的梨|30.0000|  
|14|豆腐|23.2500|  
|28|Rssle Sauerkraut|45.6000|  
|51|猪肉干|53.0000|  
|74|Longlife 豆腐|10.0000|  
|EOF|||  
  
 当最后一条记录，游标将移**EOF**设置为**True**; 否则为它的值是**False**。 同样，当光标将移之前的第一个记录**BOF**设置为**True**; 否则为它的值是**False**。 这些属性通常用于枚举在数据集中，如以下 JScript 代码段中所示。  
  
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
  
 如果这两个**BOF**并**EOF**是**True**，则**记录集**对象为空。 这两个属性将**False**为到新打开的非空**记录集**对象。 可以使用**BOF**并**EOF**属性一起用来确定如果**记录集**对象为空或不是，如以下 JScript 代码段中所示。  
  
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
  
 此方案适用于所有类型的游标和独立于基础提供程序。 如果您尝试确定的空**记录集**通过检查对象及其**RecordCount**属性值为零 (0)，或不，你必须采取预防措施，以使用适当的游标和提供程序，支持返回的结果中的记录数。  
  
 如果删除中的最后一个剩余记录**记录集**对象时，光标会处于不确定状态。 **BOF**并**EOF**属性可能会保持**False**之前尝试重新定位当前记录，视提供程序。 有关详细信息，请参阅[使用 Delete 方法删除记录](../../../ado/guide/data/deleting-records-using-the-delete-method.md)。
