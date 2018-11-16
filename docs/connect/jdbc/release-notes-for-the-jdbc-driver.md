---
title: JDBC 驱动程序的发行说明 |Microsoft Docs
ms.custom: ''
ms.date: 07/31/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 074f211e-984a-4b76-bb15-ee36f5946f12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f24089803b59e86a4fc8f8b98cd7822a11ba6c2e
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 11/13/2018
ms.locfileid: "51600768"
---
# <a name="release-notes-for-the-jdbc-driver"></a>JDBC 驱动程序的发行说明

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

## <a name="updates-in-microsoft-jdbc-driver-70-for-sql-server"></a>Microsoft JDBC Driver 7.0 for SQL Server 更新

SQL Server 的 Microsoft JDBC 驱动程序 7.0 是完全符合 JDBC API 规范 4.2。 Java 版本兼容性根据命名 7.0 包中的 jar。 例如，从 7.0 包 mssql jdbc 7.0.0.jre10.jar 文件应与 Java 10。

### <a name="support-for-jdk-10"></a>支持 JDK 10

SQL Server 的 Microsoft JDBC 驱动程序 7.0 现与 Java 开发工具包 (JDK) 版本 10.0 除了 JDK 1.8 兼容。 此更新还公开驱动程序的自动-Module-Name 作为`com.microsoft.sqlserver.jdbc`通过其清单文件。

### <a name="support-for-spatial-datatypes"></a>支持空间数据类型

SQL Server 的 Microsoft JDBC 驱动程序 7.0 现在提供对 SQL Server 空间数据类型 'Geography' 和 Geometry 支持。 有关空间数据类型的 Api 以及如何使用它们的详细信息，请参阅[此处](../../connect/jdbc/use-spatial-datatypes.md)。

### <a name="implementation-for-jdbc-43-introduced-javasqlconnection-apis-beginrequest-and-endrequest"></a>JDBC 4.3 实现引入了 java.sql.Connection API beginRequest() 和 endRequest()

SQL Server 现在实现 Microsoft JDBC 驱动程序 7.0`beginRequest()`并`endRequest()`Api 从`java.sql.Connection`类。 这些 Api 引入了 JDBC 4.3 规范和 JDK 9。 有关这些 Api 的驱动程序的实现详细信息，请参阅[此处](../../connect/jdbc/jdbc-4-3-compliance-for-the-jdbc-driver.md)。

### <a name="support-for-sql-data-discovery-and-classification"></a>支持“SQL 数据发现和分类”

SQL Server 的 Microsoft JDBC 驱动程序 7.0 与任何支持此功能的目标数据库的 SQL 数据发现和分类功能提供支持。 该驱动程序现在公开`SQLServerResultSet.getSensitivityClassification()`Api，以从提取结果集中提取此信息。

有关如何通过 JDBC 驱动程序使用此功能的详细信息，请参阅示例[此处](../../connect/jdbc/data-discovery-classification-sample.md)。

### <a name="added-new-connection-property-usebulkcopyforbatchinsert"></a>添加新的连接属性： useBulkCopyForBatchInsert

SQL Server 的 Microsoft JDBC 驱动程序 7.0 引入了新的连接属性 useBulkCopyForBatchInsert，仅支持**Azure 数据仓库**。

此属性是**禁用**的默认值，并且可以启用推送大相当于 Azure 数据仓库的数据时提高用户应用程序的性能。 启用此属性更改的批处理插入操作，以与用户提供的数据切换到大容量复制操作的行为。 有关此属性，其自身的局限性的详细信息，请参阅[此处](../../connect/jdbc/use-bulk-copy-api-batch-insert-operation.md)。

### <a name="added-new-connection-property-cancelquerytimeout"></a>添加新的连接属性： cancelQueryTimeout

SQL Server 的 Microsoft JDBC 驱动程序 7.0 引入了新的连接属性`cancelQueryTimeout`，以取消`queryTimeout`上`java.sql.Connection`和`java.sql.Statement`对象。

### <a name="added-azure-key-vault-provider-constructors"></a>添加了 Azure 密钥保管库提供程序构造函数

SQL Server 的 Microsoft JDBC 驱动程序 7.0 重新引入了先前删除的构造函数，用于`SQLServerColumnEncryptionAzureKeyVaultProvider`，通过实施的自定义方法的允许的身份验证`SQLServerKeyVaultAuthenticationCallback`提取访问令牌。

新的构造函数具有以下定义：

```java
/* This constructor is added to provide backwards compatibility with 6.0
* version of the driver. It is marked deprecated for removal in next
* stable release.
*/
@Deprecated
public SQLServerColumnEncryptionAzureKeyVaultProvider(
        SQLServerKeyVaultAuthenticationCallback authenticationCallback,
        ExecutorService executorService) throws SQLServerException;

/*New Constructor to replace the above constructor*/
public SQLServerColumnEncryptionAzureKeyVaultProvider(
            SQLServerKeyVaultAuthenticationCallback authenticationCallback) throws SQLServerException;
```

### <a name="updated-adal4j-version-to-160"></a>更新到 1.6.0 ADAL4J 版本

Microsoft JDBC 驱动程序 7.0 SQL Server 的已更新为版本 1.6.0 时 azure 与 active directory-库-用于-java (ADAL4J) 其 maven 依赖项。 有关依赖项的详细信息，请参阅[此处](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md)。

## <a name="updates-in-microsoft-jdbc-driver-64-for-sql-server"></a>Microsoft JDBC Driver 6.4 for SQL Server 中的更新

Microsoft JDBC Driver 6.4 for SQL Server 是完全符合 JDBC 规范 4.1 和 4.2。 Java 版本兼容性根据命名 6.4 包中的 jar。 例如，从 6.4 包 mssql jdbc 6.4.0.jre8.jar 文件必须使用与 Java 8。

### <a name="support-for-jdk-9"></a>支持 JDK 9

除 JDK 8.0 和 7.0 外，还支持 Java 开发工具包 (JDK) 版本 9.0。

### <a name="jdbc-43-compliance"></a>JDBC 4.3 符合性

除支持 4.1 和 4.2 外，还支持 Java Database Connectivity API 4.3 规范。 JDBC 4.3 API 方法是添加但尚未实现。 有关详细信息，请参阅 [JDBC 驱动程序的 JDBC 4.3 符合性](../../connect/jdbc/jdbc-4-3-compliance-for-the-jdbc-driver.md)。

### <a name="added-new-connection-property-sslprotocol"></a>添加新的连接属性： sslProtocol

添加了允许用户指定 TLS 协议关键字的连接属性。 可能的值为:"TLS"、"TLSv1"、"TLSv1.1"、"TLSv1.2"。 请参阅[SSLProtocol](https://github.com/Microsoft/mssql-jdbc/wiki/SSLProtocol)有关详细信息。

### <a name="deprecated-connection-property-fipsprovider"></a>不推荐使用连接属性： fipsProvider

从接受的连接属性的列表中删除连接属性"fipsProvider"。 查看详细信息[此处](https://github.com/Microsoft/mssql-jdbc/pull/460)。

### <a name="added-connection-properties-for-specifying-custom-trustmanager"></a>已添加的连接属性，用于指定自定义 TrustManager

驱动程序现在支持使用添加了"trustManagerClass"和"trustManagerConstructorArg"连接属性。 这允许动态指定一组基于每个连接而无需修改 JVM 环境的全局设置受信任的证书。

### <a name="added-support-for-datetimesmalldatetime-in-table-valued-parameters-tvp"></a>添加了的对 datetime/smalldatetime 类型在表值参数 (TVP)

现在，驱动程序在使用表值参数 (TVP) 时支持数据类型 DATETIME 和 SMALLDATETIME。

### <a name="added-support-for-sqlvariant-datatype"></a>添加了对 sql_variant 数据类型支持

JDBC 驱动程序现在支持 sql_variant 数据类型与 SQL Server 一起使用。 Sql_variant 还支持与功能，如表值参数 (TVP) 和 BulkCopy 具有以下限制：

1. 对于日期值： 时使用 TVP 填充包含 sql_variant 列中存储的 datetime/smalldatetime/date 值的表，在结果集上调用 getDateTime()/getSmallDateTime()/getDate() 方法不起作用并引发以下异常： `java java.lang.String cannot be cast to java.sql.Timestamp`
    解决方法：改为使用“getString()”或“getObject()”方法。

2. 对于 null 值，结合使用 TVP 与 SQL 变量

如果使用 TVP 填充一个表并将 NULL 值发送给 sql_variant 列类型，您会遇到异常，因为当前不支持对 TVP 中的列类型 sql_variant 插入 NULL 值。

### <a name="implemented-prepared-statement-metadata-caching"></a>实现已准备的语句元数据缓存

JDBC 驱动程序已实现准备语句元数据缓存，以改进性能。 驱动程序现在支持在驱动程序中使用"disableStatementPooling"和"statementPoolingCacheSize"连接属性的缓存准备语句元数据。 默认情况下，该功能被禁用。 可在[此处](../../connect/jdbc/prepared-statement-metadata-caching-for-the-jdbc-driver.md)找到详细信息。

### <a name="added-support-for-aad-integrated-authentication-on-linuxmac"></a>添加了对 AAD 在 Linux/Mac 上的集成身份验证支持

JDBC 驱动程序现在还支持通过 Kerberos 在所有支持的操作系统 (Windows/Linux/Mac) 上进行 Azure Active Directory 集成身份验证。 或者，Windows 操作系统上，用户可以使用身份验证 sqljdbc_auth.dll。

### <a name="updated-adal4j-version-to-140"></a>更新的 ADAL4J 版本为 1.4.0

JDBC 驱动程序已更新为版本 1.4.0 其 maven 依赖于 azure 的与 active directory-库-用于-java (ADAL4J)。 有关依赖关系的详细信息，请参阅[此处](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md)

## <a name="updates-in-microsoft-jdbc-driver-62-for-sql-server"></a>Microsoft JDBC Driver 6.2 for SQL Server 中的更新

Microsoft JDBC Driver 6.2 for SQL Server 是完全符合 JDBC 规范 4.1 和 4.2。 Java 版本兼容性根据命名 6.2 包中的 jar。 例如，从 6.2 包 mssql jdbc 6.2.2.jre8.jar 文件被建议用于 Java 8。

> [!NOTE]  
> 2017 年 6 月 29 日发布的 JDBC 6.2 RTW 中找到的元数据缓存改进出现问题。 改进已回滚，并且新的 jar （版本 6.2.1） 已于 2017 年 7 月 17 日发布。 
>
> Azure 密钥保管库依赖库版本升级到 1.0.0 的另一个改进进行，并且新 jar （版本 6.2.2） 已于 2017 年 10 月 19 日发布。
>
> 在下载最新的更新在 JDBC Driver 6.2 [Microsoft 下载中心](https://go.microsoft.com/fwlink/?linkid=852460)， [GitHub](https://github.com/Microsoft/mssql-jdbc/releases/tag/v6.2.2)，并[Maven 中央](https://search.maven.org/#search%7Cgav%7C1%7Cg%3A%22com.microsoft.sqlserver%22%20AND%20a%3A%22mssql-jdbc%22)。 请更新项目以使用 6.2.2 发布 jar。 请查看发行说明[v6.2.1](https://github.com/Microsoft/mssql-jdbc/releases/tag/v6.2.1)并[v6.2.2](https://github.com/Microsoft/mssql-jdbc/releases/tag/v6.2.2)的更多详细信息。

### <a name="azure-active-directory-aad-support-for-linux"></a>适用于 Linux 的 azure Active Directory (AAD) 支持

在 Linux 应用程序连接到 Azure SQL 数据库使用 AAD 身份验证通过用户名/密码和访问令牌的方法。

### <a name="federal-information-processing-standard-fips-enabled-jvms"></a>联邦信息处理标准 (FIPS) 启用 Jvm

JDBC 驱动程序现在可在运行以 FIPS 140 兼容模式，以满足联邦标准和法规遵从性的 Jvm 上。

### <a name="kerberos-authentication-improvements"></a>Kerberos 身份验证的改进

JDBC 驱动程序现在具有对支持：

- 其中 Kerberos 配置不能为已修改或无法检索新令牌或 keytab 的应用程序的主体/密码方法。 此方法可用于仅允许 Kerberos 身份验证的 SQL server 进行身份验证。
- 跨领域身份验证使用 Kerberos 集成身份验证，而无需显式设置服务器 SPN。 该驱动程序现在会自动计算领域即使它未对其提供。
- 通过接受 Kerberos 约束委派模拟用户凭据作为通过数据源的 GSS 凭据对象。 此模拟的凭据然后用于建立 Kerberos 连接。

### <a name="added-timeouts"></a>添加了的超时

JDBC 驱动程序现在支持以下可配置超时值可以更改基于应用程序的需求：

- 若要控制运行查询时发生超时之前等待的秒数的查询超时值。
- 若要指定要在套接字上发生超时之前等待的毫秒数读取，或接受的套接字超时。

## <a name="updates-in-microsoft-jdbc-driver-61-for-sql-server"></a>Microsoft JDBC Driver 6.1 for SQL Server 中的更新

SQL Server 的 Microsoft JDBC 驱动程序 6.1 是完全符合 JDBC 规范 4.1 和 4.2。 这是初始的开源版本的 JDBC 驱动程序，其中包含 mssql jdbc 6.1.0.jre8.jar mssql jdbc 6.1.0.jre7.jar 文件，它们分别对应于 Java 版本兼容性。

## <a name="updates-in-microsoft-jdbc-driver-60-for-sql-server"></a>Microsoft JDBC Driver 6.0 for SQL Server 中的更新

Microsoft JDBC Driver 6.0 for SQL Server 是完全符合 JDBC 规范 4.1 和 4.2。 根据其符合性的 JDBC API 版本命名的 jar，6.0 程序包中。 例如，6.0 程序包中的 sqljdbc42.jar 文件与 JDBC API 4.2 兼容。 同样，sqljdbc41.jar 文件与 JDBC 4.1 API 兼容。

若要确保具有正确 sqljdbc42.jar 或 sqljdbc41.jar，运行以下代码行。 如果输出是"驱动程序版本： 6.0.7507.100"，你具有 JDBC Driver 6.0 包。

```java
Connection conn = DriverManager.getConnection("jdbc:sqlserver://<server>;user=<user>;password=<password>;");
System.out.println("Driver version: " + conn.getMetaData().getDriverVersion());
```

### <a name="always-encrypted"></a>始终加密

支持 SQL Server 2016 中最近发布的 Always Encrypted 功能，该功能是确保敏感数据决不会在 SQL Server 实例中以纯文本形式被看到的全新安全功能。 始终加密工作方式是以透明方式加密应用程序中的数据，从而使 SQL Server 将只处理加密数据而非纯文本值。 即使 SQL 实例或主机计算机遭到破坏，攻击者也只能获得敏感数据的加密文本。 有关详细信息，请参阅[对 JDBC 驱动程序使用 Always Encrypted](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md)。

### <a name="internationalized-domain-name-idn"></a>国际化域名 (IDN)

支持服务器名称的国际化域名 (IDN)。 有关详细信息，请参阅上使用国际域名[JDBC 驱动程序的国际化功能](../../connect/jdbc/international-features-of-the-jdbc-driver.md)页。

### <a name="parameterized-query"></a>参数化查询

现在支持针对复杂查询（如子查询和/或联接）用预定义语句检索参数元数据。 请注意此改进仅在使用 SQL Server 2012 和更新版本时才可用。

### <a name="azure-active-directory-aad"></a>Azure Active Directory (AAD)

AAD 身份验证是一种连接到 Azure SQL 数据库 v12 的机制在 AAD 中使用的标识。 使用 AAD 身份验证以集中管理数据库用户的标识且作为 SQL Server 身份验证的一种替代方法使用。 可通过 JDBC Driver 6.0 指定 JDBC 连接字符串中的 AAD 凭据以连接到 Azure SQL DB。 有关详细信息，请参阅上的身份验证属性[连接属性设置](../../connect/jdbc/setting-the-connection-properties.md)页。

### <a name="table-valued-parameters"></a>表值参数

表值参数提供了一将多行数据从客户端应用程序封送到 SQL Server 的种简单方法，而无需进行多次往返或特殊的服务器端逻辑来处理数据。 可使用表值参数来封装客户端应用程序中的数据行，并以单个参数化命令将数据发送到服务器。 然后可以操作通过使用 TRANSACT-SQL 在表变量中存储传入的数据行。 有关详细信息，请参阅[Using Table-Valued 参数](../../connect/jdbc/using-table-valued-parameters.md)。

### <a name="alwayson-availability-groups-ag"></a>AlwaysOn 可用性组 (AG)

该驱动程序现在支持透明连接到 AlwaysOn 可用性组。 驱动程序快速发现服务器基础结构的当前 AlwaysOn 拓扑，并以透明的方式连接到当前的活动服务器。

## <a name="updates-in-microsoft-jdbc-driver-42-for-sql-server-and-later"></a>Microsoft JDBC Driver 4.2 for SQL Server 及更高版本中的更新

Microsoft JDBC Driver 4.2 for SQL Server 是完全符合 JDBC 规范 4.1 和 4.2。 根据其符合性的 JDBC API 版本命名 4.2 程序包中的 jar。 例如，从 4.2 程序包 sqljdbc42.jar 文件与 JDBC API 4.2 兼容。 同样，sqljdbc41.jar 文件与 JDBC 4.1 API 兼容。

若要确保具有正确 sqljdbc42.jar 或 sqljdbc41.jar，运行以下代码行。 如果输出是"驱动程序版本： 4.2.6420.100"，你具有 JDBC Driver 4.2 包。

```java
Connection conn = DriverManager.getConnection("jdbc:sqlserver://<server>;user=<user>;password=<password>;");
System.out.println("Driver version: " + conn.getMetaData().getDriverVersion());
```

### <a name="support-for-jdk-8"></a>支持 JDK 8

除 JDK 7.0、6.0 和 5.0 外，还支持 Java 开发工具包 (JDK) 8.0 版。

### <a name="jdbc-41-and-42-compliance"></a>JDBC 4.1 和 4.2 的遵从性

对 Java Database Connectivity API 4.1 和 4.2 规范以及 4.0 的支持。 有关详细信息，请参阅[JDBC 驱动程序的 JDBC 4.1 合规性](../../connect/jdbc/jdbc-4-1-compliance-for-the-jdbc-driver.md)并[JDBC 驱动程序的 JDBC 4.2 合规性](../../connect/jdbc/jdbc-4-2-compliance-for-the-jdbc-driver.md)。

### <a name="bulk-copy"></a>大容量复制

大容量复制功能用于将大量数据快速复制到 SQL Server 数据库的表或视图中。 请参阅[通过 JDBC 驱动程序使用大容量复制](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md)。

### <a name="xa-transaction-rollback-option"></a>XA 事务回滚选项

为现有自动回滚尚未准备好的事务新增了超时选项。 有关详细信息，请参阅[了解 XA 事务](../../connect/jdbc/understanding-xa-transactions.md)。

### <a name="new-kerberos-principal-connection-property"></a>新的 Kerberos 主体连接属性

新增了连接属性，以便增强与 Kerberos 连接的灵活性。 有关详细信息，请参阅[使用 Kerberos 集成身份验证连接到 SQL Server](../../connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md)。

## <a name="updates-in-microsoft-jdbc-driver-41-for-sql-server-and-later"></a>Microsoft JDBC Driver 4.2 for SQL Server 及更高版本中的更新

### <a name="support-for-jdk-7"></a>支持 JDK 7

除 JDK 6.0 和 5.0 外，还支持 Java 开发工具包 (JDK) 版本 7.0。

## <a name="itanium-not-supported-for-jdbc-driver-64-60-42-and-41-applications"></a>Itanium 不支持 JDBC Driver 6.4、6.0、4.2 和 4.1 应用程序

不支持适用于 SQL Server 应用程序 的 Microsoft JDBC 驱动程序 6.4、6.0、4.2 和 4.1 在 Itanium 计算机上运行。

## <a name="see-also"></a>另请参阅

[JDBC 驱动程序的概述](../../connect/jdbc/overview-of-the-jdbc-driver.md)
