---
title: 保留数据 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- persisting data [ADO]
- data updates [ADO], persisting data
- data persistence [ADO]
- updating data [ADO], persisting data
ms.assetid: 21c162ca-2845-4dd8-a49d-e715aba8c461
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 0f2d47229b7383c11740ca3d7a20ad8e420931a5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66700472"
---
# <a name="persisting-data"></a>保留数据
（例如，使用便携式计算机） 的可移植计算已经生成了可以在这两个连接和断开连接状态中运行的应用程序的需要。 ADO 现已支持这通过让开发人员能够保存客户端游标**记录集**到磁盘并重新加载它更高版本。  
  
 有几种方案可以在其中使用此类功能，其中包括：  
  
-   **传输：** 当在旅途中使应用程序，非常重要提供进行更改和添加新记录，然后可以重新连接到数据库中更高版本和已提交的功能。  
  
-   **如果很少更新查找：** 通常在应用程序，表将用作查找-例如，状态税务表。 它们不经常更新，并且是只读的。 而不是重新读取此数据从服务器每次启动应用程序时，应用程序可以只需将数据从加载本地持久化**记录集**。  
  
 在 ADO 中，保存和加载**记录集**，使用**Recordset.Save**并**Recordset.Open(,,,adCmdFile)** ADO 方法**记录集**对象。  
  
 可以使用**记录集保存**方法以持久保存在 ADO**记录集**到磁盘上的文件。 (您还可以保存**记录集**到 ADO **Stream**对象。 **Stream**对象将更高版本在指南中讨论。)更高版本，可以使用**开放**方法以重新打开**记录集**时已准备好使用它。 默认情况下，将保存 ADO**记录集**专用的 Microsoft 高级数据 TableGram (ADTG) 格式。 使用指定此二进制格式**adPersistADTG PersistFormatEnum**值。 或者，您可以选择保存你**记录集**作为 XML 而不使用带**adPersistXML**。 有关以 XML 形式保存记录集的详细信息，请参阅[以 XML 格式保留记录](../../../ado/guide/data/persisting-records-in-xml-format.md)。  
  
 语法**保存**方法如下所示：  
  
```  
  
recordset.  
Save  
Destination, PersistFormat  
  
```  
  
 首次保存**记录集**，也可不指定*目标*。 如果省略*目标*，将使用设置为的值的名称创建一个新的文件[源](../../../ado/reference/ado-api/source-property-ado-recordset.md)属性**记录集**。  
  
 省略*目标*当您随后调用**保存**后会发生第一次保存或运行时错误。 如果您随后调用**保存**有一个新*目标*，则**记录集**保存到新的目标。 但是，新的目标和原始目标会将打开。  
  
 **保存**不会关闭**记录集**或*目标*，因此可以继续使用**记录集**并保存所做的最新更改。 *目标*保持打开状态，直到**记录集**处于关闭状态，在这段时间的其他应用程序可以读取但不是写入*目标*。  
  
 出于安全性原因**保存**方法允许仅从由 Microsoft Internet Explorer 执行的脚本的低和自定义安全设置的使用。  
  
 如果**保存**方法时异步调用**记录集**提取、 执行，或更新操作正在进行，**保存**等待，直到异步操作完成。  
  
 保存记录开头的第一行**记录集**。 当**保存**方法完成后，当前行位置移动到的第一行**记录集**。  
  
 为获得最佳结果，设置[CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md)属性设置为**adUseClient**与**保存**。 如果您的提供程序不支持所有必要的功能，保存**记录集**对象时，游标服务将提供该功能。  
  
 当**记录集**与一起持久保留**CursorLocation**属性设置为**adUseServer**，为更新功能**记录集**限制。 通常情况下，仅限单个表中的更新、 插入和删除操作允许 （依赖于提供程序功能）。 [重新同步](../../../ado/reference/ado-api/resync-method.md)方法也是在此配置中不可用。  
  
 因为*目标*参数可接受任何对象支持 OLE DB **IStream**接口，您可以保存**记录集**直接对 ASP **响应**对象。  
  
 在以下示例中，**保存**并**打开**方法用于保存**记录集**和更高版本重新打开它：  
  
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
  
## <a name="remarks"></a>备注  
 本部分包含以下主题。  
  
-   [更多有关记录集暂留的信息](../../../ado/guide/data/more-about-recordset-persistence.md)  
  
-   [保留筛选记录集和分层记录集](../../../ado/guide/data/persisting-filtered-and-hierarchical-recordsets.md)  
  
-   [以 XML 格式保留记录](../../../ado/guide/data/persisting-records-in-xml-format.md)
