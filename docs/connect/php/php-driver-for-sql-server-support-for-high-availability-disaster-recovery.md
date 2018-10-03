---
title: 对高可用性和灾难恢复的 Microsoft Drivers for PHP for SQL Server 的支持 |Microsoft Docs
ms.custom: ''
ms.date: 07/31/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 73a80821-d345-4fea-b076-f4aabeb4af3e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8f81353dcf7dc3af6b8cdcccba287b425d2139af
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47838229"
---
# <a name="support-for-high-availability-disaster-recovery"></a>支持高可用性、灾难恢复
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

本主题讨论了对高可用性、灾难恢复的 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 支持（3.0 版中的新增功能）- [!INCLUDE[ssHADR](../../includes/sshadr_md.md)]。  在 [!INCLUDE[ssHADR](../../includes/sshadr_md.md)] 中添加了 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 支持。 有关 [!INCLUDE[ssHADR](../../includes/sshadr_md.md)]的详细信息，请参阅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 联机丛书。  
  
在 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 3.0 版中，可在连接属性中指定（高可用性、灾难恢复）可用性组 (AG) 的可用性组侦听程序。 如果将 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 应用程序连接到具有故障转移功能的 AlwaysOn 数据库，则在故障转移后，会断开原始连接，并且该应用程序必须建立一个新的连接才能继续运行。  
  
如果未连接到某一可用性组侦听程序，并且多个 IP 地址与一个主机名关联，则 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 将按顺序循环访问与 DNS 条目关联的所有 IP 地址。 如果 DNS 服务器返回的第一个 IP 地址未绑定到任何网络接口卡 (NIC)，则上述遍历操作可能会用时较长。 连接到可用性组侦听程序时，[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 尝试建立与所有 IP 地址的并行连接，如果连接尝试成功，则驱动程序将放弃所有挂起的连接尝试。  
  
> [!NOTE]  
> 增大连接超时值和实现连接重试逻辑将增加应用程序连接到可用性组的概率。 此外，由于可用性组进行故障转移而可能使连接失败，您应实现连接重试逻辑，重试失败的连接，直至重新连接。  
  
## <a name="connecting-with-multisubnetfailover"></a>使用 MultiSubnetFailover 进行连接  
MultiSubnetFailover 连接属性指示应用程序正部署在某一可用性组或故障转移群集实例中，并且 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 将尝试通过连接到所有 IP 地址来连接到主 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例上的数据库。 为连接指定 MultiSubnetFailover=true 后，客户端将在比操作系统的默认 TCP 重传间隔更短的时间内重试 TCP 连接尝试。 这样，就可以在对 AlwaysOn 可用性组或 AlwaysOn 故障转移群集实例执行故障转移之后更快地进行重新连接，这一点同时适用于单子网和多子网可用性组和故障转移群集实例。  
  
在连接到 SQL Server 2012 可用性组侦听程序或 SQL Server 2012 故障转移群集实例时，应始终指定 MultiSubnetFailover=True。 MultiSubnetFailover 可加快 SQL Server 2012 中所有可用性组和故障转移群集实例的故障转移速度，并且显著缩短单子网和多子网 AlwaysOn 拓扑的故障转移时间。 在多子网故障转移过程中，客户端将尝试并行进行连接。 子网故障转移期间，[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 将积极地重试 TCP 连接。  
  
有关详细信息中的连接字符串关键字[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]，请参阅[连接选项](../../connect/php/connection-options.md)。  
  
如果在连接到非可用性组侦听程序或非故障转移群集实例时指定了 MultiSubnetFailover=true，可能会对性能造成负面影响，因此不支持这样做。  
  
使用以下准则可以连接到可用性组中的服务器：  
  
-   连接到单子网或多子网时使用 **MultiSubnetFailover** 连接属性，这二者的性能都会得到改进。  
  
-   若要连接到某一可用性组，请在您的连接字符串中将该可用性组的可用性组侦听器指定为服务器。  
  
-   连接到配置有超过 64 个 IP 地址的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例将导致连接失败。  
  
-   基于以下身份验证类型，使用 **MultiSubnetFailover** 连接属性的应用程序的行为不受影响：[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 身份验证、Kerberos 身份验证或 Windows 身份验证。  
  
-   增加 loginTimeout 的值，以延长故障转移时间并减少应用程序连接重试次数。  
  
-   不支持分布式事务。  
  
如果只读路由不起作用，则连接到可用性组中的辅助副本位置在以下情况下将失败：  
  
- 如果未将辅助副本位置配置为接受连接。  
  
- 如果应用程序使用 **ApplicationIntent=ReadWrite**（在下文中介绍）且将次要副本位置配置为只读访问。  
  
如果将主副本配置为拒绝只读工作负荷且连接字符串包含 **ApplicationIntent=ReadOnly**，连接将失败。  

## <a name="transparent-network-ip-resolution-tnir"></a>透明网络 IP 解析 (TNIR)

透明网络 IP 解析了 (TNIR) 是现有 MultiSubnetFailover 功能的修订版本。 第一个解析主机名的 IP 不响应，并且有多个 Ip 与主机名关联时，它会影响该驱动程序的连接顺序。 MultiSubnetFailover 以及他们提供以下四个连接序列： 

- 启用了 TNIR & MultiSubnetFailover 已禁用： 尝试一个 IP 后, 跟并行中的所有 Ip
- 启用了 TNIR & MultiSubnetFailover 启用： 尝试并行中的所有 Ip
- 已禁用了 TNIR & MultiSubnetFailover 已禁用： 所有 Ip 都尝试一个接一个
- 已禁用了 TNIR & MultiSubnetFailover 启用： 尝试并行中的所有 Ip

默认情况下，启用了 TNIR 和 MultiSubnetFailover 默认处于禁用状态。

这是启用了 TNIR 和 MultiSubnetFailover 使用 PDO_SQLSRV 驱动程序的示例：

```
<?php
$serverName = "yourservername";
$username = "yourusername";
$password = "yourpassword";
$connectionString = "sqlsrv:Server=$serverName; TransparentNetworkIPResolution=Enabled; MultiSubnetFailover=yes";
try {
    $conn = new PDO($connectionString, $username, $password, array(PDO::ATTR_ERRMODE => PDO::ERRMODE_EXCEPTION));
    // your code 
    // more of your code
    // when done, close the connection
    unset($conn);
} catch(PDOException $e) {
    print_r($e->errorInfo);
}
?>
```

## <a name="upgrading-to-use-multi-subnet-clusters-from-database-mirroring"></a>升级以便使用来自数据库镜像的多子网群集  
如果连接字符串中已存在 **MultiSubnetFailover** 和 **Failover_Partner** 连接关键字，将出现连接错误。 如果使用 **MultiSubnetFailover** 且 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 返回一个故障转移伙伴响应指示它是数据库镜像对的一部分，也将出现错误。  
  
如果将当前使用数据库镜像的 [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] 应用程序升级到多子网方案，则应删除 Failover_Partner 连接属性并使用设置为“是”的 MultiSubnetFailover 替换它，并且还应使用可用性组侦听程序替换连接字符串中的服务器名称。 如果连接字符串使用 Failover_Partner 和 MultiSubnetFailover=true，驱动程序将生成一个错误。 但是，如果连接字符串使用 Failover_Partner 和 MultiSubnetFailover=false（或 ApplicationIntent=ReadWrite），则该应用程序将使用数据库镜像。  
  
如果数据库镜像用于 AG 中的主数据库，并且 MultiSubnetFailover=true 用于连接到主数据库（而非连接到可用性组侦听程序）的连接字符串中，则驱动程序将返回错误。  


[!INCLUDE[specify-application-intent_read-only-routing](~/includes/paragraph-content/specify-application-intent-read-only-routing.md)]


## <a name="see-also"></a>另请参阅  
[连接到服务器](../../connect/php/connecting-to-the-server.md)  
  
