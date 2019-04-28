---
title: Move 方法 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::Move
- Recordset15::raw_Move
helpviewer_keywords:
- Move method [ADO]
ms.assetid: 13fe9381-d00b-4f4a-9162-83c3f21b3837
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c8306a7d8e3247e77579d0bebc9147c3f9a1cc56
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62863484"
---
# <a name="move-method-ado"></a>Move 方法 (ADO)
移动中的当前记录的位置[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
recordset.Move NumRecords, Start  
```  
  
#### <a name="parameters"></a>Parameters  
 *NumRecords*  
 有符号**长**表达式，指定当前记录位置移动的记录数。  
  
 *开始*  
 可选。 一个**字符串**值或**变体**的计算结果为书签。 此外可以使用[BookmarkEnum](../../../ado/reference/ado-api/bookmarkenum.md)值。  
  
## <a name="remarks"></a>备注  
 **移动**方法支持对所有**记录集**对象。  
  
 如果*NumRecords*参数为大于零，将当前记录的位置向前移动 (年底**记录集**)。 如果*NumRecords*小于零，将当前记录位置向后移动 (的开头**记录集**)。  
  
 如果**移动**调用会将当前记录位置移动到之前的第一个记录点，ADO 将当前记录设置为之前的第一个记录中记录集的位置 ([BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)是 **，则返回 True**). 试图移动时，向后**BOF**属性已**True**生成一个错误。  
  
 如果**移动**调用会将当前记录位置移动到点，在最后一条记录后，ADO 记录集中的最后一个记录后将当前记录设置为位置 ([EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)是 **，则返回 True**). 试图移动时，向前**EOF**属性已**True**生成一个错误。  
  
 调用**移动**方法从一个空**记录集**对象生成一个错误。  
  
 如果传递*启动*参数，与此书签的记录在移动假设**记录集**对象支持书签。 如果未指定，移动是相对于当前记录。  
  
 如果使用的[CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md)属性以在本地缓存从提供程序，记录传递*NumRecords*移动缓存记录的当前组之外的当前记录位置的参数强制 ADO 要检索的记录，从目标记录开始新的组。 **CacheSize**属性确定新检索组的大小和目标记录是检索到的第一个记录。  
  
 如果**记录集**对象是只进，则用户仍可以传递*NumRecords*参数小于零，提供目标位于当前缓存的记录集内。 如果**移动**调用将使当前记录位置移动到第一个缓存的记录之前的记录将会出错。 因此，您可以使用支持通过支持仅向前滚动的提供程序的完整滚动记录缓存。 由于缓存的记录加载到内存中，应避免缓存超过所需数量的记录。 即使只进**记录集**对象支持向后移动这样一来，调用[MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)任何方法只进**记录集**仍将对象生成错误。  
  
> [!NOTE]
>  向后移动中只进的支持**记录集**不可预测的这取决于您的提供程序。 如果当前记录定位后的最后一个记录完**记录集**，**移动**向后不会获得正确的当前位置。  
  
## <a name="applies-to"></a>适用范围  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>请参阅  
 [Move 方法示例 (VB)](../../../ado/reference/ado-api/move-method-example-vb.md)   
 [Move 方法示例 (VBScript)](../../../ado/reference/ado-api/move-method-example-vbscript.md)   
 [Move 方法示例 （VC + +）](../../../ado/reference/ado-api/move-method-example-vc.md)   
 [MoveFirst、 MoveLast、 MoveNext 和 MovePrevious 方法 (ADO)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)   
 [MoveFirst、 MoveLast、 MoveNext 和 MovePrevious 方法 (RDS)](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)   
 [MoveRecord 方法 (ADO)](../../../ado/reference/ado-api/moverecord-method-ado.md)
