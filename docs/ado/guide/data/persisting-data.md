---
title: "保存数据 |Microsoft 文档"
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
helpviewer_keywords:
- persisting data [ADO]
- data updates [ADO], persisting data
- data persistence [ADO]
- updating data [ADO], persisting data
ms.assetid: 21c162ca-2845-4dd8-a49d-e715aba8c461
caps.latest.revision: "13"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ddcd99ce0c8b59cff252f2e1aa5cf97696298cc5
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="persisting-data"></a>保存数据
（例如，使用便携式计算机） 的可移植计算已生成可以在连接和断开连接状态中运行的应用程序的需求。 ADO 通过让能够保存客户端游标的开发人员添加了对此支持**记录集**到磁盘，然后重新加载它更高版本。  
  
 有几种方案，你无法在其中使用此类型的功能，包括以下：  
  
-   **旅行：**时旅途采用应用程序，则必须提供能够更改和添加新的记录，然后可以重新连接到数据库中更高版本并提交。  
  
-   **不经常更新查找：**通常在应用程序，表用作查找 — 例如，状态税务表。 它们不经常更新，并且是只读的。 而不是需要重新读取此数据从服务器每次启动应用程序时，应用程序可以只需将数据加载从本地持久化**记录集**。  
  
 在 ADO 中，保存和加载**记录集**，使用**Recordset.Save**和**Recordset.Open(,,,adCmdFile)**方法 ADO**记录集**对象。  
  
 你可以使用**记录集保存**方法以保留你 ADO**记录集**到磁盘上的文件。 (你还可以保存**记录集**到 ADO**流**对象。 **流式传输**对象将更高版本在指南中讨论。)稍后，你可以使用**打开**方法重新打开**记录集**当你准备好要使用它。 默认情况下，ADO 将保存**记录集**为专有的 Microsoft 高级数据表图 (ADTG) 格式。 使用指定此二进制格式**adPersistADTG PersistFormatEnum**值。 或者，你可以选择保存你**记录集**为 XML，而不使用扩展**xml 格式持久化记录**。 有关记录集保存为 XML 的详细信息，请参阅[保留的记录，采用 XML 格式](../../../ado/guide/data/persisting-records-in-xml-format.md)。  
  
 语法**保存**方法是，如下所示：  
  
```  
  
recordset.  
Save  
Destination, PersistFormat  
  
```  
  
 第一次保存**记录集**，它是可选若要指定*目标*。 如果省略*目标*，将使用设置为的值的名称创建一个新文件[源](../../../ado/reference/ado-api/source-property-ado-recordset.md)属性**记录集**。  
  
 省略*目标*当你随后调用**保存**后将会出现第一次保存或运行时错误。 如果您随后调用**保存**用新*目标*、**记录集**保存到新的目标位置。 但是，新的目标和原始目标将将打开。  
  
 **保存**不会关闭**记录集**或*目标*，因此可以继续使用**记录集**并保存最新更改。 *目标*保持打开状态，除非**记录集**已关闭，在这段时间的其他应用程序可以读取但不是向写入*目标*。  
  
 出于安全，**保存**方法允许仅从由 Microsoft Internet Explorer 中执行的脚本的低和自定义安全设置的使用。  
  
 如果**保存**时异步调用方法**记录集**提取、 执行，或更新操作正在进行，**保存**等待，直到在异步操作完成。  
  
 记录保存开头的第一行**记录集**。 当**保存**方法运行完毕后，当前行位置移动到的第一行**记录集**。  
  
 为获得最佳结果，设置[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)属性**adUseClient**与**保存**。 如果你的提供程序不支持所有必要的功能，保存**记录集**对象，则游标服务将提供该功能。  
  
 当**记录集**一起持久化**CursorLocation**属性设置为**adUseServer**，使用的更新功能**记录集**限制。 通常情况下，仅单表更新、 插入和删除允许 （依赖于提供程序功能）。 [重新同步](../../../ado/reference/ado-api/resync-method.md)方法也将在此配置中不可用。  
  
 因为*目标*参数可接受任何对象支持 OLE DB **IStream**接口，可以保存**记录集**直接对 ASP **响应**对象。  
  
 在下面的示例中，**保存**和**打开**方法用于保存**记录集**和以后重新打开它：  
  
```  
'BeginPersist  
   conn.ConnectionString = _  
   "Provider=SQLOLEDB;Data Source=MySQLServer;" _  
      & "Integrated Security=SSPI;Initial Catalog=pubs"  
   conn.Open  
  
   conn.Execute "create table testtable (dbkey int " & _  
      "primary key, field1 char(10))"  
   conn.Execute "insert into testtable values (1, 'string1')"  
  
   Set rst.ActiveConnection = conn  
   rst.CursorLocation = adUseClient  
  
   rst.Open "select * from testtable", conn, adOpenStatic, _  
      adLockBatchOptimistic  
  
   'Change the row on the client  
   rst!field1 = "NewValue"  
  
   'Save to a file--the .dat extension is an example; choose  
   'your own extension. The changes will be saved in the file  
   'as well as the original data.  
   MyFile = Dir("c:\temp\temptbl.dat")  
   If MyFile <> "" Then  
       Kill "c:\temp\temptbl.dat"  
   End If  
  
   rst.Save "c:\temp\temptbl.dat", adPersistADTG  
   Set rst = Nothing  
  
   'Now reload the data from the file  
   Set rst = New ADODB.Recordset  
   rst.Open "c:\temp\temptbl.dat", , adOpenStatic, _  
      adLockBatchOptimistic, adCmdFile  
  
   Debug.Print "After Loading the file from disk"  
   Debug.Print "   Current Edited Value: " & rst!field1.Value  
   Debug.Print "   Value Before Editing: " & rst!field1.OriginalValue  
  
   'Note that you can reconnect to a connection and  
   'submit the changes to the data source  
   Set rst.ActiveConnection = conn  
   rst.UpdateBatch  
'EndPersist  
```  
  
## <a name="remarks"></a>Remarks  
 本部分包含以下主题。  
  
-   [更多有关记录集暂留的信息](../../../ado/guide/data/more-about-recordset-persistence.md)  
  
-   [保留筛选记录集和分层记录集](../../../ado/guide/data/persisting-filtered-and-hierarchical-recordsets.md)  
  
-   [以 XML 格式保留记录](../../../ado/guide/data/persisting-records-in-xml-format.md)
