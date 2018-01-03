---
title: "创建表的示例 (VB) 之间的新外键关系 |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
dev_langs: VB
helpviewer_keywords:
- Key Type property [ADOX], Visual Basic example
- RelatedTable property [ADOX], Visual Basic example
- Keys Append method [ADOX], Visual Basic example
- UpdateRule property [ADOX], Visual Basic example
- RelatedColumn property [ADOX], Visual Basic example
ms.assetid: 13b5b1c3-6af6-439e-bb65-976578ba6bc2
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 20b9ad65e6d9f4352db96848e8f096710fcf2db2
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="keys-append-method-key-type-relatedcolumn-relatedtable-and-updaterule-properties-example-vb"></a>密钥追加方法、 密钥类型、 RelatedColumn、 RelatedTable 和 UpdateRule 属性示例 (VB)
下面的代码演示如何创建新的外键关系，两个名为的现有表之间**客户**和**订单**。  
  
```  
' BeginCreateKeyVB  
Sub Main()  
    On Error GoTo CreateKeyError  
  
    Dim kyForeign As New ADOX.Key  
    Dim cat As New ADOX.Catalog  
  
    ' Connect to the catalog.  
    cat.ActiveConnection = "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "Data Source='Northwind.mdb';"  
  
    ' Define the foreign key.  
    kyForeign.Name = "CustOrder"  
    kyForeign.Type = adKeyForeign  
    kyForeign.RelatedTable = "Customers"  
    kyForeign.Columns.Append "CustomerId"  
    kyForeign.Columns("CustomerId").RelatedColumn = "CustomerId"  
    kyForeign.UpdateRule = adRICascade  
  
    ' Append the foreign key to the keys collection.  
    cat.Tables("Orders").Keys.Append kyForeign  
  
    'Delete the key t demonstrate the Delete method.  
    cat.Tables("Orders").Keys.Delete kyForeign.Name  
  
    'Clean up.  
    Set cat.ActiveConnection = Nothing  
    Set cat = Nothing  
    Set kyForeign = Nothing  
    Exit Sub  
  
CreateKeyError:  
    Set cat = Nothing  
    Set kyForeign = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
  
End Sub  
' EndCreateKeyVB  
```  
  
## <a name="see-also"></a>另请参阅  
 [Append 方法 （ADOX 列）](../../../ado/reference/adox-api/append-method-adox-columns.md)   
 [Append 方法 （ADOX 键）](../../../ado/reference/adox-api/append-method-adox-keys.md)   
 [目录对象 (ADOX)](../../../ado/reference/adox-api/catalog-object-adox.md)   
 [列对象 (ADOX)](../../../ado/reference/adox-api/column-object-adox.md)   
 [列集合 (ADOX)](../../../ado/reference/adox-api/columns-collection-adox.md)   
 [密钥对象 (ADOX)](../../../ado/reference/adox-api/key-object-adox.md)   
 [键集合 (ADOX)](../../../ado/reference/adox-api/keys-collection-adox.md)   
 [Name 属性 (ADOX)](../../../ado/reference/adox-api/name-property-adox.md)   
 [RelatedColumn 属性 (ADOX)](../../../ado/reference/adox-api/relatedcolumn-property-adox.md)   
 [RelatedTable 属性 (ADOX)](../../../ado/reference/adox-api/relatedtable-property-adox.md)   
 [表对象 (ADOX)](../../../ado/reference/adox-api/table-object-adox.md)   
 [表集合 (ADOX)](../../../ado/reference/adox-api/tables-collection-adox.md)   
 [类型属性 （密钥） (ADOX)](../../../ado/reference/adox-api/type-property-key-adox.md)   
 [UpdateRule 属性 (ADOX)](../../../ado/reference/adox-api/updaterule-property-adox.md)
