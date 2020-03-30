---
title: 服务器网络配置 | Microsoft Docs
ms.custom: ''
ms.date: 07/27/2016
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- Named Pipes [SQL Server], configuring
- connections [SQL Server], server network configuration
- Database Engine [SQL Server], network configurations
- server network configuration [SQL Server]
- protocols [SQL Server], choosing
- ports [SQL Server], changing
- server configuration [SQL Server]
ms.assetid: 890c09a1-6dad-4931-aceb-901c02ae34c5
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 826a2b2305354807b6db7bbb167f86d165b98b45
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2020
ms.locfileid: "68025608"
---
# <a name="server-network-configuration"></a>服务器网络配置
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  服务器网络配置任务包括启用协议、修改协议使用的端口或管道、配置加密、配置 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服务、在网络上显示或隐藏 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 以及注册服务器主体名称。 大多数情况下，无须更改服务器网络配置。 只在有特殊的网络要求时才需要重新配置服务器网络协议。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的网络配置是使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器完成的。 对于早期版本的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，请使用这些产品附带的服务器网络实用工具。  
  
## <a name="protocols"></a>协议  
 使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置管理器可以启用或禁用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用的协议，并为这些协议配置可用选项。 可以启用多个协议。 必须启用客户端要使用的所有协议。 所有协议都具有同等的服务器访问权限。 有关应使用何种协议的信息，请参阅 [启用或禁用服务器网络协议](../../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md) 和 [默认 SQL Server 网络协议配置](../../database-engine/configure-windows/default-sql-server-network-protocol-configuration.md)。  
  
### <a name="changing-a-port"></a>更改端口  
 可以配置 TCP/IP 协议以侦听指定的端口。 默认情况下， [!INCLUDE[ssDE](../../includes/ssde-md.md)] 的默认实例侦听 TCP 端口 1433。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 和 [!INCLUDE[ssEW](../../includes/ssew-md.md)] 的命名实例配置为使用动态端口。 这意味着启动 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务时，它们将选择可用的端口。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服务可帮助客户端在连接时识别端口。  
  
 配置为使用动态端口后，在每次启动时 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用的端口可能都会发生变化。 如果通过防火墙连接到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ，则必须打开 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]使用的端口。 将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 配置为使用特定端口，这样就可以将防火墙配置为允许与服务器通信。 有关详细信息，请参阅[将服务器配置为侦听特定 TCP 端口（SQL Sever 配置管理器）](../../database-engine/configure-windows/configure-a-server-to-listen-on-a-specific-tcp-port.md)。  
  
### <a name="changing-a-named-pipe"></a>更改命名管道  
 您可以配置命名管道协议以侦听指定的命名管道。 默认情况下，对于默认实例，[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 的默认实例将侦听管道 \\\\.\pipe\sql\query，而对于命名实例，将侦听管道 \\\\.\pipe\MSSQL$*实例名>\sql\query\<* 。 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 只能侦听一个命名管道，但您可以根据需要将该管道更改为其他名称。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服务可帮助客户端在连接时识别管道。 有关详细信息，请参阅[将服务器配置为侦听更改管道（SQL Sever 配置管理器）](../../database-engine/configure-windows/configure-a-server-to-listen-on-an-alternate-pipe.md)。  
  
## <a name="force-encryption"></a>强行加密  
 可以将[!INCLUDE[ssDE](../../includes/ssde-md.md)]配置为在与客户端应用程序通信时要求加密。 有关详细信息，请参阅[启用数据库引擎的加密连接（SQL Server 配置管理器）](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)。  
  
## <a name="extended-protection-for-authentication"></a>身份验证的扩展保护  
 对于支持扩展保护的操作系统，提供通过使用渠道绑定和服务绑定对针对验证的扩展保护的支持。 有关详细信息，请参阅 [使用扩展保护连接到数据库引擎](../../database-engine/configure-windows/connect-to-the-database-engine-using-extended-protection.md)。  
  
## <a name="authenticating-by-using-kerberos"></a>使用 Kerberos 进行身份验证  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支持 Kerberos 身份验证。 有关详细信息，请参阅 [为 Kerberos 连接注册服务主体名称](../../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md) 和 [Microsoft Kerberos Configuration Manager for SQL Server](https://www.microsoft.com/download/details.aspx?id=39046)  
  
### <a name="registering-a-server-principal-name-spn"></a>注册服务器主体名称 (SPN)  
 Kerberos 身份验证服务使用 SPN 对服务进行身份验证。 有关详细信息，请参阅 [为 Kerberos 连接注册服务主体名称](../../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md)。  
  
 在通过 NTLM 进行连接时，还可以使用 SPN 来使客户端身份验证更安全。 有关详细信息，请参阅 [使用扩展保护连接到数据库引擎](../../database-engine/configure-windows/connect-to-the-database-engine-using-extended-protection.md)。  
  
## <a name="sql-server-browser-service"></a>SQL Server Browser Service  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服务在服务器上运行，可帮助客户端计算机查找 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]的实例。 无需对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 服务进行配置，但是必须采用某些连接方案运行此服务。 有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 的详细信息，请参阅 [SQL Server Browser 服务（数据库引擎和 SSAS）](../../database-engine/configure-windows/sql-server-browser-service-database-engine-and-ssas.md)  
  
## <a name="hiding-sql-server"></a>隐藏 SQL Server  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 在运行时会用每个已安装实例的名称、版本和连接信息来响应查询。 对于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]， **HideInstance** 标志指示 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser 不应对此服务器实例的相关信息做出响应。 客户端应用程序仍然可以连接，但是必须提供所需的连接信息。 有关详细信息，请参阅 [隐藏 SQL Server 数据引擎实例](../../database-engine/configure-windows/hide-an-instance-of-sql-server-database-engine.md)。  
  
## <a name="related-content"></a>相关内容  
 [客户端网络配置](../../database-engine/configure-windows/client-network-configuration.md)  
  
 [管理数据库引擎服务](../../database-engine/configure-windows/manage-the-database-engine-services.md)  
  
  
