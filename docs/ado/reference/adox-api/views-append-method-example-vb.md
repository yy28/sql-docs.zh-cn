---
description: 视图 Append 方法示例 (VB)
title: " (VB) 查看 Append 方法示例 |Microsoft Docs"
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
author: rothja
ms.author: jroth
ms.openlocfilehash: a481db1f6b185c082dc26cc8ede030938bbfce9b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88439319"
---
# <a name="views-append-method-example-vb"></a>视图 Append 方法示例 (VB)
下面的代码演示如何使用 [命令](../../../ado/reference/ado-api/command-object-ado.md) 对象和 [Views](../../../ado/reference/adox-api/views-collection-adox.md) 集合 [Append](../../../ado/reference/adox-api/append-method-adox-views.md) 方法在基础数据源中创建新视图。  
  
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
 [ActiveConnection 属性 (ADOX) ](../../../ado/reference/adox-api/activeconnection-property-adox.md)   
 [) 的 Append 视图 (追加方法 ](../../../ado/reference/adox-api/append-method-adox-views.md)   
 [目录对象 (ADOX) ](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [视图对象 (ADOX) ](../../../ado/reference/adox-api/view-object-adox.md)   
 [视图集合 (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)
