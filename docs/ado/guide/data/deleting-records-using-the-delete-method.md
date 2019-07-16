---
title: 删除记录使用 Delete 方法 |Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925555"
---
# <a name="deleting-records-using-the-delete-method"></a>使用 Delete 方法删除记录
使用**删除**方法将当前记录或一组中的记录标记**记录集**对象以备删除。 如果**记录集**对象不允许记录删除，就会出错。 如果要立即更新模式中，删除数据库中立即执行。 如果不能 （由于数据库完整性的冲突，例如） 已成功删除了记录，该记录将保持在编辑模式下调用后面**更新。** 这意味着更新使用必须取消[CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md)之前移出当前记录 (例如，使用[关闭](../../../ado/reference/ado-api/close-method-ado.md)，[移动](../../../ado/reference/ado-api/move-method-ado.md)，或[NextRecordset](../../../ado/reference/ado-api/nextrecordset-method-ado.md))。  
  
 如果要在批更新模式中，记录将被标记为从缓存中删除，并在调用时，会发生实际删除**UpdateBatch**方法。 (若要查看已删除的记录，请设置**筛选器**属性设置为**adFilterAffectedRecords**后**删除**称为。)  
  
 尝试从已删除的记录中检索字段值将生成错误。 删除当前记录后, 已删除的记录保持最新，直到你将移动到另一条记录。 一次您移开的已删除的记录，将不再可访问。  
  
 如果将嵌套在事务中的删除，则可以使用恢复已删除的记录**RollbackTrans**方法。 如果要在批更新模式中，您可以通过使用取消挂起的删除或挂起的删除操作组**CancelBatch**方法。  
  
 如果尝试删除的记录将因与基础数据发生冲突而失败 （例如，一条记录已由另一个用户删除），访问接口将返回到的警告**错误**集合，但不会停止程序执行。 仅当在所有请求的记录上不存在冲突，将发生运行时错误。  
  
 如果**唯一表**设置动态属性和**记录集**是执行多个表的联接操作的结果**删除**方法将仅删除行从表中名为**唯一表**属性。  
  
 **删除**方法采用一个可选参数，可以指定哪些记录受到**删除**操作。 为此参数唯一有效的值为以下 ADO **AffectEnum**枚举常量：  
  
-   **adAffectCurrent**影响仅当前记录。  
  
-   **adAffectGroup**影响满足当前的记录**筛选器**属性设置。 **筛选器**属性必须设置为**FilterGroupEnum**值或数组**书签**要使用此选项。  
  
 下面的代码演示示例： 指定**adAffectGroup**调用时**删除**方法。 此示例将某些记录添加到示例**记录集**并更新数据库。 然后它将筛选**记录集**使用**adFilterAffectedRecords**筛选器枚举的常数，但仍将新添加的记录显示在**记录集。** 最后，调用**删除**方法，并指定所有满足当前的记录**筛选器**应删除属性的设置 （新记录）。  
  
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
