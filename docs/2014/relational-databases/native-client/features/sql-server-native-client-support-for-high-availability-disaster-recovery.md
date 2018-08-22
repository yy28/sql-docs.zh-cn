---
title: 对高可用性和灾难恢复的 SQL Server Native Client 支持 |Microsoft Docs
ms.custom: ''
ms.date: 2016-08-31
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 2b06186b-4090-4728-b96b-90d6ebd9f66f
caps.latest.revision: 36
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 71966f354dee7259273b24adf149045b009deb10
ms.sourcegitcommit: 79d4dc820767f7836720ce26a61097ba5a5f23f2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/16/2018
ms.locfileid: "40395458"
---
# <a name="sql-server-native-client-support-for-high-availability-disaster-recovery"></a>对高可用性、灾难恢复的 SQL Server Native Client 支持
  本主题讨论 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 对于 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]的支持（[!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 新增功能）。 有关 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 的详细信息，请参阅[可用性组侦听程序、客户端连接和应用程序故障转移 (SQL Server)](../../../database-engine/listeners-client-connectivity-application-failover.md)、[创建和配置可用性组 (SQL Server)](../../../database-engine/availability-groups/windows/creation-and-configuration-of-availability-groups-sql-server.md)、[故障转移群集和 AlwaysOn 可用性组 (SQL Server)](../../../database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md) 和[活动次要副本：可读次要副本（AlwaysOn 可用性组）](../../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)。  
  
 您可以在连接字符串中指定给定可用性组的可用性组侦听器。 如果某一 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 应用程序连接到故障转移的可用性组中的某个数据库，则原始连接将被断开，并且应用程序必须打开一个新连接，以便在故障转移后继续工作。  
  
 如果您未连接到某一可用性组侦听器，并且多个 IP 地址与主机名相关联，则 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 将按顺序遍历与 DNS 条目关联的所有 IP 地址。 如果 DNS 服务器返回的第一个 IP 地址未绑定到任何网络接口卡 (NIC)，则上述遍历操作可能会用时较长。 在连接到某一可用性组侦听器时，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 将尝试并行建立与所有 IP 地址的连接；如果某一连接尝试成功，则驱动程序将放弃所有挂起的连接尝试。  
  
> [!NOTE]  
>  增大连接超时值和实现连接重试逻辑将增加应用程序连接到可用性组的概率。 此外，由于可用性组进行故障转移而可能使连接失败，您应实现连接重试逻辑，重试失败的连接，直至重新连接。  
  
## <a name="connecting-with-multisubnetfailover"></a>使用 MultiSubnetFailover 进行连接  
 在连接到 SQL Server 2012 可用性组侦听器或 SQL Server 2012 故障转移群集实例时，应始终指定 `MultiSubnetFailover=Yes`。 `MultiSubnetFailover` 可加快 SQL Server 2012 中所有可用性组和故障转移群集实例的故障转移速度，并且将显著缩短单子网和多子网 AlwaysOn 拓扑的故障转移时间。 在多子网故障转移过程中，客户端将尝试并行进行连接。 在子网故障转移过程中，[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 将会主动重试 TCP 连接。  
  
 `MultiSubnetFailover` 连接属性指示应用程序正部署在某一可用性组或故障转移群集实例中，并且 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 将尝试通过连接到所有 IP 地址来连接到主 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例上的数据库。 当为连接指定 `MultiSubnetFailover=Yes` 时，客户端将以比操作系统的默认 TCP 重新传输间隔更快的速度重试建立 TCP 连接。 这样，就可以在对 AlwaysOn 可用性组或 AlwaysOn 故障转移群集实例执行故障转移之后更快地进行重新连接，这一点同时适用于单子网和多子网可用性组和故障转移群集实例。  
  
 有关连接字符串关键字的详细信息，请参阅 [将连接字符串关键字用于 SQL Server Native Client](../applications/using-connection-string-keywords-with-sql-server-native-client.md)。  
  
 指定`MultiSubnetFailover=Yes`时连接到的内容以外的可用性组侦听器或故障转移群集实例可能会导致性能下降，和不受支持。  
  
 使用以下准则可以连接到可用性组或故障转移群集实例中的服务器：  
  
-   在连接到单子网或多子网时使用 `MultiSubnetFailover` 连接属性；这将改进这两者的性能。  
  
-   若要连接到某一可用性组，请在您的连接字符串中将该可用性组的可用性组侦听器指定为服务器。  
  
-   连接到配置有超过 64 个 IP 地址的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例将导致连接失败。  
  
-   基于以下身份验证类型，使用 `MultiSubnetFailover` 连接属性的应用程序的行为将不会受到影响：[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 身份验证、Kerberos 身份验证或 Windows 身份验证。  
  
-   您可以增加 `loginTimeout` 的值，以便满足故障转移时间和减少应用程序连接重试次数。  
  
-   不支持分布式事务。  
  
 如果只读路由不起作用，则连接到可用性组中的辅助副本位置在以下情况下将失败：  
  
1.  如果未将辅助副本位置配置为接受连接。  
  
2.  如果应用程序使用 `ApplicationIntent=ReadWrite`（在下面论述）且将辅助副本位置配置为只读访问。  
  
 如果主副本配置为拒绝只读工作负荷且连接字符串包含连接将失败`ApplicationIntent=ReadOnly`。  
  
## <a name="upgrading-to-use-multi-subnet-clusters-from-database-mirroring"></a>升级以便使用来自数据库镜像的多子网群集  
 如果连接字符串中已存在 `MultiSubnetFailover` 和 `Failover_Partner` 连接关键字，将出现连接错误。 如果使用 `MultiSubnetFailover` 且 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 返回一个故障转移伙伴响应指示它是数据库镜像对的一部分，也将出现错误。  
  
 如果您将当前使用数据库镜像的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 应用程序升级到多子网方案，则应删除 `Failover_Partner` 连接属性并且使用设置为 `MultiSubnetFailover` 的 `Yes` 替换它，并且还应使用可用性组侦听器替换连接字符串中的服务器名称。 如果连接字符串使用`Failover_Partner`和`MultiSubnetFailover=Yes`，驱动程序将生成错误。 但是，如果连接字符串使用`Failover_Partner`并`MultiSubnetFailover=No`(或`ApplicationIntent=ReadWrite`)，该应用程序将使用数据库镜像。  
  
 如果数据库镜像用于可用性组中的主数据库，并且 `MultiSubnetFailover=Yes` 用于连接到主数据库（而非连接到可用性组侦听器）的连接字符串中，则驱动程序将返回错误。  
  
## <a name="specifying-application-intent"></a>指定应用程序意向  
 如果 `ApplicationIntent=ReadOnly`，在连接到某一启用了 AlwaysOn 的数据库时，客户端将请求读取工作负荷。 服务器在连接时和在执行 USE 数据库语句的过程中将强制该意向，但仅针对启用了 AlwaysOn 的数据库。  
  
 `ApplicationIntent`关键字不适用于早期的只读数据库。  
  
 数据库可允许或禁止目标 AlwaysOn 数据库上的读取工作负荷。 (这通过`ALLOW_CONNECTIONS`子句`PRIMARY_ROLE`并`SECONDARY_ROLE`[!INCLUDE[tsql](../../../includes/tsql-md.md)]语句。)  
  
 `ApplicationIntent`关键字用于启用只读路由。  
  
## <a name="read-only-routing"></a>只读路由  
 只读路由是一项可确保数据库只读副本的可用性的功能。 启用只读路由：  
  
1.  您必须连接到某一 AlwaysOn 可用性组侦听器。  
  
2.  `ApplicationIntent` 连接字符串关键字必须设置为 `ReadOnly`。  
  
3.  数据库管理员必须配置该可用性组以便启用只读路由。  
  
 使用只读路由的多个连接可能不会全部连接到相同的只读副本。 对数据库同步进行更改或对服务器的路由配置进行更改可能导致客户端连接到不同的只读副本。 若要确保所有只读请求都连接到相同的只读副本，请勿将可用性组侦听器传递到 `Server` 连接字符串关键字。 而是指定只读实例的名称。  
  
 只读路由所用的时间可能会长于连接到主副本的时间，因为只读路由首先连接到主副本，然后查找可用的最佳可读取辅助副本。 为此，应增加您的登录超时。  
  
## <a name="odbc"></a>ODBC  
 添加了两个 ODBC 连接字符串关键字以在 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] Native Client 中支持 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]：  
  
-   `ApplicationIntent`  
  
-   `MultiSubnetFailover`  
  
 有关 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 中 ODBC 连接字符串关键字的详细信息，请参阅[将连接字符串关键字用于 SQL Server Native Client](../applications/using-connection-string-keywords-with-sql-server-native-client.md)。  
  
 等效的连接属性为：  
  
-   `SQL_COPT_SS_APPLICATION_INTENT`  
  
-   `SQL_COPT_SS_MULTISUBNET_FAILOVER`  
  
 有关 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 中的 ODBC 连接属性的详细信息，请参阅 [SQLSetConnectAttr](../../native-client-odbc-api/sqlsetconnectattr.md)。  
  
 从 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 开始，将在使用 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] Native Client 驱动程序的 DSN 的 ODBC 数据源管理器中公开 `ApplicationIntent` 和 `MultiSubnetFailover` 关键字的功能。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client ODBC 应用程序可以使用以下三个函数之一进行连接：  
  
|函数|Description|  
|--------------|-----------------|  
|[SQLBrowseConnect](../../native-client-odbc-api/sqlbrowseconnect.md)|`SQLBrowseConnect` 返回的服务器列表将不包括 VNN。 如果服务器是独立服务器，或是 Windows Server Failover Clustering (WSFC) 群集中的主服务器或辅助服务器，该群集包含已为 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 启用的两个或多个 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 实例，您将只能看到不带任何指示信息的服务器列表。 如果连接到服务器失败，可能是因为您已连接到某服务器而 `ApplicationIntent` 设置与该服务器配置不兼容。<br /><br /> 由于 `SQLBrowseConnect` 无法识别 Windows Server Failover Clustering (WSFC) 群集（该群集包含已为 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 启用的两个或多个 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 实例）中的服务器，`SQLBrowseConnect` 将忽略 `MultiSubnetFailover` 连接字符串关键字。|  
|[SQLConnect](../../native-client-odbc-api/sqlconnect.md)|`SQLConnect` 通过数据源名称 (DSN) 或连接属性支持 `ApplicationIntent` 和 `MultiSubnetFailover`。|  
|[SQLDriverConnect](../../native-client-odbc-api/sqldriverconnect.md)|`SQLDriverConnect` 通过连接字符串关键字、连接属性或 DSN 支持 `ApplicationIntent` 和 `MultiSubnetFailover`。|  
  
## <a name="ole-db"></a>OLE DB  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 中的 OLE DB 不支持 `MultiSubnetFailover` 关键字。  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 中的 OLE DB 将支持应用程序意向。 对于 OLE DB 应用程序，应用程序意向的行为将与 ODBC 应用程序的行为相同（请参阅上文）。  
  
 添加了一个 OLE DB 连接字符串关键字以在 [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] Native Client 中支持 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]：  
  
-   `Application Intent`  
  
 有关 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client 中连接字符串关键字的详细信息，请参阅[将连接字符串关键字用于 SQL Server Native Client](../applications/using-connection-string-keywords-with-sql-server-native-client.md)。  
  
 等效的连接属性为：  
  
-   `SSPROP_INIT_APPLICATIONINTENT`  
  
-   `DBPROP_INIT_PROVIDERSTRING`  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client OLE DB 应用程序可以使用以下方法之一来指定应用程序意向：  
  
 `IDBInitialize::Initialize`  
 `IDBInitialize::Initialize` 使用以前配置的属性集来初始化数据源并创建数据源对象。 将应用程序意向指定为访问接口属性或作为扩展属性字符串的一部分。  
  
 `IDataInitialize::GetDataSource`  
 `IDataInitialize::GetDataSource` 提取可以包含 `Application Intent` 关键字的输入连接字符串。  
  
 `IDBProperties::GetProperties`  
 `IDBProperties::GetProperties` 检索当前为数据源设置的属性的值。  您可以通过 DBPROP_INIT_PROVIDERSTRING 属性和 SSPROP_INIT_APPLICATIONINTENT 属性检索 `Application Intent` 值。  
  
 `IDBProperties::SetProperties`  
 若要设置 `ApplicationIntent` 属性值，请调用 `IDBProperties::SetProperties`，它传递 `SSPROP_INIT_APPLICATIONINTENT` 属性的值 `ReadWrite` 或 `ReadOnly` 或传递 `DBPROP_INIT_PROVIDERSTRING` 属性的值（该值包含 `ApplicationIntent=ReadOnly` 或 `ApplicationIntent=ReadWrite`）。  
  
 可以在“数据链接属性”对话框的“全部”选项卡的“应用程序意向属性”字段中指定应用程序意向。  
  
 建立隐式连接时，隐式连接将使用父连接的应用程序意向设置。 同样，从同一数据源创建的多个会话将继承数据源的应用程序意向设置。  
  
## <a name="see-also"></a>请参阅  
 [SQL Server Native Client 功能](sql-server-native-client-features.md)   
 [将连接字符串关键字用于 SQL Server Native Client](../applications/using-connection-string-keywords-with-sql-server-native-client.md)  
  
  
