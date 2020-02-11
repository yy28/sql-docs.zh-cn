---
title: Views Append 方法示例（VB） |Microsoft Docs
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
- Append method [ADOX]
ms.assetid: b5b4c082-ac29-4f49-a8b8-e21b554c9b0d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 50b24a21c54fcf23dba0748dfba31a99b5bbb1ce
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67964795"
---
# <a name="views-append-method-example-vb"></a>视图 Append 方法示例 (VB)
下面的代码演示如何使用[命令](../../../ado/reference/ado-api/command-object-ado.md)对象和[Views](../../../ado/reference/adox-api/views-collection-adox.md)集合[Append](../../../ado/reference/adox-api/append-method-adox-views.md)方法在基础数据源中创建新视图。  
  
```  
' BeginCreateViewVB  
Sub Main()  
    On Error GoTo CreateViewError  
  
    Dim cmd As New ADODB.Command  
    Dim cat As New ADOX.Catalog  
  
    ' Open the Catalog  
    cat.ActiveConnection = _  
        "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "Data Source='Northwind.mdb';"  
  
    ' Create the command representing the view.  
    cmd.CommandText = "Select * From Customers"  
  
    ' Create the new View  
    cat.Views.Append "AllCustomers", cmd  
  
    'Clean up  
    Set cat.ActiveConnection = Nothing  
    Set cat = Nothing  
    Set cmd = Nothing  
    Exit Sub  
  
CreateViewError:  
  
    Set cat = Nothing  
    Set cmd = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
' EndCreateViewVB  
```  
  
## <a name="see-also"></a>另请参阅  
 [ActiveConnection 属性（ADOX）](../../../ado/reference/adox-api/activeconnection-property-adox.md)   
 [Append 方法（ADOX 视图）](../../../ado/reference/adox-api/append-method-adox-views.md)   
 [目录对象（ADOX）](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [视图对象（ADOX）](../../../ado/reference/adox-api/view-object-adox.md)   
 [视图集合 (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)
