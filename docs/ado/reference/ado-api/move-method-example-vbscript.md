---
title: Move 方法示例 (VBScript) |Microsoft Docs
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
- Move method, VBScript example
ms.assetid: 29ec4b95-8986-4970-943f-3da3ecb207a2
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 82b09a23fd47473f45524f770806f5f7bd71f2dd
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66707396"
---
# <a name="move-method-example-vbscript"></a>Move 方法示例 (VBScript)
此示例使用[移动](../../../ado/reference/ado-api/move-method-ado.md)方法将记录指针中，基于用户输入。  
  
 使用下面的示例 Active Server Page (ASP)。 若要查看此示例中完全正常运行，必须具有源 AdvWorks.mdb （随 SDK 一起安装） 位于 C:\Program Files\Microsoft 平台 SDK\Samples\DataAccess\Rds\RDSTest\advworks.mdb 或编辑路径以反映代码示例中的数据此文件的实际位置。 这是 Microsoft Access 数据库文件。  
  
 使用**查找**找到 Adovbs.inc 的文件并将它放置在你打算使用的目录中。 剪切并粘贴到记事本或其他文本编辑器，下面的代码，然后将其保存为**MoveVBS.asp**。 你可以在任何浏览器中查看结果。  
  
 请尝试输入以字母或非整数以查看错误处理工作。  
  
```  
<!-- BeginMoveVBS -->  
<%@ Language=VBScript %>  
<%' use this meta tag instead of adovbs.inc%>  
<!--METADATA TYPE="typelib" uuid="00000205-0000-0010-8000-00AA006D2EA4" -->  
<HTML>  
<HEAD>  
<TITLE>ADO Move Methods</TITLE>  
<STYLE>  
<!--  
BODY {  
   font-family: "MS SANS SERIF",sans-serif;  
    }  
.thead1 {  
   background-color: #008080;   
   font-family: 'Arial Narrow','Arial',sans-serif;   
   font-size: x-small;  
   color: white;  
   }  
.tbody {   
   text-align: center;  
   background-color: #f7efde;  
   font-family: 'Arial Narrow','Arial',sans-serif;   
   font-size: x-small;  
    }  
-->  
</STYLE>  
</HEAD>  
<BODY>   
<H3>ADO Move Methods</H3>  
<% ' to integrate/test this code replace the   
   ' Data Source value in the Connection string%>  
<%   
    ' connection and recordset variables  
    Dim Cnxn, strCnxn  
    Dim rsCustomers, strSQLCustomers  
  
    ' open connection  
    Set Cnxn = Server.CreateObject("ADODB.Connection")  
    strCnxn = "Provider='sqloledb';Data Source=" & _  
            Request.ServerVariables("SERVER_NAME") & ";" & _  
            "Integrated Security='SSPI';Initial Catalog='Northwind';"  
  
    Cnxn.Open strCnxn  
  
     ' create and open Recordset using object refs  
    Set rsCustomers = Server.CreateObject("ADODB.Recordset")  
    strSQLCustomers = "Customers"  
  
    rsCustomers.ActiveConnection = Cnxn  
    rsCustomers.CursorLocation = adUseClient  
    rsCustomers.CursorType = adOpenKeyset  
    rsCustomers.LockType = adLockOptimistic  
    rsCustomers.Source = strSQLCustomers  
    rsCustomers.Open  
  
    'Check number of user moves this session and increment by entry  
    Session("Clicks") = Session("Clicks") + Request.Form("MoveAmount")  
    Clicks = Session("Clicks")  
    ' Move to last known recordset position plus amount passed   
    rsCustomers.Move CInt(Clicks)  
  
    'Error Handling  
    If rsCustomers.EOF Then  
        Session("Clicks") = rsCustomers.RecordCount  
        Response.Write "This is the Last Record"  
        rsCustomers.MoveLast  
    ElseIf rsCustomers.BOF Then  
        Session("Clicks") = 1  
        rsCustomers.MoveFirst  
        Response.Write "This is the First Record"  
    End If  
    %>  
  
    <H3>Current Record Number is <BR>  
    <%   
    If Session("Clicks") = 0 Then Session("Clicks") = 1  
    Response.Write(Session("Clicks") )%> of <%=rsCustomers.RecordCount%></H3>  
    <HR>  
  
    <TABLE COLSPAN=8 CELLPADDING=5 BORDER=0>  
  
    <!-- BEGIN column header row for Customer Table-->  
  
    <TR CLASS=thead1>  
       <TD>Company Name</TD>  
       <TD>Contact Name</TD>  
       <TD>City</TD>  
    </TR>  
        <% 'display%>  
        <TR CLASS=tbody>  
          <TD> <%= rsCustomers("CompanyName")%> </TD>  
          <TD> <%= rsCustomers("ContactName")%></TD>  
          <TD> <%= rsCustomers("City")%> </TD>  
        </TR>   
    </TABLE>  
  
    <HR>  
    <Input Type=Button Name=cmdDown  Value="<  ">  
    <Input Type=Button Name=cmdUp Value=" >">  
    <H5>Click Direction Arrows for Previous or Next Record  
    <BR> <BR>  
  
    <FORM Method = Post Action="MoveVbs.asp" Name=Form>  
    <TABLE>  
        <TR>  
           <TD><Input Type="Button" Name=Move Value="Move Amount "></TD>  
           <TD></TD>  
           <TD><Input Type="Text" Size="4" Name="MoveAmount" Value=0></TD>  
        <TR>  
    </TABLE>  
    Click Move Amount to use Move Method<br>  
    Enter Number of Records to Move + or - </H5>    </FORM>  
</BODY>  
  
<Script Language = "VBScript">  
  
Sub Move_OnClick  
   ' Make sure move value entered is an integer  
   If IsNumeric(Document.Form.MoveAmount.Value)Then  
      Document.Form.MoveAmount.Value = CInt(Document.Form.MoveAmount.Value)  
      Document.Form.Submit  
   Else  
      MsgBox "You Must Enter a Number", ,"ADO-ASP Example"  
      Document.Form.MoveAmount.Value = 0  
   End If  
End Sub  
  
Sub cmdDown_OnClick  
   Document.Form.MoveAmount.Value = -1  
   Document.Form.Submit  
End Sub  
  
Sub cmdUp_OnClick  
   Document.Form.MoveAmount.Value = 1  
   Document.Form.Submit  
End Sub  
</Script>  
  
<%  
    ' clean up  
    If rsCustomers.State = adStateOpen then  
        rsCustomers.Close  
    End If  
    If Cnxn.State = adStateOpen then  
        Cnxn.Close  
    End If  
%>  
</HTML>  
<!-- EndMoveVBS -->  
```  
  
## <a name="see-also"></a>请参阅  
 [Move 方法 (ADO)](../../../ado/reference/ado-api/move-method-ado.md)   
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
