---
title: Filter 和 RecordCount 属性示例（VB） |Microsoft Docs
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
- RecordCount property [ADO], Visual Basic example
- Filter property [ADO], Visual Basic example
ms.assetid: e8bc63c7-8967-438a-9a49-512478a87a15
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6f94440d9ddd0d0b5091f2a106f603397147ebda
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67918643"
---
# <a name="filter-and-recordcount-properties-example-vb"></a>Filter 和 RecordCount 属性示例 (VB)
此示例打开***Pubs***数据库的发布服务器表中的[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)。 然后，它使用[筛选器](../../../ado/reference/ado-api/filter-property.md)属性将可见记录的数目限制为特定国家/地区的发布者。 **RecordCount**属性用于显示已筛选和未筛选的记录集之间的差异。  
  
```  
'BeginFilterVB  
  
    'To integrate this code  
    'replace the data source and initial catalog values  
    'in the connection string  
  
Public Sub Main()  
    On Error GoTo ErrorHandler  
  
    ' recordset variables  
    Dim rstPublishers As ADODB.Recordset  
    Dim Cnxn As ADODB.Connection  
    Dim strCnxn As String  
    Dim SQLPublishers As String  
  
     ' criteria variables  
    Dim intPublisherCount As Integer  
    Dim strCountry As String  
    Dim strMessage As String  
  
     ' open connection  
    Set Cnxn = New ADODB.Connection  
    strCnxn = "Provider='sqloledb';Data Source='MySqlServer';" & _  
        "Initial Catalog='Pubs';Integrated Security='SSPI';"  
    Cnxn.Open strCnxn  
  
    ' open recordset with data from Publishers table  
    Set rstPublishers = New ADODB.Recordset  
    SQLPublishers = "publishers"  
    rstPublishers.Open SQLPublishers, strCnxn, adOpenStatic, , adCmdTable  
  
    intPublisherCount = rstPublishers.RecordCount  
  
    ' get user input  
    strCountry = Trim(InputBox("Enter a country to filter on (e.g. USA):"))  
  
    If strCountry <> "" Then  
        ' open a filtered Recordset object  
        rstPublishers.Filter = "Country ='" & strCountry & "'"  
  
        If rstPublishers.RecordCount = 0 Then  
            MsgBox "No publishers from that country."  
        Else  
           ' print number of records for the original recordset  
           ' and the filtered recordset  
            strMessage = "Orders in original recordset: " & _  
                vbCr & intPublisherCount & vbCr & _  
                "Orders in filtered recordset (Country = '" & _  
                strCountry & "'): " & vbCr & _  
                rstPublishers.RecordCount  
            MsgBox strMessage  
        End If  
    End If  
  
    ' clean up  
    rstPublishers.Close  
    Cnxn.Close  
    Set rstPublishers = Nothing  
    Set Cnxn = Nothing  
    Exit Sub  
  
ErrorHandler:  
    ' clean up  
    If Not rstPublishers Is Nothing Then  
        If rstPublishers.State = adStateOpen Then rstPublishers.Close  
    End If  
    Set rstPublishers = Nothing  
  
    If Not Cnxn Is Nothing Then  
        If Cnxn.State = adStateOpen Then Cnxn.Close  
    End If  
    Set Cnxn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
  
End Sub  
'EndFilterVB  
```  
  
> [!NOTE]
>  如果知道要选择的数据，则打开包含 SQL 语句的**记录集**通常更有效。 此示例演示如何仅创建一个**记录集**，并从特定的国家/地区获取记录。  
  
```  
Attribute VB_Name = "Filter"  
```  
  
## <a name="see-also"></a>另请参阅  
 [筛选器属性](../../../ado/reference/ado-api/filter-property.md)   
 [RecordCount 属性（ADO）](../../../ado/reference/ado-api/recordcount-property-ado.md)   
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
