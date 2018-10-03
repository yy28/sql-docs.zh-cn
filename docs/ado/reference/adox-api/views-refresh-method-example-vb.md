---
title: 视图 Refresh 方法示例 (VB) |Microsoft Docs
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
- Refresh method [ADOX]
ms.assetid: cdad2d66-6ade-40dc-9e74-e40cfa9bc127
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 123d7abe3248868295e8433d75d9e2a935cdc58d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47830635"
---
# <a name="views-refresh-method-example-vb"></a>视图 Refresh 方法示例 (VB)
下面的代码演示如何刷新[视图](../../../ado/reference/adox-api/views-collection-adox.md)系列[目录](../../../ado/reference/adox-api/catalog-object-adox.md)。 这必需的前[视图](../../../ado/reference/adox-api/view-object-adox.md)中的对象**目录**可访问。  
  
```  
' BeginViewsRefreshVB  
Sub Main()  
    On Error GoTo ProcedureViewsRefreshError  
  
    Dim cat As New ADOX.Catalog  
  
    ' Open the catalog.  
    cat.ActiveConnection = "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "Data Source='Northwind.mdb';"  
  
    ' Refresh the Procedures collection.  
    cat.Views.Refresh  
  
    'Clean up  
    Set cat = Nothing  
    Exit Sub  
  
ProcedureViewsRefreshError:  
  
    If Not cat Is Nothing Then  
        Set cat = Nothing  
    End If  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
' EndViewsRefreshVB  
```  
  
## <a name="see-also"></a>请参阅  
 [Refresh 方法 (ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)   
 [视图集合 (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)
