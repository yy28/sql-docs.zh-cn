---
title: ConvertToString 方法示例 (VBScript) |Microsoft Docs
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
- ConvertToString method [ADO], VBScript example
ms.assetid: edd0a01c-1a1b-4b91-9966-2529e244abae
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 7f045fdb6299fa61d69a44a9a93a5bac740efaf9
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66696986"
---
# <a name="converttostring-method-example-vbscript"></a>ConvertToString 方法示例 (VBScript)
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416)以了解详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 下面的示例演示如何将转换**记录集**为 MIME 编码的字符串，并使用**提高 ConvertToString**方法。 它还展示了如何将字符串转换回**记录集**。 剪切并粘贴到记事本或其他文本编辑器的以下代码，然后将其保存为**ConvertToString.htm**。  
  
```  
<!-- BeginConvertToStringVBS -->  
<HTML>  
<HEAD><TITLE>ConvertToString Example</TITLE><HEAD>  
<BODY>  
  
<SCRIPT LANGUAGE=VBSCRIPT>  
Sub ConvertToStringX()  
    Dim objRs, objDF, strServer, vString  
    Const adcExecSync = 1  
    Const adcFetchUpFront = 1  
  
    ' Replace value below with your server name to use without ASP.  
    strServer = "https://<%=Request.ServerVariables("SERVER_NAME")%>">  
  
    Set objDF = RDS1.CreateObject("RDSServer.DataFactory", strServer)  
    Set objRs = objDF.Query(txtConnect.Value,txtQueryRecordset.Value)  
  
    ' convert Recordset to MIME encoded string  
    vString = objDF.ConvertToString(objRs)  
  
    ' display MIME string for demo purposes  
    txtRS.value = vString  
  
    ' convert MIME string back to useable ADO Recordset   
    ' using RDS.DataControl  
    RDC1.SQL = vString  
  
    RDC1.ExecuteOptions = adcExecSync  
    RDC1.FetchOptions = adcFetchUpFront  
    RDC1.Refresh  
  
    MsgBox "RecordCount = " & RDC1.Recordset.RecordCount  
End Sub   
</SCRIPT>  
  
Connect String:   
 <INPUT TYPE=Text NAME=txtConnect SIZE=50   
    VALUE="Provider=sqloledb;Initial Catalog=pubs;Integrated Security='SSPI';">   
 <BR>  
  
Query:   
 <INPUT TYPE=Text NAME=txtQueryRecordset SIZE=50   
    VALUE="select * from authors">   
 <BR>  
  
 <INPUT TYPE=Button VALUE="ConvertToString" OnClick="ConvertToStringX()">  
 <BR>  
  
MIME Encoded RS: <BR>  
 <TEXTAREA NAME=txtRS ROWS=15 COLS=50 WRAP=virtual></TEXTAREA>  
  
<!-- RDS.DataSpace  ID RDS1 -->  
 <OBJECT ID="RDS1" WIDTH=1 HEIGHT=1  
     CLASSID="CLSID:BD96C556-65A3-11D0-983A-00C04FC29E36">  
 </OBJECT>  
  
<!-- RDS.DataControl ID RDC1 -->  
 <OBJECT ID="RDC1" WIDTH=1 HEIGHT=1   
     CLASSID="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33">  
 </OBJECT>  
</BODY>  
</HTML>  
<!-- EndConvertToStringVBS -->  
```  
  
## <a name="see-also"></a>请参阅  
 [ConvertToString 方法 (RDS)](../../../ado/reference/rds-api/converttostring-method-rds.md)   
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)




