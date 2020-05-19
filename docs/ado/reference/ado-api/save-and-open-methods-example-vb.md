---
title: Save 和 Open 方法示例（VB） |Microsoft Docs
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
- Save method [ADO], Visual Basic example
- Open method [ADO]
ms.assetid: ddccdf58-9c57-4c9b-8b7f-0cf193f955fb
author: rothja
ms.author: jroth
ms.openlocfilehash: 37237094c3778fad9c45a2ccad3eebdce02a62bc
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2020
ms.locfileid: "82755931"
---
# <a name="save-and-open-methods-example-vb"></a>Save 和 Open 方法示例 (VB)
这三个示例演示如何将[Save](../../../ado/reference/ado-api/save-method.md)和[Open](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法一起使用。  
  
 假设您正在出差，并希望从数据库中获取表。 在开始之前，你可以访问作为[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)的数据，并将其保存为可传送的形式。 到达目标后，可将**记录集**作为本地、断开连接的**记录集**访问。 对**记录集**进行更改，然后再次保存。 最后，当您返回 home 时，您将再次连接到该数据库，并将其更新为对您的路上所做的更改。  
  
 首先，访问并保存***Authors***表。  
  
```  
'BeginSaveVB  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    'recordset and connection variables  
    Dim rstAuthors As ADODB.Recordset  
    Dim Cnxn As ADODB.Connection  
    Dim strCnxn As String  
    Dim strSQLAuthors As String  
  
    ' Open connection  
    Set Cnxn = New ADODB.Connection  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    Cnxn.Open strCnxn  
  
    Set rstAuthors = New ADODB.Recordset  
    strSQLAuthors = "SELECT au_id, au_lname, au_fname, city, phone FROM Authors"  
    rstAuthors.Open strSQLAuthors, Cnxn, adOpenDynamic, adLockOptimistic, adCmdText  
  
    'For sake of illustration, save the Recordset to a diskette in XML format  
    rstAuthors.Save "c:\Pubs.xml", adPersistXML  
  
    ' clean up  
    rstAuthors.Close  
    Cnxn.Close  
    Set rstAuthors = Nothing  
    Set Cnxn = Nothing  
    Exit Sub  
  
ErrorHandler:  
    'clean up  
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
'EndSaveVB  
```  
  
 此时，您已到达目标位置。 您将作为本地、断开连接的**记录集**访问***作者***表。 你必须在用于访问保存的文件的计算机上具有**MSPersist**提供程序，a:\Pubs.xml。  
  
```  
Attribute VB_Name = "Save"  
```  
  
 最后，返回 home。 现在，用所做的更改更新数据库。  
  
```  
Attribute VB_Name = "Save"  
```  
  
## <a name="see-also"></a>另请参阅  
 [Open 方法（ADO 记录集）](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Recordset 对象（ADO）](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [有关记录集持久性的详细信息](../../../ado/guide/data/more-about-recordset-persistence.md)   
 [Save 方法](../../../ado/reference/ado-api/save-method.md)
