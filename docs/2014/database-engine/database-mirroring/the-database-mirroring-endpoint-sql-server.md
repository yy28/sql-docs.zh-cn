---
title: 数据库镜像端点 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- database mirroring [SQL Server], deployment
- database mirroring [SQL Server], endpoint
- endpoints [SQL Server], AlwaysOn Availability Groups
- endpoints [SQL Server], database mirroring
- Availability Groups [SQL Server], endpoint
ms.assetid: 39332dc5-678e-4650-9217-6aa3cdc41635
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: c18c22cf4db3f442050c739aaf68e159fd1cc230
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62754660"
---
# <a name="the-database-mirroring-endpoint-sql-server"></a>数据库镜像端点 (SQL Server)
  若要参与 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 或数据库镜像，服务器实例需要有自己专用的“数据库镜像端点”  。 此端点用途特殊，专门用于接收来自其他服务器实例的这些连接。 在某一给定服务器实例上，与任何其他服务器实例的每个 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 或数据库镜像连接都使用单个数据库镜像端点。  
  
 数据库镜像端点使用传输控制协议 (TCP) 在参与数据库镜像会话或承载可用性副本的服务器实例之间发送和接收消息。 数据库镜像端点在唯一的 TCP 端口号上进行侦听。  
  
> [!NOTE]  
>  客户端与主体服务器或主副本的连接不使用数据库镜像端点。  
  
> [!NOTE]  
>  后续版本的 Microsoft SQL Server 将删除数据库镜像功能。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用数据库镜像的应用程序，以便改用 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 。  
  
  
##  <a name="ServerNetworkAddress"></a> 服务器网络地址  
 服务器实例的网络地址（其“服务器网络地址”  或“终结点 URL”  ）包含其端点的端口号，以及主机的系统名称和域名。 端口号唯一标识特定的服务器实例。  
  
 下图具体说明了如何将同一服务器上的两个服务器实例进行唯一标识。 两个服务器实例的服务器网络地址均包含相同的系统名称 `MYSYSTEM`和域名 `Adventure-Works.MyDomain.com`。 若要使系统能够路由到服务器实例的连接，服务器网络地址需要包括与特定服务器实例的镜像端点相关联的端口号。  
  
 ![默认实例的服务器网络地址](../media/dbm-2-instances-ports-1-system.gif "默认实例的服务器网络地址")  
  
 默认情况下， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例不包含数据库镜像端点。 在建立数据库镜像会话时，必须手动创建它们。 系统管理员必须在将要参与数据库镜像的每个服务器实例中分别创建端点。 请注意，如果某一给定计算机上的多个服务器实例要求数据库镜像端点，则为每个端点都指定不同的端口号。  
  
> [!IMPORTANT]  
>  如果运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的计算机具有防火墙，则防火墙配置必须允许端点中指定的端口的传入和发送连接。  
  
 对于数据库镜像和 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]，身份验证和加密在端点配置。 有关详细信息，请参阅[针对数据库镜像和 AlwaysOn 可用性组的传输安全性&#40;SQL Server&#41;](transport-security-database-mirroring-always-on-availability.md)。  
  
> [!IMPORTANT]  
>  请勿重新配置正在使用的数据库镜像端点。 服务器实例使用彼此的端点来了解其他系统的状态。 如果重新配置端点，则可能会重新启动此端点，从而导致其他服务器实例出现错误。 这对于自动故障转移模式尤为重要，在此模式下，在伙伴上重新配置端点可能会导致故障转移。  
  
  
##  <a name="EndpointAuthenticationTypes"></a> 为数据库镜像端点确定身份验证类型  
 理解您的服务器实例的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务帐户将确定您可以将何种类型的身份验证用于数据库镜像端点十分重要，下面将阐释这一点：  
  
-   如果每个服务器实例都在某一域服务帐户下运行，则您可以将 Windows 身份验证用于您的数据库镜像端点。 如果所有服务器实例使用相同的域用户帐户运行，则正确的用户登录名将自动存在于全部两个 **master** 数据库中。 这样可简化可用性数据库的安全配置并建议这样做。  
  
     如果为某一可用性组托管可用性副本的任何服务器实例以不同的帐户身份运行，则必须在其他服务器实例上的 **master** 中创建每个登录帐户。 然后，必须向该登录名授予 CONNECT 权限，以便连接到该服务器实例的数据库镜像端点。 有关详细信息[设置的登录帐户的数据库镜像或 AlwaysOn 可用性组&#40;SQL Server&#41;](set-up-login-accounts-database-mirroring-always-on-availability.md)。  
  
     如果您的服务器实例使用 Windows 身份验证，则您可以通过使用 [!INCLUDE[tsql](../../includes/tsql-md.md)]、PowerShell 或新建可用性组向导创建数据库镜像端点。  
  
    > [!NOTE]  
    >  如果要承载可用性副本的服务器实例缺少数据库镜像端点，则新建可用性组向导可以自动创建使用 Windows 身份验证的数据库镜像端点。 有关详细信息，请参阅[使用可用性组向导 (SQL Server Management Studio)](../availability-groups/windows/use-the-availability-group-wizard-sql-server-management-studio.md)。  
  
-   如果任何服务器实例正在以内置帐户（例如 Local System、Local Service 或 Network Service）或非域帐户运行，则您必须使用证书来进行端点身份验证。 如果您正在使用证书来用于您的数据库镜像端点，则您的系统管理员必须配置每个服务器实例，以在出站连接和进站连接中使用证书。  
  
     没有使用证书来配置数据库镜像安全性的任何自动方法。 您将需要使用 CREATE ENDPOINT [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句或 `New-SqlHadrEndpoint` PowerShell cmdlet。 有关详细信息，请参阅 [CREATE ENDPOINT (Transact-SQL)](/sql/t-sql/statements/create-endpoint-transact-sql)的信息。 有关启用证书身份验证服务器实例上的信息，请参阅[数据库镜像终结点使用证书&#40;TRANSACT-SQL&#41;](use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)。  
  
  
##  <a name="RelatedTasks"></a> 相关任务  
 **配置数据库镜像端点**  
  
-   [为 Windows 身份验证创建数据库镜像终结点 (Transact-SQL)](create-a-database-mirroring-endpoint-for-windows-authentication-transact-sql.md)  
  
-   [使用数据库镜像终结点证书 (Transact-SQL)](use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)  
  
    -   [允许数据库镜像终结点使用证书进行出站连接 (Transact-SQL)](database-mirroring-use-certificates-for-outbound-connections.md)  
  
    -   [允许数据库镜像终结点将证书用于入站连接 (Transact-SQL)](database-mirroring-use-certificates-for-inbound-connections.md)  
  
-   [指定服务器网络地址（数据库镜像）](specify-a-server-network-address-database-mirroring.md)  
  
-   [在添加或修改可用性副本时指定终结点 URL (SQL Server)](../availability-groups/windows/specify-endpoint-url-adding-or-modifying-availability-replica.md)  
  
-   [使用可用性组向导 (SQL Server Management Studio)](../../ssms/sql-server-management-studio-ssms.md)  
  
 **查看有关数据库镜像端点的信息**  
  
-   [sys.database_mirroring_endpoints (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql)  
  
  
## <a name="see-also"></a>请参阅  
 [传输安全模式的数据库镜像和 AlwaysOn 可用性组&#40;SQL Server&#41;](transport-security-database-mirroring-always-on-availability.md)   
 [数据库镜像配置故障排除 (SQL Server)](troubleshoot-database-mirroring-configuration-sql-server.md)   
 [sys.dm_hadr_availability_replica_states &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-hadr-availability-replica-states-transact-sql)   
 [sys.dm_db_mirroring_connections &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/database-mirroring-sys-dm-db-mirroring-connections)  
  
  
