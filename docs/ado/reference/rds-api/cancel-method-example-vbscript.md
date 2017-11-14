---
title: "取消方法示例 (VBScript) |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- Cancel method [ADO], VBScript example
ms.assetid: 4ade106d-063d-486e-bc4d-a1a6b6e0bea9
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 018b787751e09de4ee8e40d8b2c217a0d4c4c69f
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="cancel-method-example-vbscript"></a>取消方法示例 (VBScript)
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性手册](https://www.microsoft.com/en-us/download/details.aspx?id=27416)有关详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 下面的示例演示如何读取[取消](../../../ado/reference/ado-api/cancel-method-ado.md)方法在运行时。 剪切并粘贴到记事本或其他文本编辑器下面的代码，然后将其保存为 CancelVBS.asp。 你可以在任何客户端浏览器中查看的结果。  
  
```  
<!-- BeginCancelVBS -->  
<Script Language="VBScript">  
<!--  
Sub cmdCancelAsync_OnClick  
   ' Terminates currently running AsyncExecute,  
   ' ReadyState property set to adcReadyStateLoaded,  
   ' Recordset set to Nothing  
  ADC.Cancel  
End Sub  
  
Sub cmdRefreshTable_OnClick  
   ADC.Refresh  
End Sub  
-->  
</Script>  
  
<OBJECT CLASSID="clsid:BD96C556-65A3-11D0-983A-00C04FC29E33" ID="ADC">  
.  
   <PARAM NAME="SQL" VALUE="Select FirstName, LastName from Employees">  
   <PARAM NAME="CONNECT" VALUE="Provider='sqloledb';Integrated Security='SSPI';Initial Catalog='Northwind'">  
   <PARAM NAME="Server" VALUE="http://<%=Request.ServerVariables("SERVER_NAME")%>">  
.  
</OBJECT>  
  
<TABLE DATASRC=#ADC>  
<TBODY>  
  <TR>  
    <TD><SPAN DATAFLD="FirstName"></SPAN></TD>  
    <TD><SPAN DATAFLD="LastName"></SPAN></TD>  
  </TR>  
</TBODY>  
</TABLE>  
  
<FORM>  
<INPUT type="button" value="Refresh" id=cmdRefreshTable name=cmdRefreshTable>  
<INPUT type="button" value="Cancel" id=cmdCancelAsync name=cmdCancelAsync>  
</FORM>  
<!-- EndCancelVBS -->  
```  
  
## <a name="see-also"></a>另请参阅  
 [Cancel 方法 (ADO)](../../../ado/reference/ado-api/cancel-method-ado.md)



