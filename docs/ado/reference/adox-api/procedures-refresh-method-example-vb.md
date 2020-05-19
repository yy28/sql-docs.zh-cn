---
title: 过程 Refresh 方法示例（VB） |Microsoft Docs
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
- Refresh method [ADOX], Visual Basic example
ms.assetid: 499679bd-287b-487d-bdfb-3803abffec1c
author: rothja
ms.author: jroth
ms.openlocfilehash: 162e6739a61b52922998a61c019225ef0f8d5216
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2020
ms.locfileid: "82748595"
---
# <a name="procedures-refresh-method-example-vb"></a>过程 Refresh 方法示例 (VB)
下面的代码演示如何刷新[目录](../../../ado/reference/adox-api/catalog-object-adox.md)的[过程](../../../ado/reference/adox-api/procedures-collection-adox.md)集合。 这是必需的，然后才能访问**目录**中的[过程](../../../ado/reference/adox-api/procedure-object-adox.md)对象。  
  
```  
' BeginProceduresRefreshVB  
Sub Main()  
    On Error GoTo ProcedureRefreshError  
  
    Dim cat As New ADOX.Catalog  
  
    ' Open the Catalog  
    cat.ActiveConnection = _  
        "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "Data Source='Northwind.mdb';"  
  
    ' Refresh the Procedures collection  
    cat.Procedures.Refresh  
  
    'Clean up  
    Set cat.ActiveConnection = Nothing  
    Set cat = Nothing  
    Exit Sub  
  
ProcedureRefreshError:  
    Set cat = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
' EndProceduresRefreshVB  
```  
  
## <a name="see-also"></a>另请参阅  
 [目录对象（ADOX）](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [过程集合（ADOX）](../../../ado/reference/adox-api/procedures-collection-adox.md)   
 [Refresh 方法 (ADO)](../../../ado/reference/ado-api/refresh-method-ado.md)
