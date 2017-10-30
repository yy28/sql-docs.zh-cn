---
title: "连接属性示例 (VBScript) |Microsoft 文档"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- Connect property [ADO], VBScript example
ms.assetid: 06297993-fe72-4446-aa76-3b8bc25444f6
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e3b1e74725758186cc29be811c80b6d405929dd5
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="connect-property-example-vbscript"></a>连接属性示例 (VBScript)
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性手册](https://www.microsoft.com/en-us/download/details.aspx?id=27416)有关详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 此代码演示如何设置[连接](../../../ado/reference/rds-api/connect-property-rds.md)在设计时属性：  
  
```  
<OBJECT CLASSID="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33" ID="ADC1">  
.  
   <PARAM NAME="SQL" VALUE="Select * from Sales">  
   <PARAM NAME="CONNECT" VALUE="Provider=SQLOLEDB;Integrated Security=SSPI;Initial Catalog=Pubs">  
   <PARAM NAME="Server" VALUE="http://MyWebServer">  
.  
</OBJECT>  
```  
  
 下面的示例演示如何设置**连接**属性在运行时中的 VBScript 代码。  
  
 若要测试此示例中，代码剪切并粘贴之间\<正文 > 和\</b o > 标记中普通的 HTML 文档，并将其命名**ConnectVBS.asp**。 ASP 脚本将标识你的服务器。  
  
```  
<!-- BeginConnectVBS -->  
<%@ Language=VBScript %>  
<HTML>  
<HEAD>  
<title>ADO Connect Property</title>  
  
    <%' local style sheet used for display%>  
<STYLE>  
<!--  
BODY {  
   font-family: 'Verdana','Arial','Helvetica',sans-serif;  
   BACKGROUND-COLOR:white;  
   COLOR:black;  
    }  
  
.tbody {   
   text-align: center;  
   background-color: #f7efde;  
   font-family: 'Verdana','Arial','Helvetica',sans-serif;   
   font-size: x-small;  
    }  
-->  
</STYLE>  
</HEAD>  
  
<BODY>  
<h1>ADO Connect Property (RDS)</h1>  
  
<HR>  
<H3>Set Connect Property at Run Time</H3>  
  
<% ' RDS.DataControl with no parameters set at design time %>  
<OBJECT classid="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33" ID=RDS HEIGHT=1 WIDTH=1></OBJECT>  
<% ' Bind table to control for data display  %>  
<TABLE DATASRC=#RDS>  
<TBODY>  
  <TR class="tbody">  
    <TD><SPAN DATAFLD="FirstName"></SPAN></TD>  
    <TD><SPAN DATAFLD="LastName"></SPAN></TD>  
  </TR>  
</TBODY>  
</TABLE>  
<FORM name="frmInput">  
    SERVER: <INPUT Name="txtServer" Size="103" Value="http://<%=Request.ServerVariables("SERVER_NAME")%>"><BR>  
    DATA SOURCE: <INPUT Name="txtDataSource" Size="93" Value="<%=Request.ServerVariables("SERVER_NAME")%>"><BR>  
    CONNECT: <INPUT Name="txtConnect" Size="100"><BR>  
    SQL: <INPUT Name="txtSQL" Size="110" Value="Select FirstName, LastName from Employees">  
    <BR>  
    <INPUT TYPE=BUTTON NAME="Run" VALUE="Run">  
    <h4>  
    To make data grid appear, click 'Run' to see the connect string in text box above.  
    </h4>   
</FORM>  
<Script Language="VBScript">  
  
    ' Set parameters of RDS.DataControl at Run Time  
    Sub Run_OnClick  
  
        Dim Cnxn  
            ' build connection string  
        Cnxn = "Provider='sqloledb';"  
        Cnxn = Cnxn & "Data Source="  
        Cnxn = Cnxn & document.frmInput.txtDataSource.value & ";"  
        Cnxn = Cnxn & "Initial Catalog='Northwind';"  
        Cnxn = Cnxn & "Integrated Security='SSPI';"  
            ' assign the value  
        document.frmInput.txtConnect.value = Cnxn  
        MsgBox "Here we go!"  
            ' set RDS properties  
        RDS.Server = document.frmInput.txtServer.value  
        RDS.SQL = document.frmInput.txtSQL.value  
        RDS.Connect = document.frmInput.txtConnect.value  
        RDS.Refresh  
  
    End Sub  
  
</Script>  
  
</BODY>  
</HTML>  
<!-- EndConnectVBS -->  
```  
  
## <a name="see-also"></a>另请参阅  
 [连接属性 (RDS)](../../../ado/reference/rds-api/connect-property-rds.md)






















