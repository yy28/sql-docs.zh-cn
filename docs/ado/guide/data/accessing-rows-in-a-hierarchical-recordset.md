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
manager: craigg
ms.openlocfilehash: 83b8334b4891d0b12cac59030ebf7fced871c5dd
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47773375"
---
# <a name="accessing-rows-in-a-hierarchical-recordset-example"></a>访问分层记录集 （示例） 中的行
下面的示例显示了的步骤所需访问的行以分层[记录集](../../../ado/reference/ado-api/recordset-object-ado.md):

1.  **记录集**中的对象**作者**并**titleauthor**表相关的作者 id。

2.  外部循环显示每个作者的名字和姓氏的名称、 状态和标识。

3.  在追加**记录集**从检索的每一行[字段](../../../ado/reference/ado-api/fields-collection-ado.md)集合并分配给*rstTitleAuthor*。

4.  内部循环显示四个字段从每个行中追加**记录集**。

 [StayInSync](../../../ado/reference/ado-api/stayinsync-property.md)属性设置为**false**为便于说明，以便您可以看到一章更改显式在外部循环的每次迭代中。 若要使效率更高的代码示例，可以移动分配在步骤 2 中的第一行前面的步骤 3 中，以便分配仅执行一次。 然后设置[StayInSync](../../../ado/reference/ado-api/stayinsync-property.md)属性设置为**true**，以便*rstTitleAuthor*将隐式和自动更改为相应的一章每当*rst*将移到新行。

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

## <a name="see-also"></a>请参阅
 [数据整理概述](../../../ado/guide/data/data-shaping-overview.md)[字段对象](../../../ado/reference/ado-api/field-object.md)[字段集合 (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md) [正式 Shape 语法](../../../ado/guide/data/formal-shape-grammar.md) [Microsoft 数据整理用于 OLE DB 服务（ADO 服务提供程序）](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md) [必需的提供程序数据整理](../../../ado/guide/data/required-providers-for-data-shaping.md)[形状 APPEND 子句](../../../ado/guide/data/shape-append-clause.md)[形状中的命令常规](../../../ado/guide/data/shape-commands-in-general.md) [Shape 计算子句](../../../ado/guide/data/shape-compute-clause.md) [Visual Basic for Applications 函数](../../../ado/guide/data/visual-basic-for-applications-functions.md)
