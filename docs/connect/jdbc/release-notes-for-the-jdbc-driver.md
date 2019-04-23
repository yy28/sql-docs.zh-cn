---
title: JDBC Driver 的发行说明 | Microsoft Docs
ms.custom: ''
ms.date: 04/16/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 074f211e-984a-4b76-bb15-ee36f5946f12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5e75f732fc44ee339cb3d9d47518627f264cb8cc
ms.sourcegitcommit: e2d65828faed6f4dfe625749a3b759af9caa7d91
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2019
ms.locfileid: "59671333"
---
# <a name="release-notes-for-the-microsoft-jdbc-driver"></a>Microsoft JDBC Driver 的发行说明

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

本文列出了 Microsoft JDBC Driver for SQL Server 的版本。 对于每个发行版本，将对所做的更改进行命名和说明。

## <a name="722"></a>7.2.2

### <a name="compliance"></a>遵从性

2019 年 4 月 16 日

| 符合性更改 | 详细信息 |
| :---------------- | :------ |
| 下载 JDBC Driver 7.2 的最新更新。 | &bull; &nbsp; [Microsoft 下载中心](https://go.microsoft.com/fwlink/?linkid=2063159)<br/>&bull; &nbsp; [GitHub, 7.2.2](https://github.com/Microsoft/mssql-jdbc/releases/tag/v7.2.2)<br/>&bull; &nbsp; [Maven Central](https://search.maven.org/search?q=g:com.microsoft.sqlserver) |
| 完全符合 JDBC API 规范 4.2。 | 根据 Java 版本兼容性命名 7.2 包中的 jar。<br/><br/>例如，7.2 包中的 mssql-jdbc-7.2.2.jre11.jar 文件应与 Java 11 配合使用。 |
| 除 Java 开发工具包 (JDK) 版本 1.8 外，还与 JDK 11.0 兼容。 | 除 Java 开发工具包 (JDK) 版本 1.8 外，Microsoft JDBC Driver 7.2 for SQL Server 现在还与 JDK 11.0 兼容。 |
| &nbsp; | &nbsp; |

> [!NOTE]
> 于 2019 年 1 月 31 日发布的 JDBC 7.2 Release To Web (RTW) 驱动程序中发现了 SQL 语句分析方面的问题。 所做的更改已回滚，并且新的 jar（版本 7.2.1）已于 2019 年 2 月 11 日发布。
>
> 对驱动程序进行了另一个更新来解决 ActivityID 未正确清除的问题。 新的 jar（版本 7.2.2）已于 2019 年 4 月 16 日发布。
> 
> 我们建议更新项目以使用 7.2.2 版本 jar。 有关详细信息，请查看 [GitHub, 7.2.1](https://github.com/Microsoft/mssql-jdbc/releases/tag/v7.2.1) 和 [GitHub, 7.2.2](https://github.com/Microsoft/mssql-jdbc/releases/tag/v7.2.2) 的发行说明。

### <a name="active-directory-managed-service-identity-msi-authentication"></a>Active Directory 托管服务标识 (MSI) 身份验证

| MSI 更改 | 详细信息 |
| :--------- | :------ |
| 支持 Active Directory 托管服务标识 (MSI) 身份验证模式。 | 此身份验证模式适用于支持“标识”功能的 Azure 资源。<br/><br/>两种类型的托管系统标识 (MSI) 均受驱动程序支持，可获取用于建立安全连接的 accessToken。 |
| 使用此身份验证模式的更多详细信息以及示例应用程序。 | 请参阅[使用 Azure Active Directory 身份验证进行连接](../../connect/jdbc/connecting-using-azure-active-directory-authentication.md)。 |
| &nbsp; | &nbsp; |

### <a name="introduces-open-service-gateway-initiative-osgi-support"></a>引入开放服务网关协议 (OSGi) 支持

| OSGi 更改 | 详细信息 |
| :---------- | :------ |
| 添加了 DataSourceFactory 实现。 | &bull; &nbsp; `org.osgi.service.jdbc.DataSourceFactory`<br/>&bull; &nbsp; `com.microsoft.sqlserver.jdbc.osgi.SQLServerDataSourceFactory` |
| 添加了 Activator 实现。 | &bull; &nbsp; `org.osgi.framework.BundleActivator`<br/>&bull; &nbsp; `com.microsoft.sqlserver.jdbc.osgi.Activator` |
| &nbsp; | &nbsp; |

### <a name="introduces-sqlservererror-apis"></a>引入 SQLServerError API

| 错误 API 更改 | 详细信息 |
| :--------------- | :------ |
| 引入了 SQLServerError API。 | 获取 API 以检索有关从服务器生成的错误的其他详细信息。<br/><br/>&bull; &nbsp; `SQLServerException.getSQLServerError()`<br/>&bull; &nbsp; `SQLServerError` |
| 其他详细信息。 | 请参阅[处理错误](../../connect/jdbc/handling-errors.md)。 |
| &nbsp; | &nbsp; |

### <a name="updated-microsoft-azure-active-directory-authentication-library-adal4j-for-java-version-163"></a>更新了用于 Java 的 Microsoft Azure Active Directory 身份验证库 (ADAL4J) 版本 1.6.3

| ADAL4J 更改 | 详细信息 |
| :------------ | :------ |
| 已将 ADAL4J 上的 Maven 依赖项更新为版本 1.6.3。 | &nbsp; |
| 引入了“适用于 AutoRest 的 Java 客户端运行时”作为 Maven 依赖项版本 1.6.5。 | &nbsp; |
| 其他详细信息。 | 请参阅 [Microsoft JDBC Driver for SQL Server 的功能依赖项](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md)。 |
| &nbsp; | &nbsp; |

### <a name="updated-microsoft-azure-key-vault-sdk-for-java-version-120"></a>更新了 Microsoft Azure Key Vault SDK for Java 版本 1.2.0

| Key Vault SDK 更改 | 详细信息 |
| :------------------- | :------ |
| 已将 Microsoft Azure Key Vault SDK for Java 的 Maven 依赖项更新为版本 1.2.0。 | &nbsp; |
| 引入了 Microsoft Azure SDK for Key Vault WebKey 作为 Maven 依赖项（版本 1.2.0）。 | &nbsp; |
| 其他详细信息。 | 请参阅 [Microsoft JDBC Driver for SQL Server 的功能依赖项](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md)。 |
| &nbsp; | &nbsp; |

### <a name="known-issues"></a>已知问题

| 已知问题 | 详细信息 |
| :----------- | :------ |
| 在某些情况下，参数化查询。 | 已于 2019 年 2 月发布 7.2.0 版本和 v7.2.1 的更新来解决此问题。 |
| 清除 ActivityID。 | 已于 2019 年 4 月发布 7.2.1 版本和 v7.2.2 的更新来解决此问题。 |
| &nbsp; | &nbsp; |

## <a name="70"></a>7.0

Microsoft JDBC Driver 7.0 for SQL Server 完全符合 JDBC API 规范 4.2。 根据 Java 版本兼容性命名 7.0 包中的 jar。 例如，7.0 包中的 mssql-jdbc-7.0.0.jre10.jar 文件应与 Java 10 配合使用。

### <a name="support-for-jdk-10"></a>支持 JDK 10

除 Java 开发工具包 (JDK) 版本 1.8 外，Microsoft JDBC Driver 7.0 for SQL Server 现在还与 JDK 10.0 兼容。 此更新还通过其清单文件将驱动程序的 `Automatic-Module-Name` 公开为 `com.microsoft.sqlserver.jdbc`。

### <a name="support-for-spatial-datatypes"></a>支持空间数据类型

Microsoft JDBC Driver 7.0 for SQL Server 现在提供对 SQL Server 空间数据类型 Geography 和 Geometry 的支持。 有关空间数据类型 API 以及如何使用它们的详细信息，请参阅[使用空间数据类型](../../connect/jdbc/use-spatial-datatypes.md)。

### <a name="implementation-for-jdbc-43-introduced-javasqlconnection-apis-beginrequest-and-endrequest"></a>JDBC 4.3 实现引入了 java.sql.Connection API beginRequest() 和 endRequest()

Microsoft JDBC Driver 7.0 for SQL Server 现在实现了 `java.sql.Connection` 类中的 `beginRequest()` 和 `endRequest()` API。 这些 API 是使用 JDBC 4.3 规范和 JDK 9 引入的。 有关这些 API 的驱动程序实现的详细信息，请参阅 [JDBC 驱动程序的 JDBC 4.3 符合性](../../connect/jdbc/jdbc-4-3-compliance-for-the-jdbc-driver.md)。

### <a name="support-for-sql-data-discovery-and-classification"></a>支持“SQL 数据发现和分类”

Microsoft JDBC Driver 7.0 for SQL Server 提供对 SQL 数据发现和分类的支持，以用于支持此功能的任何目标数据库。 驱动程序现在公开 `SQLServerResultSet.getSensitivityClassification()` API 以从提取的 `ResultSet` 中提取此信息。

有关如何将此功能用于 JDBC 驱动程序的详细信息，请参阅 [SQL 数据发现和分类](../../connect/jdbc/data-discovery-classification-sample.md)中的示例。

### <a name="added-connection-property-usebulkcopyforbatchinsert"></a>添加了连接属性：useBulkCopyForBatchInsert

Microsoft JDBC Driver 7.0 for SQL Server 引入了新的连接属性 `useBulkCopyForBatchInsert`。 只有 Azure SQL 数据仓库才支持此属性。

默认情况下禁用此属性。 当将大量数据推送到 Azure SQL 数据仓库时，可以启用此属性以提高用户应用程序的性能。 启用此属性将更改批插入操作的行为，以切换为对用户提供的数据执行大容量复制操作。 有关此属性及其限制的详细信息，请参阅[将大容量复制 API 用于批插入操作](../../connect/jdbc/use-bulk-copy-api-batch-insert-operation.md)。

### <a name="added-connection-property-cancelquerytimeout"></a>添加了连接属性：cancelQueryTimeout

Microsoft JDBC Driver 7.0 for SQL Server 引入了新的连接属性 `cancelQueryTimeout` 以取消 `java.sql.Connection` 和 `java.sql.Statement` 对象上的 `queryTimeout`。

### <a name="added-azure-key-vault-provider-constructors"></a>添加了 Azure Key Vault 提供程序构造函数

Microsoft JDBC Driver 7.0 for SQL Server 为 `SQLServerColumnEncryptionAzureKeyVaultProvider` 重新引入了先前删除的构造函数。 它允许通过用 `SQLServerKeyVaultAuthenticationCallback` 实现的自定义方法进行身份验证来提取访问令牌。

新的构造函数具有以下定义：

```java
/* This constructor is added to provide backward compatibility with 6.0
* version of the driver. It is marked deprecated for removal in the next
* stable release.
*/
@Deprecated
public SQLServerColumnEncryptionAzureKeyVaultProvider(
        SQLServerKeyVaultAuthenticationCallback authenticationCallback,
        ExecutorService executorService) throws SQLServerException;

/*New constructor to replace the above constructor*/
public SQLServerColumnEncryptionAzureKeyVaultProvider(
            SQLServerKeyVaultAuthenticationCallback authenticationCallback) throws SQLServerException;
```

### <a name="updated-microsoft-azure-active-directory-authentication-library-adal4j-for-java-version-160"></a>更新了“用于 Java 的 Microsoft Azure Active Directory 身份验证库 (ADAL4J)”版本 1.6.0

Microsoft JDBC Driver 7.0 for SQL Server 已将“用于 Java 的 Microsoft Azure Active Directory 身份验证库 (ADAL4J)”上的 Maven 依赖项更新为版本 1.6.0。 有关依赖项的详细信息，请参阅 [Microsoft JDBC Driver for SQL Server 的功能依赖项](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md)。

## <a name="64"></a>6.4

Microsoft JDBC Driver 6.4 for SQL Server 完全符合 JDBC 规范 4.1 和 4.2。 根据 Java 版本兼容性命名 6.4 包中的 jar。 例如，6.4 包中的 mssql-jdbc-6.4.0.jre8.jar 文件必须与 Java 8 配合使用。

### <a name="support-for-jdk-9"></a>支持 JDK 9

除了支持 JDK 8.0 和 7.0 以外，驱动程序还支持 JDK 版本 9.0。

### <a name="jdbc-43-compliance"></a>JDBC 4.3 符合性

除了支持 4.1 和 4.2 以外，驱动程序还支持 Java Database Connectivity API 4.3 规范。 JDBC 4.3 API 方法已添加，但尚未实现。 有关详细信息，请参阅 [JDBC Driver 的 JDBC 4.3 合规性](../../connect/jdbc/jdbc-4-3-compliance-for-the-jdbc-driver.md)。

### <a name="added-connection-property-sslprotocol"></a>添加了连接属性：sslProtocol

新的连接属性允许用户指定 TLS 协议关键字。 可能的值包括：“TLS”、“TLSv1”、“TLSv1.1”和“TLSv1.2”。 有关详细信息，请参阅 [SSLProtocol](https://github.com/Microsoft/mssql-jdbc/wiki/SSLProtocol)。

### <a name="deprecated-connection-property-fipsprovider"></a>弃用了连接属性：fipsProvider

连接属性 `fipsProvider` 已从接受的连接属性的列表中删除。 有关详细信息，请参阅相关的 [GitHub 拉取请求](https://github.com/Microsoft/mssql-jdbc/pull/460)。

### <a name="added-connection-properties-for-specifying-a-custom-trustmanager"></a>添加了用于指定自定义 TrustManager 的连接属性

驱动程序现在支持指定添加了 `trustManagerClass` 和 `trustManagerConstructorArg` 连接属性的自定义 TrustManager。 可以动态指定基于每个连接信任的一组证书，而无需修改 Java 虚拟机 (JVM) 环境的全局设置。

### <a name="added-support-for-datetimesmalldatetime-in-table-valued-parameters"></a>添加了对表值参数中的 datetime/smallDatetime 的支持

当使用的是表值参数 (TVP) 时，驱动程序现在支持数据类型 `datetime` 和 `smallDatetime`。

### <a name="added-support-for-the-sqlvariant-datatype"></a>添加了对 sql_variant 数据类型的支持

JDBC 驱动程序现在支持要用于 SQL Server 的 `sql_variant` 数据类型。 TVP 和大容量复制等功能也支持 `sql_variant` 数据类型，但具有以下限制：

* **对于日期值**： 

  当使用 TVP 填充包含存储在 `sql_variant` 列中的 `datetime`、`smalldatetime` 或 `date` 值的表时，对结果集调用 `getDateTime()`、`getSmallDateTime()` 或 `getDate()` 方法不起作用并引发以下异常：

  `java java.lang.String cannot be cast to java.sql.Timestamp`
    
  作为一种解决办法，可改为使用 `getString()` 或 `getObject()` 方法。

* **对 null 值结合使用 TVP 和 sql_variant**：
  
  如果使用 TVP 填充一个表，并将 NULL 值发送给 `sql_variant` 列类型，则会引发异常。 当前不支持将 NULL 值插入 TVP 中的列类型 `sql_variant`。

### <a name="implemented-prepared-statement-metadata-caching"></a>实现了预处理语句元数据缓存

JDBC 驱动程序已实现预处理语句元数据缓存以改进性能。 现在驱动程序支持使用 `disableStatementPooling` 和 `statementPoolingCacheSize` 连接属性缓存驱动程序中的预处理语句元数据。 默认情况下，该功能被禁用。 有关详细信息，请参阅 [JDBC 驱动程序的预处理语句元数据缓存](../../connect/jdbc/prepared-statement-metadata-caching-for-the-jdbc-driver.md)。

### <a name="added-support-for-azure-ad-integrated-authentication-on-linuxmac"></a>添加了对 Linux/Mac 上的 Azure AD 集成身份验证的支持

JDBC Driver 现在支持，在所有受支持的操作系统（Windows、Linux 和 Mac）上结合使用 Azure Active Directory (Azure AD) 集成身份验证和 Kerberos。 或者，在 Windows 操作系统上，用户可以使用 sqljdbc_auth.dll 进行身份验证。

### <a name="updated-microsoft-azure-active-directory-authentication-library-adal4j-for-java-version-140"></a>更新了“用于 Java 的 Microsoft Azure Active Directory 身份验证库 (ADAL4J)”版本 1.4.0

JDBC 驱动程序已将“用于 Java 的 Microsoft Azure Active Directory 身份验证库 (ADAL4J)”上的 Maven 依赖项更新为版本 1.4.0。 有关依赖项的详细信息，请参阅 [Microsoft JDBC Driver for SQL Server 的功能依赖项](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md)。

## <a name="62"></a>6.2

Microsoft JDBC Driver 6.2 for SQL Server 完全符合 JDBC 规范 4.1 和 4.2。 根据 Java 版本兼容性命名 6.2 包中的 jar。 例如，建议将 6.2 包中的 mssql-jdbc-6.2.2.jre8.jar 文件与 Java 8 配合使用。

> [!NOTE]  
> 在 2017 年 6 月 29 日发布的 JDBC 6.2 RTW 中发现了元数据缓存改进方面的问题。 改进已回滚，并且新的 jar（版本 6.2.1）已于 2017 年 7 月 17 日发布。 
>
> 另一个改进已将 Azure Key Vault 依赖库版本升级到 1.0.0，并且新的 jar（版本 6.2.2）已于 2017 年 10 月 19 日发布。
>
> 从 [Microsoft 下载中心](https://go.microsoft.com/fwlink/?linkid=852460)、[GitHub](https://github.com/Microsoft/mssql-jdbc/releases/tag/v6.2.2) 和 [Maven Central](https://search.maven.org/search?q=g:com.microsoft.sqlserver) 下载 JDBC Driver 6.2 的最新更新。 请更新项目以使用 6.2.2 版本 jar。 有关详细信息，请查看 [6.2.1](https://github.com/Microsoft/mssql-jdbc/releases/tag/v6.2.1) 和 [6.2.2](https://github.com/Microsoft/mssql-jdbc/releases/tag/v6.2.2) 的发行说明。

### <a name="azure-ad-support-for-linux"></a>适用于 Linux 的 Azure AD 支持

通过用户名/密码和访问令牌方法使用 Azure AD 身份验证将 Linux 应用程序连接到 Azure SQL 数据库。

### <a name="fips-enabled-jvms"></a>已启用 FIPS 的 JVM

JDBC 驱动程序现可在以符合美国联邦信息处理标准 (FIPS) 140 的模式运行的 JVM 上使用，以符合联邦标准。

### <a name="kerberos-authentication-improvements"></a>Kerberos 身份验证改进

JDBC 驱动程序现在具有以下支持：

- Kerberos 配置无法修改或无法检索新令牌或 keytab 的应用程序的主体/密码方法。 此方法可用于对仅允许 Kerberos 身份验证的 SQL Server 实例进行身份验证。
- 跨领域身份验证，方法是使用 Kerberos 集成身份验证，而无需明确设置服务器 SPN。 驱动程序现在会自动计算领域，即使未提供领域也是如此。
- Kerberos 约束委派，方法是通过数据源接受被模拟用户凭据作为 GSS 凭据对象。 然后，此模拟凭据用于建立 Kerberos 连接。

### <a name="added-timeouts"></a>添加了超时

JDBC 驱动程序现在支持以下可配置超时。 可以根据应用程序的需要进行更改。

- 查询超时用于控制在运行查询时发生超时之前等待的秒数。
- 套接字超时用于指定在读取或接受套接字时发生超时之前等待的毫秒数。

## <a name="61"></a>6.1

Microsoft JDBC Driver 6.1 for SQL Server 完全符合 JDBC 规范 4.1 和 4.2。 这是 JDBC 驱动程序的初始开源版本。 其中包含 mssql-jdbc-6.1.0.jre8.jar 和 mssql-jdbc-6.1.0.jre7.jar 文件，它们对应于 Java 版本兼容性。

## <a name="60"></a>6.0

Microsoft JDBC Driver 6.0 for SQL Server 完全符合 JDBC 规范 4.1 和 4.2。 根据 JDBC API 版本兼容性命名 6.0 包中的 jar。 例如，6.0 包中的 sqljdbc42.jar 文件符合 JDBC API 4.2。 同样，sqljdbc41.jar 文件符合 JDBC API 4.1。

若要确保 sqljdbc42.jar 或 sqljdbc41.jar 文件正确，请运行以下代码行。 如果输出是“Driver version: 6.0.7507.100”，则表示具有 JDBC Driver 6.0 包。

```java
Connection conn = DriverManager.getConnection("jdbc:sqlserver://<server>;user=<user>;password=<password>;");
System.out.println("Driver version: " + conn.getMetaData().getDriverVersion());
```

### <a name="always-encrypted"></a>始终加密

驱动程序支持 SQL Server 2016 中的 Always Encrypted 功能。 此功能可确保从不在 SQL Server 实例中以纯文本形式显示敏感数据。 Always Encrypted 工作方式是，以透明方式加密应用程序中的数据，这样 SQL Server 就只会处理已加密数据，而不会处理纯文本值。 即使 SQL Server 实例或主机计算机遭入侵，攻击者也只能获得敏感数据的已加密文本。 有关详细信息，请参阅[对 JDBC 驱动程序使用 Always Encrypted](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md)。

### <a name="internationalized-domain-names"></a>国际化域名

驱动程序支持服务器名称的国际化域名 (IDN)。 有关详细信息，请参阅 [JDBC 驱动程序的国际功能](../../connect/jdbc/international-features-of-the-jdbc-driver.md)一文中的“使用国际域名”。

### <a name="parameterized-queries"></a>参数化查询

驱动程序现在支持，使用已准备的语句为复杂查询（如子查询和/或联接）检索参数元数据。 请注意，此改进仅对 SQL Server 2012 及更高版本有效。

### <a name="azure-active-directory"></a>Azure Active Directory

Azure AD 身份验证是一种使用 Azure AD 标识连接到 Azure SQL 数据库 v12 的机制。 Azure AD 身份验证可用于集中管理数据库用户的标识，并替代 SQL Server 身份验证。 

可使用 JDBC Driver 6.0 指定 JDBC 连接字符串中的 Azure AD 凭据以连接到 Azure SQL 数据库。 有关详细信息，请参阅[设置连接属性](../../connect/jdbc/setting-the-connection-properties.md)一文中的身份验证属性。

### <a name="table-valued-parameters"></a>表值参数

借助 TVP，可以将多行数据从客户端应用程序轻松封送到 SQL Server，而无需进行多次往返或使用特殊的服务器端逻辑来处理数据。 可使用 TVP 来封装客户端应用程序中的数据行，并以一个参数化命令的形式将数据发送到服务器。 传入数据行将存储在随后可使用 Transact-SQL 对其进行操作的表变量中。 有关详细信息，请参阅[使用表值参数](../../connect/jdbc/using-table-valued-parameters.md)。

### <a name="always-on-availability-groups"></a>AlwaysOn 可用性组

驱动程序现在支持透明连接到 AlwaysOn 可用性组。 驱动程序快速发现服务器基础结构的当前 AlwaysOn 拓扑，并以透明方式连接到当前的活动服务器。

## <a name="42"></a>4.2

Microsoft JDBC Driver 4.2 for SQL Server 完全符合 JDBC 规范 4.1 和 4.2。 根据 JDBC API 版本兼容性命名 4.2 包中的 jar。 例如，4.2 包中的 sqljdbc42.jar 文件符合 JDBC API 4.2。 同样，sqljdbc41.jar 文件符合 JDBC API 4.1。

若要确保 sqljdbc42.jar 或 sqljdbc41.jar 文件正确，请运行以下代码行。 如果输出是“Driver version: 4.2.6420.100”，则表示具有 JDBC Driver 4.2 包。

```java
Connection conn = DriverManager.getConnection("jdbc:sqlserver://<server>;user=<user>;password=<password>;");
System.out.println("Driver version: " + conn.getMetaData().getDriverVersion());
```

### <a name="support-for-jdk-8"></a>对 JDK 8 的支持

除了支持 JDK 7.0、6.0 和 5.0 以外，驱动程序还支持 JDK 版本 8.0。

### <a name="jdbc-41-and-42-compliance"></a>JDBC 4.1 和 4.2 的遵从性

除了支持 4.0 以外，驱动程序还支持 Java Database Connectivity API 4.1 和 4.2 规范。 有关详细信息，请参阅 [JDBC 驱动程序的 JDBC 4.1 符合性](../../connect/jdbc/jdbc-4-1-compliance-for-the-jdbc-driver.md)和 [JDBC 驱动程序的 JDBC 4.2 符合性](../../connect/jdbc/jdbc-4-2-compliance-for-the-jdbc-driver.md)。

### <a name="bulk-copy"></a>大容量复制

大容量复制功能可用于将大量数据快速复制到 SQL Server 数据库中的表或视图。 有关详细信息，请参阅[结合使用大容量复制和 JDBC Driver](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md)。

### <a name="xa-transaction-rollback-option"></a>XA 事务回滚选项

驱动程序新增了适用于未准备好事务的现有自动回滚的超时选项。 有关详细信息，请参阅[了解 XA 事务](../../connect/jdbc/understanding-xa-transactions.md)。

### <a name="new-kerberos-principal-connection-property"></a>新 Kerberos 主体连接属性

驱动程序使用新连接属性，提高 Kerberos 连接灵活性。 有关详细信息，请参阅[使用 Kerberos 集成身份验证连接到 SQL Server](../../connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md)。

## <a name="41"></a>4.1

### <a name="support-for-jdk-7"></a>支持 JDK 7

除了支持 JDK 6.0 和 5.0 以外，驱动程序还支持 JDK 版本 7.0。

## <a name="itanium-not-supported-for-jdbc-driver-64-60-42-and-41-applications"></a>JDBC Driver 6.4、6.0、4.2 和 4.1 应用程序不支持 Itanium

不支持适用于 SQL Server 应用程序 的 Microsoft JDBC 驱动程序 6.4、6.0、4.2 和 4.1 在 Itanium 计算机上运行。

## <a name="see-also"></a>另请参阅

[JDBC 驱动程序的概述](../../connect/jdbc/overview-of-the-jdbc-driver.md)
