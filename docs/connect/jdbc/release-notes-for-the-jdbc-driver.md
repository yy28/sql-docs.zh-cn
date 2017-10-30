---
title: "JDBC 驱动程序的发行说明 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 074f211e-984a-4b76-bb15-ee36f5946f12
caps.latest.revision: 206
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: bd65725237fd625c40f8755e636bb4f6fa2c55ea
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="release-notes-for-the-jdbc-driver"></a>JDBC 驱动程序的发行说明
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

## <a name="updates-in-microsoft-jdbc-driver-62-for-sql-server"></a>Microsoft JDBC Driver 6.2 for SQL Server 中的更新
SQL Server 的 Microsoft JDBC 驱动程序 6.2 是完全符合 JDBC 4.1 和 4.2 的规范。 按照 Java 版本兼容性，6.0 包中包含 jar 进行命名。 例如，建议从 6.2 包 mssql jdbc 6.2.1.jre8.jar 文件与 Java 8 一起使用。 

**注意：**中发布了 2017 年 6 月 29 日 JDBC 6.2 RTW 找缓存改善的元数据的问题。 改善已回滚并且新 jar （版本 6.2.1） 已在 2017 年 7 月 17 日发行[Microsoft Download Center](https://go.microsoft.com/fwlink/?linkid=852460)， [GitHub](https://github.com/Microsoft/mssql-jdbc/releases/tag/v6.2.1)，和[Maven 中央](http://search.maven.org/#search%7Cgav%7C1%7Cg%3A%22com.microsoft.sqlserver%22%20AND%20a%3A%22mssql-jdbc%22)。 请更新你的项目以使用 6.2.1 释放 jar。 请查看[发行说明](https://github.com/Microsoft/mssql-jdbc/releases/tag/v6.2.1)有关详细信息。

**适用于 Linux 的 azure Active Directory (AAD) 支持**

连接到 Azure SQL 数据库使用通过用户名/密码和访问令牌的方法的 AAD 身份验证 Linux 应用程序。

**美国联邦信息处理标准 (FIPS) 启用 Jvm**

现在可上运行以 FIPS 140 兼容模式，以满足联邦标准和法规遵从性的 Jvm 使用 JDBC 驱动程序。 

**Kerberos 身份验证的改进** 

JDBC 驱动程序现在具有对支持： 
* 修改过的或无法检索新的令牌或 keytab Kerberos 配置不能为其中的应用程序的主体/密码方法。 此方法可以用于向 SQL Server 只允许对 Kerberos 身份验证进行身份验证。 
* 跨领域身份验证使用 Kerberos 集成身份验证，而无需显式设置服务器 SPN。 该驱动程序现在自动计算领域即使尚未提供。
* 通过接受 Kerberos 约束委派作为 GSS 凭据对象通过数据源模拟用户凭据。 然后，此模拟的凭据用于建立 Kerberos 连接。 

**添加的超时**

JDBC 驱动程序现在支持下列可配置超时可以更改基于应用程序的需求： 
* 若要控制运行查询时发生超时之前等待的秒数的查询超时值。 
* 若要指定的插槽上发生超时之前要等待的毫秒数读取，或接受的套接字超时。 

## <a name="updates-in-microsoft-jdbc-driver-61-for-sql-server"></a>Microsoft JDBC Driver 6.1 for SQL Server 中的更新

SQL Server 的 Microsoft JDBC 驱动程序 6.1 是完全符合 JDBC 4.1 和 4.2 的规范。 这是 JDBC 驱动程序的初始开源版本，其中包含 mssql jdbc 6.1.0.jre8.jar mssql jdbc 6.1.0.jre7.jar 文件，它们分别对应于的 Java 版本兼容性。 

## <a name="updates-in-microsoft-jdbc-driver-60-for-sql-server"></a>Microsoft JDBC Driver 6.0 for SQL Server 中的更新

SQL Server 的 Microsoft JDBC Driver 6.0 是完全符合 JDBC 4.1 和 4.2 的规范。 按照其符合 JDBC API 版本，6.0 包中包含 jar 进行命名。 例如，从 6.0 包 sqljdbc42.jar 文件是符合 JDBC API 4.2。 同样，sqljdbc41.jar 文件是符合 JDBC API 4.1。

若要确保你有正确的 sqljdbc42.jar 或 sqljdbc41.jar，运行以下代码行。 如果输出是"驱动程序版本： 6.0.7507.100"，你具有 JDBC Driver 6.0 包。
```
Connection conn = DriverManager.getConnection("jdbc:sqlserver://<server>;user=<user>;password=<password>;");
System.out.println("Driver version: " + conn.getMetaData().getDriverVersion());
```  
 **始终加密**  
  
 在 SQL Server 2016 中，一个新的安全功能，可确保敏感数据不会发生在以纯文本形式的 SQL Server 实例最近发布的始终加密功能的支持。 始终加密工作方式是以透明方式加密应用程序中的数据，从而使 SQL Server 将只处理加密数据而非纯文本值。 即使 SQL 实例或主机计算机遭到破坏，攻击者可以获取所有是敏感数据的加密文本。 有关详细信息，请参阅[Using Always Encrypted with JDBC 驱动程序](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md)。  
  
 **国际化的域名 (IDN)**  
  
 支持服务器名称的国际化域名 (IDN)。 有关详细信息，请参阅上使用国际域名[的 JDBC 驱动程序的国际功能](../../connect/jdbc/international-features-of-the-jdbc-driver.md)页。  
  
 **参数化的查询**  
  
 现在支持针对复杂查询（如子查询和/或联接）用预定义语句检索参数元数据。 请注意此改进仅在使用 SQL Server 2012 和更新版本时才可用。  
  
 **Azure Active Directory (AAD)**  
  
 AAD 身份验证是连接到 Azure SQL 数据库 v12 的一种机制在 AAD 中使用的标识。 使用 AAD 身份验证来集中管理标识的数据库用户和作为 SQL Server 身份验证的替代方法。 JDBC Driver 6.0，可在要连接到 Azure SQL DB 的 JDBC 连接字符串中指定你的 AAD 凭据。  有关详细信息，请参阅上的身份验证属性[设置连接属性](../../connect/jdbc/setting-the-connection-properties.md)页。  
  
 **表值参数**  
  
 表值参数提供的数据从客户端应用程序到 SQL Server 的多个行封送而无需多次往返或特殊服务器端逻辑来处理数据的简单办法。 表值参数可用于封装客户端应用程序中的数据行并将数据发送到单个参数化命令中的服务器。 可以随后会作用于通过使用 TRANSACT-SQL 的表变量中存储的传入数据行。 有关详细信息，请参阅[Using Table-Valued 参数](../../connect/jdbc/using-table-valued-parameters.md)。  
  
 **AlwaysOn 可用性组 (AG)**  
  
 该驱动程序现在支持透明连接到 AlwaysOn 可用性组。 该驱动程序快速发现当前的 AlwaysOn 拓扑的服务器基础结构，并以透明方式连接到当前的活动服务器。  
  
## <a name="updates-in-microsoft-jdbc-driver-42-for-sql-server-and-later"></a>Microsoft JDBC Driver 4.2 for SQL Server 及更高版本中的更新  
SQL Server 的 Microsoft JDBC Driver 4.2 是完全符合 JDBC 4.1 和 4.2 的规范。 按照其符合 JDBC API 版本，4.2 包中包含 jar 进行命名。 例如，从 4.2 包 sqljdbc42.jar 文件是符合 JDBC API 4.2。 同样，sqljdbc41.jar 文件是符合 JDBC API 4.1。

若要确保你有正确的 sqljdbc42.jar 或 sqljdbc41.jar，运行以下代码行。 如果输出是"驱动程序版本： 4.2.6420.100"，你具有 JDBC Driver 4.2 包。
```
Connection conn = DriverManager.getConnection("jdbc:sqlserver://<server>;user=<user>;password=<password>;");
System.out.println("Driver version: " + conn.getMetaData().getDriverVersion());
```
 **对 JDK 8 的支持**  
  
 除 JDK 7.0、6.0 和 5.0 外，还支持 Java 开发工具包 (JDK) 8.0 版。  
  
 **JDBC 4.1 和 4.2 法规遵从性**  
  
 对 Java Database Connectivity API 4.1 和 4.2 规范以及 4.0 的支持。 有关详细信息，请参阅[JDBC 驱动程序的 JDBC 4.1 符合性](../../connect/jdbc/jdbc-4-1-compliance-for-the-jdbc-driver.md)和[JDBC 驱动程序的 JDBC 4.2 法规遵从性](../../connect/jdbc/jdbc-4-2-compliance-for-the-jdbc-driver.md)。  
  
 **大容量复制**  
  
 大容量复制功能用于将大量数据快速复制到 SQL Server 数据库的表或视图中。 有关详细信息，请参阅[使用 JDBC 驱动程序使用大容量复制](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md)。  
  
 **XA 事务回滚选项**  
  
 为现有自动回滚尚未准备好的事务新增了超时选项。 有关详细信息请参阅[了解 XA 事务](../../connect/jdbc/understanding-xa-transactions.md)。  
  
 **新的 Kerberos 主体连接属性**  
  
 新增了连接属性，以便增强与 Kerberos 连接的灵活性。 有关详细信息请参阅[使用 Kerberos 集成身份验证连接到 SQL Server](../../connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md)。  
  
## <a name="updates-in-microsoft-jdbc-driver-41-for-sql-server-and-later"></a>Microsoft JDBC Driver 4.2 for SQL Server 及更高版本中的更新  
 **对 JDK 7 的支持**  
  
 除 JDK 6.0 和 5.0 外，还支持 Java 开发工具包 (JDK) 版本 7.0。  
  
## <a name="updates-in-microsoft-jdbc-driver-40-for-sql-server-and-later"></a>Microsoft JDBC Driver 4.0 for SQL Server 及更高版本中的更新  
 **有关连接到 Azure SQL 数据库的信息**  
  
 现在有一个有关连接 Azure SQL Database 的信息的主题。 请参阅[连接到 Azure SQL 数据库](../../connect/jdbc/connecting-to-an-azure-sql-database.md)有关详细信息。  
  
 **对高可用性、 灾难恢复的支持**  
  
 高可用性、 灾难恢复到的连接中的 AlwaysOn 可用性组支持[!INCLUDE[ssSQL11](../../includes/sssql11_md.md)]。 请参阅[的高可用性、 灾难恢复的 JDBC 驱动程序支持](../../connect/jdbc/jdbc-driver-support-for-high-availability-disaster-recovery.md)有关详细信息。  
  
 **使用 Kerberos 集成身份验证连接到 SQL Server**  
  
 对应用程序连接到的类型 4 Kerberos 集成身份验证的支持[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]数据库。 有关详细信息，请参阅[使用 Kerberos 集成身份验证连接到 SQL Server](../../connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md)。 (键入集成身份验证是中可用的 2 Kerberos [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 4.0 之前的版本。)  
  
 **访问扩展的事件日志中的诊断信息**  
  
 你可以访问服务器的扩展事件日志中的信息，了解连接失败的原因。 有关详细信息，请参阅[访问扩展事件日志中的诊断信息](../../connect/jdbc/accessing-diagnostic-information-in-the-extended-events-log.md)。  
  
 **稀疏列的附加支持**  
  
 如果你的应用程序已访问使用稀疏列的表中的数据，则应看到性能有所提高。 你可以 （包括稀疏列信息） 的列的信息与[getColumns 方法 &#40;SQLServerDatabaseMetaData &#41;](../../connect/jdbc/reference/getcolumns-method-sqlserverdatabasemetadata.md). 有关详细信息[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]稀疏列，请参阅[使用稀疏列](http://go.microsoft.com/fwlink/?LinkId=224244)。  
  
 **Xid.getFormatId**  
  
 从[!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)]，JDBC 驱动程序将从数据库服务器到应用程序传递格式标识符。 若要获取更新的行为，请确保服务器上的 sqljdbc_xa.dll 已更新。 Sqljdbc_xa.dll 的更新的版本复制到服务器的详细信息，请参阅[了解 XA 事务](../../connect/jdbc/understanding-xa-transactions.md)。  
  
## <a name="itanium-not-supported-for-jdbc-driver-60-42-41-and-40-applications"></a>JDBC Driver 6.0、 4.2、 4.1 和 4.0 的应用程序不支持 Itanium  
  
 Microsoft JDBC Drivers 6.0、 4.2、 4.1 和 4.0 for SQL Server 应用程序不支持在 Itanium 的计算机上运行。  
  
## <a name="see-also"></a>另请参阅  
 [JDBC 驱动程序概述](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
  
  

