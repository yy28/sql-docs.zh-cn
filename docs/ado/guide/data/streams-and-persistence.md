---
title: 流和暂留 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- persisted streams [ADO]
- streams [ADO], persistence
ms.assetid: ad5bf52c-fd10-4cfa-bf7d-fcedcaa41eea
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a2db82bb76ab58782682a612983bca3d7c4fccfe
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47701725"
---
# <a name="streams-and-persistence"></a>流和暂留
[记录集](../../../ado/reference/ado-api/recordset-object-ado.md)对象[保存](../../../ado/reference/ado-api/save-method.md)方法存储，或*仍然存在*即**记录集**在文件中，和[打开](../../../ado/reference/ado-api/open-method-ado-recordset.md)方法还原**记录集**从该文件。  
  
 使用 ADO 2.7 或更高版本，**保存**并**打开**方法，可以在保持**记录集**到[Stream](../../../ado/reference/ado-api/stream-object-ado.md)对象。 使用远程数据服务 (RDS) 和 Active Server Pages (ASP) 时，此功能是特别有用。  
  
 有关如何暂留可由本身在 ASP 页上的详细信息，请参阅当前的 ASP 文档。  
  
 以下是几个方案，展示了如何**Stream**可以使用对象和持久性。  
  
## <a name="scenario-1"></a>方案 1  
 这种情况下，只需将保存**记录集**到一个文件，再到**Stream**。 接着，它会持久的流到另一**记录集**。  
  
```  
Dim rs1 As ADODB.Recordset  
Dim rs2 As ADODB.Recordset  
Dim stm As ADODB.Stream  
  
Set rs1 = New ADODB.Recordset  
Set rs2 = New ADODB.Recordset  
Set stm = New ADODB.Stream  
  
rs1.Open   "SELECT * FROM Customers", "Provider=sqloledb;" & _  
        "Data Source=MyServer;Initial Catalog=Northwind;" & _  
        "Integrated Security=SSPI;""", adopenStatic, adLockReadOnly, adCmdText  
rs1.Save "c:\myfolder\mysubfolder\myrs.xml", adPersistXML  
rs1.Save stm, adPersistXML  
rs2.Open stm  
```  
  
## <a name="scenario-2"></a>方案 2  
 这种情况下仍然存在**记录集**成**Stream**以 XML 格式。 然后，它读取**Stream**到可以检查、 操作或显示的字符串。  
  
```  
Dim rs As ADODB.Recordset  
Dim stm As ADODB.Stream  
Dim strRst As String  
  
Set rs = New ADODB.Recordset  
Set stm = New ADODB.Stream  
  
' Open, save, and close the recordset.   
rs.Open "SELECT * FROM Customers", "Provider=sqloledb;" & _  
        "Data Source=MyServer;Initial Catalog=Northwind;" & _  
        "Integrated Security=SSPI;"""  
rs.Save stm, adPersistXML  
rs.Close  
Set rs = nothing  
  
' Put saved Recordset into a string variable.  
strRst = stm.ReadText(adReadAll)  
  
' Examine, manipulate, or display the XML data.  
...  
```  
  
## <a name="scenario-3"></a>方案 3  
 此示例代码演示了 ASP 代码保持**记录集**作为 XML 直接与**响应**对象：  
  
```  
...  
<%  
response.ContentType = "text/xml"  
  
' Create and open a Recordset.  
Set rs = Server.CreateObject("ADODB.Recordset")  
rs.Open "select * from Customers", "Provider=sqloledb;" & _  
        "Data Source=MyServer;Initial Catalog=Northwind;" & _  
        "Integrated Security=SSPI;"""  
  
' Save Recordset directly into output stream.  
rs.Save Response, adPersistXML   
  
' Close Recordset.  
rs.Close  
Set rs = nothing  
%>  
...  
```  
  
## <a name="scenario-4"></a>方案 4  
 在此方案中，ASP 代码将写入的内容**记录集**ADTG 格式到客户端。 [用于 OLE DB 的 Microsoft 游标服务](../../../ado/guide/appendixes/microsoft-cursor-service-for-ole-db-ado-service-component.md)可以使用此数据来创建已断开连接**记录集**。  
  
 RDS 上的新属性[DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)， [URL](../../../ado/reference/rds-api/url-property-rds.md)，指向生成的相应的.asp 页**记录集**。 这意味着**记录集**可以获取对象没有 RDS 的情况下使用服务器端[DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)对象或用户编写的业务对象。 这大大简化了 RDS 编程模型。  
  
 服务器端代码中，名为 http://server/directory/recordset.asp:  
  
```  
<%  
Dim rs   
Set rs = Server.CreateObject("ADODB.Recordset")  
rs.Open "select au_fname, au_lname, phone from Authors", ""& _  
        "Provider=sqloledb;Data Source=MyServer;" & _  
        "Initial Catalog=Pubs;Integrated Security=SSPI;"  
response.ContentType = "multipart/mixed"  
rs.Save response, adPersistADTG  
%>  
```  
  
 客户端的代码：  
  
```  
<HTML>  
<HEAD>  
<TITLE>RDS Query Page</TITLE>  
</HEAD>  
<body>  
<CENTER>  
<H1>Remote Data Service 2.5</H1>  
<TABLE DATASRC="#DC1">  
   <TR>   
      <TD><SPAN DATAFLD="au_fname"></SPAN></TD>  
      <TD><SPAN DATAFLD="au_lname"></SPAN></TD>  
      <TD><SPAN DATAFLD="phone"></SPAN></TD>  
   </TR>  
</TABLE>  
<BR>  
  
<OBJECT classid="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33"  
    ID=DC1 HEIGHT=1 WIDTH = 1>  
    <PARAM NAME="URL" VALUE="http://server/directory/recordset.asp">  
</OBJECT>  
  
</SCRIPT>  
</BODY>  
</HTML>  
```  
  
 开发人员也可以选择使用**记录集**客户端上的对象：  
  
```  
...  
function GetRs()   
    {  
    rs = CreateObject("ADODB.Recordset");  
    rs.Open "http://server/directory/recordset.asp"  
    DC1.SourceRecordset = rs;  
    }  
...  
```  
  
## <a name="see-also"></a>请参阅  
 [Open 方法 （ADO 记录集）](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [记录对象 (ADO)](../../../ado/reference/ado-api/record-object-ado.md)   
 [Save 方法](../../../ado/reference/ado-api/save-method.md)
