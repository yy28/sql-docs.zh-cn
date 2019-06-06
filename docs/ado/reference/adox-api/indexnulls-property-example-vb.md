---
title: IndexNulls 属性示例 (VB) |Microsoft Docs
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
- IndexNulls property [ADOX], Visual Basic example
ms.assetid: 45204669-32c0-4690-aab9-ddf0fd71ae48
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: fc1a2db077a08b37ddd6143ea7a76ebd257f2a48
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66706482"
---
# <a name="indexnulls-property-example-vb"></a>IndexNulls 属性示例 (VB)
此示例演示[IndexNulls](../../../ado/reference/adox-api/indexnulls-property-adox.md)的属性[索引](../../../ado/reference/adox-api/index-object-adox.md)。 代码将创建一个新的索引并设置的值**IndexNulls**根据用户输入 （来自名为列表 1 的列表框）。 然后，将**索引**追加到**员工**[表](../../../ado/reference/adox-api/table-object-adox.md)中*Northwind* [目录](../../../ado/reference/adox-api/catalog-object-adox.md)。 新**索引**应用于[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)基于**员工**表，以及**记录集**打开。 一条新记录添加到**员工**表中，使用**Null**中索引字段的值。 是否显示此新记录的设置决定**IndexNulls**属性。  
  
```  
' BeginIndexNullsVB  
Private Sub cmdIndexNulls_Click()  
    IndexNullsX  
End Sub  
  
Sub IndexNullsX()  
  
    Dim cnn As New ADODB.Connection  
    Dim catNorthwind As New ADOX.Catalog  
    Dim idxNew As New ADOX.Index  
    Dim rstEmployees As New ADODB.Recordset  
    Dim varBookmark As Variant  
  
    ' Connect the catalog.  
    cnn.Open "Provider=Microsoft.Jet.OLEDB.4.0;" & _  
        "data source=c:\Program Files\" & _  
        "Microsoft Office\Office\Samples\Northwind.mdb;"  
  
    Set catNorthwind.ActiveConnection = cnn  
  
    ' Append Country column to new index  
    idxNew.Columns.Append "Country"  
    idxNew.Name = "NewIndex"  
  
    ' Set IndexNulls based on user selection in listbox List1  
    Select Case List1.List(List1.ListIndex)  
        Case "Allow"  
            idxNew.IndexNulls = adIndexNullsAllow  
        Case "Ignore"  
            idxNew.IndexNulls = adIndexNullsIgnore  
        Case Else  
            End  
    End Select  
  
    'Append new index to Employees table  
    catNorthwind.Tables("Employees").Indexes.Append idxNew  
  
    rstEmployees.Index = idxNew.Name  
    rstEmployees.Open "Employees", cnn, adOpenKeyset, _  
        adLockOptimistic, adCmdTableDirect  
  
    With rstEmployees  
        ' Add a new record to the Employees table.  
        .AddNew  
        !FirstName = "Gary"  
        !LastName = "Haarsager"  
        .Update  
  
        ' Bookmark the newly added record  
        varBookmark = .Bookmark  
  
        ' Use the new index to set the order of the records.  
        .MoveFirst  
  
        Debug.Print "Index = " & .Index & _  
            ", IndexNulls = " & idxNew.IndexNulls  
        Debug.Print "  Country - Name"  
  
        ' Enumerate the Recordset. The value of the  
        ' IndexNulls property will determine if the newly  
        ' added record appears in the output.  
        Do While Not .EOF  
            Debug.Print "    " & _  
                IIf(IsNull(!Country), "[Null]", !Country) & _  
                " - " & !FirstName & " " & !LastName  
            .MoveNext  
        Loop  
  
        ' Delete new record because this is a demonstration.  
        .Bookmark = varBookmark  
        .Delete  
  
        .Close  
    End With  
  
    ' Delete new Index because this is a demonstration.  
    catNorthwind.Tables("Employees").Indexes.Delete idxNew.Name  
    Set catNorthwind = Nothing  
  
End Sub  
' EndIndexNullsVB  
```  
  
## <a name="see-also"></a>请参阅  
 [索引对象 (ADOX)](../../../ado/reference/adox-api/index-object-adox.md)   
 [IndexNulls 属性 (ADOX)](../../../ado/reference/adox-api/indexnulls-property-adox.md)
