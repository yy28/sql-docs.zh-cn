---
title: "EditMode 属性 |Microsoft 文档"
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
- Recordset15::EditMode
helpviewer_keywords:
- EditMode property
ms.assetid: a1b04bb2-8c8b-47f9-8477-bfd0368b6f68
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: be4670f359212f1079044341285ec2b0aff6c559
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="editmode-property"></a>EditMode 属性
指示当前记录的编辑状态。  
  
## <a name="return-value"></a>返回值  
 返回[EditModeEnum](../../../ado/reference/ado-api/editmodeenum.md)值。  
  
## <a name="remarks"></a>注释  
 ADO 维护一个与当前记录关联的编辑缓冲区。 此属性指示是否进行了更改到此缓冲区，或是否已创建一条新记录。 使用**EditMode**属性来确定当前记录的编辑状态。 你可以测试挂起的更改被中断编辑过程并确定是否需要使用[更新](../../../ado/reference/ado-api/update-method.md)或[正在执行](../../../ado/reference/ado-api/cancelupdate-method-ado.md)方法。  
  
 在*立即更新模式* **EditMode**属性重置为**adEditNone**后成功调用**更新**调用方法. 当调用[删除](../../../ado/reference/ado-api/delete-method-ado-recordset.md)不会成功删除或多个数据源中的记录 （例如，由于引用完整性冲突），[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)保留在编辑模式 (**EditMode** = **adEditInProgress**)。 因此，**正在执行**离开当前的记录之前必须调用 (例如，使用[移动](../../../ado/reference/ado-api/move-method-ado.md)，[签名](../../../ado/reference/ado-api/nextrecordset-method-ado.md)，或[关闭](../../../ado/reference/ado-api/close-method-ado.md) ).  
  
 在*批处理更新模式下*(在其中提供程序缓存多个更改，并将其写入到基础数据源仅在调用[UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)方法) 的值**EditMode**属性更改时执行的第一个操作，并且它不会通过调用重置**更新**方法。 后续操作不更改的值**EditMode**属性，即使执行不同操作。 例如，如果第一个操作是添加新的记录，并且第二个对更改的现有记录的属性**EditMode**仍将**adEditAdd**。 **EditMode**属性不会重置到**adEditNone**在调用后**UpdateBatch**。 若要确定在执行哪些操作，请设置[筛选器](../../../ado/reference/ado-api/filter-property.md)属性[adFilterPending](../../../ado/reference/ado-api/filtergroupenum.md) ，以便仅记录与挂起的更改将可见并检查[状态](../../../ado/reference/ado-api/status-property-ado-recordset.md)以确定对数据进行了哪些更改每个记录的属性。  
  
> [!NOTE]
>  **EditMode**可以返回有效的值，只有在当前记录。 **EditMode**将返回错误，如果[BOF 或 EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md)为 true，或如果已删除该当前记录。  
  
## <a name="applies-to"></a>适用范围  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>另请参阅  
 [游标类型、 LockType，以及 EditMode 属性示例 (VB)](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vb.md)   
 [游标类型、 LockType 和 EditMode 属性示例 （VC + +）](../../../ado/reference/ado-api/cursortype-locktype-and-editmode-properties-example-vc.md)   
 [AddNew 方法 (ADO)](../../../ado/reference/ado-api/addnew-method-ado.md)   
 [Delete 方法 （ADO 记录集）](../../../ado/reference/ado-api/delete-method-ado-recordset.md)   
 [正在执行方法 (ADO)](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [Update 方法](../../../ado/reference/ado-api/update-method.md)

