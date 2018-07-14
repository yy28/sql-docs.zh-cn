---
title: 在应用程序代码中使用 FOR XML 结果 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- FOR XML clause, application code usage
- XML [SQL Server], FOR XML clause
- ASP.NET [SQL Server]
- .NET Framework [SQL Server], FOR XML data
- ADO [SQL Server]
- XML data islands [SQL Server]
- data islands [SQL Server]
ms.assetid: 41ae67bd-ece9-49ea-8062-c8d658ab4154
caps.latest.revision: 23
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: a8cb0fb56cd1715331c5c3f0e09c4319e0b82335
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37254109"
---
# <a name="use-for-xml-results-in-application-code"></a>在应用程序代码中使用 FOR XML 结果
  通过在 SQL 查询中使用 FOR XML 子句，可以检索查询结果，甚至可以将其转换为 XML 数据。 当 FOR XML 查询结果可以在 XML 应用程序代码中使用时，您可以使用此功能执行以下操作：  
  
-   查询 SQL 表中 [XML 数据 (SQL Server)](xml-data-sql-server.md) 值的实例  
  
-   应用 [TYPE Directive in FOR XML Queries](type-directive-in-for-xml-queries.md) 以将包含文本或图像类型化数据的查询的结果返回为 XML  
  
 本主题介绍了说明这些方法的示例。  
  
## <a name="retrieving-for-xml-data-with-ado-and-xml-data-islands"></a>用 ADO 和 XML 数据岛检索 FOR XML 数据  
 ADO`Stream`对象或其他支持 COM 的对象`IStream`接口，如 Active Server Pages (ASP)`Request`和`Response`对象，可用于包含结果时你正在使用 FOR XML 查询。  
  
 例如，以下 ASP 代码显示了查询的结果`xml`数据类型列 Demographics 的 AdventureWorks 示例数据库的 Sales.Store 表中。 确切地说，该查询在 CustomerID 等于 3 的行中查找此列的实例值。  
  
```  
<!-- BeginRecordAndStreamVBS -->  
<%@ LANGUAGE = VBScript %>  
<!-- %  Option Explicit      % -->  
<!-- 'Request.ServerVariables("SERVER_NAME") & ";" & _ -->  
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
   sConn = "Provider=SQLOLEDB;Data Source=(local);" & _  
            "Initial Catalog=AdventureWorks;Integrated Security=SSPI;"  
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
   sQuery = "<ROOT xmlns:sql='urn:schemas-microsoft-com:xml-sql'><sql:query>SELECT Demographics from Sales.Store WHERE CustomerID = 3 FOR XML AUTO</sql:query></ROOT>"  
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
   Dim root  
   Set root = xmlDoc.documentElement.childNodes.Item(0).childNodes.Item(0).childNodes.Item(0)  
   For each child in root.childNodes  
      dim OutputXML  
      OutputXML = document.all("log").innerHTML  
      document.all("log").innerHTML = OutputXML & "<LI><B>" & child.nodeName &  ":</B>  " & child.Text  & "</LI>"  
   Next  
   MsgBox xmlDoc.xml  
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
  
 此示例 ASP 页包含使用 ADO 执行 FOR XML 查询并在 XML 数据岛 (MyDataIsle) 中返回 XML 结果的服务器端 VBScript。 然后，在浏览器中返回此 XML 数据岛以进行其他客户端处理。 其他客户端 VBScript 代码用于处理 XML 数据岛的内容。 先将这些内容显示为产生的 DHTML 的一部分并打开消息框来显示 XML 数据岛的预处理内容，再执行此过程。  
  
#### <a name="to-test-this-example"></a>测试此示例  
  
1.  验证是否安装了 IIS 以及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 AdventureWorks 示例数据库。  
  
     此示例需要安装 Internet Information Services (IIS) 5.0 版或更高版本并启用 ASP 支持。 此外，必须安装 AdventureWorks 示例数据库。  
  
2.  复制以前提供的代码示例，并将其粘贴到您使用的 XML 或文本编辑器中。 在 IIS 所使用的根目录中将文件另存为 RetrieveResults.asp。 此目录通常为 C:Inetpub\wwwroot。  
  
3.  使用以下 URL 在浏览器窗口中打开 ASP 页。 首先，将“MyServer”替换为“localhost”或安装了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 IIS 的服务器的实际名称。  
  
    ```  
    http://MyServer/RetrieveResults.asp  
    ```  
  
 您所看到的生成的 HTML 页结果与以下示例输出类似：  
  
##### <a name="server-side-processing"></a>服务器端处理  
 Page Generated @ 3/11/2006 3:36:02 PM  
  
 Connect String = Provider=SQLOLEDB;Data Source=MyServer;Initial Catalog=AdventureWorks;Integrated Security=SSPI；  
  
 ADO Version = 2.8  
  
 adoConn.State = 1  
  
 Query String = SELECT Demographics from Sales.Store WHERE CustomerID = 3 FOR XML AUTO  
  
 将 XML 推送到客户端进行处理  
  
##### <a name="client-side-processing-of-xml-document-mydataisle"></a>XML 文档 MyDataIsle 的客户端处理  
  
-   **AnnualSales：** 1500000  
  
-   **AnnualRevenue：** 150000  
  
-   **BankName：** Primary International  
  
-   **BusinessType：** OS  
  
-   **YearOpened：** 1974  
  
-   **Specialty：** Road  
  
-   **SquareFeet：** 38000  
  
-   **Brands：** 3  
  
-   **Internet：** DSL  
  
-   **NumberEmployees：** 40  
  
 然后，VBScript 消息框将显示以下由 FOR XML 查询结果返回的原始、未筛选的 XML 数据岛内容。  
  
```  
<ROOT xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <Sales.Store>  
    <Demographics>  
      <StoreSurvey xmlns="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/StoreSurvey">  
        <AnnualSales>1500000</AnnualSales>  
        <AnnualRevenue>150000</AnnualRevenue>  
        <BankName>Primary International</BankName>  
        <BusinessType>OS</BusinessType>  
        <YearOpened>1974</YearOpened>  
        <Specialty>Road</Specialty>  
        <SquareFeet>38000</SquareFeet>  
        <Brands>3</Brands>  
        <Internet>DSL</Internet>  
        <NumberEmployees>40</NumberEmployees>  
      </StoreSurvey>  
    </Demographics>  
  </Sales.Store>  
</ROOT>  
```  
  
## <a name="retrieving-for-xml-data-with-aspnet-and-the-net-framework"></a>用 ASP.NET 和 .NET Framework 检索 FOR XML 数据  
 与上一个示例一样，以下 ASP.NET 代码显示在 AdventureWorks 示例数据库的 Sales.Store 表中查询 `xml` 数据类型列 Demographics 的结果。 同样与上一个示例相似，该查询在 CustomerID 等于 3 的行中查找此列的实例值。  
  
 在此示例中，以下 Microsoft .NET Framework 托管 API 用于完成返回并呈现 FOR XML 查询结果：  
  
1.  `SqlConnection` 用于打开连接到 SQL Server，基于指定的连接字符串变量 strConn 的内容。  
  
2.  然后，将 `SqlDataAdapter` 用作数据适配器，它将使用 SQL 连接和指定的 SQL 查询字符串执行 FOR XML 查询。  
  
3.  执行查询后，`SqlDataAdapter.Fill`方法然后调用并传递的一个实例`DataSet,`MyDataSet，为了用 FOR XML 查询的输出填充数据集。  
  
4.  `DataSet.GetXml`然后调用方法来将查询结果作为可以在服务器生成 HTML 页面中显示的字符串返回。  
  
    ```  
    <%@ Page Language="VB" %>  
    <HTML>  
    <HEAD>  
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
    </HEAD>  
    <BODY>  
    <%  
    Dim s as String  
    s = "<H3>Server-side processing</H3>" & _  
        "Page Generated @ " & Now() & "<BR/>"  
  
    Dim SQL As String   
    SQL = "SELECT Demographics from Sales.Store WHERE CustomerID = 3 FOR XML AUTO"  
  
    Dim strConn As String   
    strConn = "Server=(local);Database=AdventureWorks;Integrated Security=SSPI;"  
  
    Dim MySqlConn As New System.Data.SqlClient.SqlConnection(strConn)  
    Dim MySqlAdapter As New System.Data.SqlClient.SqlDataAdapter(SQL,MySqlConn)  
    Dim MyDataSet As New System.Data.DataSet  
  
    MySqlConn.Open()  
    s = s & "<P>SqlConnection opened.</P>"   
  
    MySqlAdapter.Fill(MyDataSet)  
    s = s & "<P>" & MyDataSet.GetXml  & "</P>"  
  
    MySqlConn.Close()  
    s = s & "<P>SqlConnection closed.</P>"   
  
    Message.InnerHtml=s  
    %>  
    <SPAN id="Message" runat=server />  
    </BODY>  
    </HTML>  
    ```  
  
#### <a name="to-test-this-example"></a>测试此示例  
  
1.  验证是否安装了 IIS 以及 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的 AdventureWorks 示例数据库。  
  
     此示例需要安装 Internet Information Services (IIS) 5.0 版或更高版本并启用 ASP.NET 支持。 此外，必须安装 AdventureWorks 示例数据库。  
  
2.  复制以前提供的代码，并将其粘贴到您使用的 XML 或文本编辑器中。 在 IIS 所使用的根目录中将文件另存为 RetrieveResults.aspx。 此目录通常为 C:Inetpub\wwwroot。  
  
3.  使用以下 URL 在浏览器窗口中打开 ASP.NET 页。 首先，将“MyServer”替换为“localhost”或安装了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 IIS 的服务器的实际名称。  
  
    ```  
    http://MyServer/RetrieveResults.aspx  
    ```  
  
 您所看到的生成的 HTML 页结果与以下示例输出类似：  
  
##### <a name="server-side-processing"></a>服务器端处理  
  
```  
Page Generated @ 3/11/2006 3:36:02 PM  
  
SqlConnection opened.  
  
<Sales.Store><Demographics><StoreSurvey xmlns="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/StoreSurvey"><AnnualSales>1500000</AnnualSales><AnnualRevenue>150000</AnnualRevenue><BankName>Primary International</BankName><BusinessType>OS</BusinessType><YearOpened>1974</YearOpened><Specialty>Road</Specialty><SquareFeet>38000</SquareFeet><Brands>3</Brands><Internet>DSL</Internet><NumberEmployees>40</NumberEmployees></StoreSurvey></Demographics></Sales.Store>  
  
SqlConnection closed.  
```  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `xml`数据类型支持可以请求返回的 FOR XML 查询的结果将为`xml`数据类型，而不是作为字符串或图像类型的数据，通过指定[TYPE 指令](type-directive-in-for-xml-queries.md)。 在 FOR XML 查询中使用 TYPE 指令时，该指令将提供对 FOR XML 结果（与 [在应用程序中使用 XML 数据](use-xml-data-in-applications.md)中显示的结果类似）的编程访问权限。  
  
## <a name="see-also"></a>请参阅  
 [FOR XML (SQL Server)](for-xml-sql-server.md)  
  
  
