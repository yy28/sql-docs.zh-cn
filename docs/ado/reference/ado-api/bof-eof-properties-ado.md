---
title: BOF、 EOF 属性 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::BOF
- Recordset15::EOF
helpviewer_keywords:
- EOF property [ADO]
- BOF property [ADO]
ms.assetid: 36c31ab2-f3b6-4281-89b6-db7e04e38fd2
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 9a449c0e635c7fe0e63bc1f4d8b1b0b91712135d
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66696288"
---
# <a name="bof-eof-properties-ado"></a>BOF、EOF 属性 (ADO)
-   **BOF**指示当前记录的位置是在中的第一个记录之前[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象。  
  
-   **EOF**指示当前记录位于中的最后一个记录后**记录集**对象。  
  
## <a name="return-value"></a>返回值  
 **BOF**并**EOF**属性返回**布尔**值。  
  
## <a name="remarks"></a>备注  
 使用**BOF**并**EOF**的属性以确定是否**记录集**对象包含的记录或者是否已超出限制的**记录集**对象时将记录到记录。  
  
 **BOF**属性将返回**True** -(1) 如果当前记录的位置之前的第一个记录并**False** (0)，如果当前记录的位置或第一个之后记录。  
  
 **EOF**属性将返回**True**记录当前位置是否在最后一条记录后， **False**如果当前记录的位置或之前的最后一个记录。  
  
 如果任一**BOF**或**EOF**属性是**True**，没有当前记录。  
  
 如果您打开**记录集**对象，其中包含任何记录， **BOF**并**EOF**属性设置为**True** (请参阅[RecordCount](../../../ado/reference/ado-api/recordcount-property-ado.md)属性以获取有关此状态的详细信息**记录集**)。 当打开**记录集**对象，其中包含至少一个记录，第一条记录是当前记录和**BOF**并**EOF**属性是**False**.  
  
 如果删除中的最后一个剩余记录**记录集**对象， **BOF**并**EOF**属性可能会保持**False**直到若要重新定位当前记录的尝试。  
  
 此表显示了哪些**移动**方法允许使用的不同组合**BOF**并**EOF**属性。  
  
||MoveFirst、<br /><br /> MoveLast|MovePrevious，<br /><br /> 移动 < 0|移动 0|MoveNext，<br /><br /> 移动 > 0|  
|------|-----------------------------|---------------------------------|------------|-----------------------------|  
|**BOF**=**True**， **EOF**=**False**|Allowed|错误|错误|Allowed|  
|**BOF**=**False**， **EOF**= **，则返回 True**|Allowed|Allowed|错误|错误|  
|同时 **，则返回 True**|错误|错误|错误|错误|  
|同时**False**|Allowed|Allowed|Allowed|Allowed|  
  
 允许**移动**方法并不保证该方法将成功定位到一条记录; 而只是意味着，调用指定**移动**方法将不会生成错误。  
  
 下表显示了会发生什么情况**BOF**并**EOF**属性设置时调用各种**移动**方法但不能成功地定位到一条记录。  
  
||BOF|EOF|  
|------|---------|---------|  
|**MoveFirst**， **MoveLast**|设置为 **，则返回 True**|设置为 **，则返回 True**|  
|**Move** 0|无更改|无更改|  
|**MovePrevious**，**移动**< 0|设置为 **，则返回 True**|无更改|  
|**MoveNext**，**移动**> 0|无更改|设置为 **，则返回 True**|  
  
## <a name="applies-to"></a>适用范围  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>请参阅  
 [BOF、 EOF 和 Bookmark 属性示例 (VB)](../../../ado/reference/ado-api/bof-eof-and-bookmark-properties-example-vb.md)   
 [BOF、 EOF 和 Bookmark 属性示例 （VC + +）](../../../ado/reference/ado-api/bof-eof-and-bookmark-properties-example-vc.md)   
