---
title: "对 HelloData 注释 |Microsoft 文档"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- hellodata sample application [ADO]
ms.assetid: a2831d77-7040-4b73-bbae-fe0bf78107ed
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0b84d5aef9958c15682c6aeae2942487f30a6581
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="comments-on-hellodata"></a>对 HelloData 的注释
HelloData 应用程序步骤通过一个典型的 ADO 应用程序的基本操作： 获取、 检查、 编辑和更新数据。 当启动应用程序时，单击第一个按钮，**获取数据**。 这将运行**GetData**子例程。  
  
## <a name="getdata"></a>GetData  
 **GetData**有效的连接字符串置于模块级变量， *m_sConnStr*。 有关连接字符串的详细信息，请参阅[创建连接字符串](../../../ado/guide/data/creating-a-connection-string.md)。  
  
 分配错误处理程序使用 Visual Basic **OnError**语句。 有关 ADO 中的错误处理的详细信息，请参阅[错误处理](../../../ado/guide/data/error-handling.md)。 一个新**连接**创建对象时，与**CursorLocation**属性设置为**adUseClient**因为 HelloData 示例创建*断开连接的记录集*。 这意味着，一旦从数据源提取数据，与数据源物理连接已断开，但你仍可以使用在本地缓存的数据你**记录集**对象。  
  
 打开连接后，将 SQL 字符串分配给一个变量 (sSQL)。 然后创建新的一个实例**记录集**对象， `m_oRecordset1`。 在下一行代码中，打开**记录集**通过现有**连接**，并传入`sSQL`作为源的**记录集**。 在进行 SQL 字符串你决定帮助 ADO 已通过作为源**记录集**是通过传递的命令的一个文本定义**adCmdText** 最后的参数中**记录集打开**方法。 此行也设置**LockType**和**游标类型**与关联**记录集**。  
  
 下的一行代码集**MarshalOptions**属性等于**adMarshalModifiedOnly**。 **MarshalOptions**指示哪些记录应封送到的中间层 （或 Web 服务器）。 关于封送处理的详细信息，请参阅 COM 文档。 当你使用**adMarshalModifiedOnly**与客户端游标 ([CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) = **adUseClient**)，只有在已修改的记录客户端写回到中间层。 设置**MarshalOptions**到**adMarshalModifiedOnly**可以提高性能，因为更少的行被封送处理。  
  
 接下来，断开连接**记录集**通过设置其**ActiveConnection**属性等于**执行任何操作**。 详细信息，请参阅"断开连接并重新连接记录集"一节中[更新和保持数据](../../../ado/guide/data/updating-and-persisting-data.md)。  
  
 关闭与数据源的连接和销毁现有**连接**对象。 此释放它所消耗的资源。  
  
 最后一步是设置**记录集**作为**数据源**Microsoft DataGrid 控件的窗体上因此，您可以轻松地显示来自数据**记录集**上窗体。  
  
 单击第二个按钮，**检查数据**。 这将在运行**ExamineData**子例程。  
  
## <a name="examinedata"></a>ExamineData  
 ExamineData 使用多个方法和属性的**记录集**对象显示中的数据有关的信息**记录集**。 它通过使用报告的记录数**RecordCount**属性。 它循环访问**记录集**并将的值打印**AbsolutePosition**窗体上的显示文本框中的属性。 循环的值中时，在还**书签**第三条记录的属性将被放入 variant 变量*vBookmark*，以供将来使用。  
  
 例程直接向后定位到使用以前存储的书签变量的第三个记录。 例程的调用**WalkFields**子例程，循环访问**字段**集合**记录集**并显示有关每项的详细信息**字段**集合中。  
  
 最后， **ExamineData**使用**筛选器**属性**记录集**到仅使用这些记录的屏幕**CategoryId**等于2。 应用此筛选器的结果会立即显示在窗体上显示网格。  
  
 有关详细信息中所示的功能**ExamineData**子例程，请参阅[检查数据](../../../ado/guide/data/examining-data.md)。  
  
 接下来，单击第三个按钮，**编辑数据**。 这将运行**EditData**子例程。  
  
## <a name="editdata"></a>EditData  
 在代码进入**EditData**子例程，**记录集**仍筛选**CategoryId**等于 2，以便只有这些符合筛选条件的项可见。 第一次循环访问**记录集**并提高中每个可见项的价格**记录集**10%的。 值**价格**字段更改通过设置**值**与新的有效金额相等该字段的属性。  
  
 请记住，**记录集**从数据源中断开。 中所做的更改**EditData**以及仅供本地缓存的数据副本。 有关详细信息，请参阅[编辑数据](../../../ado/guide/data/editing-data.md)。  
  
 所做的更改将不会对数据源进行直到单击第四个按钮，**更新数据**。 这将运行**UpdateData**子例程。  
  
## <a name="updatedata"></a>UpdateData  
 UpdateData 首先删除筛选器已应用到**记录集**。 代码中删除和重置`m_oRecordset1`作为**数据源**为 Microsoft 绑定 DataGrid 窗体上，以便未筛选**记录集**网格中的显示。  
  
 然后，代码检查以查看是否你可以在向后移动**记录集**使用**支持**方法替换**adMovePrevious**自变量。  
  
 例程移动到第一个记录使用**MoveFirst**方法，并显示该字段的原始值和当前值，通过使用**OriginalValue**和**值**属性的**字段**对象。 这些属性，请与一起**UnderlyingValue**属性 （此处未使用） 中讨论了[更新和保持数据](../../../ado/guide/data/updating-and-persisting-data.md)。  
  
 下一步、 新**连接**创建对象并将其用于重新建立与数据源的连接。 你重新连接**记录集**通过设置新的数据源到**连接**作为**ActiveConnection**为**记录集**。 若要将更新发送到服务器，该代码调用**UpdateBatch**上**记录集**。  
  
 如果批处理更新成功，模块级标志变量中， `m_flgPriceUpdated`，设置为 True。 这将提醒你更高版本清理对数据库所做的所有更改。  
  
 最后，代码移回第一条记录**记录集**并显示原始值和当前值。 值是相同的调用后**UpdateBatch**。  
  
 有关如何更新数据的详细信息，包括要执行的操作时数据时的服务器更改你**记录集**是断开连接，请参阅[更新和保持数据](../../../ado/guide/data/updating-and-persisting-data.md)。  
  
## <a name="formunload"></a>Form_Unload  
 **Form_Unload**子例程非常重要的原因。 首先，由于这是一个示例应用程序，Form_Unload 清理对应用程序退出之前数据库所做的更改。 其次的代码演示如何直接从打开执行命令**连接**对象使用**执行**方法。 最后，它演示执行不返回行 – 查询 （更新查询） 对数据源的一个示例。
