---
title: 到流中检索结果集 |Microsoft 文档
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- streams [ADO], retrieving query results
- query results into stream [ADO]
- retrieving results into stream [ADO]
ms.assetid: 996c1321-c926-4f57-8297-85c8c20de974
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 16d1518d2ddbe5accc6b55fdc0b778a6381e1a5f
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2018
---
# <a name="retrieving-resultsets-into-streams"></a>到流中检索结果集
而不是接收结果中的传统**记录集**对象，ADO 改为到流检索查询结果。 ADO**流**对象 (或其他支持 COM 的对象**IStream**接口，如 ASP**请求**和**响应**对象) 可以用于包含这些结果。 此功能的用途之一是检索 XML 格式的结果。 使用 SQL Server，例如，XML 可以返回结果在多个方面，例如使用 SQL SELECT 查询中使用 FOR XML 子句或使用 XPath 查询。  
  
 以流格式而不是在接收查询结果**记录集**，必须指定**adExecuteStream**常量从**ExecuteOptionEnum**的参数**执行**方法**命令**对象。 如果你的提供程序支持此功能，则将在执行时流中返回结果。 你可能需要指定之前执行的代码指定其他提供程序特定属性。 例如，对于 Microsoft OLE DB Provider for SQL Server，属性，如**输出流**中**属性**集合**命令**对象必须是指定。 有关特定于 SQL Server 的动态属性与此功能相关的详细信息，请参阅 SQL Server 联机丛书中的 XML-Related 属性。  
  
## <a name="for-xml-query-example"></a>有关 XML 查询示例  
 下面的示例是在 VBScript 中写入到 Northwind 数据库：  
  
```  
<!-- BeginRecordAndStreamVBS -->  
<%@ LANGUAGE = VBScript %>  
<%  Option Explicit      %>  
  
<HTML>  
<HEAD>  
<META NAME="GENERATOR" Content="Microsoft Developer Studio"/>  
<META HTTP-EQUIV="Content-Type" content="text/html"; charset="iso-8859-1">  
<TITLE>FOR XML Query Example</TITLE>  
  
<STYLE>  
   BODY  
   {  
      FONT-FAMILY: Tahoma;  
      FONT-SIZE: 8pt;  
      OVERFLOW: auto  
   }  
  
   H3  
   {  
      FONT-FAMILY: Tahoma;  
      FONT-SIZE: 8pt;  
      OVERFLOW: auto  
   }  
</STYLE>  
  
<!-- #include file="adovbs.inc" -->  
<%  
   Response.Write "<H3>Server-side processing</H3>"  
  
   Response.Write "Page Generated @ " & Now() & "<BR/>"  
  
   Dim adoConn  
   Set adoConn = Server.CreateObject("ADODB.Connection")  
  
   Dim sConn  
   sConn = "Provider=SQLOLEDB;Data Source=" & _  
      Request.ServerVariables("SERVER_NAME") & ";" & _  
      Initial Catalog=Northwind;Integrated Security=SSPI;"  
  
   Response.write "Connect String = " & sConn & "<BR/>"  
  
   adoConn.ConnectionString = sConn  
   adoConn.CursorLocation = adUseClient  
  
   adoConn.Open  
  
   Response.write "ADO Version = " & adoConn.Version & "<BR/>"  
   Response.write "adoConn.State = " & adoConn.State & "<BR/>"  
  
   Dim adoCmd  
   Set adoCmd = Server.CreateObject("ADODB.Command")  
   Set adoCmd.ActiveConnection = adoConn  
  
   Dim sQuery  
   sQuery = "<ROOT xmlns:sql='urn:schemas-microsoft-com:xml-sql'><sql:query>SELECT * FROM PRODUCTS WHERE ProductName='Gumbr Gummibrchen' FOR XML AUTO</sql:query></ROOT>"  
  
   Response.write "Query String = " & sQuery & "<BR/>"  
  
   Dim adoStreamQuery  
   Set adoStreamQuery = Server.CreateObject("ADODB.Stream")  
   adoStreamQuery.Open  
   adoStreamQuery.WriteText sQuery, adWriteChar  
   adoStreamQuery.Position = 0  
  
   adoCmd.CommandStream = adoStreamQuery  
   adoCmd.Dialect = "{5D531CB2-E6Ed-11D2-B252-00C04F681B71}"  
  
   Response.write "Pushing XML to client for processing "  & "<BR/>"  
  
   adoCmd.Properties("Output Stream") = Response  
   Response.write "<XML ID='MyDataIsle'>"  
   adoCmd.Execute , , 1024  
   Response.write "</XML>"  
  
%>  
  
<SCRIPT language="VBScript" For="window" Event="onload">  
   Dim xmlDoc  
   Set xmlDoc = MyDataIsle.XMLDocument  
   xmlDoc.resolveExternals=false  
   xmlDoc.async=false  
  
   If xmlDoc.parseError.Reason <> "" then  
      Msgbox "parseError.Reason = " & xmlDoc.parseError.Reason  
   End If  
  
   Dim root, child  
   Set root = xmlDoc.documentElement  
   For each child in root.childNodes  
      dim OutputXML  
      OutputXML = document.all("log").innerHTML  
      document.all("log").innerHTML = OutputXML & "<LI>" & child.getAttribute("ProductName") & "</LI>"  
   Next  
</SCRIPT>  
  
</HEAD>  
  
<BODY>  
  
   <H3>Client-side processing of XML Document MyDataIsle</H3>  
   <UL id=log>  
   </UL>  
  
</BODY>  
</HTML>  
<!-- EndRecordAndStreamVBS -->  
  
```  
  
 FOR XML 子句指示 SQL Server 以 XML 文档的形式返回数据。  
  
### <a name="for-xml-syntax"></a>XML 语法  
  
```  
FOR XML [RAW|AUTO|EXPLICIT]  
```  
  
 为 XML RAW 生成具有列作为属性的值的泛型行元素。 FOR XML AUTO 使用试探法来基于表的名称的元素名称与生成的分层树。 FOR XML EXPLICIT 关系的操作完全由元数据生成通用表。  
  
 FOR XML 中选择的 SQL 语句示例：  
  
```  
SELECT * FROM PRODUCTS ORDER BY PRODUCTNAME FOR XML AUTO  
```  
  
 可以在字符串中指定该命令，如前面所示，分配给**CommandText**，或在 XML 模板查询分配给的窗体中**CommandStream**。 有关 XML 模板查询的详细信息，请参阅[命令流](../../../ado/guide/data/command-streams.md)ADO 或使用 SQL Server 联机丛书中的命令输入流中。  
  
 作为 XML 模板查询，FOR XML 查询如下所示：  
  
```  
<sql:query> SELECT * FROM PRODUCTS ORDER BY PRODUCTNAME FOR XML AUTO </sql:query>  
```  
  
 此示例指定 ASP**响应**对象**输出流**属性：  
  
```  
adoCmd.Properties("Output Stream") = Response  
```  
  
 接下来，指定**adExecuteStream**参数**执行**。 此示例包装 XML 标记来创建 XML 数据岛中的流：  
  
```  
Response.write "<XML ID=MyDataIsle>"  
adoCmd.Execute , , adExecuteStream  
Response.write "</XML>"  
```  
  
### <a name="remarks"></a>注释  
 此时，XML 流向客户端浏览器，并已准备好显示。 这可通过使用客户端 VBScript 以将 XML 文档绑定到的 DOM 和循环通过每个子节点以创建 HTML 中的产品的列表实例。
