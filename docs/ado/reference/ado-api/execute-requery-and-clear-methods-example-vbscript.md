---
title: 执行、再次查询和清除方法示例（VBScript） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- Execute method [ADO], VBScript example
- Clear method [ADO], VBScript example
- Requery method [ADO], VBScript example
ms.assetid: 3a7bbf07-2fca-4892-95f4-eec93f2d5e91
author: rothja
ms.author: jroth
ms.openlocfilehash: a0785e3e91c6d01f446e1d49b34a41beef052c48
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2020
ms.locfileid: "82760153"
---
# <a name="execute-requery-and-clear-methods-example-vbscript"></a>执行、再次查询和清除方法示例（VBScript）
此示例演示从[命令](../../../ado/reference/ado-api/command-object-ado.md)对象和[连接](../../../ado/reference/ado-api/connection-object-ado.md)对象运行时的**Execute**方法。 它还使用[Requery](../../../ado/reference/ado-api/requery-method.md)方法检索[记录集中](../../../ado/reference/ado-api/recordset-object-ado.md)的当前数据，并使用[clear](../../../ado/reference/ado-api/clear-method-ado.md)方法清除[错误](../../../ado/reference/ado-api/errors-collection-ado.md)集合的内容。 要运行此过程，需要 ExecuteCommand 和 PrintOutput 过程。  
  
 在 Active Server Page （ASP）中使用以下示例。 若要查看此完全正常运行的示例，您必须具有位于 C:\Program Files\Microsoft 平台 SDK\Samples\DataAccess\Rds\RDSTest\advworks.mdb 的数据源 Advworks-srv01 （随 SDK 示例一起安装），或者编辑示例代码中的路径以反映此文件的实际位置。 这是一个 Microsoft Access 数据库文件。  
  
 使用 "**查找**" 找到文件 Adovbs，并将其放入计划使用的目录中。 将以下代码剪切并粘贴到记事本或其他文本编辑器中，并将其保存为**ExecuteVBS**。 您可以在任何客户端浏览器中查看结果。  
  
```  
<!-- BeginExecuteVBS -->  
<%@ Language=VBScript %>  
<% ' use this meta tag instead of ADOVBS.inc%>  
<!-- METADATA TYPE="typelib" uuid="00000205-0000-0010-8000-00AA006D2EA4"  -->  
<HTML>  
<HEAD>  
<META name="VI60_DefaultClientScript"  content=VBScript>  
<META NAME="GENERATOR" Content="Microsoft Visual Studio 6.0">  
<title>ADO Execute Method</title>  
<STYLE>  
<!--  
BODY {  
   font-family: 'Verdana','Arial','Helvetica',sans-serif;  
   BACKGROUND-COLOR:white;  
   COLOR:black;  
    }  
.thead {  
   background-color: #008080;   
   font-family: 'Verdana','Arial','Helvetica',sans-serif;   
   font-size: x-small;  
   color: white;  
   }  
.thead2 {  
   background-color: #800000;   
   font-family: 'Verdana','Arial','Helvetica',sans-serif;   
   font-size: x-small;  
   color: white;  
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
<H3>ADO Execute Method</H3>  
<HR>  
<H4>Recordset Retrieved Using Connection Object</H4>  
<!--- Recordsets retrieved using Execute method of Connection and Command Objects-->  
<%   
     ' connection, command and recordset variables  
    Dim Cnxn, strCnxn  
    Dim rsCustomers, strSQLCustomers  
    Dim Cmd   
    Dim rsProducts, strSQLProducts  
  
    ' create and open connection  
    Set Cnxn = Server.CreateObject("ADODB.Connection")   
    strCnxn="Provider='sqloledb';Data Source=" & _  
            Request.ServerVariables("SERVER_NAME") & ";" & _  
            "Integrated Security='SSPI';Initial Catalog='Northwind';"  
    Cnxn.Open  strCnxn  
    ' create and open recordset  
    Set rsCustomers = Server.CreateObject("ADODB.Recordset")  
    strSQLCustomers = "Customers"  
    rsCustomers.Open strSQLCustomers, Cnxn, adOpenKeyset, adLockOptimistic, adCmdTable  
  
    '1st Recordset using Connection - Execute  
    Set rsCustomers = Cnxn.Execute(strSQLCustomers)   
  
    Set Cmd = Server.CreateObject("ADODB.Command")  
    Cmd.ActiveConnection = Cnxn  
    strSQLProducts = "SELECT * From Products"  
    Cmd.CommandText = strSQLProducts  
  
    '2nd Recordset Cmd - execute   
    Set rsProducts = Cmd.Execute  
    %>  
    <TABLE COLSPAN=8 CELLPADDING=5 BORDER=0 ALIGN=CENTER>  
    <!-- BEGIN column header row for Customer Table-->  
    <TR CLASS=thead>  
      <TH>Company Name</TH>  
      <TH>Contact Name</TH>  
      <TH>City</TH>  
    </TR>  
  
    <!--Display ADO Data from Customer Table-->  
    <%   
    Do While Not rsCustomers.EOF %>  
      <TR CLASS=tbody>  
        <TD>   
        <%= rsCustomers("CompanyName")%>   
        </TD>  
        <TD>  
        <%= rsCustomers("ContactName") %>   
        </TD>  
        <TD>   
        <%= rsCustomers("City")%>   
        </TD>  
      </TR>   
      <%   
    rsCustomers.MoveNext   
    Loop   
    %>  
</TABLE>  
  
<HR>  
<H4>Recordset Retrieved Using Command Object</H4>  
  
<TABLE CELLPADDING=5 BORDER=0 ALIGN=CENTER WIDTH="80%">  
  
<!-- BEGIN column header row for Product List Table-->  
<TR CLASS=thead2>  
  <TH>Product Name</TH>  
  <TH>Unit Price</TH>  
</TR>  
  
<!-- Display ADO Data Product List-->  
<% Do Until rsProducts.EOF %>  
  <TR CLASS=tbody>  
    <TD>  
    <%= rsProducts("ProductName")%>    
    </TD>  
    <TD>   
    <%= rsProducts("UnitPrice")%>   
    </TD>  
<%   
    rsProducts.MoveNext   
    Loop  
  
    ' clean up  
    If rsCustomers.State = adStateOpen then  
        rsCustomers.Close  
    End If  
    If rsProducts.State = adStateOpen then  
        rsProducts.Close  
    End If  
    If Cnxn.State = adStateOpen then  
        Cnxn.Close  
    End If  
    Set Cmd = Nothing  
    Set rsCustomers = Nothing  
    Set rsProducts = Nothing  
    Set Cnxn = Nothing  
%>  
</TABLE>  
  
</BODY>  
</HTML>  
<!-- EndExecuteVBS -->  
```  
  
## <a name="see-also"></a>另请参阅  
 [Clear 方法（ADO）](../../../ado/reference/ado-api/clear-method-ado.md)   
 [Command 对象（ADO）](../../../ado/reference/ado-api/command-object-ado.md)   
 [Connection 对象（ADO）](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Error 对象](../../../ado/reference/ado-api/error-object.md)   
 [Errors 集合（ADO）](../../../ado/reference/ado-api/errors-collection-ado.md)   
 [Execute 方法（ADO 命令）](../../../ado/reference/ado-api/execute-method-ado-command.md)   
 [Execute 方法（ADO 连接）](../../../ado/reference/ado-api/execute-method-ado-connection.md)   
 [Recordset 对象（ADO）](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Requery 方法](../../../ado/reference/ado-api/requery-method.md)
