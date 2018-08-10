---
title: 设置连接属性 | Microsoft Docs
ms.custom: ''
ms.date: 07/31/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: f1b62700-f046-488d-bd6b-a5cd8fc345b7
caps.latest.revision: 154
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5f9d04ebd12618c273966cbe27371918d18776a9
ms.sourcegitcommit: e02c28b0b59531bb2e4f361d7f4950b21904fb74
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 08/02/2018
ms.locfileid: "39458341"
---
# <a name="setting-the-connection-properties"></a>设置连接属性

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

可以通过多种方式指定连接字符串的属性：

- 当使用 DriverManager 类进行连接时，在连接 URL 中通过“名称=值”属性进行指定。
- 作为名称 = 值属性中的*属性*的驱动程序管理器类中的 Connect 方法的参数。
- 在驱动程序数据源的适当的 setter 方法中指定值。 例如：  
  
    ```java
    datasource.setServerName(value)  
    datasource.setDatabaseName(value)  
    ```  
  
## <a name="remarks"></a>Remarks

属性名不区分大小写，重复的属性名将按以下顺序进行解析：  
  
1. API 参数（如用户和密码）
2. 属性集合。  
3. 连接字符串中的最后一个实例。
  
此外，属性名允许使用未知的值，JDBC 驱动程序不会对这些值进行大小写验证。

允许使用同义词，并按顺序进行解析，如同处理重复的属性名。

下表列出了 JDBC 驱动程序当前可用的所有连接字符串属性。

| “属性”<br/>类型<br/>，则“默认” | 描述 |
| :------------------------------ | :---------- |
| accessToken<br/><br/>String<br/><br/>null | 此属性用于连接到 SQL 数据库使用的访问令牌。 **accessToken**不能使用连接 URL 进行设置。 |
| applicationIntent<br/><br/>String<br/><br/>ReadWrite | 连接到服务器时声明应用程序工作负荷类型。 <br/><br/>可能的值为 ReadOnly 和 ReadWrite。 <br/><br/>有关详细信息，请参阅[高可用性和灾难恢复的 JDBC 驱动程序支持](../../connect/jdbc/jdbc-driver-support-for-high-availability-disaster-recovery.md)。 |
| applicationName<br/><br/>String<br/>[&lt;=128 char]<br/><br/>null | 如果未提供名称，则使用应用程序名称或“[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]”。<br/><br/>用于在各种 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 分析和日志记录工具中标识特定的应用程序。 |
| 身份验证<br/><br/>String<br/><br/>NotSpecified | 从 Microsoft JDBC Driver 6.0 for SQL Server，此可选属性指示要用于连接的 SQL 身份验证方法。 可能的值为**ActiveDirectoryIntegrated**， **ActiveDirectoryPassword**， **SqlPassword**，以及默认**NotSpecified**.<br/><br/> 使用**ActiveDirectoryIntegrated**连接到使用集成的 Windows 身份验证的 SQL 数据库。<br/><br/> 使用**ActiveDirectoryPassword**以连接到 SQL 数据库使用的 Azure AD 主体名称和密码。<br/><br/> 使用**SqlPassword**连接到 SQL Server using**用户名**/**用户**并**密码**属性。<br/><br/> 使用**NotSpecified**如果这些身份验证方法不需要。<br/><br/> **重要说明：** 如果为 ActiveDirectoryIntegrated 设置身份验证，则需要安装以下两个库： **SQLJDBC_AUTH。DLL** （适用于 JDBC 驱动程序包） 和 Azure Active Directory 身份验证库，适用于 SQL Server (**ADALSQL。DLL**) （适用于 x86 和 amd64） 从下载中心中的不同语言中可用[Microsoft Active Directory 身份验证库，Microsoft SQL server](https://www.microsoft.com/download/details.aspx?id=48742)。 JDBC 驱动程序仅支持版本**1.0.2028.318 和更高版本**ADALSQL 的。DLL。<br/><br/> **注意：** 当身份验证属性设置为任何值以外**NotSpecified**，默认情况下的驱动程序使用安全套接字层 (SSL) 加密。<br/><br/> 有关如何配置 Azure Active Directory 身份验证信息，请访问[连接到 SQL 数据库使用 Azure Active Directory 身份验证](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/)。 |
| authenticationScheme<br/><br/>String<br/><br/>NativeAuthentication | 指示您的应用程序要使用哪一种集成安全性。 可能的值为**JavaKerberos**和默认**NativeAuthentication**。<br/><br/> 使用时**authenticationScheme = JavaKerberos**，必须在指定的完全限定的域名 (FQDN) **serverName**或**serverSpn**属性。 否则，将出现错误（Kerberos 数据库中找不到服务器）。<br/><br/> 有关使用的详细信息**authenticationScheme**，请参阅[使用 Kerberos 集成身份验证连接到 SQL Server](../../connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md)。 |
| cancelQueryTimeout<br/><br/>ssNoversion<br/><br/>-1 | 从开始 Microsoft JDBC Driver 6.4 for SQL Server，此属性可用于取消**queryTimeout**对连接设置。 查询执行挂起，并不会引发异常，如果以无提示方式删除与 SQL Server 的 TCP 连接。 此属性才适用，如果在连接上同时设置 queryTimeout。 <br/><br/>该驱动程序等待的总金额**cancelQueryTimeout** + **queryTimeout**秒，若要删除连接并关闭通道。 <br/><br/>此属性的默认值为-1，行为是无限期等待。 |
| columnEncryptionSetting<br/><br/>String<br/>["Enabled" &#124; "Disabled"]<br/><br/>禁用 | 从 Microsoft JDBC Driver 6.0 for SQL Server 开始，设置为“已启用”以使用 Always Encrypted (AE) 功能。 启用 AE后，JDBC 驱动程序以透明方式加密和解密存储在 SQL Server 中的加密数据库中的敏感数据。<br/><br/> 有关详细信息**方法是将 columnEncryptionSetting**，请参阅[JDBC 驱动程序中使用 Always Encrypted](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md)的更多详细信息。<br/><br/> **注意：** Always Encrypted，同时提供 SQL Server 2016 或更高版本。 |
| databaseName,<br/>“数据库”<br/><br/>String<br/>[&lt;=128 char]<br/><br/>null | 要连接到的数据库名称。 <br/><br/>如果未声明，则连接到默认的数据库。 |
| disableStatementPooling<br/><br/>boolean<br/>["true" &#124; "false"]<br/><br/>true | 指示是否应使用语句池的标记。 |
| enablePrepareOnFirst...<br/>PreparedStatementCall<br/><br/>boolean<br/>["true" &#124; "false"]<br/><br/>false | _enablePrepareOnFirstPreparedStatementCall_<br/><br/> 设置为"true"可通过调用启用已准备的语句句柄创建<code>sp_prepexec</code>中第一次执行已准备的语句。 <br/><br/>设置为"false"，以更改已准备的语句调用的第一次执行<code>sp_executesql</code>并不准备一条语句，它将调用第二次执行发生后<code>sp_prepexec</code>设置已准备的语句句柄。 |
| encrypt<br/><br/>boolean<br/>["true" &#124; "false"]<br/><br/>false | 如果设置为“true”，则指定在服务器安装了证书的情况下，[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 将为在客户端与服务器之间发送的所有数据使用安全套接字层 (SSL) 加密。 默认值为“false”。<br/><br/> 从 Microsoft JDBC Driver 6.0 for SQL Server，没有新连接设置身份验证，默认情况下使用 SSL 加密。 <br/><br/>有关详细信息，请参阅“authentication”属性。 |
| failoverPartner<br/><br/>String<br/><br/>null | 在数据库镜像配置中使用的故障转移服务器名称。 与主服务器进行初始连接时若发生失败，则会使用此属性；建立初始连接后，将忽略此属性。 必须与 databaseName 属性结合使用。<br/><br/> 注意：驱动程序不支持将故障转移伙伴实例的服务器实例端口号指定为连接字符串中 failoverPartner 属性的一部分。 但是，支持在同一连接字符串中指定主体服务器实例的 serverName、instanceName 和 portNumber 属性以及故障转移伙伴实例的 failoverPartner 属性。<br/><br/> 如果在 Server 连接属性中指定虚拟机名称，则无法使用数据库镜像。 有关详细信息，请参阅[JDBC 驱动程序支持对高可用性和灾难恢复](../../connect/jdbc/jdbc-driver-support-for-high-availability-disaster-recovery.md) |
| fips<br/><br/>boolean<br/>["true" &#124; "false"]<br/><br/>“false” | 此属性应为启用 FIPS 的 JVM **，则返回 true**。 |
| fipsProvider<br/><br/>String<br/><br/>null | JVM 中配置的 FIPS 提供程序。 例如，BCFIPS 或 SunPKCS11 NSS。 删除版本 6.4.0-中查看详细信息[此处](https://github.com/Microsoft/mssql-jdbc/pull/460)。 |
| gsscredential<br/><br/>org.ietf.jgss.GSSCredential<br/><br/>null | 从开始 Microsoft JDBC Driver 6.2 for SQL Server，可以在此属性中传递用户凭据以用于 Kerberos 约束委派。 <br/><br/>这应该用于**integratedSecurity**作为**true**并**JavaKerberos** **authenticationscheme**。 |
| hostNameInCertificate<br/><br/>String<br/><br/>null | 要用于验证 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] SSL 证书的主机名。<br/><br/> 如果未指定 hostNameInCertificate 属性或此属性设置为空，则 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 将使用连接 URL 上的 serverName 属性值作为主机名来验证 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] SSL 证书。<br/><br/> **注意：** 结合使用此属性**加密**/**身份验证**属性和**trustServerCertificate**属性。 此属性影响证书验证，当且仅当连接使用安全套接字层 (SSL) 加密和**trustServerCertificate**设置为"false"。 确保传递给 hostNameInCertificate 的值与服务器证书的公用名 (CN) 或使用者替代名称 (SAN) 中的 DNS 名称完全匹配，以便成功建立 SSL 连接。 有关详细信息，请参阅[了解 SSL 支持](../../connect/jdbc/understanding-ssl-support.md)。 |
| INSTANCENAME<br/><br/>String<br/>[&lt;=128 char]<br/><br/>null | 要连接到的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 实例名。 如果未指定，则连接到默认实例。 对于 instanceName 和端口均已指定的情况，请参阅有关端口的备注。<br/><br/> 如果在 Server 连接属性中指定虚拟机名称，则无法使用 instanceName 连接属性。 请参阅[高可用性和灾难恢复的 JDBC 驱动程序支持](../../connect/jdbc/jdbc-driver-support-for-high-availability-disaster-recovery.md)有关详细信息。 |
| integratedSecurity<br/><br/>boolean<br/>["true"&#124;"false"]<br/><br/>false | 设置为"true"表示，通过使用 Windows 凭据[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]Windows 操作系统上。 如果为“true”，则 JDBC 驱动程序将搜索本地计算机凭据缓存，以寻找在登录计算机或网络时已提供的凭据。<br/><br/> 设置为"true"(与**authenticationscheme = JavaKerberos**)，以指示由 Kerberos 凭据[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 有关 Kerberos 身份验证的详细信息，请参阅[使用 Kerberos 集成身份验证连接到 SQL Server](../../connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md)。 <br/><br/> 如果为“false”，则必须提供用户名和密码。 |
| jaasConfigurationName<br/><br/>String<br/><br/>SQLJDBCDriver | 从开始 Microsoft JDBC Driver 6.2 for SQL Server，SQL Server 的每个连接可以具有其自己 JAAS 登录配置文件以建立 Kerberos 连接。 可以通过此属性传递的登录配置文件的名称。 <br/> 默认情况下，驱动程序将属性设置`useDefaultCcache = true`为 IBM Jvm 和`useTicketCache = true`为其他 Jvm。 |
| keyStoreAuthentication<br/><br/>String<br/><br/>null | 从 Microsoft JDBC Driver 6.0 for SQL Server，此属性标识的无缝使用始终加密的连接设置的密钥存储区并确定用于存储密钥存储进行身份验证的身份验证机制。 Microsoft JDBC Driver 6.0 for SQL Server 支持设置向上 Java 密钥存储的无缝地使用此属性需要设置"**keyStoreAuthentication = JavaKeyStorePassword**"。 请注意，若要使用此属性，您还需要设置**keyStoreLocation**并**keyStoreSecret** Java 密钥存储的属性。 <br/><br/>有关详细信息，请参阅[对 JDBC 驱动程序使用 Always Encrypted](https://msdn.microsoft.com/library/mt591987%28v=sql.110%29.aspx?f=255&MSPPError=-2147217396)。 |
| keyStoreLocation<br/><br/>String<br/><br/>null | 当**keyStoreAuthentication = JavaKeyStorePassword**，则**keyStoreLocation**属性标识存储用于始终加密对列主密钥的 Java 密钥存储文件的路径数据。 请注意该路径必须包含的密钥存储文件名。<br/><br/>有关详细信息，请参阅[对 JDBC 驱动程序使用 Always Encrypted](https://msdn.microsoft.com/library/mt591987%28v=sql.110%29.aspx?f=255&MSPPError=-2147217396)。 |
| keyStoreSecret<br/><br/>String<br/><br/>null | 当**keyStoreAuthentication = JavaKeyStorePassword**，则**keyStoreSecret**属性标识要使用的密钥存储以及与该密钥的密码。 请注意，对于使用 Java 密钥存储的密钥存储和密钥的密码必须相同。<br/><br/>有关详细信息，请参阅[对 JDBC 驱动程序使用 Always Encrypted](https://msdn.microsoft.com/library/mt591987%28v=sql.110%29.aspx?f=255&MSPPError=-2147217396)。 |
| lastUpdateCount<br/><br/>boolean<br/>["true" &#124; "false"]<br/><br/>true | 如果值为“true”，则仅返回传递给服务器的 SQL 语句的最终更新计数，它可用于单个的 SELECT、INSERT 或 DELETE 语句中，以忽略由服务器触发器引起的其他更新计数。 将此属性设置为“false”可导致所有更新计数都被返回，包括由服务器触发器返回的更新计数。<br/><br/> 注意：此属性仅当与 [executeUpdate](../../connect/jdbc/reference/executeupdate-method-sqlserverstatement.md) 方法一起使用时才适用。 其他所有 execute 方法返回所有结果和更新计数。 此属性仅影响由服务器触发器返回的更新计数， 而不影响作为触发器执行结果的一部分的结果集或错误。 |
| lockTimeout<br/><br/>ssNoversion<br/><br/>-1 | 数据库报告锁定超时之前要等待的毫秒数。默认行为是无限期等待。 如果指定，该值将成为此连接上所有语句的默认值。 请注意， **Statement.setQueryTimeout()** 可以用来设置特定语句的超时值。 该值可为 0，这表示无需等待。 |
| loginTimeout<br/><br/>ssNoversion<br/>[0..65535]<br/><br/>15 | 因连接失败而中止连接之前驱动程序应等待的秒数。 零值表示该超时为默认系统超时，默认情况下指定为 15 秒。 非零值为因连接失败而中止连接之前驱动程序应等待的秒数。<br/><br/> 如果在 Server 连接属性中指定虚拟机名称，则应指定三分钟或更长的超时值，使故障转移连接有足够的时间连接成功。 请参阅[高可用性和灾难恢复的 JDBC 驱动程序支持](../../connect/jdbc/jdbc-driver-support-for-high-availability-disaster-recovery.md)有关详细信息。 |
| multiSubnetFailover<br/><br/>Boolean<br/><br/>false | 在连接到 [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)] 可用性组或 [!INCLUDE[ssSQL11](../../includes/sssql11_md.md)] 故障转移群集实例的可用性组侦听程序时，应始终指定 multiSubnetFailover=true。 multiSubnetFailover=true 将配置 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 以便更快地检测和连接到（当前）活动服务器。 可能的值为“True”和“False”。 请参阅[高可用性和灾难恢复的 JDBC 驱动程序支持](../../connect/jdbc/jdbc-driver-support-for-high-availability-disaster-recovery.md)有关详细信息。<br/><br/> 可以以编程方式访问带有 [getPropertyInfo](../../connect/jdbc/reference/getpropertyinfo-method-sqlserverdriver.md)、[getMultiSubnetFailover](../../connect/jdbc/reference/getmultisubnetfailover-method-sqlserverdatasource.md) 和 [setMultiSubnetFailover](../../connect/jdbc/reference/setmultisubnetfailover-method-sqlserverdatasource.md) 的 multiSubnetFailover 连接属性。<br/><br/> **注意：** 从 Microsoft JDBC Driver 6.0 for SQL Server，它不再需要设置**multiSubnetFailover**为"true"时连接到可用性组侦听器。 新属性**transparentNetworkIPResolution**，启用的默认情况下，提供的检测和连接到 （当前） 活动服务器。 |
| packetSize<br/><br/>ssNoversion<br/>[-1 &#124; 0 &#124; 512..32767]<br/><br/>8000 | 用来与 SQL Server 通信的网络包大小，以字节为单位指定。 值为 -1 表示使用服务器默认数据包大小。 值 0 表示使用最大值 32767。 如果将此属性设置为可接受范围外的值，将出现异常。<br/><br/> 重要事项：当启用加密 (encrypt=true) 时，建议不要使用 packetSize 属性。 否则，驱动程序可能引发连接错误。 有关详细信息，请参阅 [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md) 类的 [setPacketSize](../../connect/jdbc/reference/setpacketsize-method-sqlserverdatasource.md) 方法。 |
| password<br/><br/>String<br/>[&lt;=128 char]<br/><br/>null | 数据库密码，连接使用的 SQL 用户和密码的情况下。<br/>为 Kerberos 连接使用主体名称和密码，此属性设置为 Kerberos 主体密码。 |
| portNumber,<br/>port<br/><br/>ssNoversion<br/>[0..65535]<br/><br/>1433 | [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 侦听的端口。 如果在连接字符串中指定了端口号，则不会向 SQLbrowser 发出请求。 如果端口和 instanceName 都已指定，则将建立到指定端口的连接。 但是，将对 instanceName 进行验证，如果它与端口不符，将引发错误。<br/><br/> 重要事项：建议始终指定端口号，因为这比使用 SQLbrowser 更安全。 |
| queryTimeout<br/><br/>ssNoversion<br/><br/>-1 | 上一个查询，发生超时之前要等待的秒数。 默认值为-1，表示无限超时。 设置为 0 还表示无限期等待。 |
| responseBuffering<br/><br/>String<br/>["完整" &#124; "adaptive"]<br/><br/>自适应 | 如果此属性设置为“adaptive”，将只在需要时才缓冲尽可能少的数据。 默认模式为“adaptive”。<br/><br/> 如果此属性设置为“full”，当执行语句时，将从服务器读取整个结果集。<br/><br/> 注意：将 JDBC 驱动程序从版本 1.2 升级后，默认缓冲行为将为“adaptive”。 如果应用程序从未设置“responseBuffering”属性，而需要在应用程序中保留版本 1.2 的默认行为，则必须在连接属性中或使用 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 对象的 [setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) 方法将 responseBufferring 属性设置为“full”。 |
| selectMethod<br/><br/>String<br/>["直通" &#124; "cursor"]<br/><br/>直通 | 如果该属性设置为“cursor”，则对基于 TYPE_FORWARD_ONLY 和 CONCUR_READ_ONLY 游标的连接创建的每个查询，都会创建一个数据库游标。 通常仅当应用程序生成较大的结果集，以至于客户端内存无法完全容纳时，才需要使用该属性。 如果将该属性设置为“cursor”，则客户端内存中仅保留数目有限的结果集行。 <br/><br/>默认行为是在客户端内存中保留所有结果集的行。 在应用程序需要处理所有行时，此行为可提供最快性能。 |
| sendStringParameters...<br/>AsUnicode<br/><br/>boolean<br/>["true" &#124; "false"]<br/><br/>true | sendStringParametersAsUnicode<br/><br/>如果 sendStringParametersAsUnicode 属性设置为“true”，则字符串参数将以 Unicode 格式发送给服务器。<br/><br/> 如果 sendStringParametersAsUnicode 属性设置为“false”，则字符串参数将以非 Unicode 格式（例如 ASCII/MBCS 而不是 Unicode）发送给服务器。<br/><br/> sendStringParametersAsUnicode 属性的默认值为“true”。<br/><br/> **注意：** **sendStringParametersAsUnicode**发送的参数值时才检查属性**CHAR**， **VARCHAR**，或**LONGVARCHAR** JDBC 类型。 新的 JDBC 4.0 国家字符方法（例如 [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 和 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 类的 setNString、setNCharacterStream 和 setNClob 方法）始终将它们的参数值以 Unicode 格式发送到服务器，而不考虑此属性的设置。<br/><br/> 要获得 CHAR、VARCHAR 和 LONGVARCHAR JDBC 数据类型的最佳性能，应用程序应将 sendStringParametersAsUnicode 属性设置为“false”，并使用 [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 和 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 类的 setString、setCharacterStream 和 setClob 非区域字符方法。<br/><br/> 当应用程序将 sendStringParametersAsUnicode 属性设置为“false”，并在服务器端使用非区域字符方法访问 Unicode 数据类型（例如，nchar、nvarchar 和 ntext）时，如果数据库排序规则不支持非区域字符方法传递的字符串参数中的字符，则有些数据可能会丢失。<br/><br/> 请注意，应用程序应使用 setNString、 setNCharacterStream、 和 setNClob 区域字符方法[SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)并[SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md)类**NCHAR**， **NVARCHAR**，并**LONGNVARCHAR** JDBC 数据类型。 |
| sendTimeAsDatetime<br/><br/>boolean<br/>["true" &#124; "false"]<br/><br/>false | [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] JDBC Driver 3.0 中新增了此属性。<br/><br/> 设置为"true"将 java.sql.Time 值发送到与服务器[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **datetime**值。 <br/>设置为"false"，以将 java.sql.Time 值发送到与服务器[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]**时间**值。<br/><br/> 在将来的版本中此属性的默认值可能会更改。<br/><br/> 详细了解如何[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]将 java.sql.Time 值配置之前将它们发送到服务器，请参阅[如何配置 java.sql.Time 值发送到服务器](../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md)。 |
| serverName,<br/>服务器<br/><br/>String<br/><br/>null | 运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 的计算机。<br/><br/> 此外还可指定 [!INCLUDE[ssHADR](../../includes/sshadr_md.md)] 可用性组的虚拟机名称。 请参阅[高可用性和灾难恢复的 JDBC 驱动程序支持](../../connect/jdbc/jdbc-driver-support-for-high-availability-disaster-recovery.md)有关详细信息。 |
| serverNameAsACE<br/><br/>boolean<br/>["true" &#124; "false"]<br/><br/>false | 从 Microsoft JDBC Driver 6.0 for SQL Server 开始，设置为“true”以指示驱动程序应将 Unicode 服务器名称转换为 ASCII 兼容编码 (Punycode) 以进行连接。 如果此设置为 false，则驱动程序使用用户提供的服务器名称进行连接。<br/><br/> 请参阅[JDBC 驱动程序的国际化功能](../../connect/jdbc/international-features-of-the-jdbc-driver.md)的更多详细信息。 |
| serverPreparedStatement...<br/>DiscardThreshold<br/><br/>Integer<br/><br/>10 | *serverPreparedStatementDiscardThreshold*<br/><br/>从开始 JDBC Driver 6.2 for SQL Server，此属性可用于控制多少未完成预定义语句放弃操作 (<code>sp_unprepare</code>) 之前执行调用以清理服务器上未完成的句柄，则可以保留每个连接未完成. <br/><br/> 如果此属性设置为&lt;= 1，撤消已准备的语句关闭上立即执行操作。 如果设置为&gt;1 这些调用会一起批处理，以避免过于频繁调用 sp_unprepare 的开销。 |
| serverSpn<br/><br/>String<br/><br/>null | 始于 Microsoft JDBC Driver 4.2 for SQL Server，此可选属性可用于指定 Java Kerberos 连接的服务主体名称 (SPN)。  结合使用**authenticationScheme**。<br/><br/> 若要指定 SPN，它可以采用“MSSQLSvc/fqdn:port@REALM”的格式，其中 fqdn 是完全限定的域名，port 是端口号，REALM 是 SQL Server 的 Kerberos 领域的大写字母表示。<br/><br/> 注意：如果客户端的默认领域（在 Kerberos 配置中进行指定）与 SQL Server 的 Kerberos 领域相同，可选择使用 @REALM。<br/><br/> 有关使用的详细信息**serverSpn**与 Java Kerberos，请参阅[使用 Kerberos 集成身份验证连接到 SQL Server](../../connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md)。 |
| statementPooling...<br/>CacheSize<br/><br/>ssNoversion<br/><br/>0 | *statementPoolingCacheSize*<br/><br/>此属性从开始 JDBC Driver 6.4 for SQL Server，用于启用驱动程序中的准备语句处理缓存。 <br/><br/>此属性定义语句池的缓存的大小。 <br/><br/>此属性只能与结合**disableStatementPooling**连接属性应设置为"false"。 设置**disableStatementPooling**为"true"或**statementPoolingCacheSize**为 0 会禁用预定义语句处理缓存。|
| socketTimeout<br/><br/>ssNoversion<br/><br/>0 | 要在套接字上发生超时之前等待的毫秒数读取，或接受。 默认值为 0，表示无限超时。 |
| sslProtocol<br/><br/>String<br/><br/>TLS | 从开始 JDBC Driver 6.4 for SQL Server，可以使用此属性以指定要在安全的连接过程中考虑的 TLS 协议。 <br/>可能的值为： **TLS**， **TLSv1**， **TLSv1.1**，以及**TLSv1.2**。 <br/><br/>有关详细信息，请参阅[SSLProtocol](https://github.com/Microsoft/mssql-jdbc/wiki/SSLProtocol)。 |
| transparentNetwork...<br/>IPResolution<br/><br/>boolean<br/>["true" &#124; "false"]<br/><br/>true | *transparentNetworkIPResolution*<br/><br/>从 Microsoft JDBC Driver 6.0 for SQL Server，此属性提供更快的检测和连接到 （当前） 活动服务器。 可能的值为"true"和"false"，"true"是默认值。<br/><br/> 在 SQL Server 的 Microsoft JDBC Driver 6.0 之前, 应用程序必须设置连接字符串以包含"multiSubnetFailover = true"以指示它已连接到 AlwaysOn 可用性组。 如果没有设置**multiSubnetFailover**连接关键字为"true"，应用程序时可能遇到超时连接到 AlwaysOn 可用性组。 从 Microsoft JDBC Driver 6.0 for SQL Server，应用程序不会不需要设置 multiSubnetFailover 为不再 true。 <br/><br/>**注意：** 时 transparentNetworkIPResolution 超时 = true，第一个连接尝试使用 500 毫秒。 任何后续尝试使用 multiSubnetFailover 属性的使用相同的超时值逻辑。 |
| trustManagerClass<br/><br/>String<br/><br/>null | 自定义的完全限定的类名<code>javax.net.ssl.TrustManager</code>实现。 |
| trustManager...<br/>ConstructorArg<br/><br/>String<br/><br/>null | *trustManagerConstructorArg*<br/><br/>要传递到 TrustManager 的构造函数的可选参数。 如果指定 trustManagerClass 请求加密的连接，而不是默认系统 JVM 密钥存储基于 TrustManager 使用自定义 TrustManager。 |
| trustServerCertificate<br/><br/>boolean<br/>["true" &#124; "false"]<br/><br/>false | 如果设置为“true”，则指定 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 将不会验证 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] SSL 证书。<br/><br/> 如果设置为“true”，当使用 SSL 对通信层加密时，将自动信任 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] SSL 证书。<br/><br/> 如果为"false"[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]验证服务器 SSL 证书。 如果服务器证书验证失败，驱动程序将报错并终止连接。 默认值为“false”。 确保传递给 serverName 的值与服务器证书的公用名 (CN) 或使用者替代名称中的 DNS 名称完全匹配，以便成功建立 SSL 连接。 有关详细信息，请参阅[了解 SSL 支持](../../connect/jdbc/understanding-ssl-support.md)。<br/><br/> **注意：** 结合使用此属性**加密**/**身份验证**属性。 当且仅当连接使用 SSL 加密，此属性才影响服务器 SSL 证书验证。 |
| trustStore<br/><br/>String<br/><br/>null | 指向证书 trustStore 文件的路径（包括文件名）。 trustStore 文件包含客户端信任的证书的列表。<br/><br/> 如果未指定此属性或此属性设置为空，则驱动程序将依赖于信任关系管理器工厂的查找规则以确定要使用哪一个证书存储区。<br/><br/> 默认的 SunX509 TrustManagerFactory 试图按以下搜索顺序查找信任的材料：<br/><br/> 由“javax.net.ssl.trustStore”Java 虚拟机 (JVM) 系统属性指定的文件。<br/><br/> “&lt;java-home&gt;/lib/security/jssecacerts”文件。<br/><br/> “&lt;&gt;/lib/security/cacerts”文件。<br/><br/> <br/><br/> 有关详细信息，请参阅 Sun Microsystems 网站上的 SUNX509 TrustManager 接口文档。<br/><br/> **注意：** 此属性才影响证书 trustStore 查找当且仅当连接使用 SSL 加密并**trustServerCertificate**属性设置为"false"。 |
| trustStorePassword<br/><br/>String<br/><br/>null | 用于检查 trustStore 数据完整性的密码。<br/><br/> 如果设置了 trustStore 属性，但未设置 trustStorePassword 属性，则不检查 trustStore 的完整性。<br/><br/> 如果未指定 trustStore 和 trustStorePassword 属性，驱动程序将使用 JVM 系统属性“javax.net.ssl.trustStore”和“javax.net.ssl.trustStorePassword”。 如果未指定“javax.net.ssl.trustStorePassword”系统属性，则不检查 trustStore 的完整性。<br/><br/> 如果未指定 trustStore 属性，但设置了 trustStorePassword 属性，JDBC 驱动程序将使用由“javax.net.ssl.trustStore”指定作为信任存储区的文件，并使用指定的 trustStorePassword 检查信任存储区的完整性。 当客户端应用程序不希望在 JVM 系统属性中存储密码时，这一点可能是必需的。<br/><br/> **注意：** trustStorePassword 属性才影响证书 trustStore 查找当且仅当连接使用 SSL 连接和**trustServerCertificate**属性设置为"false"。 |
| trustStoreType<br/><br/>String<br/><br/>JKS | 设置此属性可指定要用于 FIPS 模式下的信任存储区类型。 <br/><br/>可能的值为**PKCS12**或由 FIPS 提供程序定义的类型。 |
| useBulkCopyFor...<br/>BatchInsert<br/><br/>boolean<br/>["true" &#124; "false"]<br/><br/>false | _useBulkCopyForBatchInsert_<br/><br/> 开始 SQL Server 的 Microsoft JDBC 驱动程序 7.0，此连接属性可以启用以使用执行批处理插入操作时使用大容量复制 API<code>java.sql.PreparedStatement</code>以改进性能。 <br/><br/>仅当目标服务器的类型，此功能是功能性**Azure 数据仓库**。 默认情况下禁用，此属性设置为"true"以启用此功能。 <br/></br> **重要说明：** 此功能仅支持完全参数化的 INSERT 查询。 如果插入查询组合的其他 SQL 查询，或包含在值中的数据，执行将回退到批处理插入的基本操作。 <br/><br/> 有关如何使用此属性的详细信息，请参阅[批处理插入操作中使用大容量复制 API](use-bulk-copy-api-batch-insert-operation.md)|
| userName,<br/>user<br/><br/>String<br/>[&lt;=128 char]<br/><br/>null | 数据库用户，如果使用的 SQL 用户和密码进行连接。<br/><br/>为 Kerberos 连接使用主体名称和密码，此属性设置为 Kerberos 主体名称。 |
| workstationID<br/><br/>String<br/>[&lt;=128 char]<br/><br/>&lt;空字符串&gt; | 工作站 ID。 用于在各种 [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] 探查和日志记录工具中标识特定的工作站。 <br/><br/>如果未指定任何内容，则将使用 &lt;空字符串&gt;。 |
| xopenStates<br/><br/>boolean<br/>["true" &#124; "false"]<br/><br/>false | 设置为“true”将指定驱动程序在异常时返回 XOPEN 兼容的状态代码。 <br/><br/>默认将返回 SQL 99 状态代码。 |
| &nbsp; | &nbsp; |

> [!NOTE]  
> [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 采用服务器的连接属性默认值，只有 ANSI_DEFAULTS 和 IMPLICIT_TRANSACTIONS 除外。 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 将 ANSI_DEFAULTS 自动设置为 ON，将 IMPLICIT_TRANSACTIONS 自动设置为 OFF。

> [!Important]
> 如果身份验证设置为 ActiveDirectoryPassword，需要在类路径中包含以下库： [azure activedirectory-库-用于-java](https://github.com/AzureAD/azure-activedirectory-library-for-java)。 可以在上找到它[Maven 存储库](https://mvnrepository.com/artifact/com.microsoft.azure/adal4j)。 若要下载的库和其依赖项的最简单方法使用 Maven: 
> 1. 首先，在系统上安装 Maven 
> 2. 转到[GitHub 页面](https://github.com/Microsoft/mssql-jdbc)的驱动程序
> 3. 下载 pom.xml 文件
> 4. 运行以下 Maven 命令，若要下载的库和其依赖项： `mvn dependency:copy-dependencies`

## <a name="see-also"></a>另请参阅

[通过 JDBC 驱动程序连接到 SQL Server](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)  
[FIPS 模式](../../connect/jdbc/fips-mode.md)
