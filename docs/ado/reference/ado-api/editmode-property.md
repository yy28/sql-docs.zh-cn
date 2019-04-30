---
title: EditMode 属性 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::EditMode
helpviewer_keywords:
- EditMode property
ms.assetid: a1b04bb2-8c8b-47f9-8477-bfd0368b6f68
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 147528e9400d6befe9d5cb3c5d3cc3f882e48ad0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63181133"
---
# <a name="editmode-property"></a>EditMode 属性
指示当前记录的编辑状态。  
  
## <a name="return-value"></a>返回值  
 返回[EditModeEnum](../../../ado/reference/ado-api/editmodeenum.md)值。  
  
## <a name="remarks"></a>备注  
 ADO 维护一个与当前记录相关联的编辑缓冲区。 此属性指示是否进行了更改到此缓冲区，或是否已创建一个新的记录。 使用**EditMode**属性来确定当前记录的编辑状态。 您可以测试挂起的更改被中断编辑过程并确定是否需要使用[更新](../../../ado/reference/ado-api/update-method.md)或[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)方法。  
  
 在中*立即更新模式* **EditMode**属性重置为**adEditNone**后在成功调用**更新**调用方法. 在调用[删除](../../../ado/reference/ado-api/delete-method-ado-recordset.md)不会成功删除的记录或数据源中的记录 （例如，由于引用完整性冲突），[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)保持在编辑模式 (**EditMode** = **adEditInProgress**)。 因此， **CancelUpdate**移出当前记录之前必须调用 (例如使用[移动](../../../ado/reference/ado-api/move-method-ado.md)， [NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)，或[关闭](../../../ado/reference/ado-api/close-method-ado.md) ).  
  
 在中*批更新模式*(提供程序将多个更改缓存并将其写入到基础数据源仅在调用[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)方法)，值**EditMode**属性更改时执行的第一个操作，它不会通过调用重置**更新**方法。 后续操作的值不更改**EditMode**属性，即使执行不同操作。 例如，如果第一个操作是添加一个新记录，并且第二个对更改的现有记录的属性**EditMode**仍会**adEditAdd**。 **EditMode**属性不会重置到**adEditNone**调用的后面**UpdateBatch**。 若要确定在执行哪些操作，请设置[筛选器](../../../ado/reference/ado-api/filter-property.md)属性设置为[adFilterPending](../../../ado/reference/ado-api/filtergroupenum.md) ，因此具有挂起的更改的唯一记录将可见并检查[状态](../../../ado/reference/ado-api/status-property-ado-recordset.md)确定对数据进行了哪些更改每个记录的属性。  
  
> [!NOTE]
>  **EditMode**没有当前记录的情况下，才可以返回有效的值。 **EditMode**将返回一个错误，如果[BOF 或 EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)为 true，或如果当前记录已被删除。  
  
## <a name="applies-to"></a>适用范围  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>请参阅  
 [CursorType、 LockType、 和 EditMode 属性示例 (VB)](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vb.md)   
 [CursorType、 LockType、 和 EditMode 属性示例 （VC + +）](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vc.md)   
 [AddNew 方法 (ADO)](../../../ado/reference/ado-api/addnew-method-ado.md)   
 [Delete 方法 （ADO 记录集）](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [CancelUpdate 方法 (ADO)](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [Update 方法](../../../ado/reference/ado-api/update-method.md)
