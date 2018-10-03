---
title: 为流检索结果集 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- streams [ADO], retrieving query results
- query results into stream [ADO]
- retrieving results into stream [ADO]
ms.assetid: 996c1321-c926-4f57-8297-85c8c20de974
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 45ba231b1523a74ac8b2c09f55e19c3dc287ef20
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47734955"
---
# <a name="retrieving-resultsets-into-streams"></a>检索流中的结果集
而不是接收结果中的传统**记录集**对象，ADO 改成流检索查询结果。 ADO **Stream**对象 (或其他支持 COM 的对象**IStream**接口，如 ASP**请求**并**响应**对象) 可用于包含这些结果。 此功能的一个用途是检索 XML 格式的结果。 借助 SQL Server，例如，XML 可以返回结果在多个方面，例如使用 SQL SELECT 查询使用 FOR XML 子句或使用 XPath 查询。  
  
 若要接收流格式而不是在查询结果**记录集**，必须指定**adExecuteStream**常量从**ExecuteOptionEnum**为的参数**Execute**方法**命令**对象。 如果您的提供程序支持此功能，将在流中执行时返回结果。 您可能需要指定其他特定于提供程序的属性之前执行的代码。 例如，对于 Microsoft OLE DB Provider for SQL Server，属性，如**输出 Stream**中**属性**的集合**命令**对象必须是指定。 与此功能相关的特定于 SQL Server 的动态属性的详细信息，请参阅 SQL Server 联机丛书中的 XML-Related 属性。  
  
## <a name="for-xml-query-example"></a>FOR XML 查询示例  
 下面的示例是用 VBScript 编写到 Northwind 数据库：  
  
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
  
### <a name="for-xml-syntax"></a>有关 XML 语法  
  
```  
FOR XML [RAW|AUTO|EXPLICIT]  
```  
  
 有关 XML RAW 生成具有列的值作为属性的泛型行元素。 FOR XML AUTO 使用试探法来生成层次结构树有基于表的名称的元素名称。 FOR XML EXPLICIT 通用表生成的具有生成完整描述了由元数据的关系。  
  
 FOR XML 中选择的 SQL 语句示例如下：  
  
```  
SELECT * FROM PRODUCTS ORDER BY PRODUCTNAME FOR XML AUTO  
```  
  
 可以在字符串中指定命令，如前面所示，分配给**CommandText**，或在 XML 模板查询分配给的窗体**CommandStream**。 有关 XML 模板查询的详细信息，请参阅[命令流](../../../ado/guide/data/command-streams.md)ADO 或使用 SQL Server 联机丛书中的命令输入流中。  
  
 作为 XML 模板查询，FOR XML 查询如下所示：  
  
```  
<sql:query> SELECT * FROM PRODUCTS ORDER BY PRODUCTNAME FOR XML AUTO </sql:query>  
```  
  
 此示例指定 ASP**响应**对象**输出 Stream**属性：  
  
```  
adoCmd.Properties("Output Stream") = Response  
```  
  
 接下来，指定**adExecuteStream**的参数**Execute**。 此示例包装在 XML 标记，以便创建 XML 数据岛中的流：  
  
```  
Response.write "<XML ID=MyDataIsle>"  
adoCmd.Execute , , adExecuteStream  
Response.write "</XML>"  
```  
  
### <a name="remarks"></a>备注  
 此时，XML 已传输到客户端浏览器，它已准备好显示。 这是通过使用客户端 VBScript 将 XML 文档绑定到的 DOM 和循环通过每个子节点，来生成 HTML 中的产品的列表实例。
