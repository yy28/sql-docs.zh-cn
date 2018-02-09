---
title: "所需客户端设置 |Microsoft 文档"
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
- DataFactory handler in RDS [ADO]
ms.assetid: e776b4e3-fcc4-4bfb-a7e8-5ffae1d83833
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5f542390110169a88b387856ca887a8b3183e01b
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2018
---
# <a name="required-client-settings"></a>必需的客户端设置
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性手册](https://www.microsoft.com/en-us/download/details.aspx?id=27416)有关详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 指定以下设置以使用自定义**DataFactory**处理程序。  
  
-   指定"提供程序 = MS 远程"中[连接对象 (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)对象[提供程序属性 (ADO)](../../../ado/reference/ado-api/provider-property-ado.md)属性或**连接**对象连接字符串"**提供程序**="关键字。  
  
-   设置[CursorLocation 属性 (ADO)](../../../ado/reference/ado-api/cursorlocation-property-ado.md)属性**adUseClient**。  
  
-   指定要在中使用的处理程序的名称[DataControl 对象 (RDS)](../../../ado/reference/rds-api/datacontrol-object-rds.md)对象的**处理程序**属性，或[记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)对象的连接字符串"**处理程序**="关键字。 (无法设置处理程序**连接**对象连接字符串。)  
  
 RDS 命名的服务器上提供一个默认处理程序**MSDFMAP。处理程序**。 （默认的自定义项文件被命名为 MSDFMAP。INI。)  
  
 **示例**  
  
 假定以下各节中**MSDFMAP。INI**和数据源名称，AdvWorks，之前已定义：  
  
```  
[connect CustomerDataBase]  
Access=ReadWrite  
Connect="DSN=AdvWorks"  
  
[sql CustomerById]  
SQL="SELECT * FROM Customers WHERE CustomerID = ?"  
```  
  
 在 Visual Basic 中编写以下代码段：  
  
## <a name="rdsdatacontrol-version"></a>RDS.DataControl 版本  
  
```  
Dim dc as New RDS.DataControl  
Set dc.Handler = "MSDFMAP.Handler"  
Set dc.Server = "http://yourServer"  
Set dc.Connect = "Data Source=CustomerDatabase"  
Set dc.SQL = "CustomerById(4)"  
dc.Refresh  
```  
  
## <a name="recordset-version"></a>记录集版本  
  
```  
Dim rs as New ADODB.Recordset  
rs.CursorLocation = adUseClient  
```  
  
 指定[处理程序属性 (RDS)](../../../ado/reference/rds-api/handler-property-rds.md)属性或关键字;[提供程序属性 (ADO)](../../../ado/reference/ado-api/provider-property-ado.md)属性或关键字; 与*CustomerById*和*CustomerDatabase*标识符。 然后打开**记录集**对象  
  
 rs.Open "CustomerById(4)", "Handler=MSDFMAP.Handler;" & _  
  
```  
"Provider=MS Remote;Data Source=CustomerDatabase;" & _  
"Remote Server=http://yourServer"  
```  
  
## <a name="see-also"></a>另请参阅  
 [自定义文件连接部分](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [自定义文件 SQL 部分](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [自定义文件 UserList 部分](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [DataFactory 自定义项](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [必需的客户端设置](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [了解自定义文件](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)   
 [编写自己的自定义处理程序](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)






















