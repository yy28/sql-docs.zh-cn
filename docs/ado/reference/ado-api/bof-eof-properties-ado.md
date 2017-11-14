---
title: "BOF，EOF 属性 (ADO) |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Recordset15::BOF
- Recordset15::EOF
helpviewer_keywords:
- EOF property [ADO]
- BOF property [ADO]
ms.assetid: 36c31ab2-f3b6-4281-89b6-db7e04e38fd2
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 93689aa347014fd3976645682a396230a38476e6
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="bof-eof-properties-ado"></a>BOF，EOF 属性 (ADO)
-   **BOF**指示当前记录位置处于之前的第一个记录[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象。  
  
-   **EOF**指示当前记录位置后中的最后一个记录**记录集**对象。  
  
## <a name="return-value"></a>返回值  
 **BOF**和**EOF**属性返回**布尔**值。  
  
## <a name="remarks"></a>注释  
 使用**BOF**和**EOF**属性来确定是否**记录集**对象包含的记录或者是否已超出限制的**记录集**对象移动到记录时。  
  
 **BOF**属性返回**True** (-1) 的当前记录的位置是否在第一条记录之前和**False** (0); 如果当前记录的位置位于或迟于第一个记录。  
  
 **EOF**属性返回**True**当前记录的位置是否在最后一条记录后和**False**如果记录当前位置位于或早于最后一条记录。  
  
 如果任一**BOF**或**EOF**属性是**True**，没有当前记录。  
  
 如果你打开**记录集**对象，其中包含任何记录， **BOF**和**EOF**属性设置为**True** (请参阅[RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md)属性以获取有关此状态的详细信息**记录集**)。 当你打开**记录集**包含至少一个记录，第一条记录的对象是当前记录和**BOF**和**EOF**属性**False**.  
  
 如果你删除中的最后一个剩余记录**记录集**对象， **BOF**和**EOF**属性可能会一直保留**False**之前尝试重新定位的当前记录。  
  
 此表显示了哪些**移动**方法允许使用的不同组合**BOF**和**EOF**属性。  
  
||MoveFirst，<br /><br /> MoveLast|MovePrevious，<br /><br /> Move < 0|Move 0|MoveNext，<br /><br /> Move > 0|  
|------|-----------------------------|---------------------------------|------------|-----------------------------|  
|**BOF**=**True**， **EOF**=**False**|Allowed|错误|错误|Allowed|  
|**BOF**=**False**， **EOF**=**True**|Allowed|Allowed|错误|错误|  
|同时**True**|错误|错误|错误|错误|  
|同时**False**|Allowed|Allowed|Allowed|Allowed|  
  
 允许**移动**方法并不保证该方法将成功定位到一条记录; 它仅意味着调用指定**移动**方法将不会生成错误。  
  
 下表显示会发生什么情况**BOF**和**EOF**属性设置，当您调用各种**移动**方法但不能成功找到一条记录。  
  
||BOF|EOF|  
|------|---------|---------|  
|**MoveFirst**， **MoveLast**|设置为**True**|设置为**True**|  
|**移动**0|没有变化|没有变化|  
|**MovePrevious**，**移动**< 0|设置为**True**|没有变化|  
|**MoveNext**，**移动**> 0|没有变化|设置为**True**|  
  
## <a name="applies-to"></a>适用范围  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [BOF、 EOF，以及书签属性示例 (VB)](../../../ado/reference/ado-api/bof-eof-and-bookmark-properties-example-vb.md)   
 [BOF、 EOF 和书签属性示例 （VC + +）](../../../ado/reference/ado-api/bof-eof-and-bookmark-properties-example-vc.md)   

