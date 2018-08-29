---
title: 断开与 SQL server 实例 |Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: smo
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Management Objects, disconnecting
- SMO [SQL Server], disconnecting
- instances of SQL Server, disconnecting
- disconnecting [SMO]
ms.assetid: 4ca7f7eb-6b3f-4c73-ac63-88afa8570b61
caps.latest.revision: 45
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e8a99d5b82f8901d66c1ad25de5de03694e5b3e1
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43109005"
---
# <a name="disconnecting-from-an-instance-of-sql-server"></a>断开与 SQL Server 实例的连接
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  手动关闭和断开[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]管理对象 (SMO) 对象不是必需的。 系统会根据需要打开和关闭连接。  
  
## <a name="connection-pooling"></a>连接池  
 当[Connect](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.connectionmanager.connect)方法调用时，不会自动释放连接。 [断开连接](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.connectionmanager.disconnect)必须显式调用方法来释放与连接池的连接。 您还可以请求不加入连接池的连接。 执行此操作通过设置[NonPooledConnection](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.connectionsettings.nonpooledconnection)的属性<xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A>属性，引用[ServerConnection](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.serverconnection.aspx)对象。  
  
## <a name="disconnecting-from-an-instance-of-sql-server-for-rmo"></a>断开 RMO 的 SQL Server 实例连接  
 在使用 RMO 进行编程时，关闭服务器连接的操作过程与使用 SMO 时略有不同。  
  
 由于对 RMO 对象的服务器连接由维护[ServerConnection](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.serverconnection.aspx)对象的实例中断开连接时也会使用此对象[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]使用 RMO 进行编程。 若要关闭的连接通过使用[ServerConnection](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.serverconnection.aspx)对象，请调用[断开连接](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.connectionmanager.disconnect)RMO 对象的方法。 在关闭连接之后，无法再使用 RMO 对象。  
  
## <a name="example"></a>示例  
若要使用所提供的任何代码示例，您必须选择创建应用程序所需的编程环境、编程模板和编程语言。 有关详细信息，请参阅[创建 Visual C&#35; Visual Studio.NET 中的 SMO 项目](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)。  
 
  
## <a name="closing-and-disconnecting-an-smo-object-in-visual-basic"></a>在 Visual Basic 中关闭和断开 SMO 对象  
 此代码示例演示如何通过设置请求非池化连接[NonPooledConnection](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.connectionsettings.nonpooledconnection)属性的<xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A>对象属性。  
  
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
 此代码示例演示如何通过设置请求非池化连接[NonPooledConnection](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.connectionsettings.nonpooledconnection)属性的<xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A>对象属性。  
  
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
  
## <a name="see-also"></a>请参阅  
 <xref:Microsoft.SqlServer.Management.Smo.Server>   
 [ServerConnection](https://msdn.microsoft.com/library/microsoft.sqlserver.management.common.serverconnection.aspx)  
  
  
