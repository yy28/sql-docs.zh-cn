---
title: "字段集合 |Microsoft 文档"
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
- Field object [ADO], fields collection
- Fields collection [ADO]
ms.assetid: 574cf36e-e5f5-403b-983c-749ef93c108f
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: ecfc7532761897cddf868dcb617c6eeb5f32bccb
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="the-fields-collection"></a>字段集合
**字段**集合是一个 ADO 的内部集合。 集合是一组有序可以作为一个单元引用的项。 有关 ADO 集合的详细信息，请参阅[ADO 对象模型](../../../ado/guide/data/ado-objects-and-collections.md)。  
  
 **字段**集合包含**字段**中对象的每个字段 （列）**记录集**。 如所有 ADO 集合，它具有**计数**和**项**属性，以及**追加**和**刷新**方法。 它还具有**正在执行**，**删除**，**重新同步**，和**更新**均不可用于其他 ADO 集合的方法。  
  
## <a name="examining-the-fields-collection"></a>检查字段集合  
 请考虑**字段**集合中的示例**记录集**在本部分中引入。 示例**记录集**派生自的 SQL 语句  
  
```  
SELECT ProductID, ProductName, UnitPrice FROM Products WHERE CategoryID = 7  
```  
  
 因此，你应该看到**的字段记录集**集合包含三个字段。  
  
```  
'BeginWalkFields  
    Dim objFields As ADODB.Fields  
    Dim intLoop As Integer  
  
    objRs.Open strSQL, strConnStr, adOpenForwardOnly, adLockReadOnly, adCmdText  
  
    Set objFields = objRs.Fields  
  
    For intLoop = 0 To (objFields.Count - 1)  
        Debug.Print objFields.Item(intLoop).Name  
    Next  
'EndWalkFields  
```  
  
 此代码只需确定数目**字段**中的对象**字段**集合使用**计数**属性，并循环访问集合，返回的值**名称**每个属性**字段**对象。 你可以使用多**字段**属性以获取有关字段的信息。 有关查询的详细信息**字段**，请参阅[字段 Object](../../../ado/guide/data/the-field-object.md)。  
  
## <a name="counting-columns"></a>计数列  
 如你所料，**计数**属性返回的实际数目**字段**中的对象**字段**集合。 由于集合的成员计数从零开始，你应始终将循环零成员开始和结束值为**计数**减 1 的属性。 如果你正在使用 Microsoft Visual Basic 并想要循环访问集合的成员，而不会检查**计数**属性，请使用**每个...下一步**命令。  
  
 如果**计数**属性为零，集合中有任何对象。  
  
## <a name="getting-to-the-field"></a>转到字段  
 与任何 ADO 集合一样，**项**属性是集合的默认属性。 它将返回单个**字段**由名称指定对象或传递给它的索引。 因此，以下语句是等效的示例**记录集**:  
  
```  
objField = objRecordset.Fields.Item("ProductID")  
objField = objRecordset.Fields("ProductID")  
objField = objRecordset.Fields.Item(0)  
objField = objRecordset.Fields(0)  
```  
  
 如果这些方法是等效的这是最佳？ 不一定。 使用索引来检索**字段**从集合速度快因为它将访问**字段**直接而无需执行字符串查找。 另一方面的顺序**字段**集合中必须已知的而且如果顺序更改，对引用**字段的**索引将必须出现的任何更改。 尽管稍微降低，使用的名称**字段**是更灵活，因为它不依赖顺序排列的**字段**集合中。  
  
## <a name="using-the-refresh-method"></a>使用刷新方法  
 与某些其他 ADO 集合，使用不同**刷新**方法**字段**集合具有明显的效果。 若要从基础数据库结构中检索更改，你必须使用**Requery**方法，或者如果**记录集**对象不支持书签， **MoveFirst**方法，这将导致再次执行针对该提供程序的命令。  
  
## <a name="adding-fields-to-a-recordset"></a>将字段添加到记录集  
 **追加**方法用于将字段添加到**记录集**。  
  
 你可以使用**追加**方法生成**记录集**以编程方式而无需打开与数据源的连接。 如果将发生运行时错误**追加**方法调用**字段**集合打开**记录集**或在**记录集**其中**ActiveConnection**设置属性。 可以将字段追加只能与**记录集**未处于打开状态，尚未连接到数据源。 但是，若要为此新追加指定的值**字段**、**记录集**必须首次打开。  
  
 开发人员通常需要一个位置来临时存储一些数据，或希望一些行为就好像它来自服务器以便在用户界面中的数据绑定可以参与的数据。 ADO (结合[Microsoft 游标服务用于 OLE DB](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md))，开发人员可以生成一个空**记录集**对象通过指定列信息并调用**打开**. 在下面的示例中，三个新字段追加到一个新**记录集**对象。 则**记录集**打开时，两个添加新记录，和**记录集**保存到文件。 (有关详细信息**记录集**持久性，请参阅[更新和保持数据](../../../ado/guide/data/updating-and-persisting-data.md)。)  
  
```  
'BeginFabricate  
    Dim objRs As ADODB.Recordset  
    Set objRs = New ADODB.Recordset  
  
    With objRs.Fields  
        .Append "StudentID", adChar, 11, adFldUpdatable  
        .Append "FullName", adVarChar, 50, adFldUpdatable  
        .Append "PhoneNmbr", adVarChar, 20, adFldUpdatable  
    End With  
  
    With objRs  
        .Open  
  
        .AddNew  
        .Fields(0) = "123-45-6789"  
        .Fields(1) = "John Doe"  
        .Fields(2) = "(425) 555-5555"  
        .Update  
  
        .AddNew  
        .Fields(0) = "123-45-6780"  
        .Fields(1) = "Jane Doe"  
        .Fields(2) = "(615) 555-1212"  
        .Update  
    End With  
  
    objRs.Save App.Path & "FabriTest.adtg", adPersistADTG  
  
    objRs.Close  
'EndFabricate  
```  
  
 使用情况**字段追加**方法不同之间**记录集**对象和**记录**对象。 有关详细信息**记录**对象，请参阅[记录和流](../../../ado/guide/data/records-and-streams.md)。  
  
## <a name="see-also"></a>另请参阅  
 [构造分层记录集](../../../ado/guide/data/fabricating-hierarchical-recordsets.md)
