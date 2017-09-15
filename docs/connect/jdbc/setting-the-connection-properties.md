---
title: "设置连接属性 |Microsoft 文档"
ms.custom: 
ms.date: 04/11/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: f1b62700-f046-488d-bd6b-a5cd8fc345b7
caps.latest.revision: 154
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 56dbb81f9d30ccb41a6247c4fefda9d6ecd703a6
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="setting-the-connection-properties"></a>设置连接属性
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  可以通过多种方式指定连接字符串的属性：  
  
-   作为名称 = 值属性中的连接 URL，来使用驱动程序管理器类连接时。  
  
-   作为名称 = 值属性中的*属性*驱动程序管理器类中的连接方法参数。  
  
-   在驱动程序数据源的适当的 setter 方法中指定值。 例如：  
  
    ```  
  
    datasource.setServerName(value)  
    datasource.setDatabaseName(value)  
  
    ```  
  
## <a name="remarks"></a>注释  
 属性名不区分大小写，重复的属性名将按以下顺序进行解析：  
  
1.  API 参数（如用户和密码）  
  
2.  属性集合。  
  
3.  连接字符串中的最后一个实例。  
  
 此外，属性名允许使用未知的值，JDBC 驱动程序不会对这些值进行大小写验证。  
  
 允许使用同义词，并按顺序进行解析，如同处理重复的属性名。  
  
 下表列出了 JDBC 驱动程序当前可用的所有连接字符串属性。  
  
|属性|类型|默认|Description|  
|--------------|----------|-------------|-----------------|  
|accessToken|字符串|null|此属性用于连接到 SQL 数据库使用访问令牌。 **accessToken**不能通过该连接 URL 设置。|  
|applicationIntent|字符串|ReadWrite|连接到服务器时声明应用程序工作负荷类型。 可能的值为**ReadOnly**和**ReadWrite**。 有关详细信息，请参阅[的高可用性、 灾难恢复的 JDBC 驱动程序支持](../../connect/jdbc/jdbc-driver-support-for-high-availability-disaster-recovery.md)。|  
|applicationName|字符串<br /><br /> [<=128 个字符]|null|应用程序名称，或"[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]"如果未提供名称。 用于标识特定的应用程序在各种[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]事件探查和日志记录工具。|  
|身份验证|字符串|NotSpecified|从 SQL Server 的 Microsoft JDBC Driver 6.0，此可选属性指示要用于连接的 SQL 身份验证方法。 可能的值为**ActiveDirectoryIntegrated**， **ActiveDirectoryPassword**， **SqlPassword**和默认**NotSpecified**。<br /><br /> 使用**ActiveDirectoryIntegrated**连接到使用集成的 Windows 身份验证的 SQL 数据库。<br /><br /> 使用**ActiveDirectoryPassword**以连接到 SQL 数据库使用 Azure AD 主体名称和密码。<br /><br /> 使用**SqlPassword**连接到 SQL Server 使用**用户名**/**用户**和**密码**属性。<br /><br /> 使用**NotSpecified**如果没有一个的这些身份验证方法需要。<br /><br /> **重要说明：**如果身份验证设置为 ActiveDirectoryIntegrated，以下两个库将需要安装： **SQLJDBC_AUTH。DLL** （JDBC 驱动程序包中可用） 和 Azure Active Directory 身份验证库，为 SQL Server (**ADALSQL。DLL**) 是提供多个语言版本 （x86 和 amd64） 从下载中心[Microsoft Active Directory 身份验证库，Microsoft SQL server](https://www.microsoft.com/en-us/download/details.aspx?id=48742)。 JDBC 驱动程序仅支持版本**1.0.2028.318 和更高版本**ADALSQL 有关。DLL。<br /><br /> **注意：**当身份验证属性设置为任何值以外**NotSpecified**，默认情况下的驱动程序使用安全套接字层 (SSL) 加密。<br /><br /> 有关如何配置 Azure Active Directory 身份验证信息，请访问[连接到 SQL 数据库使用 Azure Active Directory 身份验证](https://azure.microsoft.com/en-us/documentation/articles/sql-database-aad-authentication/)。|  
|authenticationScheme|字符串|“NativeAuthentication”|指示您的应用程序要使用哪一种集成安全性。 可能的值为**JavaKerberos**和默认**NativeAuthentication**。<br /><br /> 使用时**authenticationScheme = JavaKerberos**，必须在指定的完全限定的域名 (FQDN) **serverName**或**serverSpn**属性。 否则，将出现错误（Kerberos 数据库中找不到服务器）。<br /><br /> 有关详细信息使用**authenticationScheme**，请参阅[使用 Kerberos 集成身份验证连接到 SQL Server](../../connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md)。|  
|columnEncryptionSetting|字符串<br /><br /> ["已启用"&#124;"已禁用"]|禁用|设置为"已启用"以用于 SQL Server 的始终加密 （要从中） 功能开始与 Microsoft JDBC Driver 6.0。 启用 AE后，JDBC 驱动程序以透明方式加密和解密存储在 SQL Server 中的加密数据库中的敏感数据。<br /><br /> 请参阅[Using Always Encrypted with JDBC 驱动程序](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md)有关详细信息。<br /><br /> **注意：**始终加密是适用于 SQL Server 2016 或更高版本。|  
|databaseName、database|字符串<br /><br /> [<=128 个字符]|null|要连接到的数据库名称。 如果未声明，则连接到默认的数据库。|  
|disableStatementPooling|boolean<br /><br /> ["true"&#124;"false"]|true|当前仅支持值“true”。 如果设置为“false”，将出现异常。|  
|encrypt|boolean<br /><br /> ["true"&#124;"false"]|false|设为"true"可指定[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]的服务器是否安装了证书，客户端和服务器之间发送的所有数据使用安全套接字层 (SSL) 加密。 默认值为 false。<br /><br /> 从 SQL Server 的 Microsoft JDBC Driver 6.0，没有新连接设置身份验证，默认情况下使用 SSL 加密。 有关详细信息请参阅身份验证属性。|  
|failoverPartner|字符串|null|在数据库镜像配置中使用的故障转移服务器名称。 与主服务器进行初始连接时若发生失败，则会使用此属性；建立初始连接后，将忽略此属性。 必须与 databaseName 属性结合使用。<br /><br /> **注意：**驱动程序不支持连接字符串中的 failoverPartner 属性的一部分指定故障转移伙伴实例的服务器实例端口号。 但是，支持在同一连接字符串中指定主体服务器实例的 serverName、instanceName 和 portNumber 属性以及故障转移伙伴实例的 failoverPartner 属性。<br /><br /> 如果指定中的虚拟网络名称**服务器**连接属性不能使用数据库镜像。 请参阅[的高可用性、 灾难恢复的 JDBC 驱动程序支持](../../connect/jdbc/jdbc-driver-support-for-high-availability-disaster-recovery.md)有关详细信息。|  
|hostNameInCertificate|字符串|null|要在验证中使用的主机名[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]SSL 证书。<br /><br /> 如果 hostNameInCertificate 属性为未指定或未设置为 null，[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]将使用**serverName**上的主机名称的连接 URL，以验证属性值[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]SSL 证书。<br /><br /> **注意：**结合使用此属性**加密**/**身份验证**属性和**trustServerCertificate**属性。 此属性如何影响证书验证，当且仅当连接使用安全套接字层 (SSL) 加密与**trustServerCertificate**设置为"false"。 请确保传递给值**hostNameInCertificate**完全匹配的公用名 (CN) 或 DNS 名称中使用者备用名称 (SAN) SSL 连接的服务器证书中才能成功。 有关详细信息，请参阅[了解 SSL 支持](../../connect/jdbc/understanding-ssl-support.md)。|  
|INSTANCENAME|字符串<br /><br /> [<=128 个字符]|null|[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]要连接到实例名。 如果未指定，则连接到默认实例。 对于 instanceName 和端口均已指定的情况，请参阅有关端口的备注。<br /><br /> 如果指定中的虚拟网络名称**服务器**连接属性不能使用**instanceName**连接属性。 请参阅[的高可用性、 灾难恢复的 JDBC 驱动程序支持](../../connect/jdbc/jdbc-driver-support-for-high-availability-disaster-recovery.md)有关详细信息。|  
|integratedSecurity|boolean<br /><br /> ["true"&#124;"false"]|false|设为"true"可指示将通过使用 Windows 凭据[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]在 Windows 操作系统上。 如果为“true”，则 JDBC 驱动程序将搜索本地计算机凭据缓存，以寻找在登录计算机或网络时已提供的凭据。<br /><br /> 设置为"true"(与**authenticationscheme = JavaKerberos**)，以指示，将通过使用 Kerberos 凭据[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。 Kerberos 身份验证的详细信息，请参阅[使用 Kerberos 集成身份验证连接到 SQL Server](../../connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md)。 <br /><br /> 如果为“false”，则必须提供用户名和密码。| 
|keyStoreAuthentication|字符串|null| 从 SQL Server 的 Microsoft JDBC Driver 6.0，此属性标识的密钥存储区以无缝地为与始终加密的连接设置，并确定用于对密钥存储进行身份验证的身份验证机制。 SQL server 的 Microsoft JDBC Driver 6.0 支持设置最大 Java 密钥存储的无缝地使用你需要设置此属性"**keyStoreAuthentication = JavaKeyStorePassword**"。 请注意，若要使用此属性，你还需要设置**keyStoreLocation**和**keyStoreSecret** Java 密钥存储的属性。 <br/><br/>有关详细信息，请访问[Using Always Encrypted with JDBC 驱动程序](https://msdn.microsoft.com/library/mt591987%28v=sql.110%29.aspx?f=255&MSPPError=-2147217396)。 
|keyStoreLocation|字符串|null|当**keyStoreAuthentication = JavaKeyStorePassword**、 **keyStoreLocation**属性标识存储列主密钥用于始终加密的 Java 密钥库文件的路径数据。 请注意，路径必须包含的密钥存储区文件名。<br/><br/>有关详细信息，请访问[Using Always Encrypted with JDBC 驱动程序](https://msdn.microsoft.com/library/mt591987%28v=sql.110%29.aspx?f=255&MSPPError=-2147217396)。
|keyStoreSecret|字符串|null|当**keyStoreAuthentication = JavaKeyStorePassword**、 **keyStoreSecret**属性标识要用于 keystore 以及与该密钥的密码。 请注意，对于使用 Java 密钥存储密钥库和密钥的密码必须相同。<br/><br/>有关详细信息，请访问[Using Always Encrypted with JDBC 驱动程序](https://msdn.microsoft.com/library/mt591987%28v=sql.110%29.aspx?f=255&MSPPError=-2147217396)。
|lastUpdateCount|boolean<br /><br /> ["true"&#124;"false"]|true|如果值为“true”，则仅返回传递给服务器的 SQL 语句的最终更新计数，它可用于单个的 SELECT、INSERT 或 DELETE 语句中，以忽略由服务器触发器引起的其他更新计数。 将此属性设置为“false”可导致所有更新计数都被返回，包括由服务器触发器返回的更新计数。<br /><br /> **注意：**与一起使用时才应用此属性[executeUpdate](../../connect/jdbc/reference/executeupdate-method-sqlserverstatement.md)方法。 所有其他执行方法返回所有结果，并更新计数。 此属性仅影响由服务器触发器返回的更新计数， 而不影响作为触发器执行结果的一部分的结果集或错误。|  
|lockTimeout|int|-1|数据库报告锁定超时之前要等待的毫秒数。默认行为是无限期等待。 如果指定，该值将成为此连接上所有语句的默认值。 请注意， **Statement.setQueryTimeout()**可以用来设置特定语句的超时时间。 该值可为 0，这表示无需等待。|  
|loginTimeout|int [0..65535]|15|因连接失败而中止连接之前驱动程序应等待的秒数。 零值表示该超时为默认系统超时，默认情况下指定为 15 秒。 非零值为因连接失败而中止连接之前驱动程序应等待的秒数。<br /><br /> 如果指定中的虚拟网络名称**服务器**连接属性，你应指定超时值为三分钟或详细信息以允许足够时间进行故障转移连接成功。 请参阅[的高可用性、 灾难恢复的 JDBC 驱动程序支持](../../connect/jdbc/jdbc-driver-support-for-high-availability-disaster-recovery.md)有关详细信息。|  
|multiSubnetFailover|Boolean|false|始终指定**multiSubnetFailover = true**连接到的可用性组侦听器时[!INCLUDE[ssSQL11](../../includes/sssql11_md.md)]可用性组或[!INCLUDE[ssSQL11](../../includes/sssql11_md.md)]故障转移群集实例。 **multiSubnetFailover = true**配置[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]以便更快地检测和到 （当前） 活动服务器的连接。 可能的值为“True”和“False”。 请参阅[的高可用性、 灾难恢复的 JDBC 驱动程序支持](../../connect/jdbc/jdbc-driver-support-for-high-availability-disaster-recovery.md)有关详细信息。<br /><br /> 你可以以编程方式访问**multiSubnetFailover**连接属性[getPropertyInfo](../../connect/jdbc/reference/getpropertyinfo-method-sqlserverdriver.md)， [getMultiSubnetFailover](../../connect/jdbc/reference/getmultisubnetfailover-method-sqlserverdatasource.md)，和[setMultiSubnetFailover](../../connect/jdbc/reference/setmultisubnetfailover-method-sqlserverdatasource.md)。<br /><br /> **注意：**开头不再需要设置 multiSubnetFailover 为 true 时连接到可用性组侦听器的 SQL Server 的 Microsoft JDBC Driver 6.0。 一个新属性， **transparentNetworkIPResolution**，这通过默认情况下，提供的检测和到 （当前） 活动服务器的连接。|  
|packetSize|int [-1 &#124; 0 &#124; 512..32767]|8000|用来与 SQL Server 通信的网络包大小，以字节为单位指定。 值为 -1 表示使用服务器默认数据包大小。 值 0 表示使用最大值 32767。 如果将此属性设置为可接受范围外的值，将出现异常。<br /><br /> **重要说明：**我们不建议使用的数据包大小属性启用加密 (加密 = true)。 否则，驱动程序可能引发连接错误。 有关详细信息，请参阅[setPacketSize](../../connect/jdbc/reference/setpacketsize-method-sqlserverdatasource.md)方法[SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md)类。|  
|password|字符串<br /><br /> [<=128 个字符]|null|数据库密码，如果使用的 SQL 用户和密码进行连接。<BR/>对于 Kerberos 主体名称和密码的连接，此属性设置为 Kerberos 主体密码。|  
|portNumber、port|int [0..65535]|1433|端口其中[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]正在侦听。 如果在连接字符串中指定了端口号，则不会向 sqlbrowser 发出请求。 如果端口和 instanceName 都已指定，则将建立到指定端口的连接。 但是， **instanceName**验证和如果与的端口不匹配，则会引发错误。<br /><br /> **重要说明：**我们建议，端口号始终指定，因为这是比使用 sqlbrowser 更安全。|  
|responseBuffering|字符串<br /><br /> ["完全"&#124;"自适应"]|自适应|如果此属性设置为“adaptive”，将只在需要时才缓冲尽可能少的数据。 默认模式为“adaptive”。<br /><br /> 如果此属性设置为“full”，当执行语句时，将从服务器读取整个结果集。<br /><br /> **注意：**从升级后的 JDBC 驱动程序版本 1.2，缓冲行为的默认行为将是"自适应"。 如果你的应用程序已永远不会设置"responseBuffering"属性，并且你想要保留在你的应用程序的版本 1.2 默认行为，则必须设置为"完整"responseBufferring 属性的连接属性中或通过使用[setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md)方法[SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md)对象。|  
|selectMethod|字符串<br /><br /> ["直接"&#124;"光标"]|直接|如果该属性设置为“cursor”，则对基于 TYPE_FORWARD_ONLY 和 CONCUR_READ_ONLY 游标的连接创建的每个查询，都会创建一个数据库游标。 通常仅当应用程序生成的结果集非常大，以至于客户端内存无法完全容纳时，才需要使用该属性。 如果将该属性设置为“cursor”，则客户端内存中仅保留数目有限的结果集行。 默认行为是在客户端内存中保留所有结果集的行。 在应用程序需要处理所有行时，此行为可提供最快性能。|  
|sendStringParametersAsUnicode|boolean<br /><br /> ["true"&#124;"false"]|true|如果**sendStringParametersAsUnicode**属性设置为"true"，参数发送到服务器以 Unicode 格式的字符串。<br /><br /> 如果**sendStringParametersAsUnicode**属性设置为"false"，字符串参数发送到非 Unicode 格式，如而不是 Unicode 的 ASCII/MBCS 中的服务器。<br /><br /> 默认值为**sendStringParametersAsUnicode**属性为"true"。<br /><br /> **注意：** **sendStringParametersAsUnicode**发送具有的参数值时，仅检查属性**CHAR**， **VARCHAR**，或**LONGVARCHAR** JDBC 类型。 新的 JDBC 4.0 国家字符集方法，如的 setNString、 setNCharacterStream、 setNClob 方法[SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)和[SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md)类，始终将其参数值发送到 Unicode 中而不考虑此属性设置的服务器。<br /><br /> 为了获得最佳性能与**CHAR**， **VARCHAR**，和**LONGVARCHAR** JDBC 数据类型，应用程序应设置**sendStringParametersAsUnicode**属性设置为"false"并使用 setString、 setCharacterStream 和 setClob 非 national 字符方法[SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)和[SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md)类。<br /><br /> 当应用程序将设置**sendStringParametersAsUnicode**属性设置为"false"，并使用服务器端的非 national 字符方法来访问 Unicode 数据类型 (如**nchar**， **nvarchar**和**ntext**)，如果数据库排序规则不支持通过非 national 字符方法传递的字符串参数中的字符可能会丢失某些数据。<br /><br /> 请注意，应用程序应使用的 setNString、 setNCharacterStream、 setNClob 国家字符集方法[SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)和[SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md)类**NCHAR**， **NVARCHAR**，和**LONGNVARCHAR** JDBC 数据类型。|  
|sendTimeAsDatetime|boolean<br /><br /> ["true"&#124;"false"]|true|中已添加此属性[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]JDBC Driver 3.0。<br /><br /> 为 true 时，将 java.sql.Time 值发送到作为服务器[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] **datetime**值。<br /><br /> 为 false 时，将 java.sql.Time 值发送到作为服务器[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]**时间**值。<br /><br /> **sendTimeAsDatetime**还可以进行修改以编程方式与[SQLServerDataSource.setSendTimeAsDatetime](../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md)。<br /><br /> 在将来的版本中此属性的默认值可能会更改。<br /><br /> 有关详细信息，如何[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]配置 java.sql.Time 值然后将它们发送到服务器，请参阅[如何配置 java.sql.Time 值发送到服务器](../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md)。|  
|serverName、server|字符串|null|运行的计算机[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]。<br /><br /> 你还可以指定的虚拟网络名称[!INCLUDE[ssHADR](../../includes/sshadr_md.md)]可用性组。 请参阅[的高可用性、 灾难恢复的 JDBC 驱动程序支持](../../connect/jdbc/jdbc-driver-support-for-high-availability-disaster-recovery.md)有关详细信息。|  
|serverSpn|字符串|null|始于 Microsoft JDBC Driver 4.2 for SQL Server，此可选属性可用于指定 Java Kerberos 连接的服务主体名称 (SPN)。  结合使用**authenticationScheme**。<br /><br /> 若要指定 SPN，它可以采用的形式:"MSSQLSvc/fqdn:port@REALM"其中 fqdn 是完全限定的域名，端口为端口号，领域是中大写字母的 SQL Server 的 Kerberos 领域。<br /><br /> 注意：@REALM如果客户端 （作为 Kerberos 配置中指定） 的默认领域等同于 SQL Server 的 Kerberos 领域是可选的。<br /><br /> 有关详细信息使用**serverSpn**使用 Java Kerberos，请参阅[使用 Kerberos 集成身份验证连接到 SQL Server](../../connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md)。|  
|serverNameAsACE|boolean<br /><br /> ["true"&#124;"false"]|false|从 Microsoft JDBC Driver 6.0 for SQL Server 开始，设置为“true”以指示驱动程序应将 Unicode 服务器名称转换为 ASCII 兼容编码 (Punycode) 以进行连接。 如果此设置为 false，则驱动程序使用用户提供的服务器名称进行连接。<br /><br /> 请参阅[的 JDBC 驱动程序的国际功能](../../connect/jdbc/international-features-of-the-jdbc-driver.md)有关详细信息。|  
|TransparentNetworkIPResolution|boolean<br /><br /> ["true"&#124;"false"]|true|SQL Server，此属性，transparentNetworkIPResolution 开头 Microsoft JDBC Driver 6.0，提供更快检测和到 （当前） 活动服务器的连接。 可能的值为 true 为 true 和 false 为默认值。<br /><br /> 在 SQL Server 的 Microsoft JDBC Driver 6.0 之前, 必须设置连接字符串以包括应用程序"multiSubnetFailover = true"以指示它已连接到 AlwaysOn 可用性组。 如果未设置为 true 的 multiSubnetFailover 连接关键字，应用程序可能会在连接到 AlwaysOn 可用性组时遇到超时。 从 SQL Server 的 Microsoft JDBC Driver 6.0，应用程序不必设置 multiSubnetFailover 为不再 true。 <br /><br />**注意：**时 transparentNetworkIPResolution = true，首次连接尝试使用 500ms年作为超时。 任何后续尝试所使用的 multiSubnetFailover 属性使用相同的超时逻辑。|  
|columnEncryptionSetting|boolean<br /><br /> ["true"&#124;"false"]|false|从 Microsoft JDBC Driver 6.0 for SQL Server 开始，设置为“true”以使用始终加密 (AE) 功能。 启用 AE后，JDBC 驱动程序以透明方式加密和解密存储在 SQL Server 中的加密数据库中的敏感数据。<br /><br /> 请参阅[Using Always Encrypted with JDBC 驱动程序](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md)有关详细信息。<br /><br /> **注意：**始终加密是适用于 SQL Server 2016 还是较新版本。|  
|trustServerCertificate|boolean<br /><br /> ["true"&#124;"false"]|false|设为"true"可指定[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]将不会验证[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]SSL 证书。<br /><br /> 如果为"true"， [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] SSL 证书是自动受信任的当使用 SSL 加密的通信层。<br /><br /> 如果为"false"，[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]将验证服务器 SSL 证书。 如果服务器证书验证失败，驱动程序将报错并终止连接。 默认值为"false"。 请确保传递给值**serverName**与使用者备用名称中的 SSL 连接的服务器证书中成功的公用名 (CN) 或 DNS 名称完全匹配。 有关详细信息，请参阅[了解 SSL 支持](../../connect/jdbc/understanding-ssl-support.md)。<br /><br /> **注意：**结合使用此属性**加密**/**身份验证**属性。 当且仅当连接使用 SSL 加密，则此属性仅会影响服务器 SSL 证书验证。|  
|trustStore|字符串|null|指向证书 trustStore 文件的路径（包括文件名）。 trustStore 文件包含客户端信任的证书的列表。<br /><br /> 如果未指定此属性或此属性设置为空，则驱动程序将依赖于信任关系管理器工厂的查找规则以确定要使用哪一个证书存储区。<br /><br /> **默认值 SunX509 TrustManagerFactory 尝试找到以下搜索顺序中的受信任的材料：**<br /><br /> 由“javax.net.ssl.trustStore”Java 虚拟机 (JVM) 系统属性指定的文件。<br /><br /> "\<java 主页 >/lib/安全/jssecacerts"文件。<br /><br /> "\<java 主页 >/lib/安全/cacerts"文件。<br /><br /> <br /><br /> 有关详细信息，请参阅 SUNX509 TrustManager 接口文档，Sun Microsystems Web 站点上。<br /><br /> **注意：**此属性仅影响证书 trustStore lookup 来说，当且仅当连接使用 SSL 加密和**trustServerCertificate**属性设置为"false"。|  
|trustStorePassword|字符串|null|用于检查 trustStore 数据完整性的密码。<br /><br /> 如果设置了 trustStore 属性，但未设置 trustStorePassword 属性，则不检查 trustStore 的完整性。<br /><br /> 如果未指定 trustStore 和 trustStorePassword 属性，驱动程序将使用 JVM 系统属性“javax.net.ssl.trustStore”和“javax.net.ssl.trustStorePassword”。 如果未指定“javax.net.ssl.trustStorePassword”系统属性，则不检查 trustStore 的完整性。<br /><br /> 如果未指定 trustStore 属性，但设置了 trustStorePassword 属性，JDBC 驱动程序将使用由“javax.net.ssl.trustStore”指定作为信任存储区的文件，并使用指定的 trustStorePassword 检查信任存储区的完整性。 当客户端应用程序不希望在 JVM 系统属性中存储密码时，这一点可能是必需的。<br /><br /> **注意：** trustStorePassword 属性仅影响证书 trustStore lookup 来说，当且仅当连接使用 SSL 连接和**trustServerCertificate**属性设置为"false"。|  
|userName、user|字符串<br /><br /> [<=128 个字符]|null|数据库用户，如果使用的 SQL 用户和密码进行连接。<BR/>对于 Kerberos 主体名称和密码的连接，此属性设置为 Kerberos 主体名称。|  
|workstationID|字符串<br /><br /> [<=128 个字符]|\<空字符串 >|工作站 ID。 用于标识在各种特定工作站[!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]事件探查和日志记录工具。 如果未指定，\<空字符串 > 使用。|  
|xopenStates|boolean<br /><br /> ["true"&#124;"false"]|false|设置为“true”将指定驱动程序在异常时返回 XOPEN 兼容的状态代码。 默认将返回 SQL 99 状态代码。|  
|gsscredential|org.ietf.jgss.GSSCredential|null|从 SQL Server 的 Microsoft JDBC 驱动程序 6.2，可以在此属性中传递用户凭据用于 Kerberos 约束委派。 <BR/>这应该用于**integratedSecurity**作为**true**和**JavaKerberos** **authenticationscheme**。| 
|jaasConfigurationName|字符串|SQLJDBCDriver|从 SQL Server 的 Microsoft JDBC 驱动程序 6.2，SQL Server 的每个连接可以有其自己 JAAS 登录配置文件以建立 Kerberos 连接。 可通过此属性传递登录配置文件的名称。 <BR/> 默认情况下，驱动程序将属性设置`useDefaultCcache = true`有关 IBM Jvm 和`useTicketCache = true`为其他 Jvm。|
|serverPreparedStatementDiscardThreshold|Integer|10|控制执行清理服务器上未完成的句柄的调用之前，多少未完成已准备的语句放弃操作 (sp_unprepare) 可以是未完成每个连接。 如果设置为 < = 1 取消-准备操作将在关闭已准备的语句上立即执行。 如果设置为 > 1 这些调用将可成批归入以避免调用 sp_unprepare 过于频繁的开销。|
|enablePrepareOnFirstPreparedStatementCall|boolean<br /><br /> ["true"&#124;"false"]|false|如果此配置设置为 false 的已准备的语句在首次执行将调用 sp_executesql 并做好准备一条语句，一旦第二次执行发生在它将调用 sp_prepexec 和实际安装程序已准备的语句句柄。|
|statementPoolingCacheSize|Integer|10|池中重用的可配置缓存语句| 
  
> [!NOTE]  
>  [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]使 ANSI_DEFAULTS 和 IMPLICIT_TRANSACTIONS 除外的连接属性的默认值的服务器。 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]自动将 ANSI_DEFAULTS 设置为 ON 和 IMPLICIT_TRANSACTIONS 为 OFF。  

> [!Note]
> 重要提示： 如果身份验证设置为 ActiveDirectoryPassword，下面的库将需要包括在类路径中： [azure activedirectory-库-为-java](https://github.com/AzureAD/azure-activedirectory-library-for-java)。 可以在上找到[Maven 存储库](https://mvnrepository.com/artifact/com.microsoft.azure/adal4j)。 若要下载的库和其依赖项的最简单方法使用 Maven: 
 >1. 首先，在你的系统上安装 Maven 
 >2. 转到[GitHub 页面](https://github.com/Microsoft/mssql-jdbc)驱动程序
 >3. 下载 pom.xml 文件
 >4. 运行下载的库和其依赖项的以下 Maven 命令： mvn 依赖项： 副本-依赖关系
  
## <a name="see-also"></a>另请参阅  
 [连接到 SQL Server 使用 JDBC 驱动程序](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)  
 [FIPS 模式下](../../connect/jdbc/fips-mode.md)
  
  

