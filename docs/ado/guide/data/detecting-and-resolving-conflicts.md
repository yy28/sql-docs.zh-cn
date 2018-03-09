---
title: "检测和解决冲突 |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- conflicts [ADO], detecting and resolving
- ADO, detecting and resolving conflicts
ms.assetid: b28fdd26-c1a4-40ce-a700-2b0c9d201514
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 61f54b700be8ec03e56bf63999dc7f93b8d5fcdb
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2018
---
# <a name="detecting-and-resolving-conflicts"></a>检测和解决冲突
如果你处理的记录集，在即时模式中，则要少得多的并发问题发生的机会。 另一方面，如果你的应用程序使用批处理模式更新，可能有一个不错的概率一个用户将更改的记录，然后再将保存所做的另一个用户编辑同一个记录的更改。 在这种情况下，你需要应用程序，用于正常处理冲突。 它可能是您所希望的最后一个人将更新发送到服务器"wins"。 或者，你可能想要让最新的用户来决定哪种更新应优先通过向他提供两个冲突值之间进行选择。  
  
 任何情况下，ADO 提供要处理这些类型的冲突的字段对象的 UnderlyingValue 和 OriginalValue 属性。 使用重新同步方法和记录集的筛选器属性结合使用这些属性。  
  
## <a name="remarks"></a>注释  
 当 ADO 批处理更新的过程中遇到冲突时，警告将添加到错误集合中。 因此，你应始终检查错误立即后调用 batchupdate 之后，并且如果找到它们，就会开始测试遇到了冲突的假设。 第一步是在记录集等于 adFilterConflictingRecords 上设置的筛选器属性。 这就限制了对你以上正在发生冲突的记录的记录集的视图。 如果 RecordCount 属性值等于零，在此步骤后，就知道错误由冲突之外的内容。  
  
 当你调用 batchupdate 之后时，ADO 和提供程序正在生成 SQL 语句以便在数据源上执行更新。 请记住，某些数据源可以在其使用类型的列的 WHERE 子句中的限制。  
  
 接下来，重新同步方法记录集上调用具有 AffectRecords 自变量将设置为等于 adAffectGroup 和将设置为等于 adResyncUnderlyingValues ResyncValues 自变量。 重新同步方法更新当前的记录集对象从基础数据库中的数据。 通过使用 adAffectGroup，您在确保只有可见与当前筛选器设置，即，仅冲突的记录，记录与数据库重新同步的。 如果你处理的大型的记录集，这会使显著的性能差异。 通过设置为 adResyncUnderlyingValues ResyncValues 自变量，在调用重新同步时，确保 UnderlyingValue 属性将包含从数据库 （冲突） 值时，将 Value 属性将保留由用户输入的值和OriginalValue 属性将保存的字段 （前的最后一个成功 UpdateBatch 调用已具有的值） 的原始值。 然后可以使用这些值以编程方式解决冲突或要求用户选择将使用的值。  
  
 下面的代码示例演示了此技术。 该示例人为创建使用单独的记录集调用 UpdateBatch 之前更改基础表中的值的冲突。  
  
```  
'BeginConflicts  
    strConn = "Provider=SQLOLEDB;Initial Catalog=Northwind;" & _  
              "Data Source=MySQLServer;Integrated Security=SSPI;"  
  
    strSQL = "SELECT * FROM Shippers WHERE ShipperID = 2"  
  
    'Open Rs and change a value  
    Set objRs1 = New ADODB.Recordset  
    Set objRs2 = New ADODB.Recordset  
    objRs1.CursorLocation = adUseClient  
    objRs1.Open strSQL, strConn, adOpenStatic, adLockBatchOptimistic, adCmdText  
    objRs1("Phone") = "(111) 555-1111"  
  
    'Introduce a conflict at the db...  
    objRs2.Open strSQL, strConn, adOpenKeyset, adLockOptimistic, adCmdText  
    objRs2("Phone") = "(999) 555-9999"  
    objRs2.Update  
    objRs2.Close  
    Set objRs2 = Nothing  
  
    On Error Resume Next  
    objRs1.UpdateBatch  
  
    If objRs1.ActiveConnection.Errors.Count <> 0 Then  
        Dim intConflicts As Integer  
  
        intConflicts = 0  
  
        objRs1.Filter = adFilterConflictingRecords  
  
        intConflicts = objRs1.RecordCount  
  
        'Resync so we can see the UnderlyingValue and offer user a choice.  
        'This sample only displays all three values and resets to original.  
        objRs1.Resync adAffectGroup, adResyncUnderlyingValues  
  
        If intConflicts > 0 Then  
            strMsg = "A conflict occurred with updates for " & intConflicts & _  
                     " record(s)." & vbCrLf & "The values will be restored" & _  
                     " to their original values." & vbCrLf & vbCrLf  
  
            objRs1.MoveFirst  
            While Not objRs1.EOF  
              strMsg = strMsg & "SHIPPER = " & objRs1("CompanyName") & vbCrLf  
              strMsg = strMsg & "Value = " & objRs1("Phone").Value & vbCrLf  
              strMsg = strMsg & "UnderlyingValue = " & _  
                                 objRs1("Phone").UnderlyingValue & vbCrLf  
              strMsg = strMsg & "OriginalValue = " & _  
                                 objRs1("Phone").OriginalValue & vbCrLf  
              strMsg = strMsg & vbCrLf & "Original value has been restored."  
  
              MsgBox strMsg, vbOKOnly, _  
                    "Conflict " & objRs1.AbsolutePosition & _  
                    " of " & intConflicts  
  
              objRs1("Phone").Value = objRs1("Phone").OriginalValue  
              objRs1.MoveNext  
            Wend  
  
            objRs1.UpdateBatch adAffectGroup  
        Else  
            'Other error occurred. Minimal handling in this example.  
             strMsg = "Errors occurred during the update. " & _  
                        objRs1.ActiveConnection.Errors(0).Number & " " & _  
                        objRs1.ActiveConnection.Errors(0).Description  
        End If  
  
        On Error GoTo 0  
    End If  
  
    objRs1.MoveFirst  
    objRs1.Close  
    Set objRs1 = Nothing  
'EndConflicts  
```  
  
 状态属性的当前记录或的特定字段可用于确定已发生哪种类型的冲突。  
  
 有关错误处理的详细信息，请参阅[错误处理](../../../ado/guide/data/error-handling.md)。  
  
## <a name="see-also"></a>另请参阅  
 [批处理模式](../../../ado/guide/data/batch-mode.md)
