---
title: 对 HelloData 的注释 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- hellodata sample application [ADO]
ms.assetid: a2831d77-7040-4b73-bbae-fe0bf78107ed
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e3086eff0e4a774e7f63e7ff876a9675668d5912
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47707875"
---
# <a name="comments-on-hellodata"></a>对 HelloData 的注释
HelloData 应用程序将指导逐步典型的 ADO 应用程序的基本操作： 获取、 查看、 编辑和更新数据。 当你启动应用程序时，单击第一个按钮**获取数据**。 这将运行**GetData**子例程。  
  
## <a name="getdata"></a>GetData  
 **GetData**将有效的连接字符串放入的模块级变量， *m_sConnStr*。 有关连接字符串的详细信息，请参阅[创建的连接字符串](../../../ado/guide/data/creating-a-connection-string.md)。  
  
 分配错误处理程序使用的 Visual Basic **OnError**语句。 有关在 ADO 中的错误处理的详细信息，请参阅[的错误处理](../../../ado/guide/data/error-handling.md)。 一个新**连接**创建对象，并**CursorLocation**属性设置为**adUseClient**因为 HelloData 示例创建*未连接记录集*。 这意味着，只要已从数据源中提取的数据，与数据源物理连接已断开，但您仍可以使用中本地缓存数据在**记录集**对象。  
  
 打开连接后，将为 SQL 字符串分配给一个变量 (sSQL)。 然后，创建的新实例**记录集**对象， `m_oRecordset1`。 在下一行代码中，打开**记录集**通过现有**连接**，并传入`sSQL`作为源**记录集**。 使 SQL 字符串您决定帮助 ADO 作为源已通过**记录集**命令的文本定义是通过传递**adCmdText** 的最后一个参数中**记录集已打开**方法。 此外设置此行**LockType**并**CursorType**与关联**记录集**。  
  
 代码集的下一行**MarshalOptions**属性等于**adMarshalModifiedOnly**。 **MarshalOptions**指示哪些记录应封送处理到中间层 （或 Web 服务器）。 有关封送处理的详细信息，请参阅 COM 文档。 当你使用**adMarshalModifiedOnly**与客户端游标 ([CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) = **adUseClient**)，只有在已修改的记录客户端写回到在中间层。 设置**MarshalOptions**到**adMarshalModifiedOnly**可以提高性能，因为封送更少的行。  
  
 接下来，断开**记录集**通过设置其**ActiveConnection**属性等于**Nothing**。 详细信息，请参阅"断开连接并重新连接记录集"一节中[更新和保存数据](../../../ado/guide/data/updating-and-persisting-data.md)。  
  
 关闭到数据源的连接，然后销毁现有**连接**对象。 此释放它占用的资源。  
  
 最后一步是设置**记录集**作为**数据源**Microsoft 数据网格控件在窗体上因此，可以轻松地显示从数据**记录集**上窗体。  
  
 单击第二个按钮**检查数据**。 这将在运行**ExamineData**子例程。  
  
## <a name="examinedata"></a>ExamineData  
 ExamineData 使用各种方法和属性**记录集**对象来显示有关中的数据的信息**记录集**。 它通过使用报告的记录数**RecordCount**属性。 它循环访问**记录集**，并输出的值**AbsolutePosition**中窗体上显示文本框的属性。 此外在循环中的值，而**书签**第三条记录的属性放入 variant 变量*vBookmark*，以供将来使用。  
  
 例程直接导航回使用以前存储的书签变量的第三个记录。 例程的调用**WalkFields**子例程，它循环访问**字段**的集合**记录集**，并显示有关每个详细信息**字段**集合中。  
  
 最后， **ExamineData**使用**筛选器**属性**记录集**到仅使用这些记录的屏幕**CategoryId**等于2。 应用此筛选器的结果会立即出现在窗体上显示网格。  
  
 有关详细信息中所示的功能**ExamineData**子例程中，请参阅[检查数据](../../../ado/guide/data/examining-data.md)。  
  
 接下来，单击第三个按钮**编辑数据**。 这将运行**EditData**子例程。  
  
## <a name="editdata"></a>EditData  
 当代码进入**EditData**子例程，**记录集**仍上筛选**CategoryId**等于 2，以便只满足筛选条件的项可见。 它首先循环访问**记录集**，并增加中每个可见项的价格**记录集**10%。 值**价格**字段更改通过设置**值**针对新的有效金额等于该字段的属性。  
  
 请记住，**记录集**从数据源断开连接时。 中所做的更改**EditData**仅对数据的本地缓存副本。 有关详细信息，请参阅[编辑数据](../../../ado/guide/data/editing-data.md)。  
  
 所做的更改不会在数据源上单击第四个按钮，直到**更新数据**。 这将运行**UpdateData**子例程。  
  
## <a name="updatedata"></a>UpdateData  
 UpdateData 首先删除已应用到的筛选器**记录集**。 代码中删除和重置`m_oRecordset1`作为**数据源**为 Microsoft 绑定 DataGrid 窗体上，以便未筛选**记录集**出现在网格中。  
  
 该代码会检查以查看是否可以向后移动中**记录集**通过使用**支持**方法替换**adMovePrevious**参数。  
  
 移动到第一个记录使用的例程**MoveFirst**方法，并通过使用显示字段的原始值和当前值， **OriginalValue**并**值**属性**字段**对象。 这些属性一起使用**UnderlyingValue**属性 （此处未使用） 中讨论了[更新和保存数据](../../../ado/guide/data/updating-and-persisting-data.md)。  
  
 接下来，一个新**连接**创建对象并将其用于重新建立与数据源的连接。 重新建立**记录集**到通过设置新的数据源**连接**作为**ActiveConnection**有关**记录集**。 若要将更新发送到服务器，该代码调用**UpdateBatch**上**记录集**。  
  
 如果批处理更新成功，模块级别的标志变量`m_flgPriceUpdated`，设置为 True。 这将提醒您更高版本以进行清除所有对数据库所做的更改。  
  
 最后，代码将移回第一条记录**记录集**并显示原始值和当前值。 值是相同的调用后面**UpdateBatch**。  
  
 有关如何更新数据的详细信息，包括要执行的操作时数据时的服务器更改你**记录集**是断开连接，请参阅[更新和保存数据](../../../ado/guide/data/updating-and-persisting-data.md)。  
  
## <a name="formunload"></a>Form_Unload  
 **Form_Unload**子例程是重要的原因。 首先，由于这是一个示例应用程序，Form_Unload 清理对应用程序退出前对数据库所做的更改。 其次，该代码演示如何直接从一种开放执行命令**连接**通过使用对象**Execute**方法。 最后，它显示了执行针对数据源的不返回行 – 查询 （更新查询） 的示例。
