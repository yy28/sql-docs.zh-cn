---
title: 访问分层记录集中的行 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- hierarchical Recordsets [ADO]
- data shaping [ADO], hierarchical Recordsets
ms.assetid: 25f1d2a1-6d5e-4457-aa07-5db5c75dee18
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e73b2ca96cc5e7eb7683b72aa19fd59a318b8596
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "67926359"
---
# <a name="accessing-rows-in-a-hierarchical-recordset-example"></a>访问分层记录集中的行（示例）
下面的示例演示访问分层[记录集中](../../../ado/reference/ado-api/recordset-object-ado.md)的行所需的步骤：

1.  **作者**和**titleauthor**表中的**记录集**对象均由作者 ID 相关联。

2.  外部循环显示每个作者的名字和姓氏、省/市/自治区和标识。

3.  每行的追加的**记录集**从[字段](../../../ado/reference/ado-api/fields-collection-ado.md)集合中检索并分配给*rstTitleAuthor*。

4.  内部循环显示追加的**记录集中**每一行的四个字段。

 出于说明目的， [StayInSync](../../../ado/reference/ado-api/stayinsync-property.md)属性设置为**false** ，以便您可以看到在外部循环的每次迭代中显式更改章节。 为了使代码示例更高效，你可以在步骤3中移动步骤2中第一行之前的分配，以便仅执行一次分配。 然后将[StayInSync](../../../ado/reference/ado-api/stayinsync-property.md)属性设置为**true**，以便当*rst*移动到新行时， *rstTitleAuthor*将隐式地自动更改为相应的章节。

## <a name="example"></a>示例

```
Sub datashape()
   Dim cnn As New ADODB.Connection
   Dim rst As New ADODB.Recordset
   Dim rstTitleAuthor As New ADODB.Recordset

   cnn.Provider = "MSDataShape"
   cnn.Open    "Data Provider=MSDASQL;" & _
               "Data Source=SRV;Integrated Security=SSPI;Database=Pubs"
' STEP 1
   rst.StayInSync = FALSE
   rst.Open    "SHAPE  {select * from authors} "  & _
               "APPEND ({select * from titleauthor} " & _
               "RELATE au_id TO au_id) AS chapTitleAuthor", _
               cnn
' STEP 2
   While Not rst.EOF
      Debug.Print    rst("au_fname"), rst("au_lname"), _
                     rst("state"), rst("au_id")
' STEP 3
      Set rstTitleAuthor = rst("chapTitleAuthor").Value
' STEP 4
      While Not rstTitleAuthor.EOF
         Debug.Print rstTitleAuthor(0), rstTitleAuthor(1), _
                     rstTitleAuthor(2), rstTitleAuthor(3)
         rstTitleAuthor.MoveNext
      Wend
      rst.MoveNext
   Wend
End Sub
```

## <a name="see-also"></a>另请参阅
 [数据定形概述](../../../ado/guide/data/data-shaping-overview.md)[字段对象](../../../ado/reference/ado-api/field-object.md)[字段集合（ado）](../../../ado/reference/ado-api/fields-collection-ado.md) [正式形状语法](../../../ado/guide/data/formal-shape-grammar.md) [Microsoft 数据定形服务 OLE DB （ADO 服务提供程序）](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) [记录集对象（Ado）](../../../ado/reference/ado-api/recordset-object-ado.md) [必需的数据定形的提供程序](../../../ado/guide/data/required-providers-for-data-shaping.md)形状[计算子句](../../../ado/guide/data/shape-compute-clause.md)中的[APPEND 子句](../../../ado/guide/data/shape-append-clause.md) [shape 命令](../../../ado/guide/data/shape-commands-in-general.md) [Visual Basic for Applications 函数](../../../ado/guide/data/visual-basic-for-applications-functions.md)
