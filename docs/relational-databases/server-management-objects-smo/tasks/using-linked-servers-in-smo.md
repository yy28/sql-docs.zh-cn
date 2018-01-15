---
title: "在 SMO 中使用链接的服务器 |Microsoft 文档"
ms.custom: 
ms.date: 08/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: smo
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords: linked servers [SQL Server], SMO
ms.assetid: 0ea8837b-2596-4df1-b065-3bb717c9f22c
caps.latest.revision: "36"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 53a4b6d33d1413673f4991fcaf0f4ce3687a2712
ms.sourcegitcommit: cb2f9d4db45bef37c04064a9493ac2c1d60f2c22
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/12/2018
---
# <a name="using-linked-servers-in-smo"></a>在 SMO 中使用链接服务器
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  链接服务器表示远程服务器上的 OLE DB 数据源。 远程 OLE DB 数据源链接到的实例[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]使用<xref:Microsoft.SqlServer.Management.Smo.LinkedServer>对象。  
  
 远程数据库服务器可以链接到当前实例的[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]使用 OLE DB 访问接口。 在 SMO 中，链接的服务器由表示<xref:Microsoft.SqlServer.Management.Smo.LinkedServer>对象。 <xref:Microsoft.SqlServer.Management.Smo.LinkedServer.LinkedServerLogins%2A>属性引用的集合<xref:Microsoft.SqlServer.Management.Smo.LinkedServerLogin>对象。 这些对象存储建立与链接服务器的连接所需的登录凭据。  
  
## <a name="ole-db-providers"></a>OLE-DB 访问接口  
 在 SMO 中，已安装的 OLE-DB 访问接口由 <xref:Microsoft.SqlServer.Management.Smo.OleDbProviderSettings> 对象的集合表示。  
  
## <a name="example"></a>示例  
 对于下列代码示例，您必须选择编程环境、编程模板和编程语言才能创建应用程序。 有关详细信息，请参阅[创建 Visual C &#35;Visual Studio.NET 中的 SMO 项目](../../../relational-databases/server-management-objects-smo/how-to-create-a-visual-csharp-smo-project-in-visual-studio-net.md)。  
  
## <a name="creating-a-link-to-an-ole-db-provider-server-in-visual-c"></a>在 Visual C# 中创建指向 OLE-DB 访问接口服务器的链接  
 代码示例演示如何创建一个链接[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]OLE DB，通过使用异类数据源<xref:Microsoft.SqlServer.Management.Smo.LinkedServer>对象。 通过指定[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]作为产品名称中，数据链接服务器上使用访问[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Client OLE DB 访问接口，这是正式 OLE DB 访问接口为[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
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
 代码示例演示如何创建一个链接[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]OLE DB，通过使用异类数据源<xref:Microsoft.SqlServer.Management.Smo.LinkedServer>对象。 通过指定[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]作为产品名称中，数据链接服务器上使用访问[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Client OLE DB 访问接口，这是正式 OLE DB 访问接口为[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]。  
  
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
  
  
