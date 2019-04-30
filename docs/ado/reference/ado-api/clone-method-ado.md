---
title: Clone 方法 (ADO) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset20::Clone
- Recordset20::raw_Clone
helpviewer_keywords:
- Clone method [ADO]
ms.assetid: ad49265f-1c05-4271-9bbf-7c00010ac18c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b4768c0f01c38ef72735f3577c4d581c019b4595
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63239730"
---
# <a name="clone-method-ado"></a>Clone 方法 (ADO)
创建重复[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象从现有**记录集**对象。 （可选） 指定的克隆是只读的。  
  
## <a name="syntax"></a>语法  
  
```  
  
Set rstDuplicate = rstOriginal.Clone (LockType)  
```  
  
## <a name="return-value"></a>返回值  
 返回**记录集**对象引用。  
  
#### <a name="parameters"></a>Parameters  
 *rstDuplicate*  
 对象变量，用于标识重复**记录集**要创建对象。  
  
 *rstOriginal*  
 对象变量，用于标识**记录集**对象可以进行复制。  
  
 *LockType*  
 可选。 一个[LockTypeEnum](../../../ado/reference/ado-api/locktypeenum.md)值，该值指定原始的锁类型**记录集**，或只读模式**记录集**。 有效的值为**adLockUnspecified**或**adLockReadOnly**。  
  
## <a name="remarks"></a>备注  
 使用**克隆**方法来创建多个重复**记录集**对象，尤其是如果你想要维护一组给定的记录中的多个当前记录。 使用**克隆**方法是创建和打开一个新比效率更高**记录集**使用相同的定义与原始对象。  
  
 [筛选器](../../../ado/reference/ado-api/filter-property.md)属性的原始**记录集**，如果有的话将不应用于克隆。 设置**筛选器**属性的新**记录集**筛选的结果。 复制任何现有的最简单办法**筛选器**值将为其分配直接，按如下所示。  
  
```  
rsNew.Filter = rsOriginal.Filter  
```  
  
 新创建的克隆的当前记录设置为第一条记录。  
  
 对一个做的更改**记录集**对象中是可见的所有克隆而不考虑游标类型。 但是，之后执行[Requery](../../../ado/reference/ado-api/requery-method.md)上原始**记录集**，克隆将不再同步到原始。  
  
 关闭原始**记录集**不会关闭其副本，也不关闭副本关闭原始对象或任何其他副本。  
  
 仅可以克隆**记录集**支持书签的对象。 书签值是可以互换;也就是说，从一个的书签引用**记录集**对象是指任何复本中的同一记录。  
  
 某些**记录集**触发的事件也会在所有**记录集**克隆。 但是，因为当前记录可以之间的差异在于克隆**记录集**，事件可能不是有效的克隆。 例如，如果您更改字段的值[WillChangeField](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)事件将出现在已更改**记录集**和中的所有克隆。 *字段*的参数**WillChangeField**事件的克隆**记录集**（其中不进行了更改） 将克隆的当前记录的字段引用这可能会比原始的当前记录的不同记录**记录集**发生更改。  
  
 下表提供了所有的完整列表**记录集**事件。 它指示它们是否有效以及是否使用生成的任何记录集克隆触发**克隆**方法。  
  
|Event|在克隆中触发？|  
|-----------|--------------------------|  
|[EndOfRecordset](../../../ado/reference/ado-api/endofrecordset-event-ado.md)|否|  
|[FetchComplete](../../../ado/reference/ado-api/fetchcomplete-event-ado.md)|否|  
|[FetchProgress](../../../ado/reference/ado-api/fetchprogress-event-ado.md)|否|  
|[FieldChangeComplete](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|是|  
|[MoveComplete](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)|否|  
|[RecordChangeComplete](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|是|  
|[RecordsetChangeComplete](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|否|  
|[WillChangeField](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|是|  
|[WillChangeRecord](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|是|  
|[WillChangeRecordset](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|否|  
|[WillMove](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)|否|  
  
## <a name="applies-to"></a>适用范围  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>请参阅  
 [Clone 方法示例 (VB)](../../../ado/reference/ado-api/clone-method-example-vb.md)   
 [Clone 方法示例 (VBScript)](../../../ado/reference/ado-api/clone-method-example-vbscript.md)   
 [Clone 方法示例 (VC++)](../../../ado/reference/ado-api/clone-method-example-vc.md)   
