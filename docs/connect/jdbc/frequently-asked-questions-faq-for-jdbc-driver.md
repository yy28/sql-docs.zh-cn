---
title: "常见问题 (FAQ) JDBC 驱动程序 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: cbc0e397-ecf2-4494-87b2-a492609bceae
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: e68c34ad2b9e444b39bf3ce8a5cfa33ad2dcd00c
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2017
---
# <a name="frequently-asked-questions-faq-for-jdbc-driver"></a>常见问题 (FAQ) JDBC 驱动程序
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  本文提供有关 Microsoft SQL Server JDBC 驱动程序常见问题的解答。  
  
## <a name="frequently-asked-questions"></a>常见问题  
**如何帮助改进 JDBC 驱动程序？**  
JDBC 驱动程序属于开放源代码，可以在上找到源代码[GitHub](https://github.com/microsoft/mssql-jdbc)。 你可以帮助提高驱动程序通过提出问题并导致基本代码。

**该驱动程序支持的 SQL Server 和 Java 的版本？**  
 请参阅[Microsoft JDBC Driver for SQL Server 支持矩阵](../../connect/jdbc/microsoft-jdbc-driver-for-sql-server-support-matrix.md)页面了解详细信息。  
  
 **升级我的驱动程序时，我应该知道哪些内容？**  
 Microsoft JDBC 驱动程序 6.2 支持 JDBC 4.0、 4.1 和 4.2 规范和，如下所示安装包中包括两个 JAR 类库：  
  
|JAR|JDBC 规范|JDK 版本|  
|-|-|-|  
|mssql jdbc 6.2.1.jre8.jar|JDBC 4.2、4.1 和 4.0|JDK 8.0|  
|mssql jdbc 6.2.1.jre7.jar|JDBC 4.1 和 4.0|JDK 7.0|  
 
 Microsoft JDBC 驱动程序 6.0 和 SQL Server 的 4.2 支持 JDBC 4.0、 4.1 和 4.2 规范，并且，如下所示安装包中包括两个 JAR 类库：  
  
|JAR|JDBC 规范|JDK 版本|   
|-|-|-|  
|sqljdbc42.jar|JDBC 4.2、4.1 和 4.0|JDK 8.0|  
|sqljdbc41.jar|JDBC 4.1 和 4.0|JDK 7.0|  
  
 SQL Server 的 Microsoft JDBC Driver 4.1 支持 JDBC 4.0 规范，，如下所示安装包中包括一个 JAR 类库：  
  
|JAR|JDBC 规范|JDK 版本|    
|-|-|-|  
|sqljdbc41.jar|JDBC 4.0|JDK 7.0 和 6.0|
  
 Microsoft SQL Server JDBC 驱动程序 4.0 同时支持 JDBC 3.0 和 JDBC 4.0 规格，并且每种规格的安装包中分别包含两个 JAR 类库：sqljdbc.jar 和 sqljdbc4.jar。  
  
|JAR|JDBC 规范|JDK 版本|   
|-|-|-|  
|sqljdbc4.jar|JDBC 4.0|JDK 6.0 和 5.0|  
|sqljdbc.jar|JDBC 3.0|JDK 6.0 和 5.0|  
  
 **是否需要在我的应用程序的最新的驱动程序用于我现有的 SQL Server 版本中进行任何代码更改？**  
 一般而言，驱动程序都设计为可向后兼容，因此升级驱动程序时并不需要更改现有应用程序。 中，新的驱动程序版本引入了一项重大更改， [JDBC 驱动程序的发行说明](../../connect/jdbc/release-notes-for-the-jdbc-driver.md)部分将提供有关的更改和对现有应用程序的影响的清除的详细信息。 此外，还可以查看该驱动程序附带的发行说明，了解该版本中已修复的 bug 列表和已知问题。  
  
 **该驱动程序费用是多少？**  
 Microsoft SQL Server JDBC 驱动程序是免费提供的，不需要额外付费。  
  
 **可以重新分发的驱动程序？** JDBC Drivers 4.1、 4.2、 6.0 中和 6.2 是可再发行组件。 请查看许可协议中的"可分发代码"子句。
 
 JDBC Driver 4.0 是需要注册的单独重新分发许可自由可再发行组件。 若要注册或详细信息，请参阅我们[重新分发 Microsoft JDBC Driver](../../connect/jdbc/redistributing-the-microsoft-jdbc-driver.md)。 
 
   
 **可以使用该驱动程序从 Linux 计算机访问 Microsoft SQL Server？** 可以！ 可以使用该驱动程序从 Linux、Unix 及其他非 Windows 平台访问 SQL Server。 请参阅我们[Microsoft JDBC Driver for SQL Server 支持矩阵](../../connect/jdbc/microsoft-jdbc-driver-for-sql-server-support-matrix.md)有关详细信息。  
  
 **该驱动程序是否支持安全套接字层 (SSL) 加密？** 从 1.2 版起，该驱动程序就支持安全套接字层 (SSL) 加密。 有关详细信息，请参阅[使用 SSL 加密](../../connect/jdbc/using-ssl-encryption.md)。  
  
 **SQL Server 的 Microsoft JDBC 驱动程序支持哪些身份验证类型？**  
 下表列出了可用的身份验证选项。 注意，从 4.0 版起，该驱动程序就提供了纯 Java Kerberos 身份验证选项。  
  
|||  
|-|-|  
|平台|身份验证|  
|非 Windows|纯 Java Kerberos|  
|非 Windows|SQL Server|  
|Windows|纯 Java Kerberos|  
|Windows|SQL Server|  
|Windows|具有 NTLM 备份的 Kerberos|  
|Windows|NTLM|  
  
**该驱动程序是否支持 Internet 协议版本 6 (IPv6) 地址？**  
 支持。该驱动程序支持结合使用 IPv6 地址以及连接属性集合和 serverName 连接字符串属性。 有关详细信息，请参阅[生成连接 URL](../../connect/jdbc/building-the-connection-url.md)。  
  
**什么是自适应缓冲？**  
 从 Microsoft SQL Server 2005 JDBC 驱动程序 1.2 版起，就引入了自适应缓冲。自适应缓冲的作用是在不占用服务器游标的情况下检索任何类型的大值数据。 Microsoft SQL Server JDBC 驱动程序的自适应缓冲功能提供连接字符串属性 responseBuffering，该属性可以设置为“adaptive”或“full”。 从 JDBC 驱动程序 2.0 版起，该驱动程序的默认行为就是“adaptive”。 换言之，要获取自适应缓冲行为，应用程序不必显式请求自适应行为。 不过，在 1.2 版中，缓冲模式默认为“full”，即应用程序必须显式请求自适应缓冲模式。 有关详细信息，请参阅[使用自适应缓冲](../../connect/jdbc/using-adaptive-buffering.md)主题和博客[什么 adaptiveresponse 缓冲和为何要使用它？](http://go.microsoft.com/fwlink/?LinkId=111575)。  
  
**驱动程序支持连接池？**  
 该驱动程序支持 Java 平台 Enterprise Edition 5 (Java EE 5) 连接池。 该驱动程序实现了 JDBC 3.0 所需的接口，从而参与到任何中间件应用程序供应商提供的任何连接池实现中。 该驱动程序将参与这些环境中的已池化连接。 有关详细信息，请参阅[使用连接池](../../connect/jdbc/using-connection-pooling.md)。 该驱动程序不提供自己的池实现，而是依赖第三方的 Java 应用程序服务器。  
  
**是否支持可用驱动程序？**  
 该驱动程序提供几种支持选项。 你可以将问题发布或颁发给我们[GitHub 存储库](https://github.com/microsoft/mssql-jdbc)这由 Microsoft 进行监视。 [论坛](http://go.microsoft.com/fwlink/?LinkID=246673)由 Microsoft、 MVP 和社区监视。 还可以联系 Microsoft 客户支持服务部门。 我们可能会要求你在任何第三方应用程序服务器外重现问题。 如果不能在托管的 Java 容器环境之外重现问题，你将需要联系相关的第三方，以便我们继续为你提供帮助。 我们可能会要求你在 Windows 等操作系统上重现问题，以便为你提供最佳的帮助。  
  
**与任何第三方应用程序服务器的使用进行了认证驱动程序？**
已针对各种应用程序服务器（包括 IBM WebSphere 和 SAP NetWeaver）对该驱动程序进行了测试。  
  
**如何启用跟踪？**  
 该驱动程序支持使用跟踪（或日志记录）来帮助解决在应用程序中使用 JDBC 驱动程序时遇到的问题。 为了启用客户端 JAR 跟踪的使用，JDBC 驱动程序将在 java.util.logging 中使用日志记录 API。 有关详细信息，请参阅[跟踪驱动程序操作](../../connect/jdbc/tracing-driver-operation.md)。 对于客户端 XA 跟踪，请参阅 [Data Access Tracing in SQL Server（SQL Server 中的数据访问跟踪）](http://go.microsoft.com/fwlink/?LinkId=248705)。  
  
**其中可以下载的驱动程序，例如 SQL Server 2000 JDBC 驱动程序，2005年驱动程序的较旧版本 1.0、 1.1、 或 1.2 驱动程序？**  
 这些驱动程序版本已不再受到支持，因此不能下载。 我们正在不断改善我们的 Java 连接支持。 因此，我们强烈建议你使用最新版的 JDBC 驱动程序。  
  
 **我使用的 JRE 1.4。哪个驱动程序适用于 JRE 1.4**正在使用 SAP 产品并且需要 JRE 1.4 支持的客户，您可以联系[SAPService Marketplace](http://service.sap.com/)以获取 1.2 的 Microsoft JDBC 驱动程序。  
  
**可以通过验证的 FIPS 的算法驱动程序连接？** Microsoft JDBC 驱动程序不包含任何加密算法。 如果客户使用联邦信息处理标准 (FIPS) 认为可以接受的操作系统、应用程序和 JVM 算法，并将该驱动程序配置为使用这些算法，则该驱动程序将仅使用指定的算法进行通信。  
  
  
