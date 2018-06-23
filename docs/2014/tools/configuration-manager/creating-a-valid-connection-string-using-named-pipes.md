---
title: 创建有效的连接字符串使用命名的管道 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- configmgr-client
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- connection strings [Database Engine], named pipes
- pipes [SQL Server]
- pipes [SQL Server], connecting to
- aliases [SQL Server], named pipes
- Named Pipes [SQL Server], connection strings
ms.assetid: 90930ff2-143b-4651-8ae3-297103600e4f
caps.latest.revision: 30
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 264c615e38baf39676f1310d6465bfaac2a92785
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36018768"
---
# <a name="creating-a-valid-connection-string-using-named-pipes"></a>使用 Named Pipes 创建有效的连接字符串
  除非由用户更改时的默认实例[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]侦听命名的管道协议，它使用`\\.\pipe\sql\query`作为管道名称。 段指明计算机是本地计算机，`pipe`指示连接是命名的管道和`sql\query`是管道的名称。 若要连接到默认管道，别名必须使用 `\\<computer_name>\pipe\sql\query` 作为管道名称。 如果已将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置为侦听其他管道，则管道名称必须使用该管道。 例如，如果[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用`\\.\pipe\unit\app`作为管道，必须使用别名`\\<computer_name>\pipe\unit\app`作为管道名称。  
  
 若要创建一个有效的管道名称，必须执行以下操作：  
  
-   指定 **“别名”**。  
  
-   选择**命名管道**作为**协议**。  
  
-   输入**名称通过管道传递**。 或者，你可以将保留**管道名称**空白和[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]指定后，Configuration Manager 将完成相应的管道名称**协议**和**服务器**  
  
-   指定**服务器**。 对于命名实例，可以提供服务器名称和实例名称。  
  
 连接，次[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端组件读取服务器、 协议和管道名称从指定的别名的注册表值并创建管道名称格式`np:\\<computer_name>\pipe\<pipename>`或`np:\\<IPAddress>\pipe\<pipename>`。对于命名实例，默认管道名称是`\\<computer_name>\pipe\MSSQL$<instance_name>\sql\query`。  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 防火墙关闭端口 445 默认情况下的。 因为[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]通信通过端口 445，你必须重新打开端口如果[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]配置为侦听传入的客户端连接使用命名的管道。 有关配置防火墙的信息，请参阅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 联机丛书中的“如何将防火墙配置为允许 SQL Server 访问”，或者查阅防火墙文档。  
  
## <a name="connecting-to-the-local-server"></a>连接到本地服务器  
 当连接与客户端运行在同一台计算机上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 时，可以使用 `(local)` 作为服务器名称。 由于上述方法不明确，因此不建议使用 `(local)`，但是当客户端运行在已知的计算机上时，该方法还是有用的。 例如，当为断开连接的移动用户（如销售人员，其 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将运行在便携式计算机上并存储相应的项目数据）创建应用程序时，连接到 (local) 的客户端就可以始终与运行在便携式计算机上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 保持连接。 可以使用词语 `localhost` 或句点 (.) 来取代 `(local)`。  
  
## <a name="verifying-your-connection-protocol"></a>验证连接协议  
 以下查询将返回当前连接所使用的协议。  
  
```  
SELECT net_transport   
FROM sys.dm_exec_connections   
WHERE session_id = @@SPID;  
  
```  
  
## <a name="examples"></a>示例  
 通过服务器名称连接到默认管道：  
  
```  
Alias Name         <serveralias>  
Pipe Name          <blank>  
Protocol           Named Pipes  
Server             <servername>  
  
```  
  
 通过 IP 地址连接到默认管道：  
  
```  
Alias Name         <serveralias>  
Pipe Name          <leave blank>  
Protocol           Named Pipes  
Server             <IPAddress>  
  
```  
  
 通过服务器名称连接到非默认管道：  
  
```  
Alias Name         <serveralias>  
Pipe Name          \\<servername>\pipe\unit\app  
Protocol           Named Pipes  
Server             <servername>  
  
```  
  
 通过服务器名称连接到已命名的实例：  
  
```  
Alias Name         <serveralias>  
Pipe Name          \\<servername>\pipe\MSSQL$<instancename>\SQL\query  
Protocol           Named Pipes  
Server             <servername>  
  
```  
  
 使用 `localhost`连接到本地计算机：  
  
```  
Alias Name         <serveralias>  
Pipe Name          <blank>  
Protocol           Named Pipes  
Server             localhost  
  
```  
  
 使用句点连接到本地计算机：  
  
```  
Alias Name         <serveralias>  
Pipe Name          <left blank>  
Protocol           Named Pipes  
Server             .  
  
```  
  
> [!NOTE]  
>  若要指定的网络协议**sqlcmd**参数，请参阅"如何： 连接到数据库引擎使用 sqlcmd.exe"中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]联机丛书。  
  
## <a name="see-also"></a>请参阅  
 [创建有效的连接字符串使用 Shared 的 Memory 协议](../../../2014/tools/configuration-manager/creating-a-valid-connection-string-using-shared-memory-protocol.md)   
 [使用 TCP IP 创建有效的连接字符串](../../../2014/tools/configuration-manager/creating-a-valid-connection-string-using-tcp-ip.md)   
 [选择网络协议](../../../2014/tools/configuration-manager/choosing-a-network-protocol.md)  
  
  