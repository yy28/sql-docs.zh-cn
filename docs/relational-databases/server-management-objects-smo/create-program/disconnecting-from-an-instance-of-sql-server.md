---
title: 与 SQL Server 的实例断开连接 |Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Management Objects, disconnecting
- SMO [SQL Server], disconnecting
- instances of SQL Server, disconnecting
- disconnecting [SMO]
ms.assetid: 4ca7f7eb-6b3f-4c73-ac63-88afa8570b61
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 51d3adb75a7ffe19a6f157fe51af89f831064eb6
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85898008"
---
# <a name="disconnecting-from-an-instance-of-sql-server"></a>断开与 SQL Server 实例的连接
[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../../includes/applies-to-version/sql-asdb-asdbmi-asdw.md)]

  不需要手动关闭和断开 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 管理对象 (SMO) 对象。 系统会根据需要打开和关闭连接。  
  
## <a name="connection-pooling"></a>连接池  
 调用[Connect](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.connectionmanager.connect)方法时，不会自动释放连接。 必须显式调用[Disconnect](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.connectionmanager.disconnect)方法才能释放到连接池的连接。 您还可以请求不加入连接池的连接。 可以通过设置[NonPooledConnection](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.connectionsettings.nonpooledconnection) <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> 引用[microsoft.sqlserver.management.common.serverconnection>](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.serverconnection.aspx)对象的属性的 NonPooledConnection 属性来执行此操作。  
  
## <a name="disconnecting-from-an-instance-of-sql-server-for-rmo"></a>断开 RMO 的 SQL Server 实例连接  
 在使用 RMO 进行编程时，关闭服务器连接的操作过程与使用 SMO 时略有不同。  
  
 由于 RMO 对象的服务器连接由[microsoft.sqlserver.management.common.serverconnection>](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.serverconnection.aspx)对象维护，因此当 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 你使用 RMO 进行编程时，当与的实例断开连接时，也会使用此对象。 若要使用[microsoft.sqlserver.management.common.serverconnection>](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.serverconnection.aspx)对象关闭连接，请调用 RMO 对象的[断开](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.connectionmanager.disconnect)连接方法。 在关闭连接之后，无法再使用 RMO 对象。  
  
## <a name="example"></a>示例  
若要使用所提供的任何代码示例，您必须选择创建应用程序所需的编程环境、编程模板和编程语言。 有关详细信息，请参阅[在 Visual Studio .net 中创建 Visual C&#35; SMO 项目](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)。  
 
  
## <a name="closing-and-disconnecting-an-smo-object-in-visual-basic"></a>在 Visual Basic 中关闭和断开 SMO 对象  
 此代码示例演示如何通过设置对象属性的[NonPooledConnection](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.connectionsettings.nonpooledconnection)属性来请求非池连接 <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> 。  
  
```VBNET
Dim srv As Server
srv = New Server
'Disable automatic disconnection.
srv.ConnectionContext.AutoDisconnectMode = AutoDisconnectMode.NoAutoDisconnect
'Connect to the local, default instance of SQL Server.
srv.ConnectionContext.Connect()
'The actual connection is made when a property is retrieved.
Console.WriteLine(srv.Information.Version)
'Disconnect explicitly.
srv.ConnectionContext.Disconnect()
```
  
## <a name="closing-and-disconnecting-an-smo-object-in-visual-c"></a>在 Visual C# 中关闭和断开 SMO 对象  
 此代码示例演示如何通过设置对象属性的[NonPooledConnection](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.connectionsettings.nonpooledconnection)属性来请求非池连接 <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> 。  
  
```csharp  
{   
Server srv;   
srv = new Server();   
//Disable automatic disconnection.   
srv.ConnectionContext.AutoDisconnectMode = AutoDisconnectMode.NoAutoDisconnect;   
//Connect to the local, default instance of SQL Server.   
srv.ConnectionContext.Connect();   
//The actual connection is made when a property is retrieved.   
Console.WriteLine(srv.Information.Version);   
//Disconnect explicitly.   
srv.ConnectionContext.Disconnect();  
}  
```  
  
## <a name="see-also"></a>另请参阅  
 <xref:Microsoft.SqlServer.Management.Smo.Server>   
 [Microsoft.sqlserver.management.common.serverconnection>](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.serverconnection.aspx)  
  
  
