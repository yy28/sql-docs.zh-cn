---
title: 必需的客户端设置 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- DataFactory handler in RDS [ADO]
ms.assetid: e776b4e3-fcc4-4bfb-a7e8-5ffae1d83833
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bdb99cb3d792900f48ceb69c25c7ae720c339683
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67922295"
---
# <a name="required-client-settings"></a>必需的客户端设置
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，Windows 操作系统中不再包含 RDS 服务器组件（有关详细信息，请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416)）。 在 Windows 的未来版本中将删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 指定以下设置以使用自定义**DataFactory**处理程序。  
  
-   在[连接对象（ado）](../../../ado/reference/ado-api/connection-object-ado.md)对象[提供程序属性（ado）](../../../ado/reference/ado-api/provider-property-ado.md)属性或**连接**对象连接字符串 "**Provider**=" 关键字中指定 "provider = MS Remote"。  
  
-   将[CursorLocation 属性（ADO）](../../../ado/reference/ado-api/cursorlocation-property-ado.md)属性设置为**adUseClient**。  
  
-   指定要在[DataControl 对象（RDS）](../../../ado/reference/rds-api/datacontrol-object-rds.md)对象的**处理程序**属性或[记录集对象（ADO）](../../../ado/reference/ado-api/recordset-object-ado.md)对象的连接字符串 "**handler**=" 关键字中使用的处理程序的名称。 （您不能在**连接**对象的连接字符串中设置处理程序。）  
  
 RDS 在名为 MSDFMAP 的服务器上提供了一个默认的处理程序 **。处理程序**。 （默认自定义文件被命名为 MSDFMAP。INI。）  
  
 **示例**  
  
 假定 MSDFMAP 中的以下部分 **。INI**和数据源名称 advworks-srv01 是以前定义的：  
  
```console
[connect CustomerDataBase]  
Access=ReadWrite  
Connect="DSN=AdvWorks"  
  
[sql CustomerById]  
SQL="SELECT * FROM Customers WHERE CustomerID = ?"  
```  
  
 以下代码片段以 Visual Basic 编写：  
  
## <a name="rdsdatacontrol-version"></a>RDS.DataControl 版本  
  
```vb
Dim dc as New RDS.DataControl  
Set dc.Handler = "MSDFMAP.Handler"  
Set dc.Server = "https://yourServer"  
Set dc.Connect = "Data Source=CustomerDatabase"  
Set dc.SQL = "CustomerById(4)"  
dc.Refresh  
```  
  
## <a name="recordset-version"></a>记录集版本  
  
```vb
Dim rs as New ADODB.Recordset  
rs.CursorLocation = adUseClient  
```  
  
 指定[处理程序属性（RDS）](../../../ado/reference/rds-api/handler-property-rds.md)属性或关键字;[Provider 属性（ADO）](../../../ado/reference/ado-api/provider-property-ado.md)属性或关键字;和*CustomerById*和*CustomerDatabase*标识符。 然后打开**Recordset**对象  
  
 rs-232c.打开 "CustomerById （4）"，"Handler = MSDFMAP"。处理程序; "& _  
  
```vb
"Provider=MS Remote;Data Source=CustomerDatabase;" & _  
"Remote Server=https://yourServer"  
```  
  
## <a name="see-also"></a>另请参阅  
 [自定义文件连接部分](../../../ado/guide/remote-data-service/customization-file-connect-section.md)   
 [自定义文件 SQL 部分](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [自定义文件 UserList 部分](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [自定义 DataFactory](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [必需的客户端设置](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [了解自定义文件](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)   
 [编写自己的自定义处理程序](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)

