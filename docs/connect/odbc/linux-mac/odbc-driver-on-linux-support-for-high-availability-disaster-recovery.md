---
title: "在 Linux 和 macOS 的高可用性和灾难恢复上的 ODBC 驱动程序 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: fa656c5b-a935-40bf-bc20-e517ca5cd0ba
caps.latest.revision: "16"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 53553cc88d771aeb7ef7d537309583fb49e1aaa6
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2017
---
# <a name="odbc-driver-on-linux-and-macos-support-for-high-availability-and-disaster-recovery"></a>在 Linux 和 macOS 用于高可用性和灾难恢复的支持上的 ODBC 驱动程序
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Linux 和 macOS 支持的 ODBC 驱动程序[!INCLUDE[ssHADR](../../../includes/sshadr_md.md)]。 有关 [!INCLUDE[ssHADR](../../../includes/sshadr_md.md)] 的详细信息，请参阅：  
  
-   [可用性组侦听器、 客户端连接和应用程序故障转移 (SQL Server)](http://msdn.microsoft.com/library/hh213417.aspx)  
  
-   [创建和配置可用性组 (SQL Server)](http://msdn.microsoft.com/library/ff878265.aspx)  
  
-   [故障转移群集和 AlwaysOn 可用性组 (SQL Server)](http://msdn.microsoft.com/library/ff929171.aspx)  
  
-   [活动辅助副本： 可读辅助副本 （AlwaysOn 可用性组）](http://msdn.microsoft.com/library/ff878253.aspx)  
  
您可以在连接字符串中指定给定可用性组的可用性组侦听器。 如果在 Linux 或 macOS 上的 ODBC 应用程序连接到故障转移可用性组中的数据库，原始连接已断开，且该应用程序必须打开新的连接在故障转移后继续工作。

在 Linux 和 macOS 上的 ODBC 驱动程序按顺序循环访问与 DNS 主机名，如果你没有连接到可用性组侦听器，并且多个 IP 地址与主机名关联的所有 IP 地址。

如果 DNS 服务器返回的第一个 IP 地址不是可连接的这些迭代很费时间。 连接到可用性组侦听器时，驱动程序将尝试并行建立所有 IP 地址的连接。 如果连接尝试成功，驱动程序将丢弃所有挂起的连接尝试。

> [!NOTE]  
> 由于可用性组故障转移情况下，连接可能会失败，因为实现连接重试逻辑;重试失败的连接，直到它重新连接。 增大连接超时和实现连接重试逻辑会提高连接到可用性组的几率。

## <a name="connecting-with-multisubnetfailover"></a>使用 MultiSubnetFailover 进行连接

始终指定**MultiSubnetFailover = Yes** (或**= True**) 时连接到[!INCLUDE[ssSQL11](../../../includes/sssql11_md.md)]可用性组侦听器或[!INCLUDE[ssSQL11](../../../includes/sssql11_md.md)]故障转移群集实例。 **MultiSubnetFailover**可以实现更快的故障转移的所有可用性组和故障转移群集实例中的[!INCLUDE[ssSQL11](../../../includes/sssql11_md.md)]。 **MultiSubnetFailover**也大大降低了单个和多子网 AlwaysOn 拓扑的故障转移时间。 在多子网故障转移过程中，客户端将尝试并行连接。 子网故障转移期间，该驱动程序积极地重试 TCP 连接。

**MultiSubnetFailover** 连接属性指示将在可用性组或故障转移群集实例中部署应用程序。 此驱动程序尝试连接到主计算机上数据库[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]实例尝试连接到所有 IP 地址。 在连接时**MultiSubnetFailover = Yes**，客户端的重试 TCP 连接的频率比操作系统的默认 TCP 重新传输间隔快。 **MultiSubnetFailover=Yes** 会在 AlwaysOn 可用性组或 AlwaysOn 故障转移群集实例的故障转移之后进行更快速的重新连接。 **MultiSubnetFailover = Yes**适用于单-和多-subnet 可用性组和故障转移群集实例。  

连接到可用性组侦听程序或故障转移群集实例后，请使用 **MultiSubnetFailover=Yes** 。 否则，应用程序的性能可能会产生负面影响。

连接到可用性组或故障转移群集实例中的服务器时，请注意以下事项：
  
-   指定**MultiSubnetFailover = Yes**若要连接到单个子网或多子网可用性组时提高性能。

-   指定为你的连接字符串中的服务器的可用性组的可用性组侦听器。
  
-   无法连接到[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]实例配置了 64 个以上的 IP 地址。

-   同时[!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]身份验证或 Kerberos 身份验证可与**MultiSubnetFailover = Yes**而不会影响应用程序的行为。

-   你可以提高 **loginTimeout** 的值以调整故障转移时间并减少应用程序的连接重试尝试。

-   不支持分布式事务。  
  
如果只读路由不起作用，则连接到可用性组中的辅助副本位置将在以下情况下失败：  
  
1.  如果未将辅助副本位置配置为接受连接。  
  
2.  如果应用程序使用 **ApplicationIntent=ReadWrite** 且将辅助副本位置配置为只读访问。  
  
如果将主副本配置为拒绝只读工作负荷且连接字符串包含 **ApplicationIntent=ReadOnly**，连接将失败。  
  
## <a name="specifying-application-intent"></a>指定应用程序意向  
如果使用 **ApplicationIntent=ReadOnly**，在连接到某一启用了 AlwaysOn 的数据库时，客户端将请求读取工作负荷。 在连接时和 USE 数据库语句期间但仅对启用 AlwaysOn 的数据库，服务器强制执行该意向。

**ApplicationIntent** 关键字不适用于早期的只读数据库。  

数据库可允许或禁止目标 AlwaysOn 数据库上的读取工作负荷。 (使用**ALLOW_CONNECTIONS**子句**PRIMARY_ROLE**和**SECONDARY_ROLE** [!INCLUDE[tsql](../../../includes/tsql_md.md)]语句。)  
  
**ApplicationIntent** 关键字用于启用只读路由。  
  
## <a name="read-only-routing"></a>只读路由  
只读路由是一项功能，可用于确保数据库的只读副本的可用性。 启用只读路由：  
  
1.  连接到某一“Always On 可用性组”可用性组侦听程序。  
  
2.  **ApplicationIntent** 连接字符串关键字必须设置为 **ReadOnly**。  
  
3.  数据库管理员必须配置可用性组才能启用只读路由。  
  
多个使用只读路由的连接有可能连接到不同的只读副本。 对数据库同步进行更改或对服务器的路由配置进行更改可能导致客户端连接到不同的只读副本。 若要确保所有只读请求连接到相同的只读副本，请不要向 **Server** 连接关键字传递可用性组侦听程序。 而是指定只读实例的名称。  
  
期望与只读路由的连接时间长于连接主副本的时间。 因此，增加你的登录超时。 只读路由首先会连接到主副本，然后查找最合适的可读辅助副本。  
  
## <a name="odbc-syntax"></a>ODBC 语法

两个 ODBC 连接字符串关键字均支持[!INCLUDE[ssHADR](../../../includes/sshadr_md.md)]:  
  
-   **ApplicationIntent**  
  
-   **MultiSubnetFailover**  
  
有关 ODBC 连接字符串关键字的详细信息，请参阅 [将连接字符串关键字用于 SQL Server Native Client](http://msdn.microsoft.com/library/ms130822.aspx)。  
  
等效的连接属性包括：
  
-   **SQL_COPT_SS_APPLICATION_INTENT**  
  
-   **SQL_COPT_SS_MULTISUBNET_FAILOVER**  
  
有关 ODBC 连接属性的详细信息，请参阅[SQLSetConnectAttr](http://msdn.microsoft.com/library/ms131709.aspx)。  
  
ODBC 应用程序使用[!INCLUDE[ssHADR](../../../includes/sshadr_md.md)]可以使用两个函数之一来建立连接：  
  
|函数|Description|  
|------------|---------------|  
|[SQLConnect 函数](../../../odbc/reference/syntax/sqlconnect-function.md)|**SQLConnect**同时支持**ApplicationIntent**和**MultiSubnetFailover**通过数据源名称 (DSN) 或连接属性。|  
|[SQLDriverConnect 函数](../../../odbc/reference/syntax/sqldriverconnect-function.md)|**SQLDriverConnect**支持**ApplicationIntent**和**MultiSubnetFailover**通过 DSN、 连接字符串关键字或连接属性。|
  
## <a name="see-also"></a>另请参阅  

[连接字符串关键字和数据源名称 (DSN)](../../../connect/odbc/linux-mac/connection-string-keywords-and-data-source-names-dsns.md)

[编程指南](../../../connect/odbc/linux-mac/programming-guidelines.md)

[发行说明](../../../connect/odbc/linux-mac/release-notes.md)  
