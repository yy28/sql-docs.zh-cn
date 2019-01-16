---
title: 使用 TCP IP 创建有效的连接字符串 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- connection strings [Database Engine]
- ports [SQL Server], connecting to
- TCP/IP [SQL Server], connection strings
- connection strings [Database Engine], TCP/IP
- aliases [SQL Server], TCP/IP
ms.assetid: ee5dbc2c-1fc6-42bd-bdf5-efa792557934
author: stevestein
ms.author: sstein
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
manager: craigg
ms.openlocfilehash: a237fcd5b03f8013e4a6514b87322695e6a0cf9a
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 12/11/2018
ms.locfileid: "53206166"
---
# <a name="creating-a-valid-connection-string-using-tcp-ip"></a>使用 TCP IP 创建有效的连接字符串
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]
  若要使用 TCP/IP 来创建有效的连接字符串，必须执行以下操作：  
  
-   指定 **“别名”**。  
  
-   在 **“服务器”** 框中，输入可以使用 **PING** 实用工具连接到的服务器名称或可以使用 **PING** 实用工具连接到的 IP 地址。 对于命名实例，请追加实例名称。  
  
-   在 **“协议”** 框中指定 **TCP/IP**。  
  
-   在 **“端口号”** 框中输入端口号（可选）。 默认端口号为 1433，这是服务器上默认的 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 实例的端口号。 若要连接到命名实例或未侦听端口 1433 的默认实例，则必须提供端口号，或者启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服务。 有关配置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服务的信息，请参阅 [SQL Server Browser 服务](../../tools/configuration-manager/sql-server-browser-service.md)。  
  
 连接时， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 组件将从指定别名的注册表中读取服务器、协议和端口的值，然后创建一个格式为 `tcp:<servername>[\<instancename>],<port>` 或 `tcp:<IPAddress>[\<instancename>],<port>`的连接字符串。  
  
> [!NOTE]
>  默认情况下， [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 防火墙关闭端口 1433。 由于 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 通过端口 1433 进行通信，因此，如果你将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置为使用 TCP/IP 侦听传入客户端连接，则必须重新打开该端口。 有关配置防火墙的信息，请参阅“如何为 SQL Server Access 配置防火墙”（[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 联机丛书中）或查看你的防火墙文档。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 完全支持 Internet 协议版本 4 (IPv4) 和 Internet 协议版本 6 (IPv6)。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器接受 IPv4 和 IPv6 格式的 IP 地址。 有关 IPv6 的信息，请参阅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 联机丛书中的“使用 IPv6 进行连接”。  
  
## <a name="connecting-to-the-local-server"></a>连接到本地服务器  
 当连接与客户端运行在同一台计算机上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 时，可以使用 `(local)` 作为服务器名称。 由于上述方法不明确，因此不建议使用，但是当客户端运行在已知的计算机上时，该方法还是有用的。 例如，当为断开连接的移动用户（如销售人员，其 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将运行在便携式计算机上并存储相应的项目数据）创建应用程序时，连接到 `(local)` 的客户端就可以始终与运行在便携式计算机上的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 保持连接。 可以使用词语 `localhost` 或句点 (**.**) 来取代 `(local)`。  
  
## <a name="verifying-your-connection-protocol"></a>验证连接协议  
 以下查询将返回当前连接所使用的协议。  
  
```  
SELECT net_transport   
FROM sys.dm_exec_connections   
WHERE session_id = @@SPID;  
  
```  
  
## <a name="examples"></a>示例  
 通过服务器名称进行连接：  
  
```  
Alias Name         <serveralias>  
Port No            <blank>  
Protocol           TCP/IP  
Server             <servername>  
  
```  
  
 通过服务器名称连接到已命名的实例：  
  
```  
Alias Name         <serveralias>  
Port No            <blank>  
Protocol           TCP/IP  
Server             <servername>\<instancename>  
  
```  
  
 通过服务器名称连接到指定的端口：  
  
```  
Alias Name         <serveralias>  
Port No            <port>  
Protocol           TCP/IP  
Server             <servername>  
  
```  
  
 通过 IP 地址进行连接：  
  
```  
Alias Name         <serveralias>  
Port No            <blank>  
Protocol           TCP/IP  
Server             <IPAddress>  
  
```  
  
 通过 IP 地址连接到命名实例：  
  
```  
Alias Name         <serveralias>  
Port No            <blank>  
Protocol           TCP/IP  
Server             <IPAddress>\<instancename>  
  
```  
  
 通过 IP 地址连接到指定的端口：  
  
```  
Alias Name         <serveralias>  
Port No            <port number>  
Protocol           TCP/IP  
Server             <IPAddress>  
  
```  
  
 使用 `(local)`连接到本地计算机：  
  
```  
Alias Name         <serveralias>  
Port No            <blank>  
Protocol           TCP/IP  
Server             (local)  
  
```  
  
 使用 `localhost`连接到本地计算机：  
  
```  
Alias Name         <serveralias>  
Port No            <blank>  
Protocol           TCP/IP  
Server             localhost  
  
```  
  
 连接到本地计算机 `localhost`上的命名实例：  
  
```  
Alias Name         <serveralias>  
Port No            <blank>  
Protocol           TCP/IP  
Server             localhost\<instancename>  
  
```  
  
 使用句点连接到本地计算机：  
  
```  
Alias Name         <serveralias>  
Port No            <blank>  
Protocol           TCP/IP  
Server             .  
  
```  
  
 使用句点连接到本地计算机上的命名实例：  
  
```  
Alias Name         <serveralias>  
Port No            <blank>  
Protocol           TCP/IP  
Server             .\<instancename>  
  
```  
  
> [!NOTE]  
>  有关以 sqlcmd 参数的形式指定网络协议的信息，请参阅“如何：使用 sqlcmd.exe 连接到数据库引擎”（[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 联机丛书中）。  
  
## <a name="see-also"></a>另请参阅  
 [使用 Shared Memory 协议创建有效的连接字符串](../../tools/configuration-manager/creating-a-valid-connection-string-using-shared-memory-protocol.md)   
 [使用 Named Pipes 创建有效的连接字符串](https://msdn.microsoft.com/library/90930ff2-143b-4651-8ae3-297103600e4f)   
 [选择网络协议](https://msdn.microsoft.com/library/6565fb7d-b076-4447-be90-e10d0dec359a)  
  
  
