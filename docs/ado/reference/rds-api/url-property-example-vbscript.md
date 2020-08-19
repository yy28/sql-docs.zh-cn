---
description: URL 属性示例 (VBScript)
title: " (VBScript) 的 URL 属性示例 |Microsoft Docs"
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.prod: sql
ms.prod_service: connectivity
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- URL property [ADO], VBScript example
ms.assetid: 6ae5ac50-c88c-4262-b7ab-f2b3de382a0b
author: rothja
ms.author: jroth
ms.openlocfilehash: 25a0460aa93c51f841719b1318e1413a2dcf0d99
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88438539"
---
# <a name="url-property-example-vbscript"></a>URL 属性示例 (VBScript)
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，Windows 操作系统中不再包含 RDS 服务器组件 (参阅 Windows 8 和 [Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416) ，以了解更多详细信息) 。 在 Windows 的未来版本中将删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到 [WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 下面的代码演示如何在客户端上设置 **URL** 属性以指定一个 .asp 文件，该文件随后会处理对数据源所做的更改。  
  
```  
<!-- BeginURLClientVBS -->  
<%@ Language=VBScript %>  
<html>  
<head>  
    <meta name="VI60_DefaultClientScript"  content=VBScript>  
    <meta name="GENERATOR" content="Microsoft Visual Studio 6.0">  
    <title>URL Property Example (VBScript)</title>  
<style>  
<!--  
body {  
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
</style>  
</head>  
  
<body onload=Getdata()>  
<h1>URL Property Example (VBScript)</h1>  
<OBJECT classid=clsid:BD96C556-65A3-11D0-983A-00C04FC29E33 height=1 id=ADC width=1>  
</OBJECT>  
  
<table datasrc="#ADC" align="center">  
<thead>  
<tr id="ColHeaders" class="thead2">  
   <th>FirstName</th>  
   <th>LastName</th>  
   <th>Extension</th>  
</tr>  
</thead>  
<tbody class="tbody">  
<tr>  
   <td><input datafld="FirstName" size=15> </td>  
   <td><input datafld="LastName" size=25> </td>  
   <td><input datafld="Extension" size=15> </td>  
</tr>  
</tbody>  
</table>  
  
<script Language="VBScript">  
Sub Getdata()  
  
      ADC.URL = "https://MyServer/URLServerVBS.asp"  
      ADC.Refresh  
End Sub  
  
</script>  
  
</body>  
</html>  
<!-- EndURLClientVBS -->  
```  
  
 位于 **URLServerVBS** 中的服务器端代码将更新的 **记录集** 提交到数据源。  
  
```  
<!-- BeginURLServerVBS -->  
<%@ Language=VBScript %>  
<%  
  
        ' XML output req's  
    Response.ContentType = "text/xml"  
    const adPersistXML  = 1  
  
        ' recordset vars  
    Dim strSQL, rsEmployees   
    Dim strCnxn, Cnxn  
  
    strCnxn = "Provider='sqloledb';Data Source=" & _  
            Request.ServerVariables("SERVER_NAME") & ";" & _  
            "Integrated Security='SSPI';Initial Catalog='Northwind';"  
    Set Cnxn = Server.CreateObject("ADODB.Connection")  
    Set rsEmployees = Server.CreateObject("ADODB.Recordset")  
  
    strSQL = "SELECT FirstName, LastName, Extension FROM Employees"  
  
    Cnxn.Open strCnxn  
    rsEmployees.Open strSQL, Cnxn  
  
        ' output as XML  
    rsEmployees.Save Response, adPersistXML  
  
        ' Clean up  
    rsEmployees.Close  
    Cnxn.Close  
    Set rsEmployees = Nothing  
    Set Cnxn = Nothing  
%>  
<!-- EndURLServerVBS -->  
```  
  
## <a name="see-also"></a>另请参阅  
 [URL 属性 (RDS)](../../../ado/reference/rds-api/url-property-rds.md)


