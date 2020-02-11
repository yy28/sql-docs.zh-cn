---
title: 步骤2：调用服务器程序（RDS 教程） |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- RDS tutorial [ADO], invoking server program
ms.assetid: 5e74c2da-65ee-4de4-8b41-6eac45c3632e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8ca35b952cdb228e70a2e747026214dc1cf020f9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "67922093"
---
# <a name="step-2-invoke-the-server-program-rds-tutorial"></a>步骤 2：调用服务器程序（RDS 教程）
当您在客户端*代理*上调用方法时，服务器上的实际程序将执行方法。 在此步骤中，您将在服务器上执行查询。  
  
> [!IMPORTANT]
>  从 Windows 8 和 Windows Server 2012 开始，Windows 操作系统中不再包含 RDS 服务器组件（有关详细信息，请参阅 Windows 8 和[Windows Server 2012 兼容性指南](https://www.microsoft.com/download/details.aspx?id=27416)）。 在 Windows 的未来版本中将删除 RDS 客户端组件。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。 使用 RDS 的应用程序应迁移到[WCF 数据服务](https://go.microsoft.com/fwlink/?LinkId=199565)。  
  
 **部分 A**如果在本教程中没有使用[RDSServer](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) ，则执行此步骤的最简便方法是使用[RDS。DataControl](../../../ado/reference/rds-api/datacontrol-object-rds.md)对象。 **RDS。DataControl**结合了之前创建代理的步骤，并在此步骤中发出查询。  
  
 设置**RDS。DataControl**对象[服务器](../../../ado/reference/rds-api/server-property-rds.md)属性来标识应实例化服务器程序的位置;[连接](../../../ado/reference/rds-api/connect-property-rds.md)属性以指定访问数据源的连接字符串;和[SQL](../../../ado/reference/rds-api/sql-property.md)属性来指定查询命令文本。 然后发出[Refresh](../../../ado/reference/rds-api/refresh-method-rds.md)方法，使服务器程序连接到数据源，检索查询指定的行，并将**记录集**对象返回到客户端。  
  
 本教程不使用**RDS。DataControl**，但如下所示：  
  
```vb
Sub RDSTutorial2A()  
   Dim DC as New RDS.DataControl  
   DC.Server = "https://yourServer"  
   DC.Connect = "DSN=Pubs"  
   DC.SQL = "SELECT * FROM Authors"  
   DC.Refresh  
...  
```  
  
 本教程不会调用具有 ADO 对象的 RDS，但这是它的外观：  
  
```vb
Dim rs as New ADODB.Recordset  
rs.Open "SELECT * FROM Authors","Provider=MS Remote;Data Source=Pubs;" & _  
        "Remote Server=https://yourServer;Remote Provider=SQLOLEDB;"  
```  
  
 **B 部分**执行此步骤的一般方法是调用**RDSServer. DataFactory**对象[查询](../../../ado/reference/rds-api/query-method-rds.md)方法。 该方法采用连接字符串（用于连接到数据源）和命令文本（用于指定从数据源返回的行）。  
  
 本教程使用**DataFactory**对象**查询**方法：  
  
```vb
Sub RDSTutorial2B()  
   Dim DS as New RDS.DataSpace  
   Dim DF  
   Dim RS as ADODB.Recordset  
   Set DF = DS.CreateObject("RDSServer.DataFactory", "https://yourServer")  
   Set RS = DF.Query ("DSN=Pubs", "SELECT * FROM Authors")  
...  
```  
  
## <a name="see-also"></a>另请参阅  
 [步骤3：服务器获取记录集（RDS 教程）](../../../ado/guide/remote-data-service/step-3-server-obtains-a-recordset-rds-tutorial.md)   
 [RDS 教程 (VBScript)](../../../ado/guide/remote-data-service/rds-tutorial-vbscript.md)   
