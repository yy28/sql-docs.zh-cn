---
title: JDBC 驱动程序的发行说明 |Microsoft Docs
ms.custom: ''
ms.date: 01/29/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 074f211e-984a-4b76-bb15-ee36f5946f12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4b7f863c7534421fa6e091e793297b4be3f73542
ms.sourcegitcommit: 879a5c6eca99e0e9cc946c653d4ced165905d9c6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/05/2019
ms.locfileid: "55737058"
---
# <a name="release-notes-for-the-jdbc-driver"></a>JDBC Driver 发行说明

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

## <a name="updates-in-microsoft-jdbc-driver-72-for-sql-server"></a>Microsoft JDBC Driver 7.2 for SQL Server 中的更新

适用于 SQL Server 的 Microsoft JDBC 驱动程序 7.2 是完全符合 JDBC API 规范 4.2。 Java 版本兼容性根据命名 7.2 包中的 jar。 例如，mssql jdbc 7.2.0.jre11.jar 文件从 7.2 包应使用与 Java 11 配合使用。

### <a name="support-for-jdk-11"></a>对 JDK 11 的支持

适用于 SQL Server 的 Microsoft JDBC 驱动程序 7.2 目前使用 Java 开发工具包 (JDK) 版本 11.0 除了 JDK 1.8 兼容。

### <a name="support-for-active-directory-managed-service-identity-msi-authentication"></a>支持 Active Directory 托管服务标识 (MSI) 身份验证

适用于 SQL Server 的 Microsoft JDBC 驱动程序 7.2 现在支持 Active Directory 托管服务标识 (MSI) 身份验证模式。 这种模式的身份验证是适用于 Azure 资源启用了"Identity"功能的支持。 若要获取驱动程序支持这两种类型的托管系统标识 (MSI) **accessToken**建立安全连接。

更多详细信息和示例应用程序使用此身份验证模式可在此处找到：[使用 Azure Active Directory 身份验证连接](../../connect/jdbc/connecting-using-azure-active-directory-authentication.md)

### <a name="osgi-support"></a>OSGi 支持

适用于 SQL Server 的 Microsoft JDBC 驱动程序 7.2 引入到驱动程序通过以下实现添加了 OSGi 支持`org.osgi.service.jdbc.DataSourceFactory`和`org.osgi.framework.BundleActivator`:

- `com.microsoft.sqlserver.jdbc.osgi.SQLServerDataSourceFactory`
- `com.microsoft.sqlserver.jdbc.osgi.Activator`

### <a name="sqlservererror-apis"></a>SQLServerError Api

引入了适用于 SQL Server 的 Microsoft JDBC 驱动程序 7.2`SQLServerException.getSQLServerError()`和`SQLServerError`getter Api 以检索有关从服务器所生成错误的其他详细信息。 有关详细信息，请参阅[消除错误](../../connect/jdbc/handling-errors.md)。

### <a name="updated-microsoft-azure-active-directory-authentication-library-adal4j-for-java-version-163"></a>更新了“用于 Java 的 Microsoft Azure Active Directory 身份验证库 (ADAL4J)”版本 1.6.3

适用于 SQL Server 的 Microsoft JDBC 驱动程序 7.2 已更新 Maven 依赖于"Microsoft Azure Active Directory 身份验证库 (ADAL4J) 适用于 Java"到版本 1.6.3，它还引入了"Java 客户端运行时为 AutoRest"作为 Maven 依赖项 (版本：1.6.5）。 有关依赖关系的详细信息，请参阅[适用于 SQL Server 功能的 Microsoft JDBC 驱动程序的依赖关系](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md)。

### <a name="updated-microsoft-azure-key-vault-sdk-for-java-version-120"></a>更新后的"Microsoft Azure 密钥保管库 SDK 的 Java"版本：1.2.0

适用于 SQL Server 的 Microsoft JDBC 驱动程序 7.2 已更新 Maven 依赖于"Microsoft Azure 密钥保管库 SDK 的 Java"到版本 1.2.0，它还引入了"Microsoft Azure SDK 为密钥保管库 WebKey"作为 Maven 依赖项 (版本：1.2.0）。 有关依赖关系的详细信息，请参阅[适用于 SQL Server 功能的 Microsoft JDBC 驱动程序的依赖关系](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md)。

### <a name="known-issues"></a>已知问题

使用 SQL Server 的 Microsoft JDBC 驱动程序 7.2，某些参数化查询存在一个已知的问题。 将很快发布 7.2 版 (v7.2.1) 的更新，若要解决此问题。


## <a name="updates-in-microsoft-jdbc-driver-70-for-sql-server"></a>Microsoft JDBC Driver 7.0 for SQL Server 更新

适用于 SQL Server 的 Microsoft JDBC 驱动程序 7.0 是完全符合 JDBC API 规范 4.2。 Java 版本兼容性根据命名 7.0 包中的 jar。 例如，从 7.0 包 mssql jdbc 7.0.0.jre10.jar 文件应与 Java 10。

### <a name="support-for-jdk-10"></a>支持 JDK 10

适用于 SQL Server 的 Microsoft JDBC 驱动程序 7.0 现与 Java 开发工具包 (JDK) 版本 10.0 除了 JDK 1.8 兼容。 此更新还公开的驱动程序`Automatic-Module-Name`作为`com.microsoft.sqlserver.jdbc`通过其清单文件。

### <a name="support-for-spatial-datatypes"></a>支持空间数据类型

适用于 SQL Server 的 Microsoft JDBC 驱动程序 7.0 现在提供对 SQL Server 空间数据类型 Geography 和 Geometry 的支持。 有关空间数据类型的 Api 以及如何使用它们的详细信息，请参阅[使用空间数据类型](../../connect/jdbc/use-spatial-datatypes.md)。

### <a name="implementation-for-jdbc-43-introduced-javasqlconnection-apis-beginrequest-and-endrequest"></a>JDBC 4.3 实现引入了 java.sql.Connection API beginRequest() 和 endRequest()

有关 SQL Server 现在实现的 Microsoft JDBC 驱动程序 7.0`beginRequest()`并`endRequest()`Api 从`java.sql.Connection`类。 这些 Api 引入了 JDBC 4.3 规范和 JDK 9。 有关这些 Api 的驱动程序的实现详细信息，请参阅[JDBC 驱动程序的 JDBC 4.3 符合性](../../connect/jdbc/jdbc-4-3-compliance-for-the-jdbc-driver.md)。

### <a name="support-for-sql-data-discovery-and-classification"></a>支持“SQL 数据发现和分类”

适用于 SQL Server 的 Microsoft JDBC 驱动程序 7.0 为 SQL 数据发现和使用支持此功能的任何目标数据库的分类提供支持。 该驱动程序现在公开`SQLServerResultSet.getSensitivityClassification()`Api 来提取中提取此信息`ResultSet`。

有关如何通过 JDBC 驱动程序使用此功能的详细信息，请参阅中的示例[SQL 数据发现和分类](../../connect/jdbc/data-discovery-classification-sample.md)。

### <a name="added-connection-property-usebulkcopyforbatchinsert"></a>添加了连接属性： useBulkCopyForBatchInsert

适用于 SQL Server 的 Microsoft JDBC 驱动程序 7.0 引入了新的连接属性， `useBulkCopyForBatchInsert`。 此属性仅支持 Azure SQL 数据仓库。

默认情况下禁用此属性。 您可以启用它以提高用户应用程序的性能时要将大量数据推送到 Azure SQL 数据仓库。 启用此属性将更改批插入操作，以切换到与用户提供的数据大容量复制操作的行为。 有关此属性，其自身的局限性的详细信息，请参阅[批处理中使用大容量复制 API 插入操作](../../connect/jdbc/use-bulk-copy-api-batch-insert-operation.md)。

### <a name="added-connection-property-cancelquerytimeout"></a>添加了连接属性： cancelQueryTimeout

适用于 SQL Server 的 Microsoft JDBC 驱动程序 7.0 引入了新的连接属性`cancelQueryTimeout`，以取消`queryTimeout`上`java.sql.Connection`和`java.sql.Statement`对象。

### <a name="added-azure-key-vault-provider-constructors"></a>添加了的 Azure 密钥保管库提供程序构造函数

适用于 SQL Server 的 Microsoft JDBC 驱动程序 7.0 重新引入了先前删除的构造函数，为`SQLServerColumnEncryptionAzureKeyVaultProvider`。 它允许通过自定义方法实现通过身份验证`SQLServerKeyVaultAuthenticationCallback`提取访问令牌。

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

适用于 SQL Server 的 Microsoft JDBC 驱动程序 7.0 已更新为版本 1.6.0 Maven 依赖于"Microsoft Azure Active Directory 身份验证库 (ADAL4J) 适用于 Java"。 有关依赖关系的详细信息，请参阅[适用于 SQL Server 功能的 Microsoft JDBC 驱动程序的依赖关系](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md)。

## <a name="updates-in-microsoft-jdbc-driver-64-for-sql-server"></a>Microsoft JDBC Driver 6.4 for SQL Server 中的更新

Microsoft JDBC Driver 6.4 for SQL Server 是完全符合 JDBC 规范 4.1 和 4.2。 Java 版本兼容性根据命名 6.4 包中的 jar。 例如，从 6.4 包 mssql jdbc 6.4.0.jre8.jar 文件必须使用与 Java 8。

### <a name="support-for-jdk-9"></a>支持 JDK 9

该驱动程序支持 JDK 9.0 版除了 JDK 8.0 和 7.0。

### <a name="jdbc-43-compliance"></a>JDBC 4.3 符合性

除了支持 4.1 和 4.2 以外，驱动程序还支持 Java Database Connectivity API 4.3 规范。 JDBC 4.3 API 方法是添加但尚未实现。 有关详细信息，请参阅 [JDBC Driver 的 JDBC 4.3 合规性](../../connect/jdbc/jdbc-4-3-compliance-for-the-jdbc-driver.md)。

### <a name="added-connection-property-sslprotocol"></a>添加了连接属性： sslProtocol

新的连接属性允许用户指定 TLS 协议关键字。 可能的值有："TLS"、"TLSv1"、"TLSv1.1"和"TLSv1.2"。 有关详细信息，请参阅[SSLProtocol](https://github.com/Microsoft/mssql-jdbc/wiki/SSLProtocol)。

### <a name="deprecated-connection-property-fipsprovider"></a>不推荐使用连接属性： fipsProvider

连接属性`fipsProvider`从接受的连接属性的列表中删除。 有关详细信息，请参阅相关[GitHub 拉取请求](https://github.com/Microsoft/mssql-jdbc/pull/460)。

### <a name="added-connection-properties-for-specifying-a-custom-trustmanager"></a>已添加的连接属性，用于指定自定义 TrustManager

驱动程序现在支持指定的自定义 TrustManager 添加`trustManagerClass`和`trustManagerConstructorArg`连接属性。 动态可在每个连接基础上指定一的组受信任的证书，而无需修改 Java 虚拟机 (JVM) 环境的全局设置。

### <a name="added-support-for-datetimesmalldatetime-in-table-valued-parameters"></a>添加了对表值参数中的 datetime/smalldatetime 类型支持

该驱动程序现在支持数据类型`datetime`和`smallDatetime`当使用表值参数 (Tvp)。

### <a name="added-support-for-the-sqlvariant-datatype"></a>添加了对 sql_variant 数据类型支持

JDBC 驱动程序现在支持`sql_variant`数据类型与 SQL Server 一起使用。 `sql_variant`数据类型也支持功能，例如 Tvp 和大容量复制具有以下限制：

* **对于日期值**： 

  当使用 TVP 填充一个表，包含该表`datetime`， `smalldatetime`，或`date`中存储的值`sql_variant`列中，调用`getDateTime()`， `getSmallDateTime()`，或`getDate()`对结果集的方法不起作用，引发以下异常：

  `java java.lang.String cannot be cast to java.sql.Timestamp`
    
  作为一种解决方法，使用`getString()`或`getObject()`方法相反。

* **对 null 值结合使用 TVP 和 sql_variant**：
  
  如果使用 TVP 填充一个表并将发送到的 NULL 值`sql_variant`列类型，您会遇到异常。 将 NULL 值插入列类型与`sql_variant`在 tvp 的形式当前不支持。

### <a name="implemented-prepared-statement-metadata-caching"></a>实现已准备的语句元数据缓存

JDBC 驱动程序已实现了已准备的语句元数据缓存以改进性能。 该驱动程序现在支持缓存已准备的语句中使用的驱动程序的元数据`disableStatementPooling`和`statementPoolingCacheSize`连接属性。 默认情况下，该功能被禁用。 有关详细信息，请参阅[准备好 JDBC 驱动程序的语句元数据缓存](../../connect/jdbc/prepared-statement-metadata-caching-for-the-jdbc-driver.md)。

### <a name="added-support-for-azure-ad-integrated-authentication-on-linuxmac"></a>添加了对 Azure AD 集成身份验证在 Linux/Mac 上支持

JDBC Driver 现在支持，在所有受支持的操作系统（Windows、Linux 和 Mac）上结合使用 Azure Active Directory (Azure AD) 集成身份验证和 Kerberos。 或者，在 Windows 操作系统中，用户可以使用身份验证 sqljdbc_auth.dll。

### <a name="updated-microsoft-azure-active-directory-authentication-library-adal4j-for-java-version-140"></a>更新了“用于 Java 的 Microsoft Azure Active Directory 身份验证库 (ADAL4J)”版本 1.4.0

JDBC 驱动程序已更新为版本 1.4.0 Maven 依赖于"Microsoft Azure Active Directory 身份验证库 (ADAL4J) 适用于 Java"。 有关依赖关系的详细信息，请参阅[适用于 SQL Server 功能的 Microsoft JDBC 驱动程序的依赖关系](../../connect/jdbc/feature-dependencies-of-microsoft-jdbc-driver-for-sql-server.md)。

## <a name="updates-in-microsoft-jdbc-driver-62-for-sql-server"></a>Microsoft JDBC Driver 6.2 for SQL Server 中的更新

Microsoft JDBC Driver 6.2 for SQL Server 是完全符合 JDBC 规范 4.1 和 4.2。 Java 版本兼容性根据命名 6.2 包中的 jar。 例如，从 6.2 包 mssql jdbc 6.2.2.jre8.jar 文件被建议用于 Java 8。

> [!NOTE]  
> 2017 年 6 月 29 日发布的 JDBC 6.2 RTW 中找到的元数据缓存改进出现问题。 改进已回滚，并且新的 jar （版本 6.2.1） 已于 2017 年 7 月 17 日发布。 
>
> 另一个改进升级到 1.0.0，Azure 密钥保管库依赖的库版本和新的 jar （版本 6.2.2） 已于 2017 年 10 月 19 日发布。
>
> 下载最新的更新适用于从 JDBC Driver 6.2 [Microsoft 下载中心](https://go.microsoft.com/fwlink/?linkid=852460)， [GitHub](https://github.com/Microsoft/mssql-jdbc/releases/tag/v6.2.2)，并[Maven 中央](https://search.maven.org/#search%7Cgav%7C1%7Cg%3A%22com.microsoft.sqlserver%22%20AND%20a%3A%22mssql-jdbc%22)。 请更新项目以使用 6.2.2 发布 jar。 有关详细信息，查看发行说明[6.2.1](https://github.com/Microsoft/mssql-jdbc/releases/tag/v6.2.1)并[6.2.2](https://github.com/Microsoft/mssql-jdbc/releases/tag/v6.2.2)。

### <a name="azure-ad-support-for-linux"></a>适用于 Linux 的 azure AD 支持

使用通过用户名/密码和访问令牌方法的 Azure AD 身份验证连接到 Azure SQL 数据库 Linux 应用程序。

### <a name="fips-enabled-jvms"></a>已启用 FIPS 的 Jvm

JDBC 驱动程序现在可在运行以联邦信息处理标准 (FIPS) 140 兼容模式，以满足美国联邦符合性标准的 Jvm 上。

### <a name="kerberos-authentication-improvements"></a>Kerberos 身份验证的改进

JDBC 驱动程序现在具有对支持：

- 其中 Kerberos 配置不能修改或无法检索新令牌或者 keytab 的应用程序的主体/密码方法。 此方法可用于向 SQL Server 实例允许仅 Kerberos 身份验证进行身份验证。
- 使用 Kerberos 集成身份验证，而无需显式设置服务器 SPN 的跨领域身份验证。 该驱动程序现在会自动计算领域甚至时未提供。
- 通过接受 Kerberos 约束委派模拟用户凭据作为通过数据源的 GSS 凭据对象。 此模拟的凭据然后用于建立 Kerberos 连接。

### <a name="added-timeouts"></a>添加了的超时

JDBC 驱动程序现在支持以下可配置超时。 可以根据应用程序的需要进行更改。

- 若要控制运行查询时，会发生超时之前要等待的秒数的查询超时值。
- 若要指定要在套接字上发生超时之前等待的毫秒数读取，或接受的套接字超时。

## <a name="updates-in-microsoft-jdbc-driver-61-for-sql-server"></a>Microsoft JDBC Driver 6.1 for SQL Server 中的更新

适用于 SQL Server 的 Microsoft JDBC 驱动程序 6.1 是完全符合 JDBC 规范 4.1 和 4.2。 这是初始的开源版本的 JDBC 驱动程序。 它包含 mssql jdbc 6.1.0.jre8.jar 和 mssql jdbc 6.1.0.jre7.jar 文件，它们分别对应于 Java 的版本兼容性。

## <a name="updates-in-microsoft-jdbc-driver-60-for-sql-server"></a>Microsoft JDBC Driver 6.0 for SQL Server 中的更新

Microsoft JDBC Driver 6.0 for SQL Server 是完全符合 JDBC 规范 4.1 和 4.2。 根据其符合性的 JDBC API 版本命名的 jar，6.0 程序包中。 例如，6.0 程序包中的 sqljdbc42.jar 文件与 JDBC API 4.2 兼容。 同样，sqljdbc41.jar 文件与 JDBC 4.1 API 兼容。

若要确保具有正确 sqljdbc42.jar 或 sqljdbc41.jar 文件，运行以下代码行。 如果输出是"驱动程序版本：6.0.7507.100"，你具有 JDBC Driver 6.0 包。

```java
Connection conn = DriverManager.getConnection("jdbc:sqlserver://<server>;user=<user>;password=<password>;");
System.out.println("Driver version: " + conn.getMetaData().getDriverVersion());
```

### <a name="always-encrypted"></a>始终加密

驱动程序支持在 SQL Server 2016 中的始终加密功能。 此功能可确保敏感数据永远不会以纯文本形式的 SQL Server 实例中所示。 Always Encrypted 工作方式是，以透明方式加密应用程序中的数据，这样 SQL Server 就只会处理已加密数据，而不会处理纯文本值。 即使 SQL Server 实例或主机计算机遭入侵，攻击者也只能获得敏感数据的已加密文本。 有关详细信息，请参阅[对 JDBC 驱动程序使用 Always Encrypted](../../connect/jdbc/using-always-encrypted-with-the-jdbc-driver.md)。

### <a name="internationalized-domain-names"></a>国际化域名

该驱动程序支持国际化的域名 (Idn) 服务器的名称。 详细信息，请参阅"使用国际域名"中[JDBC 驱动程序的国际化功能](../../connect/jdbc/international-features-of-the-jdbc-driver.md)一文。

### <a name="parameterized-queries"></a>参数化查询

驱动程序现在支持，使用已准备的语句为复杂查询（如子查询和/或联接）检索参数元数据。 请注意，此改进仅对 SQL Server 2012 及更高版本有效。

### <a name="azure-active-directory"></a>Azure Active Directory

Azure AD 身份验证是一种使用 Azure AD 中的标识连接到 Azure SQL 数据库 v12 的机制。 Azure AD 身份验证可用于集中管理数据库用户的标识，并替代 SQL Server 身份验证。 

JDBC Driver 6.0 可用于在要连接到 Azure SQL 数据库的 JDBC 连接字符串中指定你的 Azure AD 凭据。 有关详细信息，请参阅中的身份验证属性[连接属性设置](../../connect/jdbc/setting-the-connection-properties.md)一文。

### <a name="table-valued-parameters"></a>表值参数

借助 TVP，可以将多行数据从客户端应用程序轻松封送到 SQL Server，而无需进行多次往返或使用特殊的服务器端逻辑来处理数据。 可使用 TVP 来封装客户端应用程序中的数据行，并以一个参数化命令的形式将数据发送到服务器。 然后可以通过使用 TRANSACT-SQL 运行的表变量中存储传入的数据行。 有关详细信息，请参阅[使用表值参数](../../connect/jdbc/using-table-valued-parameters.md)。

### <a name="always-on-availability-groups"></a>Always On 可用性组

该驱动程序现在支持透明连接到 Alwayson 可用性组。 驱动程序快速发现服务器基础结构的当前 AlwaysOn 拓扑，并以透明方式连接到当前的活动服务器。

## <a name="updates-in-microsoft-jdbc-driver-42-for-sql-server-and-later"></a>Microsoft JDBC Driver 4.2 for SQL Server 及更高版本中的更新

Microsoft JDBC Driver 4.2 for SQL Server 是完全符合 JDBC 规范 4.1 和 4.2。 根据其符合性的 JDBC API 版本命名 4.2 程序包中的 jar。 例如，从 4.2 程序包 sqljdbc42.jar 文件与 JDBC API 4.2 兼容。 同样，sqljdbc41.jar 文件与 JDBC 4.1 API 兼容。

若要确保具有正确 sqljdbc42.jar 或 sqljdbc41.jar 文件，请运行以下代码行。 如果输出是"驱动程序版本：4.2.6420.100"，你具有 JDBC Driver 4.2 包。

```java
Connection conn = DriverManager.getConnection("jdbc:sqlserver://<server>;user=<user>;password=<password>;");
System.out.println("Driver version: " + conn.getMetaData().getDriverVersion());
```

### <a name="support-for-jdk-8"></a>支持 JDK 8

该驱动程序支持 JDK 版本 8.0 除 JDK 7.0、 6.0 和 5.0。

### <a name="jdbc-41-and-42-compliance"></a>JDBC 4.1 和 4.2 的遵从性

除了支持 4.0 以外，驱动程序还支持 Java Database Connectivity API 4.1 和 4.2 规范。 有关详细信息，请参阅[JDBC 驱动程序的 JDBC 4.1 合规性](../../connect/jdbc/jdbc-4-1-compliance-for-the-jdbc-driver.md)并[JDBC 驱动程序的 JDBC 4.2 合规性](../../connect/jdbc/jdbc-4-2-compliance-for-the-jdbc-driver.md)。

### <a name="bulk-copy"></a>大容量复制

大容量复制功能可用于将大量数据快速复制到 SQL Server 数据库中的表或视图。 有关详细信息，请参阅[结合使用大容量复制和 JDBC Driver](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md)。

### <a name="xa-transaction-rollback-option"></a>XA 事务回滚选项

驱动程序新增了适用于未准备好事务的现有自动回滚的超时选项。 有关详细信息，请参阅[了解 XA 事务](../../connect/jdbc/understanding-xa-transactions.md)。

### <a name="new-kerberos-principal-connection-property"></a>新 Kerberos 主体连接属性

驱动程序使用新连接属性，提高 Kerberos 连接灵活性。 有关详细信息，请参阅[使用 Kerberos 集成身份验证连接到 SQL Server](../../connect/jdbc/using-kerberos-integrated-authentication-to-connect-to-sql-server.md)。

## <a name="updates-in-microsoft-jdbc-driver-41-for-sql-server-and-later"></a>Microsoft JDBC Driver 4.2 for SQL Server 及更高版本中的更新

### <a name="support-for-jdk-7"></a>支持 JDK 7

该驱动程序支持 JDK 7.0 版除 JDK 6.0 和 5.0 外。

## <a name="itanium-not-supported-for-jdbc-driver-64-60-42-and-41-applications"></a>JDBC Driver 6.4、6.0、4.2 和 4.1 应用程序不支持 Itanium

不支持适用于 SQL Server 应用程序 的 Microsoft JDBC 驱动程序 6.4、6.0、4.2 和 4.1 在 Itanium 计算机上运行。

## <a name="see-also"></a>另请参阅

[JDBC 驱动程序的概述](../../connect/jdbc/overview-of-the-jdbc-driver.md)
