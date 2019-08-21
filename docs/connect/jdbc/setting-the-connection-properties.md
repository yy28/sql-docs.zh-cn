---
title: 设置连接属性 | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: f1b62700-f046-488d-bd6b-a5cd8fc345b7
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e32a0fffd60fe34bf0431e6060846387ff079952
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 08/14/2019
ms.locfileid: "69027759"
---
# <a name="setting-the-connection-properties"></a>设置连接属性

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

可以通过多种方式指定连接字符串的属性：

- 当使用 DriverManager 类进行连接时，在连接 URL 中通过“名称=值”属性进行指定。
- 作为 DriverManager 类中 Connect 方法的*properties*参数的 name = value 属性。
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

| 属性<br/>类型<br/>默认 | 描述 |
| :------------------------------ | :---------- |
| accessToken<br/><br/>String<br/><br/>null | 使用此属性可以使用访问令牌连接到 SQL 数据库。 不能使用连接 URL 来设置**accessToken** 。 |
| applicationIntent<br/><br/>String<br/><br/>ReadWrite | 连接到服务器时声明应用程序工作负荷类型。 <br/><br/>可能的值为 ReadOnly 和 ReadWrite   。 <br/><br/>有关详细信息，请参阅 [JDBC 驱动程序对高可用性和灾难恢复的支持](../../connect/jdbc/jdbc-driver-support-for-high-availability-disaster-recovery.md)。 |
| applicationName<br/><br/>String<br/>[&lt;=128 char]<br/><br/>null | 如果未提供名称，则使用应用程序名称或“[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]”。<br/><br/>用于在各种 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 分析和日志记录工具中标识特定的应用程序。 |
| 身份验证<br/><br/>String<br/><br/>NotSpecified | 从用于 SQL Server 的 Microsoft JDBC Driver 6.0 开始, 此可选属性指示要用于连接的 SQL 身份验证方法。 可能的值包括**ActiveDirectoryIntegrated**、 **ActiveDirectoryPassword**、 **ActiveDirectoryMSI**、 **SqlPassword**和默认的**NotSpecified**。<br/><br/> 使用**ActiveDirectoryIntegrated**通过集成 Windows 身份验证连接到 SQL 数据库。<br/><br/> 使用**ActiveDirectoryPassword**连接到使用 Azure AD 主体名称和密码的 SQL 数据库。<br/><br/> 使用**ActiveDirectoryMSI**从 azure 资源内部连接到 SQL 数据库, 例如, 使用托管服务标识 (MSI) 身份验证的 Azure 虚拟机、应用服务或 Function App。 <br><br>使用**ActiveDirectoryMSI** authentication 模式时, 驱动程序支持以下两种类型的托管标识: <br> 1._系统分配的托管标识_：默认情况下用于获取 accessToken  。 <br> 2._用户分配的托管标识_：用于获取 accessToken  ，前提是托管服务标识 (MSI) 的客户端 ID 与 msiClientId  连接属性一起指定。<br/><br/> 使用 "**用户名**/" 和 "**密码**" 属性使用**SqlPassword**连接到 SQL Server。 <br/><br/> 如果不需要这些身份验证方法, 请使用**NotSpecified** 。<br/><br/> **重要提示:** 如果身份验证设置为 ActiveDirectoryIntegrated, 则需要安装以下两个库: **SQLJDBC_AUTH。DLL** (在 JDBC 驱动程序包中提供) 和 Azure Active Directory SQL Server 的身份验证库 (**adalsql.dll)。DLL**), 它以不同的语言提供 (适用于 x86 和 amd64), 位于[Microsoft Active Directory 身份验证库的下载中心 Microsoft SQL Server](https://www.microsoft.com/download/details.aspx?id=48742)。 JDBC driver 仅支持 ADALSQL.DLL 版本的**1.0.2028.318 和更高**版本.DLL。<br/><br/> **注意:** 如果 authentication 属性设置为**NotSpecified**以外的任何值, 则默认情况下, 驱动程序将使用安全套接字层 (SSL) 加密。<br/><br/> 有关如何配置 Azure Active Directory 身份验证的信息, 请参阅[使用 Azure Active Directory 身份验证连接到 SQL 数据库](https://azure.microsoft.com/documentation/articles/sql-database-aad-authentication/)。 |
| authenticationScheme<br/><br/>String<br/><br/>NativeAuthentication | 指示您的应用程序要使用哪一种集成安全性。 可能的值包括**JavaKerberos**、 **NTLM**和默认的**NativeAuthentication**。<br/><br/> 使用**authenticationScheme = JavaKerberos**时, 必须在**serverName**或**serverSpn**属性中指定完全限定的域名 (FQDN)。 否则，将出现错误（Kerberos 数据库中找不到服务器）。<br/><br/> 若要详细了解如何使用 authenticationScheme=JavaKerberos  ，请参阅[使用 Kerberos 集成身份验证连接到 SQL Server](../../connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md)。 <br/><br/> 使用**authenticationScheme = NTLM**时, 必须在 "**域**或**域名**" 属性中使用 ntlm 指定 windows 域进行身份验证, 以及在 "**用户**" 或 "**用户名**" 和 "密码" 中使用 windows 凭据  properties。 否则, 将出现错误 (必须指定连接属性)。  |
| cancelQueryTimeout<br/><br/>INT<br/><br/>-1 | 从用于 SQL Server 的 Microsoft JDBC Driver 6.4 开始, 此属性可用于取消连接上设置的**queryTimeout** 。 如果未以静默方式删除到 SQL Server 的 TCP 连接, 则查询执行会挂起并且不会引发异常。 仅当在连接上设置了 "queryTimeout" 时, 此属性才适用。 <br/><br/>驱动程序将等待**cancelQueryTimeout** + **queryTimeout**秒总数, 以丢弃连接并关闭通道。 <br/><br/>此属性的默认值为-1, 行为是无限期等待。 |
| columnEncryptionSetting<br/><br/>String<br/>["Enabled" &#124; "Disabled"]<br/><br/>禁用 | 从 Microsoft JDBC Driver 6.0 for SQL Server 开始，设置为“已启用”以使用 Always Encrypted (AE) 功能。 启用 AE后，JDBC 驱动程序以透明方式加密和解密存储在 SQL Server 中的加密数据库中的敏感数据。<br/><br/> 有关**sqlconnectionstringbuilder.columnencryptionsetting**的详细信息, 请参阅[使用 JDBC 驱动程序的 Always Encrypted](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md)了解更多详细信息。<br/><br/> **注意:** Always Encrypted 提供 SQL Server 2016 或更高版本。 |
| databaseName,<br/>“数据库”<br/><br/>String<br/>[&lt;=128 char]<br/><br/>null | 要连接到的数据库名称。 <br/><br/>如果未声明，则连接到默认的数据库。 |
| domainName,<br/>domain<br/><br/>String<br/>null | 要在中使用 NTLM 进行身份验证的 Windows 域。 |
| disableStatementPooling<br/><br/>boolean<br/>["true" &#124; "false"]<br/><br/>true | 指示是否应使用语句池的标志。 |
| enablePrepareOnFirst...<br/>PreparedStatementCall<br/><br/>boolean<br/>["true" &#124; "false"]<br/><br/>false | _enablePrepareOnFirstPreparedStatementCall_<br/><br/> 如果设置为 "true", 则通过在首次执行预<code>sp_prepexec</code>定义语句时调用来启用准备好的语句句柄创建。 <br/><br/>如果设置为 "false", 则在第二次执行发生后, <code>sp_executesql</code>它将调用<code>sp_prepexec</code>以设置预定义的语句句柄, 以更改已准备好的语句的第一次执行, 而不是准备语句。 |
| encrypt<br/><br/>boolean<br/>["true" &#124; "false"]<br/><br/>false | 如果设置为“true”，则指定在服务器安装了证书的情况下，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 将为在客户端与服务器之间发送的所有数据使用安全套接字层 (SSL) 加密。 默认值为“false”。<br/><br/> 从用于 SQL Server 的 Microsoft JDBC Driver 6.0 开始, 有一个新的连接设置 "authentication", 它默认使用 SSL 加密。 <br/><br/>有关详细信息，请参阅“authentication”属性。 |
| failoverPartner<br/><br/>String<br/><br/>null | 在数据库镜像配置中使用的故障转移服务器名称。 与主服务器进行初始连接时若发生失败，则会使用此属性；建立初始连接后，将忽略此属性。 必须与 databaseName 属性结合使用。<br/><br/> 注意：驱动程序不支持将故障转移伙伴实例的服务器实例端口号指定为连接字符串中 failoverPartner 属性的一部分  。 但是，支持在同一连接字符串中指定主体服务器实例的 serverName、instanceName 和 portNumber 属性以及故障转移伙伴实例的 failoverPartner 属性。<br/><br/> 如果在 Server 连接属性中指定虚拟机名称，则无法使用数据库镜像  。 有关详细信息，请参阅 [JDBC 驱动程序对高可用性和灾难恢复的支持](../../connect/jdbc/jdbc-driver-support-for-high-availability-disaster-recovery.md) |
| fips<br/><br/>boolean<br/>["true" &#124; "false"]<br/><br/>“false” | 对于启用 FIPS 的 JVM, 此属性应为**true**。 |
| fipsProvider<br/><br/>String<br/><br/>null | JVM 中配置的 FIPS 提供程序。 例如, BCFIPS 或 SunPKCS11。 已在版本 v6.4.0 中删除-请在[此处](https://github.com/Microsoft/mssql-jdbc/pull/460)查看详细信息。 |
| gsscredential<br/><br/>org.ietf.jgss.GSSCredential<br/><br/>null | 从用于 SQL Server 的 Microsoft JDBC Driver 6.2 开始, 可以在此属性中传递用于 Kerberos 约束委派的用户凭据。 <br/><br/>应将此**integratedSecurity**用作**true** , 并将**JavaKerberos**用作**authenticationScheme**。 |
| hostNameInCertificate<br/><br/>String<br/><br/>null | 要用于验证 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SSL 证书的主机名。<br/><br/> 如果未指定 hostNameInCertificate 属性或此属性设置为空，则 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 将使用连接 URL 上的 serverName 属性值作为主机名来验证 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SSL 证书  。<br/><br/> **注意:** 此属性与**加密**/**身份验证**属性和**trustServerCertificate**属性结合使用。 当且仅当连接使用安全套接字层 (SSL) 加密并且**trustServerCertificate**设置为 "false" 时, 此属性才影响证书验证。 请确保传递到 hostNameInCertificate 的值与服务器证书内公用名 (CN) 或使用者替代名称 (SAN) 中的 DNS 名称相匹配，这样才能成功连接 SSL  。 有关详细信息，请参阅[了解 SSL 支持](../../connect/jdbc/understanding-ssl-support.md)。 |
| INSTANCENAME<br/><br/>String<br/>[&lt;=128 char]<br/><br/>null | 要连接到的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例名。 如果未指定，则连接到默认实例。 对于 instanceName 和端口均已指定的情况，请参阅有关端口的备注。<br/><br/> 如果在 Server 连接属性中指定虚拟机名称，则无法使用 instanceName 连接属性   。 有关详细信息，请参阅 [JDBC 驱动程序对高可用性和灾难恢复的支持](../../connect/jdbc/jdbc-driver-support-for-high-availability-disaster-recovery.md)。 |
| integratedSecurity<br/><br/>boolean<br/>["true"&#124;"false"]<br/><br/>false | 设置为 "true" 表示 windows 操作系统使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] windows 凭据。 如果为 "true", 则 JDBC 驱动程序将搜索本地计算机凭据缓存, 查找用户登录到计算机或网络时提供的凭据。<br/><br/> 设置为 "true" (with **authenticationscheme = JavaKerberos**), 以指示使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Kerberos 凭据。 若要详细了解 Kerberos 身份验证，请参阅[使用 Kerberos 集成身份验证连接到 SQL Server](../../connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md)。 <br/><br/> 设置为 "true" (使用**authenticationscheme = NTLM**), 以指示使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]NTLM 凭据。 <br/><br/> 如果为“false”，则必须提供用户名和密码。 |
| jaasConfigurationName<br/><br/>String<br/><br/>SQLJDBCDriver | 从用于 SQL Server 的 Microsoft JDBC Driver 6.2 开始, 每个与 SQL Server 的连接都可以有自己的 JAAS 登录配置文件来建立 Kerberos 连接。 可以通过此属性传递登录配置文件的名称。 <br/> 默认情况下, 针对 IBM `useDefaultCcache = true` jvm 和`useTicketCache = true`其他 jvm 的驱动程序集属性。 |
| keyStoreAuthentication<br/><br/>String<br/><br/>null | 从用于 SQL Server 的 Microsoft JDBC Driver 6.0 开始, 此属性标识要为与 Always Encrypted 无缝建立连接的密钥存储, 并确定用于对密钥存储进行身份验证的身份验证机制。 适用于 SQL Server 的 Microsoft JDBC Driver 6.0 支持使用此属性 (需要为其设置 "**keyStoreAuthentication = JavaKeyStorePassword**") 无缝设置 Java 密钥存储。 请注意, 若要使用此属性, 还需要设置 Java 密钥存储的**keyStoreLocation**和**keyStoreSecret**属性。 <br/><br/>有关详细信息，请参阅[通过 JDBC 驱动程序使用 Always Encrypted](https://msdn.microsoft.com/library/mt591987%28v=sql.110%29.aspx?f=255&MSPPError=-2147217396)。 |
| keyStoreLocation<br/><br/>String<br/><br/>null | 如果**keyStoreAuthentication = JavaKeyStorePassword**, 则**KeyStoreLocation**属性标识 Java 密钥存储文件的路径, 该文件用于存储要与 Always Encrypted 数据一起使用的列主密钥。 请注意, 该路径必须包含密钥存储文件名。<br/><br/>有关详细信息，请参阅[通过 JDBC 驱动程序使用 Always Encrypted](https://msdn.microsoft.com/library/mt591987%28v=sql.110%29.aspx?f=255&MSPPError=-2147217396)。 |
| keyStoreSecret<br/><br/>String<br/><br/>null | 如果**keyStoreAuthentication = JavaKeyStorePassword**, 则**keyStoreSecret**属性标识用于密钥存储和密钥的密码。 请注意, 对于使用 Java 密钥存储密钥存储, 密钥密码必须相同。<br/><br/>有关详细信息，请参阅[通过 JDBC 驱动程序使用 Always Encrypted](https://msdn.microsoft.com/library/mt591987%28v=sql.110%29.aspx?f=255&MSPPError=-2147217396)。 |
| lastUpdateCount<br/><br/>boolean<br/>["true" &#124; "false"]<br/><br/>true | 如果值为“true”，则仅返回传递给服务器的 SQL 语句的最终更新计数，它可用于单个的 SELECT、INSERT 或 DELETE 语句中，以忽略由服务器触发器引起的其他更新计数。 将此属性设置为“false”可导致所有更新计数都被返回，包括由服务器触发器返回的更新计数。<br/><br/> 注意：此属性仅当与 [executeUpdate](../../connect/jdbc/reference/executeupdate-method-sqlserverstatement.md) 方法一起使用时才适用  。 其他所有 execute 方法返回所有结果和更新计数。 此属性仅影响由服务器触发器返回的更新计数， 而不影响作为触发器执行结果的一部分的结果集或错误。 |
| lockTimeout<br/><br/>INT<br/><br/>-1 | 在等待多少毫秒后数据库报告锁定超时。默认行为是无限期等待。 如果指定，该值将成为此连接上所有语句的默认值。 请注意, **setQueryTimeout ()** 可用于设置特定语句的超时时间。 该值可为 0，这表示无需等待。 |
| loginTimeout<br/><br/>INT<br/>[0..65535]<br/><br/>15 | 因连接失败而中止连接之前驱动程序应等待的秒数。 零值表示该超时为默认系统超时，默认情况下指定为 15 秒。 非零值为因连接失败而中止连接之前驱动程序应等待的秒数。<br/><br/> 如果在 Server 连接属性中指定虚拟机名称，则应指定三分钟或更长的超时值，使故障转移连接有足够的时间连接成功  。 有关详细信息，请参阅 [JDBC 驱动程序对高可用性和灾难恢复的支持](../../connect/jdbc/jdbc-driver-support-for-high-availability-disaster-recovery.md)。 |
| msiClientId<br/><br/>String<br/><br/>null | 使用**ActiveDirectoryMSI** authentication 模式建立连接时, 用于获取**accessToken**的托管服务标识 (MSI) 的客户端 ID。|
| multiSubnetFailover<br/><br/>Boolean<br/><br/>false | 在连接到 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 可用性组或 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 故障转移群集实例的可用性组侦听程序时，应始终指定 multiSubnetFailover=true  。 multiSubnetFailover=true 将配置 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 以便更快地检测和连接到（当前）活动服务器  。 可能的值为“True”和“False”。 有关详细信息，请参阅 [JDBC 驱动程序对高可用性和灾难恢复的支持](../../connect/jdbc/jdbc-driver-support-for-high-availability-disaster-recovery.md)。<br/><br/> 可以以编程方式访问带有 [getPropertyInfo](../../connect/jdbc/reference/getpropertyinfo-method-sqlserverdriver.md)、[getMultiSubnetFailover](../../connect/jdbc/reference/getmultisubnetfailover-method-sqlserverdatasource.md) 和 [setMultiSubnetFailover](../../connect/jdbc/reference/setmultisubnetfailover-method-sqlserverdatasource.md) 的 multiSubnetFailover 连接属性  。<br/><br/> **注意:** 从用于 SQL Server 的 Microsoft JDBC Driver 6.0 开始, 在连接到可用性组侦听器时, 不再需要将**multiSubnetFailover**设置为 "true"。 默认情况下启用的新属性**transparentNetworkIPResolution**提供检测和连接到 (当前) 活动服务器。 |
| packetSize<br/><br/>INT<br/>[-1 &#124; 0 &#124; 512..32767]<br/><br/>8000 | 用来与 SQL Server 通信的网络包大小，以字节为单位指定。 值为 -1 表示使用服务器默认数据包大小。 值 0 表示使用最大值 32767。 如果将此属性设置为可接受范围外的值，将出现异常。<br/><br/> 重要事项：当启用加密 (encrypt=true) 时，建议不要使用 packetSize 属性  。 否则，驱动程序可能引发连接错误。 有关详细信息，请参阅 [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md) 类的 [setPacketSize](../../connect/jdbc/reference/setpacketsize-method-sqlserverdatasource.md) 方法。 |
| password<br/><br/>String<br/>[&lt;=128 char]<br/><br/>null | 与 SQL 用户和密码连接时的数据库密码。<br/>对于带有主体名称和密码的 Kerberos 连接, 此属性设置为 Kerberos 主体密码。 |
| portNumber,<br/>port<br/><br/>INT<br/>[0..65535]<br/><br/>1433 | [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 侦听的端口。 如果在连接字符串中指定了端口号，则不会向 SQLbrowser 发出请求。 如果端口和 instanceName 都已指定，则将建立到指定端口的连接。 但是，将对 instanceName 进行验证，如果它与端口不符，将引发错误  。<br/><br/> 重要事项：建议始终指定端口号，因为这比使用 SQLbrowser 更安全  。 |
| queryTimeout<br/><br/>INT<br/><br/>-1 | 查询上出现超时前等待的秒数。 默认值为-1, 表示无限期超时。 将此选项设置为0也表示无限期等待。 |
| responseBuffering<br/><br/>String<br/>["full" &#124; "adaptive"]<br/><br/>自适应 | 如果此属性设置为“adaptive”，将只在需要时才缓冲尽可能少的数据。 默认模式为“adaptive”。<br/><br/> 如果此属性设置为“full”，当执行语句时，将从服务器读取整个结果集。<br/><br/> 注意：将 JDBC 驱动程序从版本 1.2 升级后，默认缓冲行为将为“adaptive”  。 如果应用程序从未设置“responseBuffering”属性，而需要在应用程序中保留版本 1.2 的默认行为，则必须在连接属性中或使用 [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) 对象的 [setResponseBuffering](../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md) 方法将 responseBufferring 属性设置为“full”。 |
| selectMethod<br/><br/>String<br/>["direct" &#124; "cursor"]<br/><br/>直通 | 如果该属性设置为“cursor”，则对基于 TYPE_FORWARD_ONLY 和 CONCUR_READ_ONLY 游标的连接创建的每个查询，都会创建一个数据库游标   。 通常仅当应用程序生成较大的结果集，以至于客户端内存无法完全容纳时，才需要使用该属性。 如果将该属性设置为“cursor”，则客户端内存中仅保留数目有限的结果集行。 <br/><br/>默认行为是在客户端内存中保留所有结果集的行。 在应用程序需要处理所有行时，此行为可提供最快性能。 |
| sendStringParameters...<br/>AsUnicode<br/><br/>boolean<br/>["true" &#124; "false"]<br/><br/>true | sendStringParametersAsUnicode <br/><br/>如果 sendStringParametersAsUnicode 属性设置为“true”，则字符串参数将以 Unicode 格式发送给服务器  。<br/><br/> 如果 sendStringParametersAsUnicode  属性设置为“false”，则字符串参数将以非 Unicode 格式（例如 ASCII/MBCS 而不是 Unicode）发送到服务器。<br/><br/> sendStringParametersAsUnicode 属性的默认值为“true”  。<br/><br/> 请注意：仅在通过 CHAR、VARCHAR 或 LONGVARCHAR JDBC 类型发送参数值时，才检查 sendStringParametersAsUnicode 属性      新的 JDBC 4.0 国家字符方法（例如 [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 和 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 类的 setNString、setNCharacterStream 和 setNClob 方法）始终将它们的参数值以 Unicode 格式发送到服务器，而不考虑此属性的设置。<br/><br/> 要获得 CHAR、VARCHAR 和 LONGVARCHAR JDBC 数据类型的最佳性能，应用程序应将 sendStringParametersAsUnicode 属性设置为“false”，并使用 [SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) 和 [SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md) 类的 setString、setCharacterStream 和 setClob 非区域字符方法     。<br/><br/> 当应用程序将 sendStringParametersAsUnicode 属性设置为“false”，并在服务器端使用非区域字符方法访问 Unicode 数据类型（例如，nchar、nvarchar 和 ntext）时，如果数据库排序规则不支持非区域字符方法传递的字符串参数中的字符，则有些数据可能会丢失     。<br/><br/> 请注意, 应用程序应将[SQLServerPreparedStatement](../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)和[SQLServerCallableStatement](../../connect/jdbc/reference/sqlservercallablestatement-class.md)类的 SetNString、setNCharacterStream 和 setNClob 区域字符方法用于**NCHAR**、 **NVARCHAR**、和**LONGNVARCHAR** JDBC 数据类型。 |
| sendTimeAsDatetime<br/><br/>boolean<br/>["true" &#124; "false"]<br/><br/>true | [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] JDBC Driver 3.0 中新增了此属性。<br/><br/> 设置为 "true" 可将 .java 值作为[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **datetime**值发送到服务器。 <br/>如果设置为 "false", 则将 .java 值作为[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **时间**值发送到服务器。<br/><br/> 此属性的默认值当前为 "true", 并且在将来的版本中可能会更改。<br/><br/> 有关如何在将 .java 值[!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)]发送到服务器之前配置它们的详细信息, 请参阅[配置如何将 .java 值发送到服务器](../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md)。 |
| serverName,<br/>服务器<br/><br/>String<br/><br/>null | 运行 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的计算机。<br/><br/> 此外还可指定 [!INCLUDE[ssHADR](../../includes/sshadr_md.md)] 可用性组的虚拟机名称。 有关详细信息，请参阅 [JDBC 驱动程序对高可用性和灾难恢复的支持](../../connect/jdbc/jdbc-driver-support-for-high-availability-disaster-recovery.md)。 |
| serverNameAsACE<br/><br/>boolean<br/>["true" &#124; "false"]<br/><br/>false | 从 Microsoft JDBC Driver 6.0 for SQL Server 开始，设置为“true”以指示驱动程序应将 Unicode 服务器名称转换为 ASCII 兼容编码 (Punycode) 以进行连接。 如果此设置为 false，则驱动程序使用用户提供的服务器名称进行连接。<br/><br/> 有关更多详细信息, 请参阅[JDBC 驱动程序的国际功能](../../connect/jdbc/international-features-of-the-jdbc-driver.md)。 |
| serverPreparedStatement...<br/>DiscardThreshold<br/><br/>Integer<br/><br/>10 | *serverPreparedStatementDiscardThreshold*<br/><br/>从针对 SQL Server 的 JDBC Driver 6.2 开始, 此属性可用于控制在执行服务器上的清除未完成的<code>sp_unprepare</code>句柄之前, 每个连接可以完成的未完成的已准备语句丢弃操作 () 数. <br/><br/> 如果将此属性设置为&lt;1, 则在预定义的语句关闭时将立即执行 unprepare 操作。 如果将其设置为&gt;1, 则这些调用将一起分批, 以避免调用 sp_unprepare 的开销过于频繁。 |
| serverSpn<br/><br/>String<br/><br/>null | 始于 Microsoft JDBC Driver 4.2 for SQL Server，此可选属性可用于指定 Java Kerberos 连接的服务主体名称 (SPN)。  它与**authenticationScheme**结合使用。<br/><br/> 若要指定 SPN，它可以采用“MSSQLSvc/fqdn:port@REALM”的格式，其中 fqdn 是完全限定的域名，port 是端口号，REALM 是 SQL Server 的 Kerberos 领域的大写字母表示。<br/><br/> 注意：如果客户端的默认领域（在 Kerberos 配置中进行指定）与 SQL Server 的 Kerberos 领域相同，可选择使用 @REALM。<br/><br/> 若要详细了解如何将 serverSpn  与 Java Kerberos 结合使用，请参阅[使用 Kerberos 集成身份验证连接到 SQL Server](../../connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md)。 |
| statementPooling...<br/>CacheSize<br/><br/>INT<br/><br/>0 | *statementPoolingCacheSize*<br/><br/>从 JDBC Driver 6.4 开始, SQL Server, 此属性可用于在驱动程序中启用已准备好的语句句柄缓存。 <br/><br/>此属性定义语句池的缓存大小。 <br/><br/>此属性只能与应设置为 "false" 的**disableStatementPooling**连接属性结合使用。 将**disableStatementPooling**设置为 "true" 或将**statementPoolingCacheSize**设置为0会禁用预定义的语句句柄缓存。|
| socketTimeout<br/><br/>INT<br/><br/>0 | 在套接字读取或接受超时之前要等待的毫秒数。 默认值为 0, 表示无限期超时。 |
| sslProtocol<br/><br/>String<br/><br/>TLS | 从 JDBC Driver 6.4 开始, SQL Server, 此属性可用于指定在安全连接期间要考虑的 TLS 协议。 <br/>可取值包括：TLS  、TLSv1  、TLSv1.1  和 TLSv1.2  。 <br/><br/>有关详细信息, 请参阅[SSLProtocol](https://github.com/Microsoft/mssql-jdbc/wiki/SSLProtocol)。 |
| transparentNetwork...<br/>IPResolution<br/><br/>boolean<br/>["true" &#124; "false"]<br/><br/>true | *transparentNetworkIPResolution*<br/><br/>从用于 SQL Server 的 Microsoft JDBC Driver 6.0 开始, 此属性提供更快的检测和连接到 (当前) 活动服务器。 可能的值为 "true" 和 "false", 其中 "true" 是默认值。<br/><br/> 在 Microsoft JDBC Driver 6.0 for SQL Server 之前, 应用程序必须将连接字符串设置为包含 "multiSubnetFailover = true", 以指示它已连接到 AlwaysOn 可用性组。 如果不将**multiSubnetFailover**连接关键字设置为 "true", 则应用程序可能会在连接到 AlwaysOn 可用性组时遇到超时。 从用于 SQL Server 的 Microsoft JDBC Driver 6.0 开始, 应用程序无需再将 multiSubnetFailover 设置为 true。 <br/><br/>**注意:** 如果 transparentNetworkIPResolution = true, 则第一个连接尝试使用500毫秒作为超时。 任何后续尝试使用的超时逻辑都与 multiSubnetFailover 属性使用的相同。 |
| trustManagerClass<br/><br/>String<br/><br/>null | 自定义<code>javax.net.ssl.TrustManager</code>实现的完全限定类名。 |
| trustManager ...<br/>ConstructorArg<br/><br/>String<br/><br/>null | *trustManagerConstructorArg*<br/><br/>要传递给 TrustManager 的构造函数的可选参数。 如果指定 trustManagerClass 并请求加密的连接, 则将使用自定义 TrustManager, 而不是基于默认系统 JVM 基于密钥的 TrustManager。 |
| trustServerCertificate<br/><br/>boolean<br/>["true" &#124; "false"]<br/><br/>false | 如果设置为“true”，则指定 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 将不会验证 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SSL 证书。<br/><br/> 如果设置为“true”，当使用 SSL 对通信层加密时，将自动信任 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SSL 证书。<br/><br/> 如果设置为 "false" [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] , 则验证服务器 SSL 证书。 如果服务器证书验证失败，驱动程序将报错并终止连接。 默认值为“false”。 确保传递给 serverName 的值与服务器证书的公用名 (CN) 或使用者替代名称中的 DNS 名称完全匹配，以便成功建立 SSL 连接  。 有关详细信息，请参阅[了解 SSL 支持](../../connect/jdbc/understanding-ssl-support.md)。<br/><br/> **注意:** 此属性与**加密**/**身份验证**属性结合使用。 当且仅当连接使用 SSL 加密时, 此属性才影响服务器 SSL 证书验证。 |
| trustStore<br/><br/>String<br/><br/>null | 指向证书 trustStore 文件的路径（包括文件名）。 trustStore 文件包含客户端信任的证书的列表。<br/><br/> 如果未指定此属性或此属性设置为空，则驱动程序将依赖于信任关系管理器工厂的查找规则以确定要使用哪一个证书存储区。<br/><br/> 默认的 SunX509 TrustManagerFactory 试图按以下搜索顺序查找信任的材料  ：<br/><br/> 由“javax.net.ssl.trustStore”Java 虚拟机 (JVM) 系统属性指定的文件。<br/><br/> “&lt;java-home&gt;/lib/security/jssecacerts”文件。<br/><br/> “&lt;&gt;/lib/security/cacerts”文件。<br/><br/> <br/><br/> 有关详细信息，请参阅 Sun Microsystems 网站上的 SUNX509 TrustManager 接口文档。<br/><br/> **注意:** 此属性仅影响证书 trustStore 查找, 并且仅当连接使用 SSL 加密并且**trustServerCertificate**属性设置为 "false" 时才会影响。 |
| trustStorePassword<br/><br/>String<br/><br/>null | 用于检查 trustStore 数据完整性的密码。<br/><br/> 如果设置了 trustStore 属性，但未设置 trustStorePassword 属性，则不检查 trustStore 的完整性。<br/><br/> 如果未指定 trustStore 和 trustStorePassword 属性，驱动程序将使用 JVM 系统属性“javax.net.ssl.trustStore”和“javax.net.ssl.trustStorePassword”。 如果未指定“javax.net.ssl.trustStorePassword”系统属性，则不检查 trustStore 的完整性。<br/><br/> 如果未指定 trustStore 属性，但设置了 trustStorePassword 属性，JDBC 驱动程序将使用由“javax.net.ssl.trustStore”指定作为信任存储区的文件，并使用指定的 trustStorePassword 检查信任存储区的完整性。 当客户端应用程序不希望在 JVM 系统属性中存储密码时，这一点可能是必需的。<br/><br/> **注意:** 当且仅当连接使用 SSL 连接并且**trustServerCertificate**属性设置为 "false" 时, trustStorePassword 属性才影响证书 trustStore 查找。 |
| trustStoreType<br/><br/>String<br/><br/>JKS | 设置此属性以指定要用于 FIPS 模式的信任存储区类型。 <br/><br/>可能的值为**PKCS12**或由 FIPS 提供程序定义的类型。 |
| useBulkCopyFor...<br/>BatchInsert<br/><br/>boolean<br/>["true" &#124; "false"]<br/><br/>false | _useBulkCopyForBatchInsert_<br/><br/> 从用于 SQL Server 的 Microsoft JDBC Driver 7.0 开始, 可以启用此连接属性, 以在执行批处理插入操作`java.sql.PreparedStatement`时使用大容量复制 API 以提高性能。 <br/><br/>仅当目标服务器的类型为**Azure 数据仓库**时, 此功能才起作用。 默认情况下, 它处于禁用状态, 请将此属性设置为 "true" 以启用此功能。 <br/></br> 重要说明：此功能仅支持完全参数化的 INSERT 查询  。 如果插入查询与其他 SQL 查询合并, 或包含值中的数据, 则执行将回退到基本的批处理插入操作。 <br/><br/> 有关如何使用此属性的详细信息, 请参阅为[批处理插入操作使用大容量复制 API](use-bulk-copy-api-batch-insert-operation.md)|
| useFmtOnly<br /><br />boolean<br />["true" &#124; "false"]<br /><br />false | Microsoft JDBC Driver for SQL Server 从7.4 开始, 还提供了另一种方法来通过指定**useFmtOnly**连接属性从服务器查询参数元数据。 将此属性设置为 "true" 可指定驱动程序在查询`SET FMTONLY`参数元数据时应使用逻辑。 默认情况下, 此功能处于关闭状态, 不建议使用此属性, 因为`SET FMTONLY`已将其标记为不推荐使用。 **useFmtOnly**仅可用于解决中[`sp_describe_undeclared_parameters`](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-describe-undeclared-parameters-transact-sql?view=sql-server-2017)的已知问题和限制。<br/><br/> 此功能目前仅支持单一`SELECT/INSERT/UPDATE/DELETE`查询。 如果尝试将此功能用于不支持的/多个查询, 将导致驱动程序尝试分析查询, 但很可能会导致异常。<br/><br/> 有关详细信息, 请参阅[通过 UseFmtOnly 检索 java.sql.parametermetadata](../../connect/jdbc/using-usefmtonly.md)。 |
| userName,<br/>user<br/><br/>String<br/>[&lt;=128 char]<br/><br/>null | 与 SQL 用户和密码连接时的数据库用户。<br/><br/>对于带有主体名称和密码的 Kerberos 连接, 此属性设置为 Kerberos 主体名称。 |
| workstationID<br/><br/>String<br/>[&lt;=128 char]<br/><br/>&lt;空字符串&gt; | 工作站 ID。 用于在各种 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 探查和日志记录工具中标识特定的工作站。 <br/><br/>如果未指定任何内容，则将使用 &lt;空字符串&gt;。 |
| xopenStates<br/><br/>boolean<br/>["true" &#124; "false"]<br/><br/>false | 设置为“true”将指定驱动程序在异常时返回 XOPEN 兼容的状态代码。 <br/><br/>默认将返回 SQL 99 状态代码。 |
| &nbsp; | &nbsp; |

> [!NOTE]  
> [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 采用服务器的连接属性默认值，只有 ANSI_DEFAULTS 和 IMPLICIT_TRANSACTIONS 除外。 [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] 将 ANSI_DEFAULTS 自动设置为 ON，将 IMPLICIT_TRANSACTIONS 自动设置为 OFF。

> [!Important]
> 如果将身份验证设置为 ActiveDirectoryPassword, 则需要在类路径中包含以下库: [azure](https://github.com/AzureAD/azure-activedirectory-library-for-java)的。 它可在[Maven 存储库](https://mvnrepository.com/artifact/com.microsoft.azure/adal4j)中找到。 下载库及其依赖项的最简单方法是使用 Maven: 
> 1. 首先, 在系统上安装 Maven 
> 2. 请参阅驱动程序的[GitHub 页](https://github.com/Microsoft/mssql-jdbc)
> 3. 下载 pom 文件
> 4. 运行以下 Maven 命令以下载库及其依赖项:`mvn dependency:copy-dependencies`

## <a name="see-also"></a>另请参阅

[通过 JDBC 驱动程序连接到 SQL Server](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)  
[FIPS 模式](../../connect/jdbc/fips-mode.md)
