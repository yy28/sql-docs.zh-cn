---
title: "删除记录使用 Delete 方法 |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ADO, deleting records
- deleting records [ADO]
- editing data [ADO], Delete method
- Delete method [ADO]
ms.assetid: bfed5cfa-7f57-463b-9da2-0c612a079d30
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8d0a12e1d6d7e94d2f4feb69f51bb43b1e0edbb5
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="deleting-records-using-the-delete-method"></a>删除记录使用 Delete 方法
使用**删除**方法将当前记录或一组中的记录标记**记录集**对象以备删除。 如果**记录集**对象不允许记录删除，将会出错。 如果要立即更新模式中，删除数据库中会立即发生。 如果无法成功删除记录 （由于数据库完整性的冲突，例如），该记录将保持处于编辑模式的调用后**更新。** 这意味着，你必须取消更新使用[正在执行](../../../ado/reference/ado-api/cancelupdate-method-ado.md)之前离开当前记录 (例如，使用[关闭](../../../ado/reference/ado-api/close-method-ado.md)，[移动](../../../ado/reference/ado-api/move-method-ado.md)，或[签名](../../../ado/reference/ado-api/nextrecordset-method-ado.md))。  
  
 如果要在批处理更新模式下，记录将被标记为从缓存中删除，当你调用，时会发生实际删除**UpdateBatch**方法。 (若要查看已删除的记录，请设置**筛选器**属性**adFilterAffectedRecords**后**删除**称为。)  
  
 尝试从已删除的记录检索字段值将生成错误。 删除当前记录后, 已删除的记录仍保留当前直到移动到另一条记录。 一旦离开已删除的记录，它将不再可访问。  
  
 如果嵌套在事务中的删除，你可以通过使用恢复已删除的记录**不**方法。 如果要在批处理更新模式下，你可以通过使用取消的挂起的删除或组的挂起的删除**执行**方法。  
  
 如果尝试删除记录失败，因为与基础数据有冲突 （例如，记录已由另一个用户删除），该提供程序返回警告记录到**错误**集合但不会停止程序执行。 只有在所有请求的记录上冲突，则会发生运行时错误。  
  
 如果**唯一表**设置动态属性和**记录集**是执行对多个表的联接操作的结果**删除**方法将仅删除行从表中名为**唯一表**属性。  
  
 **删除**方法采用一个可选参数，允许你指定哪些记录受**删除**操作。 为此参数唯一有效的值都是以下 ADO **AffectEnum**枚举常量：  
  
-   **adAffectCurrent**影响仅当前记录。  
  
-   **adAffectGroup**影响满足当前的记录**筛选器**属性设置。 **筛选器**属性必须设置为**FilterGroupEnum**值或数组的**书签**要使用此选项。  
  
 下面的代码演示示例： 指定**adAffectGroup**调用时**删除**方法。 此示例将某些记录添加到示例**记录集**并更新数据库。 然后它筛选**记录集**使用**adFilterAffectedRecords**筛选器枚举的常数，使得只有新添加的记录以显示**记录集。** 最后，它调用**删除**方法和指定的所有记录满足当前**筛选器**应删除属性的设置 （新记录）。  
  
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
