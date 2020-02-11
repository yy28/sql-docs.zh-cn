---
title: BeginTrans、CommitTrans 和 RollbackTrans 方法示例（VB） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- RollbackTrans method [ADO], Visual Basic example
- CommitTrans method [ADO], Visual Basic example
- BeginTrans method [ADO], Visual Basic example
ms.assetid: aa7de324-cd71-4bd0-8043-24229f4a785e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0cfb65adeab6f97faca44dc917396bc02fab2fa1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67920457"
---
# <a name="begintrans-committrans-and-rollbacktrans-methods-example-vb"></a>BeginTrans、CommitTrans 和 RollbackTrans 方法示例（VB）
此示例将更改数据库的***Titles***表中所有心理学书籍的类型。 [BeginTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)方法启动了一个事务，该事务隔离对***标题***表所做的所有更改时， [CommitTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)方法会保存这些更改。 您可以使用[RollbackTrans](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)方法来撤消使用[Update](../../../ado/reference/ado-api/update-method.md)方法保存的更改。  
  
```  
'BeginBeginTransVB  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    'recordset and connection variables  
    Dim Cnxn As ADODB.Connection  
    Dim strCnxn As String  
    Dim rstTitles As ADODB.Recordset  
    Dim strSQLTitles As String  
    'record variables  
    Dim strTitle As String  
    Dim strMessage As String  
  
    ' Open connection  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    Set Cnxn = New ADODB.Connection  
    Cnxn.Open strCnxn  
  
    ' Open recordset dynamic to allow for changes  
    Set rstTitles = New ADODB.Recordset  
    strSQLTitles = "Titles"  
    rstTitles.Open strSQLTitles, Cnxn, adOpenDynamic, adLockPessimistic, adCmdTable  
  
    Cnxn.BeginTrans  
  
    ' Loop through recordset and prompt user  
    ' to change the type for a specified title  
  
    rstTitles.MoveFirst  
  
    Do Until rstTitles.EOF  
        If Trim(rstTitles!Type) = "psychology" Then  
            strTitle = rstTitles!Title  
            strMessage = "Title: " & strTitle & vbCr & _  
            "Change type to self help?"  
  
            ' If yes, change type for the specified title  
            If MsgBox(strMessage, vbYesNo) = vbYes Then  
                rstTitles!Type = "self_help"  
                rstTitles.Update  
            End If  
        End If  
    rstTitles.MoveNext  
    Loop  
  
    ' Prompt user to commit all changes made  
    If MsgBox("Save all changes?", vbYesNo) = vbYes Then  
        Cnxn.CommitTrans  
    Else  
        Cnxn.RollbackTrans  
    End If  
  
    ' Print recordset  
    rstTitles.Requery  
    rstTitles.MoveFirst  
    Do While Not rstTitles.EOF  
        Debug.Print rstTitles!Title & " - " & rstTitles!Type  
        rstTitles.MoveNext  
    Loop  
  
    ' Restore original data as this is a demo  
    rstTitles.MoveFirst  
  
    Do Until rstTitles.EOF  
        If Trim(rstTitles!Type) = "self_help" Then  
            rstTitles!Type = "psychology"  
            rstTitles.Update  
        End If  
        rstTitles.MoveNext  
    Loop  
  
    ' clean up  
    rstTitles.Close  
    Cnxn.Close  
    Set rstTitles = Nothing  
    Set Cnxn = Nothing  
    Exit Sub  
  
ErrorHandler:  
    ' clean up  
    If Not rstTitles Is Nothing Then  
        If rstTitles.State = adStateOpen Then rstTitles.Close  
    End If  
    Set rstTitles = Nothing  
  
    If Not Cnxn Is Nothing Then  
        If Cnxn.State = adStateOpen Then Cnxn.Close  
    End If  
    Set Cnxn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
  
'EndBeginTransVB  
```  
  
## <a name="see-also"></a>另请参阅  
 [BeginTrans、CommitTrans 和 RollbackTrans 方法（ADO）](../../../ado/reference/ado-api/begintrans-committrans-and-rollbacktrans-methods-ado.md)   
 [连接对象 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)
