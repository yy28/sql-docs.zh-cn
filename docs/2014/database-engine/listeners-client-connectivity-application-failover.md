---
title: 可用性组侦听器、 客户端连接和应用程序故障转移 (SQL Server) |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Availability Groups [SQL Server], listeners
- read-only routing
- read-intent connections [AlwaysOn Availability Groups]
- Availability Groups [SQL Server], configuring
- Availability Groups [SQL Server], read-only routing
- Availability Groups [SQL Server], client connectivity
ms.assetid: 76fb3eca-6b08-4610-8d79-64019dd56c44
caps.latest.revision: 46
author: rothja
ms.author: jroth
manager: jhubbard
ms.openlocfilehash: 90dc94aeebdaa99fe2884dc0874f0c01ec8212cf
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36024972"
---
# <a name="availability-group-listeners-client-connectivity-and-application-failover-sql-server"></a>可用性组侦听器、客户端连接和应用程序故障转移 (SQL Server)
  本主题包含有关 [!INCLUDE[ssHADR](../includes/sshadr-md.md)] 客户端连接和应用程序故障转移功能的注意事项的信息。  
  
> [!NOTE]  
>  对于绝大多数常见的侦听器配置，只需通过使用 [!INCLUDE[tsql](../includes/tsql-md.md)] 语句或 PowerShell cmdlet 即可创建第一个可用性组侦听器。 有关详细信息，请参阅本主题后面的 [相关任务](#RelatedTasks)。  
  
 
  
##  <a name="AGlisteners"></a> 可用性组侦听器  
 您可以通过创建一个可用性组侦听器来提供到给定可用性组的数据库的客户端连接。 可用性组侦听器是一个虚拟网络名称 (VNN)，客户端可连接到此名称以访问 AlwaysOn 可用性组的主副本或辅助副本中的数据库。 可用性组侦听器使客户端无需知道它要连接到的 SQL Server 物理实例的名称，即可连接到某个可用性副本。  无需修改客户端连接字符串，即可连接到当前主副本的当前位置。  
  
 可用性组侦听器由域名系统 (DNS) 侦听器名称、指定的侦听器端口以及一个或多个 IP 地址组成。 可用性组侦听器仅支持 TCP 协议。  在域和 NetBIOS 中，侦听器的 DNS 名称也必须唯一。  当您创建新的可用性组侦听器时，该侦听器将成为群集中的资源，并具有关联的虚拟网络名称 (VNN)、虚拟 IP (VIP) 和可用性组依赖项。 客户端使用 DNS 将 VNN 解析为多个 IP 地址，然后尝试连接到每个地址，直到连接请求成功或超时。  
  
 如果为一个或多个[可读次要副本](availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)配置了只读路由，则将主要副本的读意向客户端连接重定向到可读次要副本。 此外，如果主副本在某个 SQL Server 实例上脱机，且新的主副本在另一个 SQL Server 实例上联机，则可用性组侦听器允许客户端连接到新的主副本。  
  
 有关可用性组侦听程序的基本信息，请参阅 [创建或配置可用性组侦听程序 (SQL Server)](availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)。  
  
 
  
###  <a name="AGlConfig"></a> 可用性组侦听器配置  
 可用性组侦听器由以下各项定义：  
  
 唯一的 DNS 名称  
 这也称为虚拟网络名称 (VNN)。 适用 DNS 主机名的 Active Directory 命名规则。 有关详细信息，请参阅知识库文章： [Active Directory 中计算机、域、站点和 OU 的命名约定](http://support.microsoft.com/kb/909264) 。  
  
 一个或多个虚拟 IP 地址 (VIP)  
 为可用性组可以故障转移到的一个或多个子网配置 VIP。  
  
 IP 地址配置  
 对于给定的可用性组侦听器，IP 地址使用动态主机配置协议 (DHCP) 或者一个或多个静态 IP 地址。  
  
-   动态主机配置协议 (DHCP)  
  
     如果某个可用性组位于单个子网上，您可以将所有可用性组侦听器 IP 地址配置为使用 DHCP。 对于生产前环境，DHCP 为可用性组提供了简单的设置，该可用性组不要求对单独子网上的远程站点进行灾难恢复。 但是，您不应在生产环境中将 DHCP 和可用性组侦听器结合使用。 这是因为在停机情况下，如果 DHCP IP 租期已到，则它需要额外的时间重新注册与侦听器 DNS 名称关联的新 DHCP IP 地址。 这个额外的时间将导致客户端连接失败。  
  
-   静态 IP 地址  
  
     在生产环境中，我们建议可用性组侦听器使用静态 IP 地址。 此外，在可用性组扩展到多子网域中的子网的情况下，可用性组侦听器必须使用静态 IP 地址。  
  
 可用性组侦听器不支持混合网络配置和跨子网 DHCP。 这是因为，当发生故障转移时，动态 IP 可能已过期或被释放，这将会威胁总体高可用性。  
  
###  <a name="SelectListenerPort"></a> 选择可用性组侦听器端口  
 当配置可用性组侦听器时，您必须指定一个端口。  您可以将默认端口配置为 1433，以便允许使用客户端连接字符串以达到简化目的。 如果使用 1433，则无需在连接字符串中指定端口号。   此外，由于每个可用性组侦听器都将具有一个独立的虚拟网络名称，因此，在单个 WSFC 上配置的每个可用性组侦听器都可以配置为引用相同的默认端口 1433。  
  
 还可以指定一个非标准的侦听器端口，但是，这意味着您还需要在连接到可用性组侦听器时，在您的连接字符串中显式指定一个目标端口。  您还需要为非标准端口打开对防火墙的权限。  
  
 如果对可用性组侦听器 VNN 使用默认端口 1433，则仍需要确保群集节点上没有其他服务正在使用此端口；否则将导致端口冲突。  
  
 如果其中一个 SQL Server 实例已正在通过实例侦听器侦听 TCP 端口 1433，且在侦听端口 1433 的计算机上没有任何其他服务（包括其他 SQL Server 实例），则不会与可用性组侦听器的端口导致冲突。  这是因为，可用性组监听器在相同的服务过程中可以共享同一个 TCP 端口。  但是，不应将多个 SQL Server 实例（并行）配置为侦听同一个端口。  
  
##  <a name="ConnectToPrimary"></a> 使用侦听器连接到主副本  
 若要使用可用性组侦听器连接到主副本以进行读写访问，连接字符串应指定可用性组侦听器 DNS 名称。  如果可用性组主副本变为新副本，则将断开使用可用性组侦听器的网络名称的现有连接。  然后，将到可用性组侦听器的新连接定向到新的主副本。 如下所示是针对 ADO.NET 访问接口 (System.Data.SqlClient) 的基本连接字符串的一个示例：  
  
```  
Server=tcp: AGListener,1433;Database=MyDB;IntegratedSecurity=SSPI  
```  
  
 您仍可选择直接引用主副本或辅助副本的 SQL Server 实例名称，而不使用可用性组侦听器服务器名称，但如果您选择这样做，将会丢失新连接（自动定向到当前主副本）的优势。  还将失去只读路由的优势。  
  
##  <a name="ConnectToSecondary"></a> 使用侦听器连接到只读的辅助副本（只读路由）  
 只读路由指的是 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 将到可用性组侦听器的传入连接路由到配置为允许只读工作负荷的次要副本。 如果符合下列要求，则引用可用性组侦听器名称的传入连接可自动路由到只读副本：  
  
-   至少一个辅助副本设置为只读访问，并且每个只读辅助副本和主副本都配置为支持只读路由。 有关详细信息，请参阅 [本节中后面的为只读路由配置可用性副本](#ConfigureARsForROR)。  
  
-   连接字符串引用某一可用性组侦听器，并且将传入连接的应用程序意向设置为只读（例如，使用 ODBC 或 OLEDB 连接字符串或连接特性或属性中的 **Application Intent=ReadOnly** 关键字）。 有关详细信息，请参阅本节后面的 [只读应用程序意向和只读路由](#ReadOnlyAppIntent)。  
  
###  <a name="ConfigureARsForROR"></a> 为只读路由配置可用性副本  
 数据库管理员必须按如下所示配置可用性副本：  
  
1.  对于您要配置为可读取辅助副本的每个可用性副本，数据库管理员都必须配置以下设置，这些设置仅在辅助角色下才会生效：  
  
    -   连接访问权限必须设置为“全部”或者“只读”。  
  
    -   必须指定只读路由 URL。  
  
2.  对于上述每个副本，必须为主角色指定一个只读路由列表。 将一个或多个服务器名称指定为路由目标。  
  
####  <a name="RelatedTasksROR"></a> 相关任务  
  
-   [配置对可用性副本的只读访问 (SQL Server)](availability-groups/windows/configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
-   [为可用性组配置只读路由 (SQL Server)](availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md)  
  
###  <a name="ReadOnlyAppIntent"></a> 只读应用程序意向和只读路由  
 应用程序意向连接字符串属性表示客户端应用程序是要定向到可用性组数据库的读写版本还是只读版本的请求。 若要使用只读路由，在连接到可用性组侦听器时，客户端必须在连接字符串中使用应用程序只读意向。 如果没有只读应用程序意向，则连接到可用性组侦听器将定向到主副本上的数据库。  
  
 在登录期间，应用程序意向属性存储在客户端的会话中，然后 SQL Server 实例将处理该意向，并按照可用性组的配置和辅助副本中目标数据库的当前读写状态来确定执行什么操作。  
  
 如下所示是针对指定只读应用程序意向的 ADO.NET 访问接口 (System.Data.SqlClient) 的连接字符串的一个示例：  
  
```  
Server=tcp:AGListener,1433;Database=AdventureWorks;IntegratedSecurity=SSPI;ApplicationIntent=ReadOnly  
```  
  
 在此连接字符串示例中，客户端尝试连接到端口 1433 上名为 `AGListener` 的可用性组侦听器（如果可用性组侦听器正在侦听 1433，您也可以忽略端口）。  连接字符串具有`ApplicationIntent`属性设置为`ReadOnly`，此时使*读意向连接字符串*。  如果没有此设置，服务器将不会尝试该连接的只读路由。  
  
 可用性组的主数据库处理传入的只读路由请求，并尝试找到联接到主副本并配置为进行只读路由的只读副本。  客户端收回来自主副本服务器的连接信息，并连接到确定的只读副本。  
  
 请注意，可以将应用程序意向从客户端驱动程序发送到 SQL Server 下级实例。  在此情况下，将忽略只读的应用程序意向，并且连接将照常继续。  
  
 你可以绕过只读路由通过不将 application intent 连接属性设置为`ReadOnly`(时未指定，默认设置是`ReadWrite`在登录期间) 或通过直接连接到 SQL Server 的主副本实例而不使用可用性组侦听器名称。  如果您直接连接到只读副本，也不会发生只读路由。  
  
####  <a name="RelatedTasksApps"></a> 相关任务  
  
-   [对高可用性、灾难恢复的 SQL Server Native Client 支持](../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)  
  
-   [将连接字符串关键字用于 SQL Server Native Client](../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)  
  
##  <a name="BypassAGl"></a> 跳过可用性组侦听器  
 当可用性组侦听器支持故障转移重定向和只读路由时，客户端连接无需使用这两个功能。 客户端连接还可以直接引用 SQL Server 实例，而不是连接到可用性组侦听器。  
  
 对于 SQL Server 实例，无论连接是使用可用性组侦听器还是使用其他实例端点登录都无关紧要。  SQL Server 实例将验证目标数据库的状态，并允许或禁止基于可用性组配置和当前实例的数据库状态进行连接。  例如，如果客户端应用程序直接连接到 SQL Server 实例的端口并连接到可用性组中承载的目标数据库，且该目标数据库处于主状态和联机状态，则连接将获得成功。  如果目标数据库处于脱机或过渡状态，将无法连接到数据库。  
  
 此外，当从数据库镜像迁移到 [!INCLUDE[ssHADR](../includes/sshadr-md.md)]时，只要只有一个辅助副本存在且该副本禁止用户连接，应用程序就可以指定数据库镜像连接字符串。 有关详细信息，请参阅本节后面的 [将数据库镜像连接字符串用于可用性组](#DbmConnectionString)。  
  
###  <a name="DbmConnectionString"></a> 将数据库镜像连接字符串用于可用性组  
 如果可用性组仅拥有一个辅助副本并且未配置为允许对辅助副本进行读访问，则客户端可以通过使用数据库镜像连接字符串连接到主副本。 在将现有应用程序从数据库镜像迁移到可用性组时，此方法可能会很有用，只要您将可用性组限制为两个可用性副本（一个主副本和一个辅助副本）。 如果添加其他辅助副本，您需要为该可用性组创建一个可用性组侦听器，并更新您的应用程序以使用该可用性组侦听器 DNS 名称。  
  
 在使用数据库镜像连接字符串时，客户端可使用 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Native Client 或用于 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]的 .NET Framework 数据访问接口。 客户端提供的连接字符串必须至少提供一个服务器实例的名称，即“初始伙伴名称” ，以便标识最初承载您想要连接到的可用性副本的服务器实例。 此外，连接字符串还可以提供另一个服务器实例的名称，即“故障转移伙伴名称” ，以便标识最初将辅助副本作为故障转移伙伴名称承载的服务器实例。  
  
 有关数据库镜像连接字符串详细信息，请参阅 [将客户端连接到数据库镜像会话 (SQL Server)](database-mirroring/connect-clients-to-a-database-mirroring-session-sql-server.md)。  
  
##  <a name="CCBehaviorOnFailover"></a> 有关故障转移的客户端连接行为  
 当发生可用性组故障转移时，到可用性组的现有持久连接都将终止，并且客户端必须建立新连接才能继续使用相同的主数据库或只读辅助数据库。  当服务器端发生故障转移时，到可用性组的连接可能会失败，这就强制客户端应用程序重试连接，直至主副本完全回到联机状态。  
  
 如果在客户端应用程序的连接尝试期间但在连接超时期限之前可用性组回到联机状态，则在其内部的其中一次重试期间，客户端驱动程序可能会成功连接，并且在此情况下应用程序不会出现任何错误。  
  
##  <a name="SupportAgMultiSubnetFailover"></a> 支持可用性组多子网故障转移  
 如果您在使用支持连接字符串中的 MultiSubnetFailover 连接选项的客户端库，则可通过将 MultiSubnetFailover 设置为“True”或“Yes”（根据您在使用的访问接口的语法），优化到不同子网的可用性组故障转移。  
  
> [!NOTE]  
>  对于到可用性组侦听器以及到 SQL Server 故障转移群集实例名称的单个和多子网连接，建议使用此设置。  启用此选项将添加额外的优化，即使对于单子网方案也不例外。  
  
 `MultiSubnetFailover`连接选项仅适用于使用 TCP 网络协议，并且仅支持当连接到可用性组侦听程序时且针对任何虚拟网络名称连接到[!INCLUDE[ssCurrent](../includes/sscurrent-md.md)]。  
  
 如下所示是针对实现多子网故障转移的 ADO.NET 访问接口 (System.Data.SqlClient) 连接字符串的一个示例：  
  
```  
Server=tcp:AGListener,1433;Database=AdventureWorks;IntegratedSecurity=SSPI; MultiSubnetFailover=True  
```  
  
 `MultiSubnetFailover`连接选项应设置为`True`即使可用性组仅跨单子网。  这允许您预先配置新的客户端以支持进一步跨多个子网，而无需进一步更改客户端连接字符串，还可以优化单子网故障转移的故障转移性能。  虽然`MultiSubnetFailover`则不需要连接选项，它将提供更快的子网故障转移的优势。  这是因为，客户端驱动程序将尝试为每个与可用性组关联的 IP 地址并行打开 TCP 套接字。  客户端驱动程序将等待第一个 IP 响应成功，一旦成功，就将其用于连接。  
  
##  <a name="SSLcertificates"></a> 可用性组侦听器和 SSL 证书  
 当连接到可用性组侦听器时，如果参与的 SQL Server 实例将 SSL 证书与会话加密结合使用，则正在连接的客户端驱动程序将需要支持 SSL 证书中的“主题备用名称”以便强制加密。  SQL Server 驱动程序对于证书“主题备用名称”的支持计划用于 ADO.NET (SqlClient)、Microsoft JDBC 和 SQL Native Client (SNAC)。  
  
 必须为故障转移群集中每个参与的服务器节点配置 A X.509 证书，并在证书“主题备用名称”中设置所有可用性组侦听器的列表。  
  
 例如，如果 WSFC 具有三个可用性组侦听器，名称分别为 `AG1_listener.Adventure-Works.com`、 `AG2_listener.Adventure-Works.com`和 `AG3_listener.Adventure-Works.com`，则证书的“主题备用名称”应设置如下：  
  
```  
CN = ServerFQDN  
SAN = ServerFQDN,AG1_listener.Adventure-Works.com, AG2_listener.Adventure-Works.com, AG3_listener.Adventure-Works.com  
```  
  
##  <a name="SPNs"></a> 可用性组侦听器和服务器主体名称 (SPN)  
 必须由域管理员在 Active Directory 中为每个可用性组侦听器名称配置服务器主体名称 (SPN)，才能为到可用性组侦听器的客户端连接启用 Kerberos。 注册 SPN 时，必须使用托管可用性副本的服务器实例的服务帐户。  对于跨所有副本工作的 SPN，必须为承载可用性组的 WSFC 群集中的所有实例使用相同的服务帐户。  
  
 使用 Windows 命令行工具 `setspn` 配置 SPN。  例如，要为一组 SQL Server 实例上承载的名为 `AG1listener.Adventure-Works.com` 的可用性组配置 SPN，所有实例都应被配置为在域帐户 `corp/svclogin2`下运行：  
  
```  
setspn -A MSSQLSvc/AG1listener.Adventure-Works.com:1433 corp/svclogin2  
```  
  
 有关为 SQL Server 手动注册 SPN 的详细信息，请参阅 [为 Kerberos 连接注册服务主体名称](configure-windows/register-a-service-principal-name-for-kerberos-connections.md)。  
  
##  <a name="RelatedTasks"></a> 相关任务  
  
-   [AlwaysOn 客户端连接&#40;SQL Server&#41;](availability-groups/windows/always-on-client-connectivity-sql-server.md)
  
-   [创建或配置可用性组侦听程序 (SQL Server)](availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)  
  
-   [查看可用性组侦听程序属性 (SQL Server)](availability-groups/windows/view-availability-group-listener-properties-sql-server.md)  
  
-   [删除可用性组侦听程序 (SQL Server)](availability-groups/windows/remove-an-availability-group-listener-sql-server.md)  
  
-   [配置对可用性副本的只读访问 (SQL Server)](availability-groups/windows/configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
-   [为可用性组配置只读路由 (SQL Server)](availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md)  
  
##  <a name="RelatedContent"></a> 相关内容  
  
-   [用于高可用性和灾难恢复的 Microsoft SQL Server AlwaysOn 解决方案指南](http://go.microsoft.com/fwlink/?LinkId=227600)  
  
-   [可用性组侦听程序简介](http://blogs.msdn.com/b/sqlalwayson/archive/2012/01/16/introduction-to-the-availability-group-listener.aspx)（SQL Server AlwaysOn 团队博客）  
  
-   [SQL Server AlwaysOn 团队博客： SQL Server AlwaysOn 团队官方博客](http://blogs.msdn.com/b/sqlalwayson/)  
  
## <a name="see-also"></a>请参阅  
 [AlwaysOn 可用性组概述&#40;SQL Server&#41;](availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [AlwaysOn 客户端连接&#40;SQL Server&#41;](availability-groups/windows/always-on-client-connectivity-sql-server.md)  
 [关于对可用性副本的客户端连接访问 &#40;SQL Server&#41;](availability-groups/windows/about-client-connection-access-to-availability-replicas-sql-server.md)   
 [活动辅助副本： 可读辅助副本&#40;AlwaysOn 可用性组&#41;](availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)   
 [将客户端连接到数据库镜像会话 (SQL Server)](database-mirroring/connect-clients-to-a-database-mirroring-session-sql-server.md)
  
  