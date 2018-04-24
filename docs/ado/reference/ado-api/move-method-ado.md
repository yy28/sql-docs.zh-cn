---
title: Move 方法 (ADO) |Microsoft 文档
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::Move
- Recordset15::raw_Move
helpviewer_keywords:
- Move method [ADO]
ms.assetid: 13fe9381-d00b-4f4a-9162-83c3f21b3837
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ad30ce02316be04ca66ba52bc205ba12b8df1fac
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2018
---
# <a name="move-method-ado"></a>Move 方法 (ADO)
移动中的当前记录的位置[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象。  
  
## <a name="syntax"></a>语法  
  
```  
  
recordset.Move NumRecords, Start  
```  
  
#### <a name="parameters"></a>Parameters  
 *NumRecords*  
 有符号**长**指定的当前记录位置移动的记录数的表达式。  
  
 *开始*  
 選擇性。 A**字符串**值或**Variant**计算结果为书签。 你还可以使用[BookmarkEnum](../../../ado/reference/ado-api/bookmarkenum.md)值。  
  
## <a name="remarks"></a>注释  
 **移动**方法支持对所有**记录集**对象。  
  
 如果*NumRecords*参数为大于零，将当前记录的位置前移 (的一端**记录集**)。 如果*NumRecords*小于零，将当前记录的位置向后移动 (右边的开头**记录集**)。  
  
 如果**移动**调用会将当前记录位置移动到前面第一条记录的某个点，ADO 将当前记录设置为第一条记录之前在记录集中的位置 ([BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)是**True**). 试图移动向后在**BOF**属性已**True**生成错误。  
  
 如果**移动**调用会将当前记录位置移动到点，在最后一条记录后，ADO 记录集内的最后一个记录将当前记录设置为位置 ([EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)是**True**). 试图移动向前在**EOF**属性已**True**生成错误。  
  
 调用**移动**方法从一个空**记录集**对象生成一个错误。  
  
 如果你通过*启动*相对于与此书签记录的自变量，移动是假定**记录集**对象支持书签。 如果未指定，移动是相对于当前记录。  
  
 如果你使用[CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md)属性以在本地传递缓存提供程序，从记录*NumRecords*缓存记录的当前组之外记录的当前位置移的自变量强制 ADO 检索的记录，从目标记录开始新的组。 **CacheSize**属性确定新检索到的组中的大小和目标记录是检索的第一个记录。  
  
 如果**记录集**对象转发只，用户仍然可以将传递*NumRecords*参数小于零，则提供目标是在当前的缓存的记录集内。 如果**移动**调用将使当前记录位置移动到第一个缓存的记录之前记录将会出错。 因此，你可以使用支持通过支持仅向前滚动的提供程序的完整滚动记录缓存。 由于缓存的记录加载到内存中，你应该避免缓存非必要的更多记录。 即使只进**记录集**对象支持向后移动以这种方式，调用[MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)方法对任何只进**记录集**仍将对象生成错误。  
  
> [!NOTE]
>  支持只进中向后移动的**记录集**不可预测的这取决于你的提供商。 如果当前记录定位位置后的最新记录**记录集**，**移动**向后可能不会造成在正确的当前位置。  
  
## <a name="applies-to"></a>适用范围  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [移动方法示例 (VB)](../../../ado/reference/ado-api/move-method-example-vb.md)   
 [移动方法示例 (VBScript)](../../../ado/reference/ado-api/move-method-example-vbscript.md)   
 [移动方法示例 （VC + +）](../../../ado/reference/ado-api/move-method-example-vc.md)   
 [MoveFirst、 MoveLast、 MoveNext 和 MovePrevious 方法 (ADO)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)   
 [MoveFirst、 MoveLast、 MoveNext 和 MovePrevious 方法 (RDS)](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)   
 [MoveRecord 方法 (ADO)](../../../ado/reference/ado-api/moverecord-method-ado.md)
