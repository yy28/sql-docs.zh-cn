---
title: 断开的 SQL Server 实例 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Management Objects, disconnecting
- SMO [SQL Server], disconnecting
- instances of SQL Server, disconnecting
- disconnecting [SMO]
ms.assetid: 4ca7f7eb-6b3f-4c73-ac63-88afa8570b61
caps.latest.revision: 43
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 1f2ce4ae7ce42df42be9b6bc68c3d13acf949dba
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36125299"
---
# <a name="disconnecting-from-an-instance-of-sql-server"></a>断开与 SQL Server 实例的连接
  手动关闭和断开[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]管理对象 (SMO) 对象不是必需的。 系统会根据需要打开和关闭连接。  
  
## <a name="connection-pooling"></a>连接池  
 当<xref:Microsoft.SqlServer.Management.Common.ConnectionManager.Connect%2A>方法调用，该连接不会被自动释放。 必须显式调用 <xref:Microsoft.SqlServer.Management.Common.ConnectionManager.Disconnect%2A> 方法才能释放与连接池的连接。 您还可以请求不加入连接池的连接。 通过设置引用 <xref:Microsoft.SqlServer.Management.Common.ConnectionSettings.NonPooledConnection%2A> 对象的 <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A> 属性的 <xref:Microsoft.SqlServer.Management.Common.ServerConnection> 属性，可以实现此目的。  
  
## <a name="disconnecting-from-an-instance-of-sql-server-for-rmo"></a>断开 RMO 的 SQL Server 实例连接  
 在使用 RMO 进行编程时，关闭服务器连接的操作过程与使用 SMO 时略有不同。  
  
 因为由维护 RMO 对象的服务器连接<xref:Microsoft.SqlServer.Management.Common.ServerConnection>对象，断开的实例时，也会使用此对象[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]您通过使用 RMO 进行编程时。 若要关闭的连接通过使用<xref:Microsoft.SqlServer.Management.Common.ServerConnection>对象，请调用<xref:Microsoft.SqlServer.Management.Common.ConnectionManager.Disconnect%2A>RMO 对象的方法。 在关闭连接之后，无法再使用 RMO 对象。  
  
## <a name="example"></a>示例  
 [!INCLUDE[ssChooseProgEnv](../../../includes/sschooseprogenv-md.md)]  
  
## <a name="closing-and-disconnecting-an-smo-object-in-visual-basic"></a>在 Visual Basic 中关闭和断开 SMO 对象  
 此代码示例演示如何通过设置请求非共用连接<xref:Microsoft.SqlServer.Management.Common.ConnectionSettings.NonPooledConnection%2A>属性<xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A>对象属性。  
  
<!-- TODO: review snippet reference  [!CODE [SMO How to#SMO_VB4](SMO How to#SMO_VB4)]  -->  
  
## <a name="closing-and-disconnecting-an-smo-object-in-visual-c"></a>在 Visual C# 中关闭和断开 SMO 对象  
 此代码示例演示如何通过设置请求非共用连接<xref:Microsoft.SqlServer.Management.Common.ConnectionSettings.NonPooledConnection%2A>属性<xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A>对象属性。  
  
```  
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
 <xref:Microsoft.SqlServer.Management.Common.ServerConnection>  
  
  