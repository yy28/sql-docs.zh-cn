---
title: RDS 教程 (VBScript) |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- RDS tutorial [ADO], VBScript
ms.assetid: e2a48c4d-88b1-43ff-a202-9cdec54997d2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d45347bcdf212158fb6a0ee9f4599e1e1b00ff54
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67922429"
---
# <a name="rds-tutorial-vbscript"></a>RDS 教程 (VBScript)
这是 RDS 教程中，用 Microsoft Visual Basic Scripting Edition。 本教程的目的的说明，请参阅[RDS 教程](../../../ado/guide/remote-data-service/rds-tutorial.md)。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416)以了解详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 在本教程中， [rds。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)和[rds。DataSpace](../../../ado/reference/rds-api/dataspace-object-rds.md)创建在设计时-也就是说，它们定义对象标记，如下： `<OBJECT>...</OBJECT>`。 或者，他们可以创建在运行时[CreateObject 方法 (RDS)](../../../ado/reference/rds-api/createobject-method-rds.md)方法。 例如， **rds。DataControl**对象无法创建与此类似：  
  
```vb
Set DC = Server.CreateObject("RDS.DataControl")  
   <!-- RDS.DataControl -->  
   <OBJECT   
      ID="DC1" CLASSID="CLSID:BD96C556-65A3-11D0-983A-00C04FC29E33">  
   </OBJECT>  
  
   <!-- RDS.DataSpace -->  
   <OBJECT   
      ID="DS1" WIDTH=1 HEIGHT=1  
      CLASSID="CLSID:BD96C556-65A3-11D0-983A-00C04FC29E36">  
   </OBJECT>  
  
   <SCRIPT LANGUAGE="VBScript">  
  
   Sub RDSTutorial()  
   Dim DF1   
```  
  
## <a name="step-1---specify-a-server-program"></a>步骤 1-指定服务器程序  
 VBScript 可以发现通过访问 VBScript 运行 IIS Web 服务器的名称**Request.ServerVariables**提供给 Active Server Pages 的方法：  
  
```vb
"https://<%=Request.ServerVariables("SERVER_NAME")%>"  
```  
  
 但是，对于本教程，使用虚服务器，"您的服务器"。  
  
> [!NOTE]
>  注意到的数据类型**ByRef**参数。 VBScript 不允许你指定变量的类型，因此您必须始终传递**变体**。 使用 HTTP 时，RDS 将允许您将传递给需要非变体，如果您调用与它的方法的一个变体**rds。DataSpace**对象[CreateObject](../../../ado/reference/rds-api/createobject-method-rds.md)方法。 使用 DCOM 或进程内服务器时，必须与客户端和服务器端的参数类型匹配，否则将收到"类型不匹配"错误。  
  
```vb
Set DF1 = DS1.CreateObject("RDSServer.DataFactory", "https://yourServer")  
```  
  
## <a name="step-2a---invoke-the-server-program-with-rdsdatacontrol"></a>步骤 2a-调用服务器程序与 rds。数据控件  
 此示例中是只是演示的一个注释的默认行为**rds。DataControl**是执行指定的查询。  
  
```vb
<OBJECT CLASSID="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33" ID="DC1">  
   <PARAM NAME="SQL" VALUE="SELECT * FROM Authors">  
   <PARAM NAME="Connect" VALUE="DSN=Pubs;">  
   <PARAM NAME="Server" VALUE="https://yourServer/">  
</OBJECT>  
...  
<SCRIPT LANGUAGE="VBScript">  
  
Sub RDSTutorial2A()  
   Dim RS  
   DC1.Refresh  
   Set RS = DC1.Recordset  
...  
```  
  
## <a name="step-2b---invoke-the-server-program-with-rdsserverdatafactory"></a>步骤 2b-调用服务器程序，提高与  
  
## <a name="step-3---server-obtains-a-recordset"></a>步骤 3-服务器获取记录集  
  
## <a name="step-4---server-returns-the-recordset"></a>步骤 4-服务器返回记录集  
  
```vb
Set RS = DF1.Query("DSN=Pubs;", "SELECT * FROM Authors")  
```  
  
## <a name="step-5---datacontrol-is-made-usable-by-visual-controls"></a>步骤 5-数据控件是通过使用可视控件  
  
```vb
' Assign the returned recordset to the DataControl.  
  
DC1.SourceRecordset = RS  
```  
  
## <a name="step-6a---changes-are-sent-to-the-server-with-rdsdatacontrol"></a>步骤 6a-更改发送到的服务器与 rds。数据控件  
 此示例中是只是一个注释演示如何将**rds。DataControl**执行更新。  
  
```vb
<OBJECT CLASSID="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33" ID="DC1">  
   <PARAM NAME="SQL" VALUE="SELECT * FROM Authors">  
   <PARAM NAME="Connect" VALUE="DSN=Pubs;">  
   <PARAM NAME="Server" VALUE="https://yourServer/">  
</OBJECT>  
...  
<SCRIPT LANGUAGE="VBScript">  
  
Sub RDSTutorial6A()  
Dim RS  
DC1.Refresh  
...  
Set RS = DC1.Recordset  
' Edit the Recordset object...  
' The SERVER and CONNECT properties are already set from Step 2A.  
Set DC1.SourceRecordset = RS  
...  
DC1.SubmitChanges  
```  
  
## <a name="step-6b---changes-are-sent-to-the-server-with-rdsserverdatafactory"></a>步骤 6b-更改发送到提高的服务器  
  
```vb
DF.SubmitChanges "DSN=Pubs", RS  
  
End Sub  
</SCRIPT>  
</BODY>  
</HTML>  
```  
  
 **这是本教程结束。**  
  
## <a name="see-also"></a>请参阅  
 [RDS 教程](../../../ado/guide/remote-data-service/rds-tutorial.md)   
