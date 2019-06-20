---
title: 检测和解决冲突 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- conflicts [ADO], detecting and resolving
- ADO, detecting and resolving conflicts
ms.assetid: b28fdd26-c1a4-40ce-a700-2b0c9d201514
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 88d3900417bfbdaec6d2408d503b1537b8dff2da
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66702111"
---
# <a name="detecting-and-resolving-conflicts"></a>检测和解决冲突
如果您处理的记录集，在直接模式下，则要少得多的并发问题发生的机会。 另一方面，如果你的应用程序使用批处理模式更新，可能有一个好机会的另一个用户编辑同一条记录所做的更改在保存前一个用户将更改记录。 在这种情况下，您将希望应用程序来适当地处理冲突。 它可能是您所希望的最后一个人将更新发送到服务器"wins"。 或者，可能想要让最新的用户，可以决定哪种更新应优先通过为他提供两个冲突值之间进行选择。  
  
 在任何情况下，ADO 提供要处理这些类型的冲突的字段对象的 UnderlyingValue 和 OriginalValue 属性。 使用重新同步方法和记录集的筛选器属性结合使用这些属性。  
  
## <a name="remarks"></a>备注  
 当 ADO 批处理更新的过程中遇到冲突时，则将到错误集合添加一条警告。 因此，您应始终检查错误调用 batchupdate 之后，并找到它们，如果开始遇到冲突对假设进行测试后，立即。 第一步是在记录集等于 adFilterConflictingRecords 上设置筛选器属性。 这会限制上发生冲突的记录到记录集的视图。 如果 RecordCount 属性等于零，在此步骤后，您知道错误产生的冲突以外的内容。  
  
 当调用 batchupdate 之后时，ADO 和提供程序正在生成 SQL 语句，以在数据源上执行更新。 请记住，某些数据源的类型的列可以使用 WHERE 子句中的限制。  
  
 接下来，重新同步方法记录集上调用具有设置为等于 adAffectGroup 和 ResyncValues 参数设置为等于 adResyncUnderlyingValues AffectRecords 参数。 重新同步方法更新基础数据库中的当前记录集对象中的数据。 通过使用 adAffectGroup，确保仅显示与当前筛选器设置，即，仅冲突的记录，记录将与数据库同步。 如果您处理的大型记录集，这可能使显著的性能差异。 通过调用重新同步时，ResyncValues 参数设置为 adResyncUnderlyingValues，可以确保 UnderlyingValue 属性将包含从数据库 （冲突） 的值、 Value 属性将维护由用户输入的值和OriginalValue 属性将包含字段 （值之前执行最后一个成功 UpdateBatch 调用） 的原始值。 然后可以使用这些值以解决该冲突以编程方式或要求用户选择将使用的值。  
  
 这种方法是在下面的代码示例所示。 该示例人为地使用单独的记录集之前调用 UpdateBatch 更改基础表中的值创建冲突。  
  
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
  
 Status 属性的当前记录或的特定字段可用于确定已发生哪种冲突。  
  
 有关错误处理的详细信息，请参阅[的错误处理](../../../ado/guide/data/error-handling.md)。  
  
## <a name="see-also"></a>请参阅  
 [批处理模式](../../../ado/guide/data/batch-mode.md)
