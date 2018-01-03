---
title: "Clone 方法 (ADO) |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Recordset20::Clone
- Recordset20::raw_Clone
helpviewer_keywords: Clone method [ADO]
ms.assetid: ad49265f-1c05-4271-9bbf-7c00010ac18c
caps.latest.revision: "13"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b0fa4429b66b8a43bf2eecccca1fbc94597f07a5
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="clone-method-ado"></a>Clone 方法 (ADO)
创建副本[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)从现有对象**记录集**对象。 （可选） 指定的克隆是只读的。  
  
## <a name="syntax"></a>语法  
  
```  
  
Set rstDuplicate = rstOriginal.Clone (LockType)  
```  
  
## <a name="return-value"></a>返回值  
 返回**记录集**对象引用。  
  
#### <a name="parameters"></a>Parameters  
 *rstDuplicate*  
 标识重复的对象变量**记录集**要创建对象。  
  
 *rstOriginal*  
 标识的对象变量**记录集**可以进行复制的对象。  
  
 *LockType*  
 可选。 A [LockTypeEnum](../../../ado/reference/ado-api/locktypeenum.md)值，该值指定与原始的锁类型**记录集**，或只读模式**记录集**。 有效值为**adLockUnspecified**或**adLockReadOnly**。  
  
## <a name="remarks"></a>Remarks  
 使用**克隆**方法来创建多个重复**记录集**对象，尤其是如果你想要维护多个给定的一组记录中的当前记录。 使用**克隆**方法是比创建并打开新更高效**记录集**使用相同的定义作为原始的对象。  
  
 [筛选器](../../../ado/reference/ado-api/filter-property.md)属性的原始**记录集**，如果任何，不会应用于克隆。 设置**筛选器**属性的新**记录集**以筛选的结果。 将复制任何现有的最简单方法**筛选器**值是将它分配直接、，如下所示。  
  
```  
rsNew.Filter = rsOriginal.Filter  
```  
  
 新创建的克隆的当前记录设置为第一条记录。  
  
 对一个所做的更改**记录集**对象中是可见的所有克隆无论何种游标类型。 但是，之后执行[Requery](../../../ado/reference/ado-api/requery-method.md)上原始**记录集**，克隆人的进攻将不再同步到原始。  
  
 关闭原始**记录集**不会关闭其副本，也不会关闭副本关闭原始对象或任何其他副本。  
  
 你只能克隆**记录集**支持书签的对象。 书签值是可互换;即，从一个的书签引用**记录集**对象是指任何个克隆中的同一记录。  
  
 某些**记录集**触发事件是否也会在所有**记录集**克隆。 但是，因为当前记录可能而异克隆**记录集**，事件可能不是有效的克隆。 例如，如果你更改的字段值[WillChangeField](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)的事件将发生更改**记录集**和所有克隆。 *字段*参数**WillChangeField**的克隆事件**记录集**（其中不进行了更改） 将克隆，当前记录的字段引用这可能会比原始的当前记录另一条记录**记录集**发生更改。  
  
 下表提供了所有的完整列表**记录集**事件。 它指示它们是否有效且是否有任何通过使用生成的记录集克隆触发**克隆**方法。  
  
|事件|在克隆中触发？|  
|-----------|--------------------------|  
|[EndOfRecordset](../../../ado/reference/ado-api/endofrecordset-event-ado.md)|是|  
|[FetchComplete](../../../ado/reference/ado-api/fetchcomplete-event-ado.md)|是|  
|[FetchProgress](../../../ado/reference/ado-api/fetchprogress-event-ado.md)|是|  
|[FieldChangeComplete](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|是|  
|[MoveComplete](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)|是|  
|[RecordChangeComplete](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|是|  
|[RecordsetChangeComplete](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|是|  
|[WillChangeField](../../../ado/reference/ado-api/willchangefield-and-fieldchangecomplete-events-ado.md)|是|  
|[WillChangeRecord](../../../ado/reference/ado-api/willchangerecord-and-recordchangecomplete-events-ado.md)|是|  
|[WillChangeRecordset](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md)|是|  
|[WillMove](../../../ado/reference/ado-api/willmove-and-movecomplete-events-ado.md)|是|  
  
## <a name="applies-to"></a>适用范围  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [克隆方法示例 (VB)](../../../ado/reference/ado-api/clone-method-example-vb.md)   
 [克隆方法示例 (VBScript)](../../../ado/reference/ado-api/clone-method-example-vbscript.md)   
 [Clone 方法示例 (VC++)](../../../ado/reference/ado-api/clone-method-example-vc.md)   
