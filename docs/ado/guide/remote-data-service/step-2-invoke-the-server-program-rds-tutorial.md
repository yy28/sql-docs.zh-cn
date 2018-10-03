---
title: 步骤 2： 调用服务器程序 （RDS 教程） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS tutorial [ADO], invoking server program
ms.assetid: 5e74c2da-65ee-4de4-8b41-6eac45c3632e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0a2e7b62276234dcf11067395ff2512a8e93af96
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47800505"
---
# <a name="step-2-invoke-the-server-program-rds-tutorial"></a>步骤 2：调用服务器程序（RDS 教程）
调用客户端上的方法时*代理*，实际的程序在服务器上执行该方法。 在此步骤中，将在服务器上执行查询。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，不再在 Windows 操作系统中包含 RDS 服务器组件 (请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/en-us/download/details.aspx?id=27416)以了解详细信息)。 将 Windows 的未来版本中删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](http://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 **A 部分**如果您没有使用其他[提高](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)在本教程中，最方便的方法来执行此步骤是使用[rds。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)对象。 **Rds。DataControl**结合了使用此步骤中，发出查询创建一个代理的上一步。  
  
 设置**rds。DataControl**对象[服务器](../../../ado/reference/rds-api/server-property-rds.md)属性标识其中应实例化服务器程序; [Connect](../../../ado/reference/rds-api/connect-property-rds.md)属性来指定连接字符串以访问数据源; 和[SQL](../../../ado/reference/rds-api/sql-property.md)属性来指定查询命令文本。 然后，发出[刷新](../../../ado/reference/rds-api/refresh-method-rds.md)方法以使服务器程序连接到数据源，检索指定的查询中，行并返回**记录集**到客户端对象。  
  
 本教程不使用**rds。DataControl**，但这是它将如何呈现它的形式：  
  
```  
Sub RDSTutorial2A()  
   Dim DC as New RDS.DataControl  
   DC.Server = "http://yourServer"  
   DC.Connect = "DSN=Pubs"  
   DC.SQL = "SELECT * FROM Authors"  
   DC.Refresh  
...  
```  
  
 也并不在本教程使用 ADO 对象调用 RDS，但这是它将如何呈现它的形式：  
  
```  
Dim rs as New ADODB.Recordset  
rs.Open "SELECT * FROM Authors","Provider=MS Remote;Data Source=Pubs;" & _  
        "Remote Server=http://yourServer;Remote Provider=SQLOLEDB;"  
```  
  
 **B 部分**执行此步骤的常规方法是调用**提高**对象[查询](../../../ado/reference/rds-api/query-method-rds.md)方法。 该方法将连接字符串，它用于连接到数据源，将命令文本，用于指定要从数据源返回的行。  
  
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
  
## <a name="see-also"></a>请参阅  
 [步骤 3： 服务器获取记录集 （RDS 教程）](../../../ado/guide/remote-data-service/step-3-server-obtains-a-recordset-rds-tutorial.md)   
 [RDS 教程 (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   
