---
title: "步骤 6： 将更改发送到服务器 （RDS 教程） |Microsoft 文档"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- RDS tutorial [ADO], changes sent to server
ms.assetid: b1e927d6-7d50-4978-9eef-045043cdce7a
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: b811d4b5fb1809c0e528f644f28d81559d5df6b6
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="step-6-changes-are-sent-to-the-server-rds-tutorial"></a>步骤 6： 将更改发送到服务器 （RDS 教程）
如果**记录集**编辑对象，可以将任何更改 （即，对行进行添加、 更改或删除） 发回服务器。  
  
> [!NOTE]
>  可以使用 ADO 对象和 Microsoft OLE DB 远程处理提供程序隐式调用 RDS 的默认行为。 查询可以返回**记录集**s，和编辑**记录集**s 可以更新数据源。 本教程不会与 ADO 对象，调用 RDS，但这是它将显示如果确实执行此操作的方式：  
  
```  
Dim rs as New ADODB.Recordset  
rs. "SELECT * FROM Authors","=MS Remote;=Pubs;" & _  
=http://yourServer;=SQLOLEDB;"  
...              ' Edit the Recordset.  
rs.   ' The equivalent of   
...  
```  
  
 **A 部分**你仅使用这种情况下的假定[rds.DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)且**记录集**对象现在与之关联**rds.DataControl**。 [SubmitChanges](../../../ado/reference/rds-api/submitchanges-method-rds.md)方法更新任何更改的数据源**记录集**对象如果[服务器](../../../ado/reference/rds-api/server-property-rds.md)和[连接](../../../ado/reference/rds-api/connect-property-rds.md)仍然设置属性。  
  
```  
Sub RDSTutorial6A()  
Dim DC as New RDS.DataControl  
Dim RS as ADODB.Recordset  
DC. = "http://yourServer"  
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
  
 **B 部分**或者，你无法更新与服务器[提高](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)对象，指定连接和**记录集**对象。  
  
```  
Sub RDSTutorial6B()  
Dim DS As New RDS.DataSpace  
Dim RS As ADODB.Recordset  
Dim DC As New RDS.DataControl  
Dim DF As Object  
Dim blnStatus As Boolean  
Set DF = DS.("RDSServer.DataFactory", "http://yourServer")  
Set RS = DF. ("DSN=Pubs", "SELECT * FROM Authors")  
DC. = RS    ' Visual controls can now bind to DC.  
    ' Edit the Recordset.  
blnStatus = DF."DSN=Pubs", RS  
End Sub  
```  
  
 **这是本教程末尾。**  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性手册](https://www.microsoft.com/en-us/download/details.aspx?id=27416)有关详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
## <a name="see-also"></a>另请参阅  
 [Microsoft OLE DB 远程处理提供程序 （ADO 服务提供程序）](../../../ado/guide/appendixes/microsoft-ole-db-remoting-provider-ado-service-provider.md)   
 [RDS 教程](../../../ado/guide/remote-data-service/rds-tutorial.md)   
 [RDS 教程 (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   

