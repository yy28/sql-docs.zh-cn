---
title: 对高可用性、 Microsoft Drivers for PHP for SQL Server 的灾难恢复支持 |Microsoft 文档
ms.custom: ''
ms.date: 04/04/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 73a80821-d345-4fea-b076-f4aabeb4af3e
caps.latest.revision: 15
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 152ada5137bd1e803f4cfe3ef9d34d30f90acfe7
ms.sourcegitcommit: f16003fd1ca28b5e06d5700e730f681720006816
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/11/2018
ms.locfileid: "35308873"
---
# <a name="support-for-high-availability-disaster-recovery"></a>支持高可用性、灾难恢复
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

本主题讨论[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]（中添加的支持版本 3.0） 的高可用性、 灾难恢复- [!INCLUDE[ssHADR](../../includes/sshadr_md.md)]。  在 [!INCLUDE[ssHADR](../../includes/sshadr_md.md)] 中添加了 [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)] 支持。 有关 [!INCLUDE[ssHADR](../../includes/sshadr_md.md)]的详细信息，请参阅 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 联机丛书。  
  
在 3.0 版[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]，你可以指定的可用性组侦听器 （高可用性、 灾难恢复） 连接属性中的可用性组 (AG)。 如果[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]应用程序连接到故障转移的 AlwaysOn 数据库，原始连接已断开，且该应用程序必须打开新的连接在故障转移后继续工作。  
  
如果你没有连接到可用性组侦听器，并且如果多个 IP 地址关联一个主机名，[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]将按顺序循环访问与 DNS 条目关联的所有 IP 地址。 如果 DNS 服务器返回的第一个 IP 地址未绑定到任何网络接口卡 (NIC)，则上述遍历操作可能会用时较长。 当连接到可用性组侦听器，[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]进行的通信，如果连接尝试建立与所有 IP 地址的连接尝试成功，则将驱动程序将丢弃所有挂起的连接尝试。  
  
> [!NOTE]  
> 增大连接超时值和实现连接重试逻辑将增加应用程序连接到可用性组的概率。 此外，由于可用性组进行故障转移而可能使连接失败，您应实现连接重试逻辑，重试失败的连接，直至重新连接。  
  
## <a name="connecting-with-multisubnetfailover"></a>使用 MultiSubnetFailover 进行连接  
**MultiSubnetFailover**连接属性指示在某一可用性组或故障转移群集实例，并部署应用程序[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]将尝试连接到主上的数据库[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]实例尝试连接到所有 IP 地址。 当**MultiSubnetFailover = true**指定对于连接，则客户端的重试 TCP 连接的频率比操作系统的默认 TCP 重新传输间隔快。 这样，就可以在对 AlwaysOn 可用性组或 AlwaysOn 故障转移群集实例执行故障转移之后更快地进行重新连接，这一点同时适用于单子网和多子网可用性组和故障转移群集实例。  
  
始终指定**MultiSubnetFailover = True**时连接到 SQL Server 2012 可用性组侦听器或 SQL Server 2012 故障转移群集实例。 **MultiSubnetFailover**可更快的故障转移支持的所有可用性组和 SQL Server 2012 中的故障转移群集实例并显著减少单个和多子网 AlwaysOn 拓扑的故障转移时间。 在多子网故障转移过程中，客户端将尝试并行进行连接。 在子网故障转移，[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]将积极重试 TCP 连接。  
  
有关详细信息中的连接字符串关键字[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]，请参阅[连接选项](../../connect/php/connection-options.md)。  
  
指定**MultiSubnetFailover = true**时连接到内容以外的可用性组侦听器或故障转移群集实例可能会导致性能下降，并且不支持。  
  
使用以下准则可以连接到可用性组中的服务器：  
  
-   连接到单子网或多子网时使用 **MultiSubnetFailover** 连接属性，这二者的性能都会得到改进。  
  
-   若要连接到某一可用性组，请在您的连接字符串中将该可用性组的可用性组侦听器指定为服务器。  
  
-   连接到配置有超过 64 个 IP 地址的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 实例将导致连接失败。  
  
-   基于以下身份验证类型，使用 **MultiSubnetFailover** 连接属性的应用程序的行为不受影响：[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 身份验证、Kerberos 身份验证或 Windows 身份验证。  
  
-   值增加**loginTimeout**以调整故障转移时间并减少应用程序连接重试尝试。  
  
-   不支持分布式事务。  
  
如果只读路由不起作用，则连接到可用性组中的辅助副本位置在以下情况下将失败：  
  
1.  如果未将辅助副本位置配置为接受连接。  
  
2.  如果应用程序使用 **ApplicationIntent=ReadWrite**（在下文中介绍）且将次要副本位置配置为只读访问。  
  
如果将主副本配置为拒绝只读工作负荷且连接字符串包含 **ApplicationIntent=ReadOnly**，连接将失败。  
  
## <a name="upgrading-to-use-multi-subnet-clusters-from-database-mirroring"></a>升级以便使用来自数据库镜像的多子网群集  
如果连接字符串中已存在 **MultiSubnetFailover** 和 **Failover_Partner** 连接关键字，将出现连接错误。 如果使用 **MultiSubnetFailover** 且 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 返回一个故障转移伙伴响应指示它是数据库镜像对的一部分，也将出现错误。  
  
如果升级[!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]应用程序当前使用数据库镜像到多子网方案中，你应该删除**Failover_Partner**连接属性并将其替换**MultiSubnetFailover**设置为**是**并将连接字符串中的服务器名称替换为可用性组侦听器。 如果使用的连接字符串**Failover_Partner**和**MultiSubnetFailover = true**，驱动程序将生成错误。 但是，如果使用的连接字符串**Failover_Partner**和**MultiSubnetFailover = false** (或**ApplicationIntent = ReadWrite**)，应用程序将使用数据库镜像。  
  
该驱动程序将返回错误，如果在 AG 中，在主数据库上使用数据库镜像，并且**MultiSubnetFailover = true**在连接到主数据库而不是到可用性组的连接字符串中使用侦听器。  


[!INCLUDE[specify-application-intent_read-only-routing](~/includes/paragraph-content/specify-application-intent-read-only-routing.md)]


## <a name="see-also"></a>请参阅  
[连接到服务器](../../connect/php/connecting-to-the-server.md)  
  
