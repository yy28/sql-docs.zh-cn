---
title: JDBC 驱动程序对高可用性和灾难恢复的支持 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 62de4be6-b027-427d-a7e5-352960e42877
caps.latest.revision: 40
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1136f55327ad68063c55e8f841930759a28fe576
ms.sourcegitcommit: 603d2e588ac7b36060fa0cc9c8621ff2a6c0fcc7
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2018
ms.locfileid: "42786422"
---
# <a name="jdbc-driver-support-for-high-availability-disaster-recovery"></a>JDBC 驱动程序对高可用性和灾难恢复的支持
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  本主题介绍 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 对于高可用性和灾难恢复的支持 -- [!INCLUDE[ssHADR](../../includes/sshadr_md.md)]。 有关 [!INCLUDE[ssHADR](../../includes/sshadr_md.md)]的详细信息，请参阅 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 联机丛书。  
  
 从 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 4.0 版本开始，可以在连接属性中指定（高可用性、灾难恢复）可用性组 (AG) 的可用性组侦听器。 如果将 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 应用程序连接到具有故障转移功能的 AlwaysOn 数据库，则在故障转移后，会断开原始连接，并且该应用程序必须建立一个新的连接才能继续运行。 [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)] 中新增了以下[连接属性](../../connect/jdbc/setting-the-connection-properties.md)：  
  
-   **multiSubnetFailover**  
  
-   **applicationIntent**
 
在连接到可用性组的可用性组侦听程序或故障转移群集实例时可指定 multiSubnetFailover=true。 请注意， **multiSubnetFailover**是默认值为 false。 使用**applicationIntent**声明应用程序工作负荷类型。 请参见各节更多详细信息。
 
对于 SQL Server，新的连接属性从版本 6.0 的 Microsoft JDBC Driver **transparentNetworkIPResolution** (了 TNIR) 将添加为透明连接到 Always On 可用性组或一个具有服务器关联的多个 IP 地址。 当**transparentNetworkIPResolution**为 true，驱动程序将尝试连接到第一个可用的 IP 地址。 如果第一次尝试失败，该驱动程序将尝试连接到并行中的所有 IP 地址，直到在超时到期，当其中一个成功放弃所有挂起的连接尝试。   

请注意：
* transparentNetworkIPResolution 是默认情况下，则返回 true
* 如果 multiSubnetFailover 是 true，则忽略 transparentNetworkIPResolution
* 如果使用数据库镜像，则忽略 transparentNetworkIPResolution
* 如果有超过 64 个 IP 地址，则忽略 transparentNetworkIPResolution
* 如果 transparentNetworkIPResolution 为 true，首次连接尝试使用的超时值为 500 毫秒。 连接尝试的其余部分遵循相同的逻辑如下所示 multiSubnetFailover 功能。 

> [!NOTE]  
如果你是使用 Microsoft JDBC Driver 4.2 （或降低） 适用于 SQL Server，并且**multiSubnetFailover**为 false，[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]尝试连接到第一个 IP 地址。 如果 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 无法建立与第一个 IP 地址的连接，则连接将失败。 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 将不会尝试连接到与此服务器关联的任何后续 IP 地址。 

  
> [!NOTE]  
>  增大连接超时值和实现连接重试逻辑将增加应用程序连接到可用性组的概率。 此外，由于可用性组进行故障转移而可能使连接失败，您应实现连接重试逻辑，重试失败的连接，直至重新连接。  
  
 
  
## <a name="connecting-with-multisubnetfailover"></a>使用 MultiSubnetFailover 进行连接  
 在连接到 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 可用性组或 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 故障转移群集实例的可用性组侦听程序时，应始终指定 multiSubnetFailover=true。 multiSubnetFailover 可加快 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 中所有可用性组和故障转移群集实例的故障转移速度，并且将显著缩短单子网和多子网 AlwaysOn 拓扑的故障转移时间。 在多子网故障转移过程中，客户端将尝试并行进行连接。 子网故障转移期间，[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 将积极地重试 TCP 连接。  
  
 multiSubnetFailover 连接属性指示应用程序正部署在某一可用性组或故障转移群集实例中，并且 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 将尝试通过试图连接到所有 IP 地址来连接到主 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例上的数据库。 为连接指定 MultiSubnetFailover=true 后，客户端将在比操作系统的默认 TCP 重传间隔更短的时间内重试 TCP 连接尝试。 这样，就可以在对 AlwaysOn 可用性组或 AlwaysOn 故障转移群集实例执行故障转移之后更快地进行重新连接，这一点同时适用于单子网和多子网可用性组和故障转移群集实例。  
  
 有关详细信息中的连接字符串关键字[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]，请参阅[连接属性设置](../../connect/jdbc/setting-the-connection-properties.md)。  
  
 如果在连接到非可用性组侦听程序或故障转移群集实例时指定 multiSubnetFailover=true，则可能会对性能造成负面影响，因此不支持这样做。  
  
 如果未安装安全管理器，默认情况下，Java 虚拟机将缓存虚拟 IP 地址 (VIP) 一段时间（由您的 JDK 实现和 Java 属性 networkaddress.cache.ttl 和 networkaddress.cache.negative.ttl 定义）。 如果已安装 JDK 安全管理器，默认情况下，Java 虚拟机将缓存 VIP 且不会刷新缓存。 您应将 Java 虚拟机缓存的“生存时间”(networkaddress.cache.ttl) 设置为“一天”。 如果您未将默认生存时间更改为“一天（左右）”，则添加或更新 VIP 后，不会清除 Java 虚拟机缓存中的旧值。 有关 networkaddress.cache.ttl 和 networkaddress.cache.negative.ttl 的详细信息，请参阅[ http://download.oracle.com/javase/6/docs/technotes/guides/net/properties.html ](http://download.oracle.com/javase/6/docs/technotes/guides/net/properties.html)。  
  
 使用以下准则可以连接到可用性组或故障转移群集实例中的服务器：  
  
-   如果该驱动程序将生成错误**instanceName**相同的连接字符串中使用连接属性**multiSubnetFailover**连接属性。 这反映一个事实：可用性组中未使用 SQL Browser。 但是，如果**portNumber**还指定连接属性，则驱动程序将忽略**instanceName** ，并使用**portNumber**。  
  
-   连接到单子网或多子网时使用 multiSubnetFailover 连接属性，这二者的性能都会得到改进。  
  
-   若要连接到某一可用性组，请在您的连接字符串中将该可用性组的可用性组侦听器指定为服务器。 例如，jdbc:sqlserver://VNN1。  
  
-   连接到配置有超过 64 个 IP 地址的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例将导致连接失败。  
  
-   基于以下身份验证类型，使用 multiSubnetFailover 连接属性的应用程序的行为不受到影响：[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证、Kerberos 身份验证或 Windows 身份验证。  
  
-   增加 loginTimeout 的值，以延长故障转移时间并减少应用程序连接重试次数。  
  
-   不支持分布式事务。  
  
 如果只读路由不起作用，则连接到可用性组中的辅助副本位置在以下情况下将失败：  
  
1.  如果未将辅助副本位置配置为接受连接。  
  
2.  如果应用程序使用 applicationIntent=ReadWrite（将在下文中介绍）并且次要副本位置被配置为只读访问。  
  
 如果将主副本配置为拒绝只读工作负荷且连接字符串包含 **ApplicationIntent=ReadOnly**，连接将失败。  
  
## <a name="upgrading-to-use-multi-subnet-clusters-from-database-mirroring"></a>升级以便使用来自数据库镜像的多子网群集  
 如果将当前使用数据库镜像的 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 应用程序升级到多子网方案，则应删除 failoverPartner 连接属性并替换成已设置为“true”的 multiSubnetFailover，并且还应使用可用性组侦听程序替换连接字符串中的服务器名称。 如果连接字符串使用 failoverPartner 和 multiSubnetFailover=true，驱动程序将生成一个错误。 但是，如果连接字符串使用 failoverPartner 和 multiSubnetFailover=false（或 ApplicationIntent=ReadWrite），则此应用程序将使用数据库镜像。  
  
 如果数据库镜像在 AG 中的主数据库上使用，并且如果 multiSubnetFailover=true 用于连接到主数据库（而非可用性组侦听程序）的连接字符串中，驱动程序则将返回一个错误。  


[!INCLUDE[specify-application-intent_read-only-routing](~/includes/paragraph-content/specify-application-intent-read-only-routing.md)]


## <a name="new-methods-supporting-multisubnetfailover-and-applicationintent"></a>支持 multiSubnetFailover 和 applicationIntent 的新增方法  
 以下方法，您可以以编程方式访问**multiSubnetFailover**， **applicationIntent**并**transparentNetworkIPResolution**连接字符串关键字：  
  
-   [SQLServerDataSource.getApplicationIntent](../../connect/jdbc/reference/getapplicationintent-method-sqlserverdatasource.md)  
  
-   [SQLServerDataSource.setApplicationIntent](../../connect/jdbc/reference/setapplicationintent-method-sqlserverdatasource.md)  
  
-   [SQLServerDataSource.getMultiSubnetFailover](../../connect/jdbc/reference/getmultisubnetfailover-method-sqlserverdatasource.md)  
  
-   [SQLServerDataSource.setMultiSubnetFailover](../../connect/jdbc/reference/setmultisubnetfailover-method-sqlserverdatasource.md)  
  
-   [SQLServerDriver.getPropertyInfo](../../connect/jdbc/reference/getpropertyinfo-method-sqlserverdriver.md)  

-   SQLServerDataSource.setTransparentNetworkIPResolution

-   SQLServerDataSource.getTransparentNetworkIPResolution
  
 **GetMultiSubnetFailover**， **setMultiSubnetFailover**， **getApplicationIntent**， **setApplicationIntent**， **getTransparentNetworkIPResolution**并**setTransparentNetworkIPResolution**方法也会添加到[SQLServerDataSource 类](../../connect/jdbc/reference/sqlserverdatasource-class.md)， [SQLServerConnectionPoolDataSource 类](../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md)，并[SQLServerXADataSource 类](../../connect/jdbc/reference/sqlserverxadatasource-class.md)。  
  
## <a name="ssl-certificate-validation"></a>SSL 证书验证  
 可用性组包含多个物理服务器。 [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)] 新增了对 SSL 证书中使用者替代名称的支持，因此多台主机可与同一个证书相关联。 有关 SSL 的详细信息，请参阅[了解 SSL 支持](../../connect/jdbc/understanding-ssl-support.md)。  
  
## <a name="see-also"></a>另请参阅  
 [通过 JDBC 驱动程序连接到 SQL Server](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)   
 [设置连接属性](../../connect/jdbc/setting-the-connection-properties.md)  
  
  
