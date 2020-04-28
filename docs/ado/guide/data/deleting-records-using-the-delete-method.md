---
title: 使用 Delete 方法删除记录 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- ADO, deleting records
- deleting records [ADO]
- editing data [ADO], Delete method
- Delete method [ADO]
ms.assetid: bfed5cfa-7f57-463b-9da2-0c612a079d30
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5a862a244f06c64767f41529b4fff36881895a0b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "67925555"
---
# <a name="deleting-records-using-the-delete-method"></a>使用 Delete 方法删除记录
使用**Delete**方法将当前记录或记录**集**对象中的一组记录标记为删除。 如果**记录集**对象不允许删除记录，则会发生错误。 如果处于立即更新模式，则会立即删除数据库中的删除操作。 如果无法成功删除记录（例如，由于数据库完整性冲突），则在调用 Update 后，该记录将继续处于编辑模式 **。** 这意味着，必须先使用[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)取消更新，然后再离开当前记录（例如，使用[Close](../../../ado/reference/ado-api/close-method-ado.md)、 [Move](../../../ado/reference/ado-api/move-method-ado.md)或[NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md)）。  
  
 如果处于批处理更新模式，记录将标记为从缓存中删除，并且在调用**UpdateBatch**方法时会发生实际的删除。 （若要查看已删除的记录，请在调用**Delete**后将**Filter**属性设置为**adFilterAffectedRecords** 。）  
  
 尝试从已删除的记录中检索字段值将生成错误。 删除当前记录后，删除的记录将保持当前状态，直到您移到另一记录为止。 离开删除的记录后，它将无法再访问。  
  
 如果在事务中嵌套删除，则可以使用**RollbackTrans**方法恢复已删除的记录。 如果处于批处理更新模式，可以使用**CancelBatch**方法取消挂起的删除或挂起的删除组。  
  
 如果由于与基础数据发生冲突而导致删除记录的尝试失败（例如，记录已被其他用户删除），则提供程序会将警告返回到**错误**集合，但不会暂停程序执行。 仅当所有请求的记录上发生冲突时才会发生运行时错误。  
  
 如果设置了 "**唯一表**动态" 属性，并且**记录集**是对多个表执行联接操作的结果，则**delete**方法将仅删除 "**唯一表**" 属性中命名的表中的行。  
  
 **Delete**方法采用一个可选参数，该参数可用于指定哪些记录受**删除**操作的影响。 此参数的有效值只有下面的一个： **AffectEnum**  
  
-   **adAffectCurrent**仅影响当前记录。  
  
-   **adAffectGroup**仅影响满足当前**Filter**属性设置的记录。 **筛选器**属性必须设置为**FilterGroupEnum**值或**书签**数组才能使用此选项。  
  
 下面的代码演示了在调用**Delete**方法时指定**adAffectGroup**的示例。 此示例向示例**记录集**添加一些记录，并更新数据库。 然后，它使用**adFilterAffectedRecords**筛选器枚举常量来筛选**记录集**，该常量仅保留在**记录集中**可见的新添加的记录。 最后，它调用**Delete**方法，并指定应删除满足当前**Filter**属性设置（新记录）的所有记录。  
  
```  
'BeginDeleteGroup  
    'add some bogus records  
    With objRs  
        For i = 0 To 8  
            .AddNew  
            .Fields("CompanyName") = "Shipper Number " & i + 1  
            .Fields("Phone") = "(425) 555-000" & (i + 1)  
            .Update  
        Next i  
  
        ' update  
        .UpdateBatch  
  
        'filter on newly added records  
        .Filter = adFilterAffectedRecords  
        Debug.Print "Deleting the " & .RecordCount & _  
                    " records you just added."  
  
        'delete the newly added bogus records  
        .Delete adAffectGroup  
        .Filter = adFilterNone  
        Debug.Print .RecordCount & " records remain."  
    End With  
'EndDeleteGroup  
```
