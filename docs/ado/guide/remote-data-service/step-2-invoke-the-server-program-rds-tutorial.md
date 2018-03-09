---
title: "步骤 2： 调用服务器程序 （RDS 教程） |Microsoft 文档"
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
- RDS tutorial [ADO], invoking server program
ms.assetid: 5e74c2da-65ee-4de4-8b41-6eac45c3632e
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3dcff87b21f9c9c85281d0f5798e3364d15732e9
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2018
---
# <a name="step-2-invoke-the-server-program-rds-tutorial"></a>步骤 2： 调用服务器程序 （RDS 教程）
客户端上的方法的调用时*代理*，实际的程序在服务器上执行该方法。 在此步骤中，将在服务器上执行查询。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性手册](https://www.microsoft.com/en-us/download/details.aspx?id=27416)有关详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 **A 部分**如果不使用[提高](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)是最方便的方法来执行此步骤使用在本教程中， [rds.DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)对象。 **Rds.DataControl**结合使用此步骤中，发出查询创建代理的上一步。  
  
 设置**rds.DataControl**对象[服务器](../../../ado/reference/rds-api/server-property-rds.md)属性来标识其中应实例化服务器程序;[连接](../../../ado/reference/rds-api/connect-property-rds.md)属性来指定要访问数据源; 的连接字符串和[SQL](../../../ado/reference/rds-api/sql-property.md)属性指定的查询命令文本。 然后发出[刷新](../../../ado/reference/rds-api/refresh-method-rds.md)方法以使服务器程序连接到数据源、 检索指定的查询中的行并返回**记录集**到客户端的对象。  
  
 本教程不使用**rds.DataControl**，但这是它将显示如果确实执行此操作的方式：  
  
```  
Sub RDSTutorial2A()  
   Dim DC as New RDS.DataControl  
   DC.Server = "http://yourServer"  
   DC.Connect = "DSN=Pubs"  
   DC.SQL = "SELECT * FROM Authors"  
   DC.Refresh  
...  
```  
  
 也并不本教程与 ADO 对象，调用 RDS，但这是如何就像它未：  
  
```  
Dim rs as New ADODB.Recordset  
rs.Open "SELECT * FROM Authors","Provider=MS Remote;Data Source=Pubs;" & _  
        "Remote Server=http://yourServer;Remote Provider=SQLOLEDB;"  
```  
  
 **B 部分**执行此步骤的常规方法是调用**提高**对象[查询](../../../ado/reference/rds-api/query-method-rds.md)方法。 该方法采用是用来连接到数据源，一个连接字符串和命令文本，用于指定要从数据源返回的行。  
  
 本教程使用**DataFactory**对象**查询**方法：  
  
```  
Sub RDSTutorial2B()  
   Dim DS as New RDS.DataSpace  
   Dim DF  
   Dim RS as ADODB.Recordset  
   Set DF = DS.CreateObject("RDSServer.DataFactory", "http://yourServer")  
   Set RS = DF.Query ("DSN=Pubs", "SELECT * FROM Authors")  
...  
```  
  
## <a name="see-also"></a>另请参阅  
 [步骤 3： 服务器获取记录集 （RDS 教程）](../../../ado/guide/remote-data-service/step-3-server-obtains-a-recordset-rds-tutorial.md)   
 [RDS 教程 (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   
