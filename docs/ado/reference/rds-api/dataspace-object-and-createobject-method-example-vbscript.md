---
title: DataSpace 对象和 CreateObject 方法示例 (VBScript) |Microsoft Docs
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
- DataSpace object [RDS], VBScript example
- CreateObject method [ADO], VBScript example
ms.assetid: 12b0e160-5e5c-441f-bed7-ac0bd061e003
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d24d67f3c798c061fe10c932f36aa4e7f007f772
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63134421"
---
# <a name="dataspace-object-and-createobject-method-example-vbscript"></a>DataSpace 对象和 CreateObject 方法示例 (VBScript)
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416)以了解详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 下面的示例演示如何使用[CreateObject](../../../ado/reference/rds-api/createobject-method-rds.md)方法的[rds。DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md)默认业务对象时，[提高](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)。 若要测试此示例中，代码剪切并粘贴此之间\<正文 > 和\</b o d > 标记中普通的 HTML 文档并将其命名**DataSpaceVBS.asp**。 ASP 脚本将识别您的服务器。  
  
```  
<!-- BeginDataSpaceVBS -->  
<html>  
<head>  
<!--use the following META tag instead of adovbs.inc-->  
<!--METADATA TYPE="typelib" uuid="00000205-0000-0010-8000-00AA006D2EA4" -->  
    <meta name="VI60_DefaultClientScript"  content=VBScript>  
    <meta name="GENERATOR" content="Microsoft Visual Studio 6.0">  
    <title>DataSpace Object and CreateObject Method Example (VBScript)</title>  
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
  
<body>  
<h1>DataSpace Object and CreateObject Method Example (VBScript)</h1>  
  
<H2>RDS API Code Examples</H2>  
<HR>  
<H3>Using Query Method of RDSServer.DataFactory</H3>  
  
<!-- RDS.DataSpace  ID rdsDS-->  
<OBJECT ID="rdsDS" WIDTH=1 HEIGHT=1  
CLASSID="CLSID:BD96C556-65A3-11D0-983A-00C04FC29E36">  
</OBJECT>  
  
<!-- RDS.DataControl with parameters set at run time -->  
<OBJECT classid="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33"  
   ID=RDS WIDTH=1 HEIGHT=1>  
</OBJECT>  
  
<TABLE DATASRC=#RDS>  
<TBODY>  
  <TR>  
    <TD><SPAN DATAFLD="FirstName"></SPAN></TD>  
    <TD><SPAN DATAFLD="LastName"></SPAN></TD>  
  </TR>  
</TBODY>  
</TABLE>  
  
<HR>  
<INPUT TYPE=BUTTON NAME="Run" VALUE="Run">  
  
<H4>Click Run -  
The <i>CreateObject</i> Method of the RDS.DataSpace Object Creates an instance of the RDSServer.DataFactory.  
The <i>Query</i> Method of the RDSServer.DataFactory is used to bring back a Recordset.</H4>  
  
<Script Language="VBScript">  
  
    Dim rdsDF  
    Dim strServer  
    Dim strCnxn  
    Dim strSQL  
  
    strServer = "https://<%=Request.ServerVariables("SERVER_NAME")%>"  
    strCnxn = "Provider='sqloledb';Data Source=" & _  
            "<%=Request.ServerVariables("SERVER_NAME")%>" & ";" & _  
            "Integrated Security='SSPI';Initial Catalog='Northwind';"  
    strSQL = "Select FirstName, LastName from Employees"  
  
    Sub Run_OnClick()  
  
       Dim rs        
        ' Create Data Factory  
       Set rdsDF = rdsDS.CreateObject("RDSServer.DataFactory", strServer)  
        'Get Recordset    
       Set rs = rdsDF.Query(strCnxn, strSQL)     
       ' Use  RDS.DataControl to bind Recordset to data-aware Table above  
       RDS.SourceRecordset = rs  
  
    End Sub  
</Script>  
  
</body>  
</html>  
<!-- EndDataSpaceVBS -->  
```  
  
 下面的示例演示如何使用**CreateObject**方法来创建自定义业务对象，VbBusObj.VbBusObjCls 的实例。 它还使用脚本来标识 Web 服务器名称 Active Server Pages。  
  
 若要查看完整示例，请打开示例应用程序选择器。 在中**客户端层**列中，选择**在 Internet Explorer 中的 VBScript**。 在中**中间层**列中，选择**自定义 Visual Basic 业务对象**。  
  
> [!NOTE]
>  如果您要连接到的数据源提供程序支持 Windows 身份验证，则应指定**Trusted_Connection = yes**或**Integrated Security = SSPI**而不是用户 ID 和密码在连接字符串中的信息。  
  
```  
Sub Window_OnLoad()  
   strServer = "https://<%=Request.ServerVariables("SERVER_NAME")%>"  
   Set BO = ADS1.CreateObject("VbBusObj.VbBusObjCls", strServer)  
   txtConnect.Value = "dsn=Pubs;uid=MyUserID;pwd=MyPassword;"  
   txtGetRecordset.Value = "Select * From authors for Browse"  
End Sub  
```  
  
## <a name="see-also"></a>请参阅  
 [CreateObject 方法 (RDS)](../../../ado/reference/rds-api/createobject-method-rds.md)   
 [DataSpace 对象 (RDS)](../../../ado/reference/rds-api/dataspace-object-rds.md)


