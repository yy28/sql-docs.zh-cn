---
title: Linux 和 macOS 上的 ODBC 驱动程序 - 高可用性和灾难恢复 | Microsoft Docs
ms.custom: ''
ms.date: 04/05/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: fa656c5b-a935-40bf-bc20-e517ca5cd0ba
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: f53fc932ced3c5a4e002c9938a9af6a2b8d410e1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66798774"
---
# <a name="odbc-driver-on-linux-and-macos-support-for-high-availability-and-disaster-recovery"></a>Linux 和 macOS 上的 ODBC 驱动程序对高可用性和灾难恢复的支持
[!INCLUDE[Driver_ODBC_Download](../../../includes/driver_odbc_download.md)]

Linux 和 macOS 的 ODBC 驱动程序支持 [!INCLUDE[ssHADR](../../../includes/sshadr_md.md)]。 有关 [!INCLUDE[ssHADR](../../../includes/sshadr_md.md)]的详细信息，请参阅：  
  
-   [可用性组侦听器、客户端连接和应用程序故障转移 (SQL Server)](https://msdn.microsoft.com/library/hh213417.aspx)  
  
-   [创建和配置可用性组 (SQL Server)](https://msdn.microsoft.com/library/ff878265.aspx)  
  
-   [故障转移群集和 AlwaysOn 可用性组 (SQL Server)](https://msdn.microsoft.com/library/ff929171.aspx)  
  
-   [活动次要副本：可读次要副本（AlwaysOn 可用性组）](https://msdn.microsoft.com/library/ff878253.aspx)  
  
您可以在连接字符串中指定给定可用性组的可用性组侦听器。 如果某一在 Linux 或 macOS 上的 ODBC 应用程序连接到进行故障转移的可用性组中的某个数据库，原始连接则将被断开，并且应用程序必须打开一个新的连接才能在故障转移后继续工作。

如果未连接到可用性组侦听程序，则 Linux 和 macOS 上的 ODBC 驱动程序将按顺序循环访问与 DNS 主机名关联的所有 IP 地址，会有多个 IP 地址与该主机名关联。

如果 DNS 服务器的第一个返回 IP 地址不可连接，则此类循环访问可能非常耗时。 当连接到可用性组侦听程序时，驱动程序将尝试建立与所有 IP 地址的并行连接。 如果连接尝试成功，驱动程序将丢弃所有挂起的连接尝试。

> [!NOTE]  
> 由于可用性组故障转移而可能使连接失败，因此请实现连接重试逻辑；重试失败的连接直至重新连接后为止。 增大连接超时和实现连接重试逻辑会提高连接到可用性组的几率。

## <a name="connecting-with-multisubnetfailover"></a>使用 MultiSubnetFailover 进行连接

当连接到 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 可用性组侦听程序或 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 故障转移群集实例时，应始终指定 MultiSubnetFailover=Yes  。 MultiSubnetFailover 会为 [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] 中的所有可用性组和故障转移群集实例启用更快速的故障转移  。 MultiSubnetFailover 还可以显著缩短单子网和多子网 AlwaysOn 拓扑的故障转移时间  。 在多子网故障转移过程中，客户端将尝试并行连接。 在子网故障转移期间，驱动程序会主动重试 TCP 连接。

**MultiSubnetFailover** 连接属性指示将在可用性组或故障转移群集实例中部署应用程序。 驱动程序会通过尝试连接到所有的 IP 地址，从而连接到主 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例上的数据库。 当与 MultiSubnetFailover=Yes连接时，客户端将以比操作系统默认的 TCP 重新传输间隔更快的速度重新尝试建立 TCP 连接  。 **MultiSubnetFailover=Yes** 会在 AlwaysOn 可用性组或 AlwaysOn 故障转移群集实例的故障转移之后进行更快速的重新连接。 MultiSubnetFailover=Yes 同时适用于单子网和多子网可用性组和故障转移群集实例  。  

连接到可用性组侦听程序或故障转移群集实例后，请使用 **MultiSubnetFailover=Yes** 。 否则，应用程序性能可能会受到负面影响。

在连接到可用性组或故障转移群集实例中的服务器时，请注意以下事项：
  
-   指定 MultiSubnetFailover=Yes 以在连接到单子网或多子网可用性组时提高性能  。

-   在连接字符串中将可用性组的可用性组侦听程序指定为服务器。
  
-   不能连接到配置了超过 64 个 IP 地址的 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 实例。

-   [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] 身份验证或 Kerberos 身份验证都可以用于 MultiSubnetFailover=Yes，并且不会影响应用程序的行为  。

-   你可以提高 **loginTimeout** 的值以调整故障转移时间并减少应用程序的连接重试尝试。

-   不支持分布式事务。  
  
如果只读路由不起作用，则连接到可用性组中的辅助副本位置将在以下情况下失败：  
  
1.  如果未将辅助副本位置配置为接受连接。  
  
2.  如果应用程序使用 **ApplicationIntent=ReadWrite** 且将辅助副本位置配置为只读访问。  
  
如果将主副本配置为拒绝只读工作负荷且连接字符串包含 **ApplicationIntent=ReadOnly**，连接将失败。  


[!INCLUDE[specify-application-intent_read-only-routing](~/includes/paragraph-content/specify-application-intent-read-only-routing.md)]


## <a name="odbc-syntax"></a>ODBC 语法

两个 ODBC 连接字符串关键字均支持 [!INCLUDE[ssHADR](../../../includes/sshadr_md.md)]：  
  
-   **ApplicationIntent**  
  
-   **MultiSubnetFailover**  
  
有关 ODBC 连接字符串关键字的详细信息，请参阅 [将连接字符串关键字用于 SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)。  
  
等效的连接属性为：
  
-   **SQL_COPT_SS_APPLICATION_INTENT**  
  
-   **SQL_COPT_SS_MULTISUBNET_FAILOVER**  
  
有关 ODBC 连接属性的详细信息，请参阅 [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)。  
  
使用 [!INCLUDE[ssHADR](../../../includes/sshadr_md.md)] 的 ODBC 驱动程序应用程序可以使用以下两个函数之一来建立连接：  
  
|函数|描述|  
|------------|---------------|  
|[SQLConnect 函数](../../../odbc/reference/syntax/sqlconnect-function.md)|SQLConnect 通过数据源名称 (DSN) 或连接属性同时支持 ApplicationIntent 和 MultiSubnetFailover    。|  
|[SQLDriverConnect 函数](../../../odbc/reference/syntax/sqldriverconnect-function.md)|SQLDriverConnect 通过 DSN、连接字符串关键字或连接属性支持 ApplicationIntent 和 MultiSubnetFailover    。|
  
## <a name="see-also"></a>另请参阅  

[连接字符串关键字和数据源名称 (DSN)](../../../connect/odbc/linux-mac/connection-string-keywords-and-data-source-names-dsns.md)

[编程指南](../../../connect/odbc/linux-mac/programming-guidelines.md)

[发行说明](../../../connect/odbc/linux-mac/release-notes-odbc-sql-server-linux-mac.md)  
