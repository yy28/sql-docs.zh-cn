---
title: 视图 Delete 方法示例 (VB) |Microsoft Docs
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
- Delete method [ADOX]
ms.assetid: 17df2a83-4166-4df8-8c17-0a33aaac8582
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 15070d0d89e63bc84e4a4a9ca0ed9091d9f0878e
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66697057"
---
# <a name="views-delete-method-example-vb"></a>视图 Delete 方法示例 (VB)
下面的代码演示如何使用[删除](../../../ado/reference/adox-api/delete-method-adox-collections.md)方法从目录中删除视图。  
  
```  
' BeginDeleteViewVB  
Sub Main()  
    On Error GoTo DeleteViewError  
  
    Dim cat As New ADOX.Catalog  
  
    ' Open the catalog  
    cat.ActiveConnection = "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "Data Source='Northwind.mdb';"  
  
    'Delete the View  
    cat.Views.Delete "AllCustomers"  
  
    'Clean up  
    Set cat.ActiveConnection = Nothing  
    Set cat = Nothing  
    Exit Sub  
  
DeleteViewError:  
    Set cat = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
' EndDeleteViewVB  
```  
  
## <a name="see-also"></a>请参阅  
 [Delete 方法 （ADOX 集合）](../../../ado/reference/adox-api/delete-method-adox-collections.md)   
 [视图集合 (ADOX)](../../../ado/reference/adox-api/views-collection-adox.md)
