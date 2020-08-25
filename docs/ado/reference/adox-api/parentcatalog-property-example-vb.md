---
description: ParentCatalog 属性示例 (VB)
title: ParentCatalog 属性示例 (VB) |Microsoft Docs
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
- ParentCatalog property [ADOX], Visual Basic example
ms.assetid: 448bc850-7584-4c5f-89f3-5f4fee88b259
author: rothja
ms.author: jroth
ms.openlocfilehash: 66e80c85d1361c99499c91685d46e2df29b59957
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/24/2020
ms.locfileid: "88769806"
---
# <a name="parentcatalog-property-example-vb"></a>ParentCatalog 属性示例 (VB)
下面的代码演示了如何在将表追加到目录之前，使用 [ParentCatalog](./parentcatalog-property-adox.md) 属性访问特定于提供程序的属性。 属性为 **自动增量**，这会在 Microsoft Jet 数据库中创建自动增量字段。  
  
```  
' BeginCreateAutoIncrColumnVB  
Sub Main()  
    On Error GoTo CreateAutoIncrColumnError  
  
    Dim cnn As New ADODB.Connection  
    Dim cat As New ADOX.Catalog  
    Dim tbl As New ADOX.Table  
  
    cnn.Open "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "Data Source='Northwind.mdb';"  
    Set cat.ActiveConnection = cnn  
  
    With tbl  
        .Name = "MyContacts"  
        Set .ParentCatalog = cat  
        ' Create fields and append them to the new Table object.  
        .Columns.Append "ContactId", adInteger  
        ' Make the ContactId column and auto incrementing column  
        .Columns("ContactId").Properties("AutoIncrement") = True  
        .Columns.Append "CustomerID", adVarWChar  
        .Columns.Append "FirstName", adVarWChar  
        .Columns.Append "LastName", adVarWChar  
        .Columns.Append "Phone", adVarWChar, 20  
        .Columns.Append "Notes", adLongVarWChar  
    End With  
  
    cat.Tables.Append tbl  
    Debug.Print "Table 'MyContacts' is added."  
  
    ' Delete the table as this is a demonstration.  
    cat.Tables.Delete tbl.Name  
    Debug.Print "Table 'MyContacts' is delete."  
  
    'Clean up  
    cnn.Close  
    Set cat = Nothing  
    Set tbl = Nothing  
    Set cnn = Nothing  
    Exit Sub  
  
CreateAutoIncrColumnError:  
  
    Set cat = Nothing  
    Set tbl = Nothing  
  
    If Not cnn Is Nothing Then  
        If cnn.State = adStateOpen Then cnn.Close  
    End If  
    Set cnn = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
  
End Sub  
' EndCreateAutoIncrColumnVB  
```  
  
## <a name="see-also"></a>另请参阅  
 [Append 列 (追加方法) ](./append-method-adox-columns.md)   
 [Append 表 (追加方法) ](./append-method-adox-tables.md)   
 [目录对象 (ADOX) ](./catalog-object-adox.md)   
 [列对象 (ADOX) ](./column-object-adox.md)   
 [列集合 (ADOX) ](./columns-collection-adox.md)   
 [名称属性 (ADOX) ](./name-property-adox.md)   
 [ParentCatalog 属性 (ADOX) ](./parentcatalog-property-adox.md)   
 [Table 对象 (ADOX) ](./table-object-adox.md)   
 [Type 属性（列）(ADOX)](./type-property-column-adox.md)