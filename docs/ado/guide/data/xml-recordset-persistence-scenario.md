---
title: "XML 记录集持久化方案 |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- XML persistence [ADO], persistence scenario
ms.assetid: 353d569a-043a-4397-9ee6-564c4af8d5f6
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cf4899425669d8c65b6b3661fb75e8bf37091ce9
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2018
---
# <a name="xml-recordset-persistence-scenario"></a>XML 记录集持久化方案
在此方案中，你将创建的 Active Server Pages (ASP) 应用程序直接与 ASP 响应对象保存记录集对象的内容。  
  
> [!NOTE]
>  此方案需要你的服务器具有 Internet 信息服务器 5.0 (IIS) 或更高版本安装。  
  
 返回的记录集显示在 Internet Explorer 中使用[DataControl 对象 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)。  
  
 以下步骤是创建此方案所需的：  
  
-   设置应用程序  
  
-   获取数据  
  
-   将数据发送  
  
-   接收并显示数据  
  
## <a name="step-1-set-up-the-application"></a>步骤 1： 设置应用程序  
 创建脚本权限的名为"XMLPersist"的 IIS 虚拟目录。 虚拟目录指向，一个名为"XMLResponse.asp，"其他命名"Default.htm。"的文件夹中创建两个新的文本文件  
  
## <a name="step-2-get-the-data"></a>步骤 2： 获取数据  
 在此步骤中，你将编写代码以打开 ADO 记录集并准备将其发送到客户端。 使用文本编辑器，（如记事本） 打开文件 XMLResponse.asp 并插入以下代码。  
  
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
  
 请务必更改的值`Data Source`中的参数`strCon`为你的 Microsoft SQL Server 计算机的名称。  
  
 使文件保持打开状态并转到下一步。  
  
## <a name="step-3-send-the-data"></a>步骤 3： 将数据发送  
 现在，你已记录集，必须直接将其发送到客户端，通过将它作为 XML 保存到 ASP 响应对象。 将以下代码添加到 XMLResponse.asp 底部。  
  
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
  
 请注意，将 ASP 响应对象指定为目标，记录集[Save 方法](../../../ado/reference/ado-api/save-method.md)。 Save 方法的目标可以是任何对象都支持为 IStream 接口，如 ADO[流对象 (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)，或包括为保存记录集的完整路径的文件名。  
  
 保存并转到下一步之前关闭 XMLResponse.asp。 此外将从默认 ADO 库安装文件夹的 adovbs.inc 文件复制到保存 XMLResponse.asp 文件的相同文件夹中。  
  
## <a name="step-4-receive-and-display-the-data"></a>步骤 4： 接收并显示数据  
 在此步骤中将某一 HTML 文件创建具有一个嵌入[DataControl 对象 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)点在 XMLResponse.asp 文件，以获取记录集的对象。 使用文本编辑器，（如记事本） 打开 default.htm 并添加下面的代码。 将在 URL 中的"sqlserver"替换为你的服务器的名称。  
  
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
  
 关闭 default.htm 文件，并将其保存到保存 XMLResponse.asp 的相同文件夹。 使用 Internet Explorer 4.0 版或更高版本，打开 URL http://*sqlserver*/XMLPersist/default.htm 并观察结果。 绑定的 DHTML 表中显示的数据。 现在打开 URL http:// *sqlserver* /XMLPersist/XMLResponse.asp 并观察结果。 显示的 XML。  
  
## <a name="see-also"></a>另请参阅  
 [Save 方法](../../../ado/reference/ado-api/save-method.md)   
 [以 XML 格式保留记录](../../../ado/guide/data/persisting-records-in-xml-format.md)
