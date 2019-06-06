---
title: 排序属性示例 (VB) |Microsoft Docs
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
- Sort property [ADO], Visual Basic example
ms.assetid: fc2fd40b-65d6-4023-90a3-90c9a88ef6cf
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 537ca70a2741cb1226602af5406529eaa281fcd6
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66711217"
---
# <a name="sort-property-example-vb"></a>Sort 属性示例 (VB)
此示例使用[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象的[排序](../../../ado/reference/ado-api/sort-property.md)属性来重新排列的行**记录集**派生自***作者***的表***Pubs***数据库。 辅助实用工具例程打印每个行。  
  
```  
'BeginSortVB  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
     ' connection and recordset variables  
    Dim Cnxn As New ADODB.Connection  
    Dim rstAuthors As New ADODB.Recordset  
    Dim strCnxn As String  
    Dim strSQLAuthors As String  
  
    Dim strTitle As String  
  
    ' Open connection  
    Set Cnxn = New ADODB.Connection  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    Cnxn.Open strCnxn  
  
    ' open client-side recordset to enable sort method  
    Set rstAuthors = New ADODB.Recordset  
    rstAuthors.CursorLocation = adUseClient  
    strSQLAuthors = "SELECT * FROM Authors"  
    rstAuthors.Open strSQLAuthors, Cnxn, adOpenStatic, adLockReadOnly, adCmdText  
  
     ' sort the recordset last name ascending  
    rstAuthors.Sort = "au_lname ASC, au_fname ASC"  
     ' show output  
    Debug.Print "Last Name Ascending:"  
    Debug.Print "First Name  Last Name" & vbCr  
  
    rstAuthors.MoveFirst  
    Do Until rstAuthors.EOF  
        Debug.Print rstAuthors!au_fname & " " & rstAuthors!au_lname  
        rstAuthors.MoveNext  
    Loop  
  
     ' sort the recordset last name descending  
    rstAuthors.Sort = "au_lname DESC, au_fname ASC"  
     ' show output  
    Debug.Print "Last Name Descending"  
    Debug.Print "First Name  Last Name" & vbCr  
  
    Do Until rstAuthors.EOF  
        Debug.Print rstAuthors!au_fname & " " & rstAuthors!au_lname  
        rstAuthors.MoveNext  
    Loop  
  
    ' clean up  
    rstAuthors.Close  
    Cnxn.Close  
    Set rstAuthors = Nothing  
    Set Cnxn = Nothing  
    Exit Sub  
  
ErrorHandler:  
    ' clean up  
    If Not rstAuthors Is Nothing Then  
        If rstAuthors.State = adStateOpen Then rstAuthors.Close  
    End If  
    Set rstAuthors = Nothing  
  
    If Not Cnxn Is Nothing Then  
        If Cnxn.State = adStateOpen Then Cnxn.Close  
    End If  
    Set Cnxn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
'EndSortVB  
```  
  
 这是打印给定的标题和指定的内容的辅助实用工具例程**记录集**。  
  
```  
Attribute VB_Name = "Sort"  
```  
  
## <a name="see-also"></a>请参阅  
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Sort 属性](../../../ado/reference/ado-api/sort-property.md)
