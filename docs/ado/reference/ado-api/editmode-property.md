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
ms.openlocfilehash: c0ffc6fb258799b0ab0bb03e7acbd922f6a67d1f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "67918985"
---
# <a name="editmode-property"></a>EditMode 属性
指示当前记录的编辑状态。  
  
## <a name="return-value"></a>返回值  
 返回[EditModeEnum](../../../ado/reference/ado-api/editmodeenum.md)值。  
  
## <a name="remarks"></a>备注  
 ADO 维护与当前记录相关联的编辑缓冲区。 此属性指示是否已对此缓冲区进行了更改，或者是否已创建新记录。 使用**EditMode**属性可确定当前记录的编辑状态。 如果编辑进程已中断并确定是否需要使用[Update](../../../ado/reference/ado-api/update-method.md)或[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)方法，则可以测试挂起的更改。  
  
 在*即时更新模式*中，在调用**update**方法的成功调用后， **EditMode**属性重置为**adEditNone** 。 当调用[delete](../../../ado/reference/ado-api/delete-method-ado-recordset.md)时，如果不能成功删除数据源中的记录或记录（例如，由于存在引用完整性冲突），则[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)将保持编辑模式（**EditMode** = **adEditInProgress**）。 因此，在从当前记录开始之前，必须先调用**CancelUpdate** （例如，[移动](../../../ado/reference/ado-api/move-method-ado.md)、 [NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)或[关闭](../../../ado/reference/ado-api/close-method-ado.md)）。  
  
 在*批处理更新模式*（其中，提供程序缓存多个更改并仅在调用[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)方法时将它们写入基础数据源）时，在执行第一个操作时，将更改**EditMode**属性的值，而不会在调用**update**方法时对其进行重置。 即使执行了不同的操作，后续操作也不会更改**EditMode**属性的值。 例如，如果第一个操作是添加一条新记录，第二个操作对现有记录进行了更改，则**EditMode**的属性仍将为**adEditAdd**。 直到调用**UpdateBatch**后， **EditMode**属性才会重置为**adEditNone** 。 若要确定执行了哪些操作，请将[Filter](../../../ado/reference/ado-api/filter-property.md)属性设置为[adFilterPending](../../../ado/reference/ado-api/filtergroupenum.md) ，以便仅显示具有挂起更改的记录，并检查每个记录的[Status](../../../ado/reference/ado-api/status-property-ado-recordset.md)属性以确定对数据所做的更改。  
  
> [!NOTE]
>  仅当存在当前记录时， **EditMode**才可以返回有效的值。 如果[BOF 或 EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)为 true，则**EditMode**将返回错误，如果当前记录已被删除，则返回错误。  
  
## <a name="applies-to"></a>应用于  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [CursorType、LockType 和 EditMode 属性示例（VB）](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vb.md)   
 [CursorType、LockType 和 EditMode 属性示例（VC + +）](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vc.md)   
 [AddNew 方法（ADO）](../../../ado/reference/ado-api/addnew-method-ado.md)   
 [Delete 方法（ADO 记录集）](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [CancelUpdate 方法（ADO）](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [Update 方法](../../../ado/reference/ado-api/update-method.md)
