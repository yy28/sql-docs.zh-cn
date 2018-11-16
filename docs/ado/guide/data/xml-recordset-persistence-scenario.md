---
title: XML 记录集暂留方案 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- XML persistence [ADO], persistence scenario
ms.assetid: 353d569a-043a-4397-9ee6-564c4af8d5f6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 65f4705eb926c116d935384163cffe4f33b11a88
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/13/2018
ms.locfileid: "51600237"
---
# <a name="xml-recordset-persistence-scenario"></a>XML 记录集暂留方案
在此方案中，将创建记录集对象的内容保存直接向 ASP 响应对象的 Active Server Pages (ASP) 应用程序。  
  
> [!NOTE]
>  此方案需要你的服务器具有 Internet Information Server 5.0 (IIS) 或更高版本安装。  
  
 返回的记录集显示在 Internet Explorer 中使用[DataControl 对象 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)。  
  
 以下步骤是创建此方案所必需的：  
  
-   设置应用程序  
  
-   获取数据  
  
-   将数据发送  
  
-   接收和显示数据  
  
## <a name="step-1-set-up-the-application"></a>步骤 1： 设置应用程序  
 创建权限脚本创建名为"XMLPersist"的 IIS 虚拟目录。 在虚拟目录指向，一个名为"XMLResponse.asp，"其他名为"Default.htm。"的文件夹中创建两个新的文本文件  
  
## <a name="step-2-get-the-data"></a>步骤 2： 获取数据  
 在此步骤中，将编写代码以打开 ADO 记录集，并准备将其发送给客户端。 使用文本编辑器，例如记事本，打开文件 XMLResponse.asp 并插入以下代码。  
  
```  
<%@ language="VBScript" %>  
  
<!-- #include file='adovbs.inc' -->  
  
<%  
  Dim strSQL, strCon  
  Dim adoRec   
  Dim adoCon   
  Dim xmlDoc   
  
  ' You will need to change "MySQLServer" below to the name of the SQL   
  ' server machine to which you want to connect.  
  strCon = "Provider=sqloledb;Data Source=MySQLServer;Initial Catalog=Pubs;Integrated Security=SSPI;"  
  Set adoCon = server.createObject("ADODB.Connection")  
  adoCon.Open strCon  
  
  strSQL = "SELECT Title, Price FROM Titles ORDER BY Price"  
  Set adoRec = Server.CreateObject("ADODB.Recordset")  
  adoRec.Open strSQL, adoCon, adOpenStatic, adLockOptimistic, adCmdText  
```  
  
 请务必更改的值`Data Source`中的参数`strCon`到 Microsoft SQL Server 计算机的名称。  
  
 使文件保持打开，然后继续执行下一步。  
  
## <a name="step-3-send-the-data"></a>步骤 3： 将数据发送  
 现在，已记录集，必须直接将其发送到客户端，通过将其作为 XML 保存到 ASP 响应对象。 将以下代码添加到 XMLResponse.asp 的底部。  
  
```  
  Response.ContentType = "text/xml"  
  Response.Expires = 0  
  Response.Buffer = False  
  
  Response.Write "<?xml version='1.0'?>" & vbNewLine  
  adoRec.save Response, adPersistXML  
  adoRec.Close  
  Set adoRec=Nothing  
%>  
```  
  
 请注意，ASP 响应对象指定为记录集目标[Save 方法](../../../ado/reference/ado-api/save-method.md)。 保存方法的目标可以是任何对象，支持的 IStream 接口，如 ADO [Stream 对象 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)，或包含记录集是要保存的完整路径的文件名。  
  
 保存并转到下一步之前关闭 XMLResponse.asp。 此外将从默认 ADO 库安装文件夹的 adovbs.inc 文件复制到 XMLResponse.asp 文件的保存位置的相同文件夹中。  
  
## <a name="step-4-receive-and-display-the-data"></a>步骤 4： 接收和显示数据  
 在此步骤中将某一 HTML 文件创建使用嵌入[DataControl 对象 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)指向 XMLResponse.asp 文件，以获取记录集的对象。 使用文本编辑器，如记事本，打开 default.htm 并添加以下代码。 在 URL 中的"sqlserver"替换为你的服务器的名称。  
  
```  
<HTML>  
<HEAD><TITLE>ADO Recordset Persistence Sample</TITLE></HEAD>  
<BODY>  
  
<TABLE DATASRC="#RDC1" border="1">  
  <TR>  
<TD><SPAN DATAFLD="title"></SPAN></TD>  
<TD><SPAN DATAFLD="price"></SPAN></TD>  
  </TR>  
</TABLE>  
<OBJECT CLASSID="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33" ID="RDC1">  
   <PARAM NAME="URL" VALUE="XMLResponse.asp">  
</OBJECT>  
  
</BODY>  
</HTML>  
```  
  
 关闭 default.htm 文件，并将其保存到保存 XMLResponse.asp 的同一个文件夹。 使用 Internet Explorer 4.0 或更高版本，打开 URL https://*sqlserver*/XMLPersist/default.htm 并观察结果。 在绑定的 DHTML 表中显示的数据。 现在打开 URL https:// *sqlserver* /XMLPersist/XMLResponse.asp 并观察结果。 显示 XML。  
  
## <a name="see-also"></a>请参阅  
 [保存方法](../../../ado/reference/ado-api/save-method.md)   
 [以 XML 格式保留记录](../../../ado/guide/data/persisting-records-in-xml-format.md)
