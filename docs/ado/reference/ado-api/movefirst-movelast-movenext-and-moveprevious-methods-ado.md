---
title: MoveFirst、 MoveLast、 MoveNext 和 MovePrevious 方法 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
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
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 83e216f15da49150481af18ee98aac1f604b2394
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66707481"
---
# <a name="movefirst-movelast-movenext-and-moveprevious-methods-ado"></a>MoveFirst、 MoveLast、 MoveNext 和 MovePrevious 方法 (ADO)
将移动到 first、 last、 下一步，或上一个记录中指定[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象并将该记录的当前记录。  
  
## <a name="syntax"></a>语法  
  
```  
  
recordset.{MoveFirst | MoveLast | MoveNext | MovePrevious}  
```  
  
## <a name="remarks"></a>备注  
 使用**MoveFirst**方法将当前记录位置移动到中的第一个记录**记录集**。  
  
 使用**MoveLast**方法将当前记录位置移到最后一个记录中**记录集**。 **记录集**对象必须支持书签或向后的光标的移动; 否则为方法调用将生成错误。  
  
 调用**MoveFirst**或**MoveLast**时**记录集**为空 (同时**BOF**并**EOF**为 True） 将生成错误。  
  
 使用**MoveNext**方法来移动当前记录放置一条记录前滚 (底部的**记录集**)。 如果最后一条记录的当前记录，并且你调用**MoveNext**方法，ADO 将设置的当前记录为位置后的最后一个记录**记录集**([EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)是 **，则返回 true**)。 试图移动时，向前**EOF**属性已**True**生成一个错误。  
  
 在 ADO 中 2.5 及更高版本，当**记录集**已筛选或排序，且当前记录的数据已更改，调用**MoveNext**方法将移动光标两个记录将从当前记录转发. 这是因为当前记录更改时下, 一条记录将成为新的当前记录。 调用**MoveNext**更改将从新的当前记录中移动光标一条记录前滚之后。 这是不同于 ADO 2.1 中的行为和更早版本。 在这些早期版本中的已排序或筛选的当前记录的数据更改**记录集**不会更改当前记录的位置和**MoveNext**将光标移到下一条记录紧跟当前记录。  
  
 使用**MovePrevious**方法来移动当前记录放置一条记录向后 (在顶部**记录集**)。 **记录集**对象必须支持书签或向后的光标的移动; 否则为方法调用将生成错误。 如果第一条记录的当前记录，并且你调用**MovePrevious**方法，则 ADO 会将当前记录设置为中的第一个记录之前的位置**记录集**([BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)是 **，则返回 True**)。 试图移动时，向后**BOF**属性已**True**生成一个错误。 如果**记录集**对象不支持向后的光标的移动或书签**MovePrevious**方法将生成错误。  
  
 如果**记录集**是只进和你想要支持同时向前和向后滚动，可以使用[CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md)属性来创建将支持向后的光标的移动的记录缓存通过[移动](../../../ado/reference/ado-api/move-method-ado.md)方法。 由于缓存的记录加载到内存中，应避免缓存不必要的更多记录。 您可以调用**MoveFirst**中只进方法**记录集**对象; 这样做可能会导致要重新执行生成的命令的提供程序**记录集**对象.  
  
## <a name="applies-to"></a>适用范围  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>请参阅  
 [MoveFirst、 MoveLast、 MoveNext 和 MovePrevious 方法示例 (VB)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-example-vb.md)   
 [MoveFirst、 MoveLast、 MoveNext 和 MovePrevious 方法示例 (VBScript)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-example-vbscript.md)   
 [MoveFirst、 MoveLast、 MoveNext 和 MovePrevious 方法示例 （VC + +）](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-example-vc.md)   
 [Move 方法 (ADO)](../../../ado/reference/ado-api/move-method-ado.md)   
 [MoveFirst、 MoveLast、 MoveNext 和 MovePrevious 方法 (RDS)](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)   
 [MoveRecord 方法 (ADO)](../../../ado/reference/ado-api/moverecord-method-ado.md)
