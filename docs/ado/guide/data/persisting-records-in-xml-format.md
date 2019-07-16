---
title: 以 XML 格式保留记录 |Microsoft Docs
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
- XML persistence [ADO]
- updating data [ADO], persisting data
ms.assetid: f3113ec4-ae31-428f-89c6-bc1024f128ea
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 263f83093c46f4265559fe0b1844112687d4fc67
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924596"
---
# <a name="persisting-records-in-xml-format"></a>以 XML 格式保留记录
ADTG 格式类似**记录集**暂留以 XML 格式使用 Microsoft OLE DB 永久性提供程序实现。 此提供程序从已保存的 XML 文件或流，其中包含生成的 ADO 的架构信息生成只进、 只读的行集。 同样，可能需要 ADO**记录集**，生成的 XML，并将其保存到文件或任何对象，该实现 COM 对象**IStream**接口。 (事实上，一个文件是支持的对象只是另一个示例**IStream**。)对于版本 2.5 及更高版本，ADO 依赖于在 Microsoft XML 分析器 (MSXML) 若要将 XML 加载到**记录集**; 因此 msxml.dll 是必需的。  
  
> [!NOTE]
>  保存层次结构时，将应用一些限制**记录集**（数据形状） 为 XML 格式。 如果不能保存到 XML 层次结构**记录集**包含挂起的更新，且不能保存参数化分层**记录集**。 有关详细信息，请参阅[持久保存筛选和分层记录集](../../../ado/guide/data/persisting-filtered-and-hierarchical-recordsets.md)。  
  
 若要将数据保存到 XML 并将其重新加载的最简单方法同样通过 ADO 是与**保存**并**打开**方法，分别。 下面的 ADO 代码示例演示如何保存中的数据**标题**到名为 titles.sav 文件表。  
  
```  
Dim rs as new Recordset  
Dim rs2 as new Recordset  
Dim c as new Connection  
Dim s as new Stream  
  
' Query the Titles table.  
c.Open "provider=sqloledb;data source=MySQLServer;initial catalog=pubs;Integrated Security='SSPI'"  
rs.cursorlocation = adUseClient  
rs.Open "select * from titles", c, adOpenStatic  
  
' Save to the file in the XML format. Note that if you don't specify   
' adPersistXML, a binary format (ADTG) will be used by default.  
rs.Save "titles.sav", adPersistXML  
  
' Save the recordset into the ADO Stream object.  
rs.save s, adPersistXML  
rs.Close  
c.Close  
  
set rs = nothing  
  
' Reopen the file.  
rs.Open "titles.sav",,,,adCmdFile  
' Open the Stream back into a Recordset.  
rs2.open s  
```  
  
 ADO 始终仍然存在整个**记录集**对象。 如果你想要保留的行的子集**记录集**对象，请使用**筛选器**方法，以缩小行或更改你的选择子句。 但是，你必须打开**记录集**与客户端游标的对象 (**CursorLocation** = **adUseClient**) 使用**筛选**用于保存行的子集的方法。 例如，若要检索以字母"b"开头的标题，您可以应用筛选器打开到**记录集**对象：  
  
```  
rs.Filter "title_id like 'B*'"  
rs.Save "btitles.sav", adPersistXML  
```  
  
 ADO 始终使用客户端游标引擎行集来生成可滚动，可存为书签**记录集**基于只进数据暂留提供程序生成的对象。  
  
 本部分包含以下主题。  
  
-   [XML 暂留格式](../../../ado/guide/data/xml-persistence-format.md)  
  
-   [命名空间](../../../ado/guide/data/namespaces.md)  
  
-   [架构部分](../../../ado/guide/data/schema-section.md)  
  
-   [数据部分](../../../ado/guide/data/data-section.md)  
  
-   [XML 中的分层记录集](../../../ado/guide/data/hierarchical-recordsets-in-xml.md)  
  
-   [XML 中的记录集动态属性](../../../ado/guide/data/recordset-dynamic-properties-in-xml.md)  
  
-   [XSLT 转换](../../../ado/guide/data/xslt-transformations.md)  
  
-   [保存到 XML DOM 对象](../../../ado/guide/data/saving-to-the-xml-dom-object.md)  
  
-   [XML 安全注意事项](../../../ado/guide/data/xml-security-considerations.md)  
  
-   [XML 记录集暂留方案](../../../ado/guide/data/xml-recordset-persistence-scenario.md)
