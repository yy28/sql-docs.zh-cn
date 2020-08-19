---
description: 视图 Refresh 方法示例 (VB)
title: " (VB) 的视图刷新方法示例 |Microsoft Docs"
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 3112670df34b0e74e359ef0e514d9acdc8620788
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88439269"
---
# <a name="views-refresh-method-example-vb"></a>视图 Refresh 方法示例 (VB)
下面的代码演示如何刷新[目录](../../../ado/reference/adox-api/catalog-object-adox.md)的[Views](../../../ado/reference/adox-api/views-collection-adox.md)集合。 这是必需的，才能访问**目录**中的[视图](../../../ado/reference/adox-api/view-object-adox.md)对象。  
  
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
  
## <a name="see-also"></a>另请参阅  
 [ (ADO 的 Refresh 方法) ](../../../ado/reference/ado-api/refresh-method-ado.md)   
 [视图集合 (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)
