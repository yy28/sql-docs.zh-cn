---
title: "保留记录采用 XML 格式 |Microsoft 文档"
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
- persisting data [ADO]
- data updates [ADO], persisting data
- data persistence [ADO]
- XML persistence [ADO]
- updating data [ADO], persisting data
ms.assetid: f3113ec4-ae31-428f-89c6-bc1024f128ea
caps.latest.revision: "17"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 719d6d0575f90f3460de6e8b1285b6a59cf7f791
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="persisting-records-in-xml-format"></a>保留记录采用 XML 格式
ADTG 格式类似**记录集**以 XML 格式的持久性通过 Microsoft OLE DB 永久性提供程序实现。 此提供程序从已保存的 XML 文件或流，其中包含生成 ADO 的架构信息生成只进、 只读的行集。 同样，可能需要 ADO**记录集**、 生成 XML，并将其保存到文件或任何对象，该实现 COM 对象**IStream**接口。 (事实上，一个文件是支持的对象的另一个示例**IStream**。)对于版本 2.5 及更高版本，ADO 依赖上 Microsoft XML 分析器 (MSXML) 将 XML 加载到**记录集**; 因此 msxml.dll 是必需的。  
  
> [!NOTE]
>  保存层次结构时存在一些限制**记录集**（数据形状） 为 XML 格式。 如果不能保存到 XML 分层**记录集**包含挂起的更新，且不能保存参数化分层**记录集**。 有关详细信息，请参阅[保持筛选和分层记录集](../../../ado/guide/data/persisting-filtered-and-hierarchical-recordsets.md)。  
  
 最简单方法将数据保存到 XML 并重新加载它再次通过 ADO 是使用**保存**和**打开**方法，分别。 下面的 ADO 代码示例演示如何保存中的数据**标题**表添加到名为 titles.sav 的文件。  
  
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
  
 ADO 始终仍然存在整个**记录集**对象。 如果你想要保留的行的子集**记录集**对象，请使用**筛选器**方法可以缩小行或更改所选内容子句。 但是，你必须打开**记录集**与客户端游标的对象 (**CursorLocation** = **adUseClient**) 使用**筛选**方法保存的行的子集。 例如，若要检索以字母"b"开头的标题，你可以应用筛选器为打开**记录集**对象：  
  
```  
rs.Filter "title_id like 'B*'"  
rs.Save "btitles.sav", adPersistXML  
```  
  
 ADO 始终使用客户端游标引擎行集生成可滚动的 bookmarkable**记录集**永久性提供程序生成的只进数据上的对象。  
  
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
