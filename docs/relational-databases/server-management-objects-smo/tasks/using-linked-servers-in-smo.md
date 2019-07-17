---
title: 在 SMO 中使用链接的服务器 |Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- linked servers [SQL Server], SMO
ms.assetid: 0ea8837b-2596-4df1-b065-3bb717c9f22c
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a48f7a2baf9ab59a2f08040ebc1df8b058631829
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68030007"
---
# <a name="using-linked-servers-in-smo"></a>在 SMO 中使用链接服务器
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  链接服务器表示远程服务器上的 OLE DB 数据源。 远程 OLE DB 数据源是使用 <xref:Microsoft.SqlServer.Management.Smo.LinkedServer> 对象链接到 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例的。  
  
 可以使用 OLE DB 访问接口将远程数据库服务器链接到当前 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例。 在 SMO 中，链接服务器由 <xref:Microsoft.SqlServer.Management.Smo.LinkedServer> 对象表示。 <xref:Microsoft.SqlServer.Management.Smo.LinkedServer.LinkedServerLogins%2A> 属性引用 <xref:Microsoft.SqlServer.Management.Smo.LinkedServerLogin> 对象的集合。 这些对象存储建立与链接服务器的连接所需的登录凭据。  
  
## <a name="ole-db-providers"></a>OLE-DB 访问接口  
 在 SMO 中，已安装的 OLE-DB 访问接口由 <xref:Microsoft.SqlServer.Management.Smo.OleDbProviderSettings> 对象的集合表示。  
  
## <a name="example"></a>示例  
 对于下列代码示例，您必须选择编程环境、编程模板和编程语言才能创建应用程序。 有关详细信息，请参阅[创建 Visual C&#35; Visual Studio.NET 中的 SMO 项目](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)。  
  
## <a name="creating-a-link-to-an-ole-db-provider-server-in-visual-c"></a>在 Visual C# 中创建指向 OLE-DB 访问接口服务器的链接  
 此代码示例说明如何使用 <xref:Microsoft.SqlServer.Management.Smo.LinkedServer> 对象创建指向异类数据源 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] OLE DB 的链接。 通过指定 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 作为产品名称，使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Client OLE DB 访问接口即可在链接服务器上访问数据，该接口是 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]的正式 OLE DB 访问接口。  
  
```csharp  
//Connect to the local, default instance of SQL Server.   
{   
   Server srv = new Server();   
   //Create a linked server.   
   LinkedServer lsrv = default(LinkedServer);   
   lsrv = new LinkedServer(srv, "OLEDBSRV");   
   //When the product name is SQL Server the remaining properties are   
   //not required to be set.   
   lsrv.ProductName = "SQL Server";   
   lsrv.Create();   
}   
```  
  
## <a name="creating-a-link-to-an-ole-db-provider-server-in-powershell"></a>在 PowerShell 中创建指向 OLE-DB 访问接口服务器的链接  
 此代码示例说明如何使用 <xref:Microsoft.SqlServer.Management.Smo.LinkedServer> 对象创建指向异类数据源 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] OLE DB 的链接。 通过指定 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 作为产品名称，使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Client OLE DB 访问接口即可在链接服务器上访问数据，该接口是 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]的正式 OLE DB 访问接口。  
  
```powershell  
#Get a server object which corresponds to the default instance  
$svr = New-Object -TypeName Microsoft.SqlServer.Management.SMO.Server  
  
#Create a linked server object which corresponds to an OLEDB type of SQL server product  
$lsvr = New-Object -TypeName Microsoft.SqlServer.Management.SMO.LinkedServer -argumentlist $svr,"OLEDBSRV"  
  
#When the product name is SQL Server the remaining properties are not required to be set.   
$lsvr.ProductName = "SQL Server"  
  
#Create the Database Object  
$lsvr.Create()   
```  
  
  
