---
title: 登录到 SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- SQL Server, logging in
- services [SQL Server], logging in
- TCP connection string
- connecting to the Database Engine
- logins [SQL Server], about logging in
- named pipe connection string
- log ins [SQL Server]
- shared memory connection string
- logging in [SQL Server]
- logins [SQL Server]
ms.assetid: 77158a9a-d638-4818-90a1-cb2eb57df514
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 35366fbbeac73a551546f2778592f03da5c7e1e7
ms.sourcegitcommit: c19696d3d67161ce78aaa5340964da3256bf602d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/29/2018
ms.locfileid: "52617667"
---
# <a name="logging-in-to-sql-server"></a>登录到 SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  使用任何图形管理工具或从命令提示符处，都可以登录到 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。  
  
 使用图形管理工具（如 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ）登录到 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]实例时，系统将会提示您提供服务器名称、 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名和密码（如果需要）。 如果使用 Windows 身份验证登录到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，则不必在每次访问 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]实例时都提供 SQL Server 登录名。 相反地， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将使用您的 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 帐户自动登录。 如果在混合模式身份验证（ [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和Windows 身份验证模式）下运行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，并选择使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证登录，则必须提供 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名和密码。 请尽可能使用 Windows 身份验证。  
  
> [!NOTE]  
>  如果安装 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]时选择了区分大小写的排序规则，则您的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 登录名也将区分大小写。  
  
## <a name="format-for-specifying-the-name-of-sql-server"></a>指定 SQL Server 名称的格式  
 连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 实例时，必须指定 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例的名称。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例是默认实例（未命名实例），则指定安装了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的计算机的名称或该计算机的 IP 地址。 如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例是命名实例（如 SQLEXPRESS），则指定安装了 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的计算机的名称或该计算机的 IP 地址，并添加斜杠和实例名称。  
  
 以下示例连接到名为 APPHOST 的计算机上运行的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例。 指定命名实例时，这些示例使用实例名称 SQLEXPRESS。  
  
 **示例：**  
  
|实例类型|服务器名称条目|  
|----------------------|-------------------------------|  
|连接到使用默认协议的默认实例。|APPHOST|  
|连接到使用默认协议的命名实例。 |APPHOST\SQLEXPRESS|  
|连接到同一计算机上的默认实例，该计算机使用期间来指示该实例在本地计算机上运行。|实例时都提供 SQL Server 登录名。|  
|连接到同一计算机上的命名实例，该计算机使用期间来指示该实例在本地计算机上运行。|.\SQLEXPRESS|  
|连接到同一计算机上的默认实例，该计算机使用 localhost 指示该实例在本地计算机上运行。|localhost|  
|连接到同一计算机上的命名实例，该计算机使用 localhost 指示该实例在本地计算机上运行。|localhost\SQLEXPRESS|  
|连接到同一计算机上的默认实例，该计算机使用 (local) 指示该实例在本地计算机上运行。|(local)|  
|连接到同一计算机上的命名实例，该计算机使用 (local) 指示该实例在本地计算机上运行。|(local)\SQLEXPRESS|  
|连接到强制共享内存连接的同一计算机上的默认实例。|lpc:APPHOST|  
|连接到强制共享内存连接的同一计算机上的命名实例。|lpc:APPHOST\SQLEXPRESS|  
|连接到使用 IP 地址侦听 TCP 地址 192.168.17.28 的默认实例。|192.168.17.28|  
|连接到使用 IP 地址侦听 TCP 地址 192.168.17.28 的命名实例。|192.168.17.28\SQLEXPRESS|  
|通过指定正在使用的端口（此情况下为 2828）连接到未在侦听默认 TCP 端口的默认实例。 （如果 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 正在侦听默认端口 (1433)，则不需要指定端口号。）|APPHOST,2828|  
|连接到指定 TCP 端口（此情况下为 2828）上的命名实例。 （如果 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服务未在主机上运行，则通常需要指定端口号。）|APPHOST,2828|  
|通过同时指定正在使用的 IP 地址和 TCP 端口（在此情况下为 2828）连接到未在侦听默认 TCP 端口的默认实例。|192.168.17.28,2828|  
|通过同时指定正在使用的 IP 地址和 TCP 端口（在此情况下为 2828）连接到命名实例。|192.168.17.28\SQLEXPRESS,2828|  
|使用名称连接到强制 TCP 连接的默认实例。|tcp:APPHOST|  
|使用名称连接到强制 TCP 连接的命名实例。|tcp:APPHOST\SQLEXPRESS|  
|通过指定命名管道名称连接到默认实例。|\\\APPHOST\pipe\SQL\query|  
|通过指定命名管道名称连接到命名实例。|\\\APPHOST\pipe\MSSQL$SQLEXPRESS\SQL\query|  
|使用名称连接到强制命名管道连接的默认实例。|np:APPHOST|  
|使用名称连接到强制命名管道连接的命名实例。|np:APPHOST\SQLEXPRESS|  
  
## <a name="verifying-your-connection-protocol"></a>验证连接协议  
 连接到 [!INCLUDE[ssDE](../../includes/ssde-md.md)]时，以下查询将返回用于当前连接的协议以及身份验证方法（NTLM 或 Kerberos），并且指示连接是否加密。  
  
```sql  
SELECT net_transport, auth_scheme, encrypt_option   
FROM sys.dm_exec_connections   
WHERE session_id = @@SPID;  
```  
  
## <a name="related-tasks"></a>Related Tasks  
 [登录到 SQL Server 实例（命令提示符）](../../database-engine/configure-windows/log-in-to-an-instance-of-sql-server-command-prompt.md)  
  
 以下资源可以帮助您解决连接问题。  
  
-   [如何排除连接到 SQL Server 数据库引擎时的故障](https://social.technet.microsoft.com/wiki/contents/articles/how-to-troubleshoot-connecting-to-the-sql-server-database-engine.aspx)  
  
-   [解决 SQL 连接问题的步骤](https://blogs.msdn.com/b/sql_protocols/archive/2008/04/30/steps-to-troubleshoot-connectivity-issues.aspx)  
  
## <a name="related-content"></a>相关内容  
 [选择身份验证模式](../../relational-databases/security/choose-an-authentication-mode.md)  
  
 [使用 sqlcmd 实用工具](../../relational-databases/scripting/sqlcmd-use-the-utility.md)  
  
 [创建登录名](../../t-sql/lesson-2-configuring-permissions-on-database-objects.md)
  
  
