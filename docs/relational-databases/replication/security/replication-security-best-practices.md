---
title: 复制安全最佳做法 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- security [SQL Server replication], best practices
- security [SQL Server replication], between domains
- authentication [SQL Server replication]
- Internet [SQL Server replication], security
ms.assetid: 1ab2635d-0992-4c99-b17d-041d02ec9a7c
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: cbda6137d9b844b13485c63488fad9efa85366c7
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/09/2019
ms.locfileid: "54131557"
---
# <a name="replication-security-best-practices"></a>复制安全最佳实践
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  复制在分布式环境（从单个域中的 Intranet 到在不受信任的域之间通过 Internet 访问数据的应用程序）中移动数据。 理解在这些不同环境下保护复制连接的最佳方法非常重要。  
  
 下面是在所有环境中均与复制相关的信息：  
  
-   使用行业标准方法 [如虚拟专用网络 (VPN)、安全套接字层 (SSL) 或 IP 安全 (IPSEC)] 加密复制拓扑中计算机间的连接。 有关详细信息，请参阅[启用数据库引擎的加密连接（SQL Server 配置管理器）](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)。 有关使用 VPN 和 SSL 在 Internet 上复制数据的信息，请参阅 [Securing Replication Over the Internet](../../../relational-databases/replication/security/securing-replication-over-the-internet.md)。  
  
     如果使用 SSL 来确保复制拓扑中计算机间的连接安全，请为每个复制代理的 **-EncryptionLevel** 参数指定值 **1** 或 **2** （建议指定值 **2** ）。 值 **1** 指定使用加密，但是代理不验证 SSL 服务器证书是否由可信颁发者签名；值 **2** 指定证书要经过验证。 代理参数可以在代理配置文件和命令行中指定。 有关详细信息，请参阅：  
  
    -   [处理复制代理配置文件](../../../relational-databases/replication/agents/work-with-replication-agent-profiles.md)  
  
    -   [查看和修改复制代理命令提示符参数 &#40;SQL Server Management Studio&#41;](../../../relational-databases/replication/agents/view-and-modify-replication-agent-command-prompt-parameters.md)  
  
    -   [Replication Agent Executables Concepts](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md)  
  
-   以不同的 Windows 帐户运行每个复制代理，并对所有复制代理连接使用 Windows 身份验证。 有关指定帐户的详细信息，请参阅[复制的标识和访问控制](../../../relational-databases/replication/security/identity-and-access-control-replication.md)。  
  
-   仅对每个代理授予其所需的权限。 有关详细信息，请参阅 [Replication Agent Security Model](../../../relational-databases/replication/security/replication-agent-security-model.md)中的“代理所需权限”部分。  
  
-   确保所有合并代理和分发代理帐户均在发布访问列表 (PAL) 中。 有关详细信息，请参阅[保护发布服务器](../../../relational-databases/replication/security/secure-the-publisher.md)。  
  
-   遵循最小权限原则，仅对 PAL 中的帐户授予其执行复制任务所需的权限。 不要向复制不需要的任何固定服务器角色添加登录帐户。  
  
-   配置快照共享，以允许所有合并代理和分发代理进行读访问。 对于具有参数化筛选器的发布的快照，请确保将每个文件夹配置为仅允许相应的合并代理帐户进行访问。  
  
-   配置快照共享，以允许快照代理进行写权限。  
  
-   如果使用的是请求订阅，请为快照文件夹使用网络共享，而不要使用本地路径。  
  
 如果复制拓扑中包含的计算机位于不同的域中，或位于彼此未建立信任关系的域中，则可以对代理建立的连接使用 Windows 身份验证或 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 身份验证（有关域的详细信息，请参阅 Windows 文档）。 建议使用 Windows 身份验证作为最佳安全配置。  
  
-   使用 Windows 身份验证：  
  
    -   为适当节点处的每个代理添加一个本地 Windows 帐户（而非域帐户），在每个节点都使用同一名称和密码。 例如，推送订阅的分发代理在分发服务器上运行，并与分发服务器和订阅服务器建立连接。 应将分发代理的 Windows 帐户添加到分发服务器和订阅服务器。  
  
    -   确保给定代理（例如订阅的分发代理）在每台计算机上都以同一帐户运行。  
  
-   使用 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 身份验证：  
  
    -   为适当节点处的每个代理添加一个 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 帐户，在每个节点都使用同一名称和密码。 例如，推送订阅的分发代理在分发服务器上运行，并与分发服务器和订阅服务器建立连接。 应将分发代理的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 帐户添加到分发服务器和订阅服务器。  
  
    -   确保给定代理（例如订阅的分发代理）在每台计算机上都以同一帐户建立连接。  
  
    -   需要 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 身份验证时，UNC 快照共享通常无法访问（例如，防火墙可能阻止访问）。 在这种情况下，可以通过文件传输协议 (FTP) 将快照传输到订阅服务器。 有关详细信息，请参阅[通过 FTP 传输快照](../../../relational-databases/replication//publish/deliver-a-snapshot-through-ftp.md)。  
  
## <a name="see-also"></a>另请参阅  
 [启用数据库引擎的加密连接（SQL Server 配置管理器）](../../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)   
 [通过 Internet 复制](../../../relational-databases/replication/replication-over-the-internet.md)   
 [保护订阅服务器](../../../relational-databases/replication/security/secure-the-subscriber.md)   
 [保护分发服务器](../../../relational-databases/replication/security/secure-the-distributor.md)   
 [保护发布服务器](../../../relational-databases/replication/security/secure-the-publisher.md)   
 [查看和修改复制安全设置](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)  
  
  
