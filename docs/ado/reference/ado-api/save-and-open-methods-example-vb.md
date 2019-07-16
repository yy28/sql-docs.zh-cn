---
title: Save 和 Open 方法示例 (VB) |Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6d42488f8f167cc7c98f663478c742963d24253c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67931198"
---
# <a name="save-and-open-methods-example-vb"></a>Save 和 Open 方法示例 (VB)
这三个示例演示如何[保存](../../../ado/reference/ado-api/save-method.md)并[打开](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法可以一起使用。  
  
 假定您将在出差并且想要参加巡回赛从数据库表。 在之前，访问将数据作为[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)并将其保存在可移植的窗体中。 当您在目标中，您可以访问**记录集**为本地，断开连接**记录集**。 进行更改**记录集**，然后再次保存。 最后，您回到家时，您将再次连接到数据库并更新与公路所做的更改。  
  
 首先，访问，并保存***作者***表。  
  
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
  
 此时，您已到达目标。 将访问***作者***表为本地，断开连接**记录集**。 您必须具有**MSPersist**您用来访问保存在文件中，在计算机上的提供程序 a:\Pubs.xml。  
  
```  
Attribute VB_Name = "Save"  
```  
  
 最后，您返回主页。 现在使用所做的更改更新数据库。  
  
```  
Attribute VB_Name = "Save"  
```  
  
## <a name="see-also"></a>请参阅  
 [Open 方法 （ADO 记录集）](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [有关记录集暂留的详细信息](../../../ado/guide/data/more-about-recordset-persistence.md)   
 [Save 方法](../../../ado/reference/ado-api/save-method.md)
