---
title: 针对高可用性、 灾难恢复的 JDBC 驱动程序支持 |Microsoft 文档
ms.custom: ''
ms.date: 04/04/2018
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 62de4be6-b027-427d-a7e5-352960e42877
caps.latest.revision: 40
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 5ad954bb250765d29dd6600ca98e4a01844f1831
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="jdbc-driver-support-for-high-availability-disaster-recovery"></a>JDBC 驱动程序对高可用性和灾难恢复的支持
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  本主题讨论[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]支持高可用性、 灾难恢复- [!INCLUDE[ssHADR](../../includes/sshadr_md.md)]。 有关 [!INCLUDE[ssHADR](../../includes/sshadr_md.md)]的详细信息，请参阅 [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)] 联机丛书。  
  
 从 4.0 版开始[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]，你可以指定的可用性组侦听器 （高可用性、 灾难恢复） 连接属性中的可用性组 (AG)。 如果[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]应用程序连接到故障转移的 AlwaysOn 数据库，原始连接已断开，且该应用程序必须打开新的连接在故障转移后继续工作。 以下[连接属性](../../connect/jdbc/setting-the-connection-properties.md)中增加了[!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)]:  
  
-   **multiSubnetFailover**  
  
-   **applicationIntent**
 
指定 multiSubnetFailover = true，连接到可用性组或故障转移群集实例的可用性组侦听器时。 请注意， **multiSubnetFailover**为 false，默认情况下。 使用**applicationIntent**来声明的应用程序工作负荷类型。 请参阅下面有关详细信息的部分。
 
对于 SQL Server，新的连接属性中的 Microsoft JDBC Driver 6.0 版开始**transparentNetworkIPResolution** (TNIR) 将添加为透明连接到 Always On 可用性组或具有的服务器关联的多个 IP 地址。 当**transparentNetworkIPResolution**为 true，该驱动程序尝试连接到第一个可用的 IP 地址。 如果首次尝试失败，该驱动程序将尝试连接到并行的所有 IP 地址，直到在超时过期，如果其中一个成功，则放弃所有挂起的连接尝试。   

请注意：
* 默认情况下，transparentNetworkIPResolution 适用
* 如果 multiSubnetFailover 为 true，则忽略 transparentNetworkIPResolution
* 如果使用数据库镜像，则忽略 transparentNetworkIPResolution
* 如果有 64 个以上的 IP 地址，则忽略 transparentNetworkIPResolution
* 如果 transparentNetworkIPResolution 为 true，则首次连接尝试使用 500ms年的超时值。 连接尝试的其余部分按照如下所示 multiSubnetFailover 功能相同的逻辑。 

> [!NOTE]  
如果你使用的 Microsoft JDBC Driver 4.2 （或降低） for SQL Server 并且**multiSubnetFailover**为 false，[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]尝试连接到第一个 IP 地址。 如果[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]无法建立与第一个 IP 地址，则连接将失败的连接。 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]不会尝试连接到任何后续的 IP 地址与服务器关联。 

  
> [!NOTE]  
>  增大连接超时值和实现连接重试逻辑将增加应用程序连接到可用性组的概率。 此外，由于可用性组进行故障转移而可能使连接失败，您应实现连接重试逻辑，重试失败的连接，直至重新连接。  
  
 
  
## <a name="connecting-with-multisubnetfailover"></a>使用 MultiSubnetFailover 进行连接  
 始终指定**multiSubnetFailover = true**连接到的可用性组侦听器时[!INCLUDE[ssSQL11](../../includes/sssql11_md.md)]可用性组或[!INCLUDE[ssSQL11](../../includes/sssql11_md.md)]故障转移群集实例。 **multiSubnetFailover**可以实现更快的故障转移的所有可用性组和故障转移群集实例中的[!INCLUDE[ssSQL11](../../includes/sssql11_md.md)]和将显著减少单个和多子网 AlwaysOn 拓扑的故障转移时间。 在多子网故障转移过程中，客户端将尝试并行进行连接。 在子网故障转移，[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]将积极重试 TCP 连接。  
  
 **MultiSubnetFailover**连接属性指示在某一可用性组或故障转移群集实例，并部署应用程序[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]将尝试连接到主上的数据库[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]实例尝试连接到所有 IP 地址。 当**MultiSubnetFailover = true**指定对于连接，则客户端的重试 TCP 连接的频率比操作系统的默认 TCP 重新传输间隔快。 这样，就可以在对 AlwaysOn 可用性组或 AlwaysOn 故障转移群集实例执行故障转移之后更快地进行重新连接，这一点同时适用于单子网和多子网可用性组和故障转移群集实例。  
  
 有关详细信息中的连接字符串关键字[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]，请参阅[设置连接属性](../../connect/jdbc/setting-the-connection-properties.md)。  
  
 指定**multiSubnetFailover = true**时连接到内容以外的可用性组侦听器或故障转移群集实例可能会导致性能下降，并且不支持。  
  
 如果未安装安全管理器，默认情况下，Java 虚拟机将缓存虚拟 IP 地址 (VIP) 一段时间（由您的 JDK 实现和 Java 属性 networkaddress.cache.ttl 和 networkaddress.cache.negative.ttl 定义）。 如果已安装 JDK 安全管理器，默认情况下，Java 虚拟机将缓存 VIP 且不会刷新缓存。 您应将 Java 虚拟机缓存的“生存时间”(networkaddress.cache.ttl) 设置为“一天”。 如果您未将默认生存时间更改为“一天（左右）”，则添加或更新 VIP 后，不会清除 Java 虚拟机缓存中的旧值。 有关 networkaddress.cache.ttl 和 networkaddress.cache.negative.ttl 的详细信息，请参阅[ http://download.oracle.com/javase/6/docs/technotes/guides/net/properties.html ](http://download.oracle.com/javase/6/docs/technotes/guides/net/properties.html)。  
  
 使用以下准则可以连接到可用性组或故障转移群集实例中的服务器：  
  
-   如果该驱动程序将生成错误**instanceName**在相同的连接字符串中使用连接属性**multiSubnetFailover**连接属性。 这反映一个事实：可用性组中未使用 SQL Browser。 但是，如果**portNumber**还指定连接属性，该驱动程序将忽略**instanceName**并用**portNumber**。  
  
-   使用**multiSubnetFailover**连接属性连接到单个子网或多子网时，它将提高对两者的性能。  
  
-   若要连接到某一可用性组，请在您的连接字符串中将该可用性组的可用性组侦听器指定为服务器。 例如，jdbc:sqlserver://VNN1。  
  
-   连接到配置有超过 64 个 IP 地址的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 实例将导致连接失败。  
  
-   使用的应用程序的行为**multiSubnetFailover**连接属性不受影响基于身份验证类型：[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]身份验证、 Kerberos 身份验证或 Windows 身份验证。  
  
-   值增加**loginTimeout**以调整故障转移时间并减少应用程序连接重试尝试。  
  
-   不支持分布式事务。  
  
 如果只读路由不起作用，则连接到可用性组中的辅助副本位置在以下情况下将失败：  
  
1.  如果未将辅助副本位置配置为接受连接。  
  
2.  如果应用程序使用**applicationIntent = ReadWrite** （下文讨论） 和辅助副本位置配置为只读访问权限。  
  
 如果将主副本配置为拒绝只读工作负荷且连接字符串包含 **ApplicationIntent=ReadOnly**，连接将失败。  
  
## <a name="upgrading-to-use-multi-subnet-clusters-from-database-mirroring"></a>升级以便使用来自数据库镜像的多子网群集  
 如果升级[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]应用程序当前使用数据库镜像到多子网方案中，你应该删除**failoverPartner**连接属性并将其替换**multiSubnetFailover**设置为**true**并将连接字符串中的服务器名称替换为可用性组侦听器。 如果使用的连接字符串**failoverPartner**和**multiSubnetFailover = true**，驱动程序将生成错误。 但是，如果使用的连接字符串**failoverPartner**和**multiSubnetFailover = false** (或**ApplicationIntent = ReadWrite**)，应用程序将使用数据库镜像。  
  
 该驱动程序将返回错误，如果在 AG 中，在主数据库上使用数据库镜像，并且**multiSubnetFailover = true**在连接到主数据库而不是到可用性组的连接字符串中使用侦听器。  


[!INCLUDE[specify-application-intent_read-only-routing](~/includes/paragraph-content/specify-application-intent-read-only-routing.md)]


## <a name="new-methods-supporting-multisubnetfailover-and-applicationintent"></a>支持 multiSubnetFailover 和 applicationIntent 的新增方法  
 以下方法为你提供以编程方式访问**multiSubnetFailover**， **applicationIntent**和**transparentNetworkIPResolution**连接字符串关键字：  
  
-   [SQLServerDataSource.getApplicationIntent](../../connect/jdbc/reference/getapplicationintent-method-sqlserverdatasource.md)  
  
-   [SQLServerDataSource.setApplicationIntent](../../connect/jdbc/reference/setapplicationintent-method-sqlserverdatasource.md)  
  
-   [SQLServerDataSource.getMultiSubnetFailover](../../connect/jdbc/reference/getmultisubnetfailover-method-sqlserverdatasource.md)  
  
-   [SQLServerDataSource.setMultiSubnetFailover](../../connect/jdbc/reference/setmultisubnetfailover-method-sqlserverdatasource.md)  
  
-   [SQLServerDriver.getPropertyInfo](../../connect/jdbc/reference/getpropertyinfo-method-sqlserverdriver.md)  

-   SQLServerDataSource.setTransparentNetworkIPResolution

-   SQLServerDataSource.getTransparentNetworkIPResolution
  
 **GetMultiSubnetFailover**， **setMultiSubnetFailover**， **getApplicationIntent**， **setApplicationIntent**， **getTransparentNetworkIPResolution**和**setTransparentNetworkIPResolution**方法也会添加到[SQLServerDataSource 类](../../connect/jdbc/reference/sqlserverdatasource-class.md)， [SQLServerConnectionPoolDataSource 类](../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md)，和[SQLServerXADataSource 类](../../connect/jdbc/reference/sqlserverxadatasource-class.md)。  
  
## <a name="ssl-certificate-validation"></a>SSL 证书验证  
 可用性组包含多个物理服务器。 [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)] 增加了对支持**使用者备用名称**中以便多个主机可以使用相同的证书相关联的 SSL 证书。 有关 SSL 的详细信息，请参阅[了解 SSL 支持](../../connect/jdbc/understanding-ssl-support.md)。  
  
## <a name="see-also"></a>另请参阅  
 [连接到 SQL Server 使用 JDBC 驱动程序](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)   
 [设置连接属性](../../connect/jdbc/setting-the-connection-properties.md)  
  
  
