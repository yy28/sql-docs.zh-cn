---
title: 步骤 6： 将更改发送到服务器 （RDS 教程） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS tutorial [ADO], changes sent to server
ms.assetid: b1e927d6-7d50-4978-9eef-045043cdce7a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8bfeb9ad607fc35c055e025fcc67435323d3143e
ms.sourcegitcommit: 1a5448747ccb2e13e8f3d9f04012ba5ae04bb0a3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/12/2018
ms.locfileid: "51559964"
---
# <a name="step-6-changes-are-sent-to-the-server-rds-tutorial"></a>步骤 6：将更改发送到服务器（RDS 教程）
如果**记录集**编辑对象，可以将任何更改 （即，对行进行添加、 更改或删除） 发回服务器。  
  
> [!NOTE]
>  可以使用 ADO 对象和 Microsoft OLE DB 远程处理提供程序隐式调用 RDS 的默认行为。 查询可以返回**记录集**s，并编辑**记录集**s 可以更新数据源。 本教程不会调用与 ADO 对象，RDS，但这是它将如何呈现它的形式：  
  
```vb
Dim rs as New ADODB.Recordset  
rs. "SELECT * FROM Authors","=MS Remote;=Pubs;" & _  
=https://yourServer;=SQLOLEDB;"  
...              ' Edit the Recordset.  
rs.   ' The equivalent of   
...  
```  
  
 **A 部分**假设您仅使用这种情况下的[rds。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)并且**记录集**对象现在与**rds。DataControl**。 [SubmitChanges](../../../ado/reference/rds-api/submitchanges-method-rds.md)方法的任何更改会更新数据源**记录集**对象如果[Server](../../../ado/reference/rds-api/server-property-rds.md)并[Connect](../../../ado/reference/rds-api/connect-property-rds.md)仍设置属性。  
  
```vb
Sub RDSTutorial6A()  
Dim DC as New RDS.DataControl  
Dim RS as ADODB.Recordset  
DC. = "https://yourServer"  
DC. = "DSN=Pubs"  
DC. = "SELECT * FROM Authors"  
DC.  
...  
Set RS = DC.  
   ' Edit the Recordset.  
...  
DC.  
...  
```  
  
 **B 部分**或者，你可以更新与服务器[提高](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)对象，指定的连接和一个**记录集**对象。  
  
```vb
Sub RDSTutorial6B()  
Dim DS As New RDS.DataSpace  
Dim RS As ADODB.Recordset  
Dim DC As New RDS.DataControl  
Dim DF As Object  
Dim blnStatus As Boolean  
Set DF = DS.("RDSServer.DataFactory", "https://yourServer")  
Set RS = DF. ("DSN=Pubs", "SELECT * FROM Authors")  
DC. = RS    ' Visual controls can now bind to DC.  
    ' Edit the Recordset.  
blnStatus = DF."DSN=Pubs", RS  
End Sub  
```  
  
 **这是本教程结束。**  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416)以了解详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="see-also"></a>请参阅  
 [Microsoft OLE DB 远程处理提供程序 （ADO 服务提供程序）](../../../ado/guide/appendixes/microsoft-ole-db-remoting-provider-ado-service-provider.md)   
 [RDS 教程](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [RDS 教程 (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   
