---
title: "MoveFirst、 MoveLast、 MoveNext 和 MovePrevious 方法 (ADO) |Microsoft 文档"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Recordset15::MoveLast
- Recordset15::MoveNext
- Recordset15::raw_MoveNext
- Recordset15::raw_MovePrevious
- Recordset15::MoveFirst
- Recordset15::raw_MoveLast
- Recordset15::MovePrevious
- Recordset15::raw_MoveFirst
helpviewer_keywords:
- MoveNext method [ADO]
- MoveLast method [ADO]
- MoveFirst method [ADO]
- MovePrevious method [ADO]
ms.assetid: a61a01a7-5b33-4150-9126-21dfa63654cb
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: cda6c82147648f35adb80012d0810d514d08de86
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="movefirst-movelast-movenext-and-moveprevious-methods-ado"></a>MoveFirst、 MoveLast、 MoveNext 和 MovePrevious 方法 (ADO)
将移动到第一个，最后，在指定的下一步，或上一个记录[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象并将该记录的当前记录。  
  
## <a name="syntax"></a>语法  
  
```  
  
recordset.{MoveFirst | MoveLast | MoveNext | MovePrevious}  
```  
  
## <a name="remarks"></a>注释  
 使用**MoveFirst**方法将记录当前位置移到中的第一个记录**记录集**。  
  
 使用**MoveLast**方法，以使当前的记录位置移动到最后一个记录中**记录集**。 **记录集**对象必须支持书签或向后的光标移动; 否则，该方法调用将生成错误。  
  
 调用**MoveFirst**或**MoveLast**时**记录集**为空 (同时**BOF**和**EOF**为 True） 将生成错误。  
  
 使用**MoveNext**方法来移动当前记录向前定位一个记录 (底部**记录集**)。 如果最后一条记录的当前记录，并且你调用**MoveNext**方法，ADO 将设置当前记录为位置后的最新记录**记录集**([EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)是**True**)。 试图移动向前在**EOF**属性已**True**生成错误。  
  
 在 ADO 2.5 及更高版本，在**记录集**已筛选或排序，且当前记录的数据已更改，调用**MoveNext**方法将移动光标两个记录将从当前记录转发. 这是因为当前记录更改时下, 一条记录将成为新的当前记录。 调用**MoveNext**更改将从新的当前记录中移动光标一条记录转发后。 这是不同于 ADO 2.1 中的行为和更早版本。 在这些早期版本中，更改中的排序或筛选的当前记录的数据**记录集**不会更改的当前记录的位置和**MoveNext**将光标移动到下一条记录立即后的当前记录。  
  
 使用**MovePrevious**方法来移动当前记录的位置向后的一条记录 (的上端**记录集**)。 **记录集**对象必须支持书签或向后的光标移动; 否则，该方法调用将生成错误。 如果第一条记录的当前记录，并且你调用**MovePrevious**方法，则 ADO 会将当前记录设置为之前的第一个记录的位置**记录集**([BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)是**True**)。 试图移动向后在**BOF**属性已**True**生成错误。 如果**记录集**对象不支持书签或向后的光标移动**MovePrevious**方法将生成错误。  
  
 如果**记录集**是只进和你想要支持同时向前和向后滚动，可以使用[CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md)要创建将支持向后的光标移动记录缓存属性通过[移动](../../../ado/reference/ado-api/move-method-ado.md)方法。 由于缓存的记录加载到内存中，你应该避免缓存比所需的更多记录。 你可以调用**MoveFirst**中只进方法**记录集**对象; 这样做可能会导致要重新执行生成的命令的提供程序**记录集**对象.  
  
## <a name="applies-to"></a>适用范围  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [MoveFirst、 MoveLast、 MoveNext 和 MovePrevious 方法示例 (VB)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-example-vb.md)   
 [MoveFirst、 MoveLast、 MoveNext 和 MovePrevious 方法示例 (VBScript)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-example-vbscript.md)   
 [MoveFirst、 MoveLast、 MoveNext 和 MovePrevious 方法示例 （VC + +）](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-example-vc.md)   
 [Move 方法 (ADO)](../../../ado/reference/ado-api/move-method-ado.md)   
 [MoveFirst、 MoveLast、 MoveNext 和 MovePrevious 方法 (RDS)](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)   
 [移动记录方法 (ADO)](../../../ado/reference/ado-api/moverecord-method-ado.md)

