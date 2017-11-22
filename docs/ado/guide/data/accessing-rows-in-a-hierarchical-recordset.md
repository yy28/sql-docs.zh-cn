---
title: "访问在分层记录集中的行 |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- hierarchical Recordsets [ADO]
- data shaping [ADO], hierarchical Recordsets
ms.assetid: 25f1d2a1-6d5e-4457-aa07-5db5c75dee18
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 351650e6445c0d8f85751349d243bc8870fd8c2f
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="accessing-rows-in-a-hierarchical-recordset-example"></a>访问分层记录集 （示例） 中的行
下面的示例显示的步骤所必需的访问的行以分层[记录集](../../../ado/reference/ado-api/recordset-object-ado.md):

1.  **记录集**对象从**作者**和**示**表相关的作者 id。

2.  外部循环显示每个作者的名字和姓氏、 状态和标识。

3.  追加**记录集**每一行检索从[字段](../../../ado/reference/ado-api/fields-collection-ado.md)集合并分配给*rstTitleAuthor*。

4.  内部循环显示从每个行的四个字段中追加**记录集**。

 [StayInSync](../../../ado/reference/ado-api/stayinsync-property.md)属性设置为**false**对于演示目的，以便你可以看到章更改显式外部循环每次迭代中。 若要使更高效的代码示例，可以移动分配在步骤 2 中的第一行前面的步骤 3 中，以便分配仅执行一次。 然后设置[StayInSync](../../../ado/reference/ado-api/stayinsync-property.md)属性**true**，以便*rstTitleAuthor*将隐式和自动更改为相应章每当*rst*移动至一个新行。

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
 [数据定形概述](../../../ado/guide/data/data-shaping-overview.md)[字段对象](../../../ado/reference/ado-api/field-object.md)[字段集合 (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md) [正式形状语法](../../../ado/guide/data/formal-shape-grammar.md)[调整服务的 Microsoft 数据OLE DB （ADO 服务提供商）](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md) [必需的提供程序数据成型](../../../ado/guide/data/required-providers-for-data-shaping.md)[调整 APPEND 子句](../../../ado/guide/data/shape-append-clause.md) [形状的命令通常](../../../ado/guide/data/shape-commands-in-general.md)[形状计算子句](../../../ado/guide/data/shape-compute-clause.md) [Visual Basic 应用程序函数](../../../ado/guide/data/visual-basic-for-applications-functions.md)
