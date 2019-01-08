---
title: 为可用性组配置只读路由 (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 10/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- read-only routing
- Availability Groups [SQL Server], readable secondary replicas
- Availability Groups [SQL Server], read-only routing
- readable secondary replicas
- Availability Groups [SQL Server], client connectivity
- Availability Groups [SQL Server], active secondary replicas
ms.assetid: 7bd89ddd-0403-4930-a5eb-3c78718533d4
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3af17b9ee12846fc89e406420fa6405cb59e0af3
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/13/2018
ms.locfileid: "53367923"
---
# <a name="configure-read-only-routing-for-an-availability-group-sql-server"></a>为可用性组配置只读路由 (SQL Server)
  若要配置 AlwaysOn 可用性组以便在 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]中支持只读路由，您可以使用 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 或 PowerShell。 只读路由指的是 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 将符合条件的只读连接请求路由到可用的 AlwaysOn [可读次要副本](active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)（即，配置为在辅助角色下运行时允许只读工作负荷的副本）的能力。 为支持只读路由，可用性组必须具备[可用性组侦听器](../../listeners-client-connectivity-application-failover.md)。 只读客户端必须将其连接请求定向到此侦听器，并且客户端的连接字符串必须将应用程序意向指定为“只读”。 也就是说，它们必须是 *读意向连接请求*。  
  
> [!NOTE]
>  有关如何配置可读次要副本的信息，请参阅 [配置对可用性副本的只读访问 (SQL Server)](configure-read-only-access-on-an-availability-replica-sql-server.md)。  
> 
> 
> 
> [!NOTE]
>  [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]不支持配置只读路由。  
  

  
##  <a name="BeforeYouBegin"></a> 开始之前  
  
###  <a name="Prerequisites"></a> 先决条件  
  
-   可用性组必须拥有可用性组侦听器。 有关详细信息，请参阅 [创建或配置可用性组侦听程序 (SQL Server)](create-or-configure-an-availability-group-listener-sql-server.md)。  
  
-   一个或多个可用性副本必须配置为接受只读辅助角色中 (即，要[可读辅助副本](active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)(AlwaysOn %20Availability %20groups\).md))。 有关详细信息，请参阅 [配置对可用性副本的只读访问 (SQL Server)](configure-read-only-access-on-an-availability-replica-sql-server.md)。  
  
-   您必须连接到承载当前主副本的服务器实例。  
  
###  <a name="RORReplicaProperties"></a> 为支持只读路由，您需要配置哪些副本属性？  
  
-   对于要支持只读路由的每个可读次要副本，你需要指定 *只读路由 URL*。 此 URL 仅在本地副本在辅助角色下运行时起作用。 必须根据需要在逐个副本的基础上指定只读路由 URL。 每个只读路由 URL 都用于将读意向请求路由到一个特定的可读辅助副本。 通常，向每个可读辅助副本分配一个只读路由 URL。  
  
     有关计算可用性副本的只读路由 URL 的信息，请参阅 [Calculating read_only_routing_url for AlwaysOn](https://blogs.msdn.com/b/mattn/archive/2012/04/25/calculating-read-only-routing-url-for-alwayson.aspx)（计算 AlwaysOn 的 read_only_routing_url）。  
  
-   对于您要在其作为主副本时支持只读路由的每个可用性副本，您都需要指定一个“只读路由列表” 。 一个给定的只读路由列表仅在本地副本在主角色下运行时才起作用。 必须根据需要在逐个副本的基础上指定此列表。 通常，每个只读路由列表中将包含各只读路由 URL，并且在列表的末尾具有本地副本的 URL。  
  
    > [!NOTE]  
    >  读意向连接请求将被路由到当前主副本的只读路由列表上的第一个可用可读辅助副本。 没有负载平衡。  
  
> [!NOTE]  
>  有关可用性组侦听程序的信息，以及只读路由的详细信息，请参阅 [可用性组侦听程序、客户端连接和应用程序故障转移 (SQL Server)](../../listeners-client-connectivity-application-failover.md)。  
  
###  <a name="Security"></a> 安全性  
  
####  <a name="Permissions"></a> Permissions  
  
|任务|权限|  
|----------|-----------------|  
|在创建可用性组时配置副本|需要 **sysadmin** 固定服务器角色的成员资格，以及 CREATE AVAILABILITY GROUP 服务器权限、ALTER ANY AVAILABILITY GROUP 权限或 CONTROL SERVER 权限。|  
|修改可用性副本|对可用性组要求 ALTER AVAILABILITY GROUP 权限、CONTROL AVAILABILITY GROUP 权限、ALTER ANY AVAILABILITY GROUP 权限或 CONTROL SERVER 权限。|  
  
##  <a name="TsqlProcedure"></a> 使用 Transact-SQL  
 **若要配置只读路由**  
  
> [!NOTE]  
>  有关代码示例，请参阅本节后面的 [示例 (Transact-SQL)](#TsqlExample)。  
  
1.  连接到承载主副本的服务器实例。  
  
2.  若要指定的是新可用性组的副本，请使用 [CREATE AVAILABILITY GROUP](/sql/t-sql/statements/create-availability-group-transact-sql)[!INCLUDE[tsql](../../../includes/tsql-md.md)] 语句。 如果正在添加或修改现有可用性组的副本，请使用 [ALTER AVAILABILITY GROUP](/sql/t-sql/statements/alter-availability-group-transact-sql)[!INCLUDE[tsql](../../../includes/tsql-md.md)] 语句。  
  
    -   若要配置辅助角色的只读路由，请在 ADD REPLICA 或 MODIFY REPLICA WITH 子句中指定 SECONDARY_ROLE 选项，如下所示：  
  
         SECONDARY_ROLE **(** READ_ONLY_ROUTING_URL **='** TCP **://*`system-address`*:*`port`*)**  
  
         只读路由 URL 的参数如下所示：  
  
         *system-address*  
         一个字符串，例如系统名称、完全限定的域名或 IP 地址，它们明确标识了目标计算机系统。  
  
         *port*  
         一个端口号，由 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例的数据库引擎使用。  
  
         例如：   `SECONDARY_ROLE (READ_ONLY_ROUTING_URL = N'TCP://COMPUTER01.contoso.com:1433')`  
  
         如果副本已配置为允许只读连接，则在 MODIFY REPLICA 子句中，ALLOW_CONNECTIONS 是可选的。  
  
         有关详细信息，请参阅 [计算 AlwaysOn 的 read_only_routing_url](https://blogs.msdn.com/b/mattn/archive/2012/04/25/calculating-read-only-routing-url-for-alwayson.aspx)。  
  
    -   若要配置主角色的只读路由，请在 ADD REPLICA 或 MODIFY REPLICA WITH 子句中指定 PRIMARY_ROLE 选项，如下所示：  
  
         PRIMARY_ROLE **(** READ_ONLY_ROUTING_LIST **= ('*`server`*'** [ **，**...*n* ] **))**  
  
         其中， *server* 标识一个托管可用性组中的只读次要副本的服务器实例。  
  
         例如：   `PRIMARY_ROLE (READ_ONLY_ROUTING_LIST=('Server1','Server2'))`  
  
        > [!NOTE]  
        >  您必须先设置只读路由 URL，然后才能配置只读路由列表。  
  
###  <a name="TsqlExample"></a> 示例 (Transact-SQL)  
 以下示例将修改现有可用性组 `AG1` 的两个可用性副本以支持只读路由（如果其中一个副本拥有主角色）。 为了标识承载可用性副本的服务器实例，此示例指定了实例名称 `COMPUTER01` 和 `COMPUTER02`。  
  
```  
ALTER AVAILABILITY GROUP [AG1]  
 MODIFY REPLICA ON  
N'COMPUTER01' WITH   
(SECONDARY_ROLE (ALLOW_CONNECTIONS = READ_ONLY));  
ALTER AVAILABILITY GROUP [AG1]  
 MODIFY REPLICA ON  
N'COMPUTER01' WITH   
(SECONDARY_ROLE (READ_ONLY_ROUTING_URL = N'TCP://COMPUTER01.contoso.com:1433'));  
  
ALTER AVAILABILITY GROUP [AG1]  
 MODIFY REPLICA ON  
N'COMPUTER02' WITH   
(SECONDARY_ROLE (ALLOW_CONNECTIONS = READ_ONLY));  
ALTER AVAILABILITY GROUP [AG1]  
 MODIFY REPLICA ON  
N'COMPUTER02' WITH   
(SECONDARY_ROLE (READ_ONLY_ROUTING_URL = N'TCP://COMPUTER02.contoso.com:1433'));  
  
ALTER AVAILABILITY GROUP [AG1]   
MODIFY REPLICA ON  
N'COMPUTER01' WITH   
(PRIMARY_ROLE (READ_ONLY_ROUTING_LIST=('COMPUTER02','COMPUTER01')));  
  
ALTER AVAILABILITY GROUP [AG1]   
MODIFY REPLICA ON  
N'COMPUTER02' WITH   
(PRIMARY_ROLE (READ_ONLY_ROUTING_LIST=('COMPUTER01','COMPUTER02')));  
GO  
  
```  
  
##  <a name="PowerShellProcedure"></a> 使用 PowerShell  
 **若要配置只读路由**  
  
> [!NOTE]  
>  有关代码示例，请参阅本节后面的 [示例 (PowerShell)](#PSExample)。  
  
1.  将默认的 (`cd`) 设置为承载主副本的服务器实例。  
  
2.  在将可用性副本添加到可用性组中时，请使用 `New-SqlAvailabilityReplica` cmdlet。 在修改现有可用性副本时，请使用 `Set-SqlAvailabilityReplica` cmdlet。 相关参数如下：  
  
    -   若要配置辅助角色的只读路由，请指定**ReadonlyRoutingConnectionUrl"*`url`*"** 参数。  
  
         其中， *url* 是当路由到副本时要用于建立只读连接的连接完全限定域名 (FQDN) 和端口。 例如：  `-ReadonlyRoutingConnectionUrl "TCP://DBSERVER8.manufacturing.Adventure-Works.com:7024"`  
  
         有关详细信息，请参阅 [计算 AlwaysOn 的 read_only_routing_url](https://blogs.msdn.com/b/mattn/archive/2012/04/25/calculating-read-only-routing-url-for-alwayson.aspx)。  
  
    -   若要配置主角色的连接访问，请指定**ReadonlyRoutingList"*`server`*"** [ **，**...*n* ]，其中*server*标识一个托管可用性组中的只读次要副本的服务器实例。 例如：  `-ReadOnlyRoutingList "SecondaryServer","PrimaryServer"`  
  
        > [!NOTE]  
        >  您必须先设置副本的只读路由 URL，然后才能为其配置只读路由列表。  
  
    > [!NOTE]  
    >  若要查看 cmdlet 的语法，请在 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] PowerShell 环境中使用 `Get-Help` cmdlet。 有关详细信息，请参阅 [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md)。  
  
 **设置和使用 SQL Server PowerShell 提供程序**  
  
-   [SQL Server PowerShell 提供程序](../../../powershell/sql-server-powershell-provider.md)  
  
-   [Get Help SQL Server PowerShell](../../../powershell/sql-server-powershell.md)  
  
###  <a name="PSExample"></a> 示例 (PowerShell)  
 以下示例在可用性组中配置主副本和一个辅助副本以进行只读路由。 首先，该示例将向每个副本分配一个只读路由 URL。 然后，在主副本上设置只读路由列表。 连接字符串中的设置了“ReadOnly”属性的连接将被重定向到辅助副本。 如果此辅助副本不可读（由 `ConnectionModeInSecondaryRole` 设置确定），则连接将被定向回主副本。  
  
```  
Set-Location SQLSERVER:\SQL\PrimaryServer\default\AvailabilityGroups\MyAg  
$primaryReplica = Get-Item "AvailabilityReplicas\PrimaryServer"  
$secondaryReplica = Get-Item "AvailabilityReplicas\SecondaryServer"  
  
Set-SqlAvailabilityReplica -ReadOnlyRoutingConnectionUrl "TCP://PrimaryServer.domain.com:1433" -InputObject $primaryReplica  
Set-SqlAvailabilityReplica -ReadOnlyRoutingConnectionUrl "TCP://SecondaryServer.domain.com:1433" -InputObject $secondaryReplica  
Set-SqlAvailabilityReplica -ReadOnlyRoutingList "SecondaryServer","PrimaryServer" -InputObject $primaryReplica  
```  
  
##  <a name="FollowUp"></a> 跟进：配置只读路由之后  
 在这两种角色中配置当前主副本和可读辅助副本以支持只读路由后，可读辅助副本可接收/读取来自通过可用性组侦听器连接的客户端的读意向连接。  
  
> [!TIP]  
>  使用时[bcp 实用工具](../../../tools/bcp-utility.md)或[sqlcmd 实用工具](../../../tools/sqlcmd-utility.md)，可以通过指定指定只读访问到启用了任何辅助副本的只读访问`-K ReadOnly`切换。  
  
###  <a name="ConnStringReqsRecs"></a> 针对客户端连接字符串的要求和建议  
 对于要使用只读路由的客户端应用程序，其连接字符串必须满足以下要求：  
  
-   使用 TCP 协议。  
  
-   将应用程序意向特性/属性设置为只读。  
  
-   引用配置为支持只读路由的可用性组的侦听器。  
  
-   引用该可用性组中的数据库。  
  
 此外，建议连接字符串启用多子网故障转移，这将支持每个子网上的每个副本的并行客户端线程。 这将最大程度地减小故障转移后的客户端重新连接时间。  
  
 连接字符串的语法取决于应用程序正在使用的 SQL Server 提供程序。 以下用于 SQL Server 的 .NET Framework 数据访问接口 4.0.2 的示例连接字符串说明了使用只读路由时所需的和建议的连接字符串的部分。  
  
```  
Server=tcp:MyAgListener,1433;Database=Db1;IntegratedSecurity=SSPI;ApplicationIntent=ReadOnly;MultiSubnetFailover=True  
```  
  
 有关只读应用程序意向和只读路由器详细信息，请参阅 [可用性组侦听程序、客户端连接和应用程序故障转移 (SQL Server)](../../listeners-client-connectivity-application-failover.md)。  
  
### <a name="if-read-only-routing-is-not-working-correctly"></a>如果只读路由未正确工作  
 有关解决只读路由配置问题的信息，请参阅[只读路由未正确工作是](troubleshoot-always-on-availability-groups-configuration-sql-server.md)。  
  
##  <a name="RelatedTasks"></a> 相关任务  
 **查看只读路由配置**  
  
-   [sys.availability_read_only_routing_lists (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-availability-read-only-routing-lists-transact-sql)  
  
-   [sys.availability_replicas (Transact-SQL)](/sql/relational-databases/system-catalog-views/sys-availability-replicas-transact-sql)（**read_only_routing_url** 列）  
  
 **配置客户端连接访问**  
  
-   [创建或配置可用性组侦听程序 (SQL Server)](create-or-configure-an-availability-group-listener-sql-server.md)  
  
-   [配置对可用性副本的只读访问 (SQL Server)](configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
 **在应用程序中使用连接字符串**  
  
-   [对高可用性、灾难恢复的 SQL Server Native Client 支持](../../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)  
  
-   [将连接字符串关键字用于 SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)  
  
##  <a name="RelatedContent"></a> 相关内容  
  
-   **博客：**  
  
     [计算 AlwaysOn 的 read_only_routing_url](https://blogs.msdn.com/b/mattn/archive/2012/04/25/calculating-read-only-routing-url-for-alwayson.aspx)  
  
     [SQL Server AlwaysOn 团队博客：SQL Server AlwaysOn 团队官方博客](https://blogs.msdn.com/b/sqlalwayson/)  
  
     [CSS SQL Server 工程师博客](https://blogs.msdn.com/b/psssql/)  
  
-   **白皮书：**  
  
     [针对 SQL Server 2012 的 Microsoft 白皮书](https://msdn.microsoft.com/library/hh403491.aspx)  
  
     [SQL Server 客户咨询团队白皮书](http://sqlcat.com/)  
  
## <a name="see-also"></a>请参阅  
 [AlwaysOn 可用性组概述&#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [AlwaysOn 可用性组概述&#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [活动辅助副本：可读辅助副本 （AlwaysOn 可用性组）](active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)   
 [关于对可用性副本的客户端连接访问 &#40;SQL Server&#41;](about-client-connection-access-to-availability-replicas-sql-server.md)   
 [可用性组侦听程序、客户端连接和应用程序故障转移 (SQL Server)](../../listeners-client-connectivity-application-failover.md)  
  
  
