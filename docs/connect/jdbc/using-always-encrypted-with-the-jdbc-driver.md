---
title: JDBC 驱动程序使用始终加密 |Microsoft 文档
ms.custom: ''
ms.date: 3/14/2018
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 271c0438-8af1-45e5-b96a-4b1cabe32707
caps.latest.revision: ''
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 425f965c37e1d148a267566bd1980eb345cadfc6
ms.sourcegitcommit: 2e130e9f3ce8a7ffe373d7fba8b09e937c216386
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/28/2018
---
# <a name="using-always-encrypted-with-the-jdbc-driver"></a>JDBC 驱动程序使用始终加密
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

此页提供有关如何开发使用 Java 应用程序的信息[始终加密](../../relational-databases/security/encryption/always-encrypted-database-engine.md)和 Microsoft JDBC Driver 6.0 （或更高版本） for SQL Server。

始终加密允许客户端加密敏感数据，并且永远不会显示数据或 SQL Server 或 Azure SQL 数据库的加密密钥。 始终加密的 SQL Server 启用驱动程序，如 Microsoft JDBC Driver 6.0 （或更高版本），通过以透明方式加密和解密在客户端应用程序中的敏感数据来实现此行为。 该驱动程序自动确定哪个查询参数相对应的始终加密数据库列，并对这些参数的值进行加密，再将它们发送到 SQL Server 或 Azure SQL 数据库。 同样，该驱动程序以透明方式对查询结果中从加密数据库列检索到的数据进行解密。 有关详细信息，请参阅[始终加密 （数据库引擎）](../../relational-databases/security/encryption/always-encrypted-database-engine.md)和[始终加密 API 参考 JDBC 驱动程序](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)。

## <a name="prerequisites"></a>必要條件
- 请确保 Microsoft JDBC Driver 6.0 （或更高版本） 为您的开发计算机上安装 SQL Server。 
- 下载并安装 Java Cryptography Extension (JCE) Unlimited Strength Jurisdiction Policy Files。  请务必阅读有关安装说明和相关详细信息上可能的导出/导入问题的 zip 文件中包含的自述文件。  

    - 如果使用 mssql jdbc X.X.X.jre7.jar 或 sqljdbc41.jar，可以从下载的策略文件[Java 加密扩展 (JCE) 不受限制的强度管辖策略文件 7 下载](http://www.oracle.com/technetwork/java/javase/downloads/jce-7-download-432124.html)

    - 如果使用 mssql jdbc X.X.X.jre8.jar 或 sqljdbc42.jar，可以从下载的策略文件[Java 加密扩展 (JCE) 不受限制的强度管辖策略文件 8 下载](http://www.oracle.com/technetwork/java/javase/downloads/jce8-download-2133166.html)

    - 如果使用 mssql jdbc X.X.X.jre9.jar，不需要下载任何策略文件。 Java 9 中的管辖策略默认为不受限制的强度加密。

## <a name="working-with-column-master-key-stores"></a>使用列主密钥存储
若要加密或解密加密列的数据，SQL Server 维护列加密密钥。 列加密密钥存储在数据库元数据中的加密形式。 每个列加密密钥具有相应列主密钥用于加密列加密密钥。 数据库元数据不包含列主密钥。 由客户端仅持有这些密钥。 但是数据库元数据包含有关列主密匙相对于客户端的存储位置的信息。 例如，数据库元数据可能会说，密钥库包含列主密钥是 Windows 证书存储，用于加密和解密的特定证书位于 Windows 证书存储区中的特定路径。 如果客户端 Windows 证书存储中有权访问该证书，它可以获取证书。 然后可以使用证书来解密列加密密钥。 然后可以使用该加密密钥进行解密或加密使用列加密密钥的加密列的数据。

Microsoft JDBC Driver for SQL Server 通信密钥库使用的列主密钥存储提供程序，这是一个类的实例派生自**SQLServerColumnEncryptionKeyStoreProvider**。

### <a name="using-built-in-column-master-key-store-providers"></a>使用内置列主密钥存储提供程序
Microsoft JDBC Driver for SQL Server 附带以下内置列主密钥存储提供程序。 这些提供程序的一些预先注册具有特定的提供程序名称 （用来查找该提供程序），但有些需要其他凭据或显式注册。

| 类 | Description | 提供程序（查找）名称 |预先注册？|
|:---|:---|:---|:---|
|**SQLServerColumnEncryptionAzureKeyVaultProvider**| 用于 Azure 密钥保管库的密钥库的提供程序。| AZURE_KEY_VAULT|否|
|**SQLServerColumnEncryptionCertificateStoreProvider**| 用于 Windows 证书存储的提供程序。|MSSQL_CERTIFICATE_STORE|是
|**SQLServerColumnEncryptionJavaKeyStoreProvider**| 用于 Java 密钥库的提供程序|MSSQL_JAVA_KEYSTORE|是|

对于预注册的 keystore 提供程序，你不需要进行任何应用程序代码更改，以使用这些提供程序，但请注意以下各项：

- 你 （或你的 DBA） 需要确保列主密钥元数据中配置的提供程序名称正确，以及列主密钥路径符合对于给定的提供程序有效的密钥路径格式。 建议你配置使用的工具，如 SQL Server Management Studio，在发出 CREATE COLUMN MASTER KEY (TRANSACT-SQL) 语句时自动生成的有效提供程序名称和密钥路径的密钥。
- 确保你的应用程序可以访问该密钥在密钥存储区。 此任务可能涉及授予你的应用程序访问的键和/或密钥存储，具体取决于密钥存储区中，或执行其他特定于密钥存储区中的配置步骤。 例如，对于使用 SQLServerColumnEncryptionJavaKeyStoreProvider，你需要提供位置和密钥存储的连接属性中的密码。 

所有这些 keystore 提供程序均在以下各节中的更多详细信息中有述。 只需实现一个 keystore 提供程序使用始终加密。

### <a name="using-azure-key-vault-provider"></a>使用 Azure 密钥保管库提供程序
Azure 密钥保管库是一个方便的选项来存储和管理 Always encrypted 列主密匙，（尤其是当你的应用程序在 Azure 中托管的）。 Microsoft JDBC Driver for SQL Server 包括内置提供程序，SQLServerColumnEncryptionAzureKeyVaultProvider，具有 Azure 密钥保管库中存储的密钥的应用程序。 此提供程序的名称是 AZURE_KEY_VAULT。 若要使用 Azure 密钥保管库存储区提供程序，应用程序开发人员需要在 Azure 密钥保管库中创建保管库和密钥，并在 Azure Active Directory 中创建应用程序注册。 已注册的应用程序必须授予获取，解密，为创建用于 Always Encrypted 密钥保管库定义的访问策略中的加密、 解包密钥、 包装的密钥，并验证权限。 有关如何设置密钥保管库和创建列主密钥的详细信息，请参阅[Azure 密钥保管库 – Step by Step](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step/)和[Azure 密钥保管库中创建列主密匙](../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md#creating-column-master-keys-in-azure-key-vault)。

对于在此页上，如果你已创建 Azure 密钥保管库的示例基于列主密钥和使用 SQL Server Management Studio 的列加密密钥，用于重新创建它们的 T-SQL 脚本可能类似于此示例中使用其自身特定**KEY_路径**和**ENCRYPTED_VALUE**:

```
CREATE COLUMN MASTER KEY [MyCMK]
WITH
(
    KEY_STORE_PROVIDER_NAME = N'AZURE_KEY_VAULT',
    KEY_PATH = N'https://<MyKeyValutName>.vault.azure.net:443/keys/Always-Encrypted-Auto1/c61f01860f37302457fa512bb7e7f4e8'
)

CREATE COLUMN ENCRYPTION KEY [MyCEK]
WITH VALUES
(
    COLUMN_MASTER_KEY = [MyCMK],
    ALGORITHM = 'RSA_OAEP',
    ENCRYPTED_VALUE = 0x01BA000001680074507400700073003A002F002F006400610076006...
)
```

若要使用 Azure 密钥保管库，客户端应用程序需要实例化 SQLServerColumnEncryptionAzureKeyVaultProvider 并将其注册到该驱动程序。

此处是初始化 SQLServerColumnEncryptionAzureKeyVaultProvider 的一个示例：  

```
SQLServerColumnEncryptionAzureKeyVaultProvider akvProvider = new SQLServerColumnEncryptionAzureKeyVaultProvider(clientID, clientKey);
```

**clientID**是 Azure Active Directory 实例中的应用程序注册的应用程序 ID。 **clientKey**在该应用程序，它提供 API 访问 Azure 密钥保管库下注册是密钥密码。

应用程序创建的 SQLServerColumnEncryptionAzureKeyVaultProvider 实例后，应用程序必须注册使用 SQLServerConnection.registerColumnEncryptionKeyStoreProviders() 方法的驱动程序的实例。 强烈建议使用默认查找名称 AZURE_KEY_VAULT，可以通过调用 SQLServerColumnEncryptionAzureKeyVaultProvider.getName() API 来获取注册实例。 使用默认名称，将允许你使用 SQL Server Management Studio 或 PowerShell 等工具来设置和管理 （工具使用的默认名称以生成列主密钥的元数据对象） 的始终加密密钥。 下面的示例演示正在注册 Azure 密钥保管库提供程序。 SQLServerConnection.registerColumnEncryptionKeyStoreProviders() 方法的详细信息，请参阅[始终加密 API 参考 JDBC 驱动程序](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)。

```
Map<String, SQLServerColumnEncryptionKeyStoreProvider> keyStoreMap = new HashMap<String, SQLServerColumnEncryptionKeyStoreProvider>();
keyStoreMap.put(akvProvider.getName(), akvProvider);
SQLServerConnection.registerColumnEncryptionKeyStoreProviders(keyStoreMap);
```

> [!IMPORTANT]
>  如果你使用 Azure 密钥保管库 keystore 提供程序，JDBC 驱动程序的 Azure 密钥保管库实现这些库 （GitHub) 它必须是包含你的应用程序上具有依赖关系：
>
>  [azure-sdk-for-java](https://github.com/Azure/azure-sdk-for-java)
>
>  [azure-activedirectory-library-for-java libraries](https://github.com/AzureAD/azure-activedirectory-library-for-java)
>
> 有关如何在一个 Maven 项目中包括这些依赖关系的示例，请参阅[下载 ADAL4J 和 AKV 依赖关系使用 Apache Maven](https://github.com/Microsoft/mssql-jdbc/wiki/Download-ADAL4J-And-AKV-Dependencies-with-Apache-Maven)

### <a name="using-windows-certificate-store-provider"></a>使用 Windows 证书存储区提供程序
SQLServerColumnEncryptionCertificateStoreProvider 可以用于在 Windows 证书存储中存储列主密钥。 使用 SQL Server Management Studio (SSMS) 始终加密向导或其他支持的工具的列主密钥和列加密密钥定义在数据库中创建。 可以使用相同的向导可以用于始终加密的数据作为列主密钥的 Windows 证书存储中生成自签名的证书。 有关列主密钥和列加密密钥的 T-SQL 语法的详细信息，请参阅[CREATE COLUMN MASTER KEY](../../t-sql/statements/create-column-master-key-transact-sql.md)和[CREATE COLUMN ENCRPTION KEY](../../t-sql/statements/create-column-encryption-key-transact-sql.md)分别。

该名称的 SQLServerColumnEncryptionCertificateStoreProvider 是 MSSQL_CERTIFICATE_STORE，并且可通过提供程序对象 getName() API 查询。 它自动注册由驱动程序，并可无缝而无需任何应用程序更改。

对于在此页上，如果你已创建 Windows 证书存储区的示例基于列主密钥和使用 SQL Server Management Studio 的列加密密钥，用于重新创建它们的 T-SQL 脚本可能类似于此示例中使用其自身特定**KEY_PATH**和**ENCRYPTED_VALUE**:

```
CREATE COLUMN MASTER KEY [MyCMK]
WITH
(
    KEY_STORE_PROVIDER_NAME = N'MSSQL_CERTIFICATE_STORE',
    KEY_PATH = N'CurrentUser/My/A2A91F59C461B559E4D962DA9D2BC6131B32CB91'
)

CREATE COLUMN ENCRYPTION KEY [MyCEK]
WITH VALUES
(
    COLUMN_MASTER_KEY = [MyCMK],
    ALGORITHM = 'RSA_OAEP',
    ENCRYPTED_VALUE = 0x016E000001630075007200720065006E0074007500730065007200...
)
```

> [!IMPORTANT]
> 尽管这篇文章中的其他 keystore 提供程序可在所有驱动程序支持的平台上，是 Windows 仅在操作系统上可用的 JDBC 驱动程序的 SQLServerColumnEncryptionCertificateStoreProvider 实现。 它具有 sqljdbc_auth.dll 驱动程序包中提供的依赖关系。 若要使用此提供程序，请将 sqljdbc_auth.dll 文件复制到装有 JDBC 驱动程序的计算机上的 Windows 系统路径上的目录。 也可以设置 java.libary.path 系统属性以指定 sqljdbc_auth.dll 的目录。 如果您运行 32 位的 Java 虚拟机 (JVM)，则使用 x86 文件夹中的 sqljdbc_auth.dll 文件，即使操作系统是 x64 版本也不例外。 如果您在 x64 处理器上运行 64 位 JVM，则使用 x64 文件夹中的 sqljdbc_auth.dll 文件。 例如，如果你使用的 32 位 JVM 和 JDBC 驱动程序安装在默认目录，你可以通过使用以下虚拟机 (VM) 参数启动 Java 应用程序时指定的 DLL 的位置： `-Djava.library.path=C:\Microsoft JDBC Driver <version> for SQL Server\sqljdbc_<version>\enu\auth\x86`

### <a name="using-java-key-store-provider"></a>使用 Java 密钥存储提供程序
JDBC 驱动程序附带了 Java 密钥存储的内置密钥存储提供程序实现。 如果**keyStoreAuthentication**连接字符串中存在连接字符串属性，则和设置为"JavaKeyStorePassword"，该驱动程序自动实例化并注册用于 Java 密钥存储提供程序。 Java 密钥存储提供程序的名称是 MSSQL_JAVA_KEYSTORE。 此名称还可以通过使用 SQLServerColumnEncryptionJavaKeyStoreProvider.getName() API 查询。 

有三个允许客户端应用程序指定该驱动程序必须向 Java 密钥存储进行身份验证的凭据的连接字符串属性。 该驱动程序初始化提供程序基于连接字符串中这三个属性的值。

**keyStoreAuthentication:**标识要使用的 Java 密钥存储区。 Microsoft JDBC Driver 6.0 和更高版本的 SQL Server，你可以进行身份验证到 Java 密钥存储只能通过此属性。 对于 Java 密钥存储，此属性的值必须是`JavaKeyStorePassword`。

**keyStoreLocation:**存储列主密钥的 Java 密钥库文件的路径。 路径包括 keystore 文件名。

**keyStoreSecret:**机密/密码用于 keystore 以及与该密钥。 表示使用 Java 密钥存储、 密钥库和密钥的密码必须相同。

此处是提供这些凭据连接字符串中的一个示例：

```
String connectionString = "jdbc:sqlserver://localhost;user=<user>;password=<password>;columnEncryptionSetting=Enabled;keyStoreAuthentication=JavaKeyStorePassword;keyStoreLocation=<path_to_the_keystore_file>;keyStoreSecret=<keystore_key_password>";
```

你还可以获取或设置使用 SQLServerDataSource 对象这些设置。 有关详细信息，请参阅[始终加密 API 参考 JDBC 驱动程序](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)。

JDBC 驱动程序自动实例化 SQLServerColumnEncryptionJavaKeyStoreProvider 连接属性中存在这些凭据时。

### <a name="creating-a-column-master-key-for-the-java-key-store"></a>创建 Java 密钥存储列主密钥
SQLServerColumnEncryptionJavaKeyStoreProvider 可以用于 JKS 或 PKCS12 keystore 类型。 若要创建或导入要与此提供程序使用的密钥使用 Java [keytool](http://docs.oracle.com/javase/7/docs/technotes/tools/windows/keytool.html)实用程序。 密钥长度必须为密钥库本身的相同密码。 下面是如何创建一个公钥和使用 keytool 实用工具及其关联的私钥的示例：

```
keytool -genkeypair -keyalg RSA -alias AlwaysEncryptedKey -keystore keystore.jks -storepass mypassword -validity 360 -keysize 2048 -storetype jks
```

此命令创建一个公钥，并将其包装的自签名证书，存储在密钥存储区 keystore.jks 以及其关联的私钥的 X.509 中。 在密钥存储区的此项都由别名 AlwaysEncryptedKey 标识。

下面是同一个使用 PKCS12 存储类型的示例：

```
keytool -genkeypair -keyalg RSA -alias AlwaysEncryptedKey -keystore keystore.pfx -storepass mypassword -validity 360 -keysize 2048 -storetype pkcs12 -keypass mypassword
```

如果密钥库的类型 PKCS12，keytool 实用工具将不提示输入密钥的密码和密钥的密码需要随附-keypass 选项，因为 SQLServerColumnEncryptionJavaKeyStoreProvider 需要密钥库和密钥具有相同密码。

你还可以从 Windows 证书存储以.pfx 格式导出证书，然后，使用 SQLServerColumnEncryptionJavaKeyStoreProvider。 导出的证书可以还将导入 Java 密钥存储为 JKS keystore 类型。

在创建后 keytool 条目，需要 keystore 提供程序名称和密钥路径的数据库中创建列主密钥元数据。 有关如何创建列主密钥元数据的详细信息，请参阅[CREATE COLUMN MASTER KEY](../../t-sql/statements/create-column-master-key-transact-sql.md)。 有关 SQLServerColumnEncryptionJavaKeyStoreProvider，注册表项路径是只需密钥的别名和 SQLServerColumnEncryptionJavaKeyStoreProvider 的名称是 MSSQL_JAVA_KEYSTORE。 你还可以查询使用 getName() 公共 API SQLServerColumnEncryptionJavaKeyStoreProvider 类的此名称。 

用于创建列主密钥的 T-SQL 语法是：

```
CREATE COLUMN MASTER KEY [<CMK_name>]
WITH
(
    KEY_STORE_PROVIDER_NAME = N'MSSQL_JAVA_KEYSTORE',
    KEY_PATH = N'<key_alias>'
)
```

对于 AlwaysEncryptedKey 上述步骤中创建，将为列主密钥定义：

```
CREATE COLUMN MASTER KEY [MyCMK]
WITH
(
    KEY_STORE_PROVIDER_NAME = N'MSSQL_JAVA_KEYSTORE',
    KEY_PATH = N'AlwaysEncryptedKey'
)
```

> [!NOTE]
> 内置的 SQL Server management Studio 功能无法创建 Java 密钥存储区的列主密钥定义。 必须以编程方式使用 T-SQL 命令。

### <a name="creating-a-column-encryption-key-for-the-java-key-store"></a>创建 Java 密钥存储区的列加密密钥
SQL Server Management Studio 或任何其他工具无法用于创建使用 Java 密钥存储中的列主密钥的加密密钥的列。 客户端应用程序必须创建使用 SQLServerColumnEncryptionJavaKeyStoreProvider 类以编程方式的列加密密钥。 有关详细信息，请参阅[使用列主密钥存储提供程序进行编程密钥预配](#using-column-master-key-store-providers-for-programmatic-key-provisioning)。

### <a name="implementing-a-custom-column-master-key-store-provider"></a>实现自定义列主密钥存储提供程序
如果你想要在现有提供程序不支持的密钥库中存储列主密钥，则可以通过扩展 SQLServerColumnEncryptionKeyStoreProvider 类并注册使用的提供程序实现自定义提供程序SQLServerConnection.registerColumnEncryptionKeyStoreProviders() 方法。

```
public class MyCustomKeyStore extends SQLServerColumnEncryptionKeyStoreProvider{  
    private String name = "MY_CUSTOM_KEYSTORE";

    public void setName(String name)
    {
        this.name = name;
    }

    public String getName()
    {
        return name;
    }

    public byte[] encryptColumnEncryptionKey(String masterKeyPath, String encryptionAlgorithm, byte[] plainTextColumnEncryptionKey)
    {
        // Logic for encrypting the column encryption key
    }

    public byte[] decryptColumnEncryptionKey(String masterKeyPath, String encryptionAlgorithm, byte[] encryptedColumnEncryptionKey)
    {
        // Logic for decrypting the column encryption key
    }
}
```

注册提供程序：

```
SQLServerColumnEncryptionKeyStoreProvider storeProvider = new MyCustomKeyStore();
Map<String, SQLServerColumnEncryptionKeyStoreProvider> keyStoreMap = new HashMap<String, SQLServerColumnEncryptionKeyStoreProvider>();
keyStoreMap.put(storeProvider.getName(), storeProvider);
SQLServerConnection.registerColumnEncryptionKeyStoreProviders(keyStoreMap);
```

## <a name="using-column-master-key-store-providers-for-programmatic-key-provisioning"></a>使用列主密钥存储提供程序进行编程密钥预配
在访问加密的列时，Microsoft JDBC Driver for SQL Server 将以透明方式查找，并调用正确的列主密钥存储提供程序来解密列加密密钥。 通常情况下，普通的应用程序代码不会直接调用列主密钥存储提供程序。 但是，你可能会实例化并调用一个提供程序以编程方式来设置和管理始终加密密钥。 此步骤可能为了生成加密的列加密密钥，并作为一部分列主密钥轮替，例如解密列加密密钥。 有关详细信息，请参阅 [Always Encrypted 密钥管理概述](../../relational-databases/security/encryption/overview-of-key-management-for-always-encrypted.md)。

如果你使用自定义 keystore 提供程序，实现您自己的密钥管理工具可能需要用。 使用密钥存储在 Windows 证书存储或 Azure 密钥保管库中时，你可以使用现有工具，如 SQL Server Management Studio 或 PowerShell，管理和预配密钥。 使用 Java 密钥存储中存储的密钥时，你需要以编程方式预配密钥。 下面的示例演示如何使用 SQLServerColumnEncryptionJavaKeyStoreProvider 类与 Java 密钥存储中存储的密钥的密钥进行加密。

```
import java.sql.*;
import javax.xml.bind.DatatypeConverter;
import com.microsoft.sqlserver.jdbc.SQLServerColumnEncryptionJavaKeyStoreProvider;
import com.microsoft.sqlserver.jdbc.SQLServerColumnEncryptionKeyStoreProvider;
import com.microsoft.sqlserver.jdbc.SQLServerException;

/**
 * This program demonstrates how to create a column encryption key programmatically for the Java Key Store.
 */
public class AlwaysEncrypted
{
    // Alias of the key stored in the keystore.
    private static String keyAlias = "<proide key alias>";

    // Name by which the column master key will be known in the database.
    private static String columnMasterKeyName = "MyCMK";

    // Name by which the column encryption key will be known in the database.
    private static String columnEncryptionKey = "MyCEK";

    // The location of the keystore.
    private static String keyStoreLocation = "C:\\Dev\\Always Encrypted\\keystore.jks";

    // The password of the keystore and the key.
    private static char[] keyStoreSecret = "********".toCharArray();

    /**
     * Name of the encryption algorithm used to encrypt the value of
     * the column encryption key. The algorithm for the system providers must be RSA_OAEP.
     */
    private static String algorithm = "RSA_OAEP";

    public static void main(String[] args)
    {
        String connectionString = GetConnectionString();
        try
        {
            // Note: if you are not using try-with-resources statements (as here),
            // you must remember to call close() on any Connection, Statement,
            // ResultSet objects that you create.

            // Open a connection to the database.
            Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");
            try (Connection sourceConnection = DriverManager.getConnection(connectionString))
            {
                // Instantiate the Java Key Store provider.
                SQLServerColumnEncryptionKeyStoreProvider storeProvider =
                        new SQLServerColumnEncryptionJavaKeyStoreProvider(
                                keyStoreLocation,
                                keyStoreSecret);

                byte [] encryptedCEK=getEncryptedCEK(storeProvider);

                /**
                 * Create column encryption key
                 * For more details on the syntax, see:
                 * https://docs.microsoft.com/sql/t-sql/statements/create-column-encryption-key-transact-sql
                 * Encrypted column encryption key first needs to be converted into varbinary_literal from bytes, 
                 * for which DatatypeConverter.printHexBinary is used
                 */
                String createCEKSQL = "CREATE COLUMN ENCRYPTION KEY "
                        + columnEncryptionKey
                        + " WITH VALUES ( "
                        + " COLUMN_MASTER_KEY = "
                        + columnMasterKeyName
                        + " , ALGORITHM =  '"
                        + algorithm
                        + "' , ENCRYPTED_VALUE =  0x"
                        + DatatypeConverter.printHexBinary(encryptedCEK)
                        + " ) ";

                try (Statement cekStatement = sourceConnection.createStatement())
                {
                    cekStatement.executeUpdate(createCEKSQL);
                    System.out.println("Column encryption key created with name : " + columnEncryptionKey);
                }
            }
        }
        catch (Exception e)
        {
            // Handle any errors that may have occurred.
            e.printStackTrace();
        }
    }

    // To avoid storing the sourceConnection String in your code,
    // you can retrieve it from a configuration file.
    private static String GetConnectionString()
    {
        // Create a variable for the connection string.
        String connectionUrl = "jdbc:sqlserver://localhost:1433;" +
                "databaseName=ae2;user=sa;password=********;";

        return connectionUrl;
    }

    private static byte[] getEncryptedCEK(SQLServerColumnEncryptionKeyStoreProvider storeProvider) throws SQLServerException
    {
        /**
         * Following arguments needed by SQLServerColumnEncryptionJavaKeyStoreProvider
         * 1) keyStoreLocation :
         *      Path where keystore is located, including the keystore file name.
         * 2) keyStoreSecret :
         *      Password of the keystore and the key.
         */
        String plainTextKey = "You need to give your plain text";

        // plainTextKey has to be 32 bytes with current algorithm supported
        byte[] plainCEK = plainTextKey.getBytes();

        // This will give us encrypted column encryption key in bytes
        byte[] encryptedCEK = storeProvider.encryptColumnEncryptionKey(
                keyAlias,
                algorithm,
                plainCEK);

        return encryptedCEK;
    }
}
```

## <a name="enabling-always-encrypted-for-application-queries"></a>为应用程序查询启用始终加密
若要启用的参数的加密和解密面向加密的列的查询结果的最简单方法是通过设置的值**columnEncryptionSetting**到连接字符串关键字**已启用**.

以下连接字符串是启用始终加密 JDBC 驱动程序中的一个示例：

```
String connectionString = "jdbc:sqlserver://localhost;user=<user>;password=<password>;databaseName=<database>;columnEncryptionSetting=Enabled;";
SQLServerConnection connection = (SQLServerConnection) DriverManager.getConnection(connectionString);
```

下面的代码是使用 SQLServerDataSource 对象的等效示例：

```
SQLServerDataSource ds = new SQLServerDataSource();
ds.setServerName("localhost");
ds.setUser("<user>");
ds.setPassword("<password>");
ds.setDatabaseName("<database>");
ds.setColumnEncryptionSetting("Enabled");
SQLServerConnection con = (SQLServerConnection) ds.getConnection();
```

还可以为单个查询启用始终加密。 有关详细信息，请参阅[控制始终加密的性能影响](#controlling-the-performance-impact-of-always-encrypted)。 启用始终加密不足以加密或解密才能成功。 你还需要确保：
- 应用程序具有 *查看任意列主密钥定义* 和 *查看任意列加密密钥定义* 数据库权限，这是访问数据库中始终加密密钥的相关元数据所必需的权限。 有关详细信息，请参阅[中始终加密 （数据库引擎） 的权限](../../relational-databases/security/encryption/always-encrypted-database-engine.md#database-permissions)。
- 应用程序可以访问列主密钥保护列加密密钥加密的查询的数据库列。 若要使用 Java 密钥存储提供程序，你需要提供连接字符串中的其他凭据。 有关详细信息，请参阅[使用 Java 密钥存储提供程序](#using-java-key-store-provider)。

### <a name="configuring-how-javasqltime-values-are-sent-to-the-server"></a>配置如何将 java.sql.Time 值发送到服务器
**SendTimeAsDatetime**连接属性用于配置如何将 java.sql.Time 值发送到服务器。 设置为 false 时，SQL Server 时类型作为发送时间值。 何时设置为 true，值发送为 datetime 类型的时间。 如果时间列已加密， **sendTimeAsDatetime**属性必须为 false，因为加密的列不支持从时间转换为日期时间。 另请注意，此属性是通过默认为 true，因此使用加密的时间列时将需要将其设置为 false。 否则，该驱动程序将引发异常。 从版本 6.0 的驱动程序开始，SQLServerConnection 类具有两种方法，以编程方式配置此属性的值：
 
* 公共 void setSendTimeAsDatetime (布尔 sendTimeAsDateTimeValue)
* public boolean getSendTimeAsDatetime()

此属性的详细信息，请参阅[如何配置 java.sql.Time 值发送到服务器](configuring-how-java-sql-time-values-are-sent-to-the-server.md)。

### <a name="configuring-how-string-values-are-sent-to-the-server"></a>配置如何将字符串值发送到服务器
**SendStringParametersAsUnicode**连接属性用于配置如何将字符串值发送到 SQL Server。 如果设置为 true，字符串参数发送到 Unicode 格式中的服务器。 如果设置为 false，字符串参数以非 Unicode 格式，如 ASCII 或 MBCS，而不是 Unicode 发送的。 此属性的默认值为 true。 当启用始终加密和 char/varchar/varchar(max) 列已加密、 的值**sendStringParametersAsUnicode**必须设置为 false。 如果此属性设置为 true，该驱动程序将引发异常时解密从加密的 char/varchar/varchar(max) 列具有 Unicode 字符的数据。 此属性的详细信息，请参阅[设置连接属性](../../connect/jdbc/setting-the-connection-properties.md)。
  
## <a name="retrieving-and-modifying-data-in-encrypted-columns"></a>检索和修改加密列中的数据
一旦为应用程序查询启用始终加密，你可以使用标准 JDBC Api 来检索或修改加密的数据库列中的数据。 如果你的应用程序具有所需的数据库权限，并且可以访问列主密钥，驱动程序将加密任何面向加密的列并解密从加密列检索到的数据的查询参数。

如果未启用始终加密，具有面向加密列的参数的查询将失败。 只要查询没有面向加密的列的参数，查询仍然可以从加密列检索数据。 但是，该驱动程序不会尝试解密从加密列检索到任何值，并且应用程序将收到二进制加密的数据 （作为字节数组）。

下表总结了具体取决于是否启用始终加密或不的查询的行为：

|查询特征 | 启用了始终加密，并且应用程序可以访问密钥和密钥元数据|启用了始终加密，但应用程序无法访问密钥或密钥元数据 | 禁用了始终加密|
|:---|:---|:---|:---|
| 具有面向加密列的参数的查询。 | 以透明方式加密参数值。 | 错误 | 错误|
| 从加密列检索数据，而无需面向加密的列的参数的查询。| 以透明方式解密来自加密列的结果。 应用程序收到对应于为加密的列配置的 SQL Server 类型的 JDBC 数据类型的纯文本的值。 | 错误 | 不解密来自加密列的结果。 应用程序收到字节数组形式的加密值 (byte[])。

### <a name="inserting-and-retrieving-encrypted-data-examples"></a>插入和检索加密的数据示例 
以下示例说明如何检索和修改加密列中的数据。 这些示例假定目标表具有以下架构和加密的 SSN 和 BirthDate 列。 如果配置了名为列主密钥"MyCMK"和列加密密钥名为"MyCEK"（如前面的 keystore 提供程序部分中所述），你可以使用此脚本将表创建：

```
CREATE TABLE [dbo].[Patients]([PatientId] [int] IDENTITY(1,1),
 [SSN] [char](11) COLLATE Latin1_General_BIN2
 ENCRYPTED WITH (ENCRYPTION_TYPE = DETERMINISTIC,
 ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256',
 COLUMN_ENCRYPTION_KEY = MyCEK) NOT NULL,
 [FirstName] [nvarchar](50) NULL,
 [LastName] [nvarchar](50) NULL,
 [BirthDate] [date]
 ENCRYPTED WITH (ENCRYPTION_TYPE = RANDOMIZED,
 ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256',
 COLUMN_ENCRYPTION_KEY = MyCEK) NOT NULL
 PRIMARY KEY CLUSTERED ([PatientId] ASC) ON [PRIMARY])
 GO
```

对于每个 Java 代码示例中，将需要记下的位置中插入特定于密钥库的代码。

如果你在使用 Azure 密钥保管库密钥存储提供程序：

```
    String clientID = "<Azure Application ID>";
    String clientKey = "<Azure Application API Key Password>";
    SQLServerColumnEncryptionAzureKeyVaultProvider akvProvider = new SQLServerColumnEncryptionAzureKeyVaultProvider(clientID, clientKey);
    Map<String, SQLServerColumnEncryptionKeyStoreProvider> keyStoreMap = new HashMap<String, SQLServerColumnEncryptionKeyStoreProvider>();
    keyStoreMap.put(akvProvider.getName(), akvProvider);
    SQLServerConnection.registerColumnEncryptionKeyStoreProviders(keyStoreMap);
    String connectionString = "jdbc:sqlserver://localhost:1433;databaseName=Clinic;user=sa;password=******;columnEncryptionSetting=Enabled;";
```

如果你在使用 Windows 证书存储区 keystore 提供程序：

```
    String connectionString = "jdbc:sqlserver://localhost:1433;databaseName=Clinic;user=sa;password=******;columnEncryptionSetting=Enabled;";
```

如果你在使用 Java 密钥存储 keystore 提供程序：

```
    String connectionString = "jdbc:sqlserver://localhost:1433;databaseName=Clinic;user=sa;password=******;columnEncryptionSetting=Enabled;keyStoreAuthentication=JavaKeyStorePassword;keyStoreLocation=<path to jks or pfx file>;keyStoreSecret=<keystore secret/password>";
```

### <a name="inserting-data-example"></a>插入数据示例
此示例向 Patients 表插入一行。 请注意以下各项：
- 对于示例代码中的加密，没有什么特定的注意事项。 Microsoft JDBC Driver for SQL Server 自动检测并加密面向加密的列的参数。 此行为透明使向加密对应用程序。
- 插入到数据库列，包括加密的列的值作为参数使用 SQLServerPreparedStatement 传递。 使用参数时是可选的 （尽管它强烈建议，因为它有助于防止 SQL 注入），将值发送到非加密列时，它是必要条件面向加密的列的值。 如果插入到加密列的值作为查询语句中嵌入的文本传递，查询将失败，因为该驱动程序将不能确定目标加密列中的值，它将不加密的值。 因此，服务器会因为与加密列不兼容而拒绝它们。
- 程序打印的所有值都将以纯文本形式，如 Microsoft JDBC Driver for SQL Server 将以透明方式解密从加密列检索的数据。
- 如果你正在使用 WHERE 子句，在 WHERE 子句需要用于以便驱动程序可以以透明方式对其进行加密发送到数据库之前，作为参数传递的值的查找。 在下面的示例中，作为参数传递 SSN 但 LastName 传递为文本，如姓氏未加密。
- 用于面向 SSN 列的参数的 setter 方法是 setString()，映射到 char/varchar SQL Server 数据类型。 如果此参数，使用的 setter 方法已 setNString()，映射到 nchar/nvarchar，查询将失败，因为始终加密不支持从加密的 nchar/nvarchar 值转换为加密的 char/varchar 值。

```
try
{
    <Insert keystore-specific code here>

    Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");
    try (Connection sourceConnection = DriverManager.getConnection(connectionString))
    {
        String insertRecord="INSERT INTO [dbo].[Patients] VALUES (?, ?, ?, ?)";
        try (PreparedStatement insertStatement = sourceConnection.prepareStatement(insertRecord))
        {
            insertStatement.setString(1, "795-73-9838");
            insertStatement.setString(2, "Catherine");
            insertStatement.setString(3, "Abel");
            insertStatement.setDate(4, Date.valueOf("1996-09-10"));
            insertStatement.executeUpdate();
            System.out.println("1 record inserted.\n");
        }
    }
}
catch (Exception e)
{
    e.printStackTrace();
}
```

### <a name="retrieving-plaintext-data-example"></a>检索纯文本数据示例
下面的示例演示如何根据加密的值和从加密列中的检索纯文本数据的筛选数据。 请注意以下各项：
- 在 WHERE 子句来筛选 SSN 列需要用于以便 Microsoft JDBC Driver for SQL Server 可以以透明方式对其进行加密发送到数据库之前，作为参数传递的值。
- 程序打印的所有值都将以纯文本形式，如 Microsoft JDBC Driver for SQL Server 将以透明方式解密从 SSN 和 BirthDate 列中检索的数据。

> [!NOTE]
> 如果使用确定性加密对列进行加密，则查询可以在其上执行相等比较。 有关详细信息，请参阅[中始终加密 （数据库引擎） 的选择确定性或随机加密](../../relational-databases/security/encryption/always-encrypted-database-engine.md#selecting--deterministic-or-randomized-encryption)。

```
try
{
    <Insert keystore-specific code here>

    Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");
    try (Connection sourceConnection = DriverManager.getConnection(connectionString))
    {
        String filterRecord="SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE SSN = ?;";
    
        try (PreparedStatement selectStatement = sourceConnection.prepareStatement(filterRecord))
        {
            selectStatement.setString(1, "795-73-9838");
            ResultSet rs = selectStatement.executeQuery();
            while(rs.next())
            {
                System.out.println("SSN: " +rs.getString("SSN") +
                    ", FirstName: " + rs.getString("FirstName") +
                    ", LastName:"+ rs.getString("LastName")+
                    ", Date of Birth: " + rs.getString("BirthDate"));
            }
        }
    }
}
catch (Exception e)  
{  
    e.printStackTrace();  
}
```
  
### <a name="retrieving-encrypted-data-example"></a>检索加密的数据示例
如果未启用始终加密，只要查询没有面向加密列的参数，就仍然可以从加密列中检索数据。

下面的示例演示从加密列中检索二进制加密的数据。 请注意以下各项：
- 由于连接字符串中未启用始终加密，因此查询将 （该程序将值转换为字符串） 的字节数组形式返回 SSN 和 BirthDate 的加密的值。
- 如果禁用始终加密，从加密列中检索数据的查询可以有参数，但前提是所有参数均不面向加密列。 按姓氏，未加密数据库中的以下查询筛选器。 如果查询按 SSN 或 BirthDate 进行筛选，则将失败。

```
try
{
    String connectionString  = "jdbc:sqlserver://localhost:1433;" + "databaseName=Clinic;user=sa;password=******";

    Class.forName("com.microsoft.sqlserver.jdbc.SQLServerDriver");
    try (Connection sourceConnection = DriverManager.getConnection(connectionString))
    {
        String filterRecord="SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE LastName = ?;";

        try (PreparedStatement selectStatement = sourceConnection.prepareStatement(filterRecord))
        {
            selectStatement.setString(1, "Abel");
            ResultSet rs = selectStatement.executeQuery();
            while (rs.next())
            {
                System.out.println("SSN: " + rs.getString("SSN") +
                    ", FirstName: " + rs.getString("FirstName") +
                    ", LastName:"+ rs.getString("LastName") +
                    ", Date of Birth: " + rs.getString("BirthDate"));
            }
        }
    }
}
catch (Exception e)
{
    e.printStackTrace();
}
```

### <a name="avoiding-common-problems-when-querying-encrypted-columns"></a>避免查询加密列时的常见问题
查询从 Java 应用程序和几个指导说明了如何避免它们的加密的列时，本部分介绍常见错误的类别。

### <a name="unsupported-data-type-conversion-errors"></a>不支持的数据类型转换错误
始终加密支持对加密数据类型进行若干种转换。 请参阅[始终加密 （数据库引擎）](../../relational-databases/security/encryption/always-encrypted-database-engine.md)有关受支持的类型转换的详细列表。 下面是你可以执行哪些操作来避免数据类型转换错误。 请确保：

- 将参数的值传递面向加密列时，你可以使用正确的 setter 方法。 确保在支持的参数的 SQL Server 数据类型转换为目标类型的列或参数的 SQL Server 数据类型正是与目标列的类型相同。 API 方法已添加到要将对应于特定的 SQL Server 数据类型的参数传递的 SQLServerPreparedStatement、 SQLServerCallableStatement 和 SQLServerResultSet 类。 例如，如果未加密的列，则可以使用 setTimestamp() 方法将参数传递到 datetime2 或日期时间列。 但在加密列时将需要使用的具体方法表示数据库中的列的类型。 例如，使用 setTimestamp() 将值传递给加密的 datetime2 列并使用 setDateTime() 将值传递到加密的日期时间列。 请参阅[始终加密 API 参考 JDBC 驱动程序](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)有关新的 Api 的完整列表。
- 对于面向列的 decimal 和 numeric SQL Server 数据类型的参数，其精度和小数位数与为目标列配置的精度和小数位数相同。 API 方法已添加到 SQLServerPreparedStatement、 SQLServerCallableStatement 和 SQLServerResultSet 类，以接受精度和小数位数以及参数/列，表示 decimal 和 numeric 数据类型的数据值。 请参阅[始终加密 API 参考 JDBC 驱动程序](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)有关新/重载 Api 的完整列表。  
- 秒的小数部分精度/刻度面向列的 datetime2、 datetimeoffset 或时间 SQL Server 数据类型的参数不是大于秒的小数部分精度/小数位数中修改目标列的值的查询的目标列. API 方法已添加到 SQLServerPreparedStatement、 SQLServerCallableStatement 和 SQLServerResultSet 类，以接受以及表示这些数据类型的参数的数据值的秒的小数部分精度/缩放。 有关新/重载 Api 的完整列表，请参阅[始终加密 API 参考 JDBC 驱动程序](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)。   

### <a name="errors-due-to-incorrect-connection-properties"></a>由于不正确的连接属性的错误
本部分介绍如何配置连接设置正确，若要使用始终加密数据。 由于加密的数据类型支持有限的转换**sendTimeAsDatetime**和**sendStringParametersAsUnicode**连接设置时使用加密的列需要正确配置。 请确保： 
- [sendTimeAsDatetime](setting-the-connection-properties.md)将数据插入加密时间列时，将连接设置设置为 false。 有关详细信息，请参阅[配置如何将 java.sql.Time 值发送到服务器](configuring-how-java-sql-time-values-are-sent-to-the-server.md)。
- [sendStringParametersAsUnicode](setting-the-connection-properties.md)连接设置为 true （或保留为默认值） 时将数据插入加密 char/varchar/varchar(max) 列。

### <a name="errors-due-to-passing-plaintext-instead-of-encrypted-values"></a>由于传递纯文本而非加密值而发生的错误
面向加密列的任何值都需要在应用程序内加密。 尝试插入/修改或者按纯文本值加密列进行筛选将导致错误类似于此：

```
com.microsoft.sqlserver.jdbc.SQLServerException: Operand type clash: varchar is incompatible with varchar(8000) encrypted with (encryption_type = 'DETERMINISTIC', encryption_algorithm_name = 'AEAD_AES_256_CBC_HMAC_SHA_256', column_encryption_key_name = 'MyCEK', column_encryption_key_database_name = 'ae') collation_name = 'SQL_Latin1_General_CP1_CI_AS'
```

为防止发生此类错误，请确保：
- 为面向加密的列 （为连接字符串或者为特定的查询） 的应用程序查询启用始终加密。
- 使用已准备的语句和参数以发送数据面向加密列。 下面的示例演示不正确筛选的文本/常量对加密列 (SSN)，而不是作为参数传递内的文本的查询。 此查询将会失败：

```
ResultSet rs = connection.createStatement().executeQuery("SELECT * FROM Customers WHERE SSN='795-73-9838'");
```

## <a name="force-encryption-on-input-parameters"></a>在输入参数上强制加密
使用始终加密时，强行加密功能强制实施参数加密。 如果使用强制加密，并且 SQL Server 通知驱动程序参数不需要进行加密，使用参数则查询将失败。 此属性提供针对安全攻击的额外保护，这些攻击涉及受损 SQL Server 向客户端提供不正确的加密元数据，这可能会导致数据泄漏。 中的 SQLServerPreparedStatement 和 SQLServerCallableStatement 类和更新的组 * 方法\*SQLServerResultSet 类中的方法重载以接受布尔参数来指定强制加密设置。 如果此参数的值为 false，该驱动程序不会强制对参数加密。 如果强制加密设置为 true，查询参数将只发送如果目标列已加密，并且针对连接还是的语句上启用始终加密。 使用此属性提供一层额外的安全，确保，驱动程序不会错误地发送数据到 SQL Server 以纯文本形式时这预计可以进行加密。

使用强制的加密设置都重载方法的 SQLServerPreparedStatement 和 SQLServerCallableStatement 方法详细信息，请参阅[始终加密 API 参考 JDBC 驱动程序](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)  

## <a name="controlling-the-performance-impact-of-always-encrypted"></a>控制始终加密的性能影响
由于始终加密是客户端加密技术，则会将大部分性能开销观察到在客户端，不是数据库中。 除加密和解密操作的成本，在客户端的性能开销的其他源是：
- 额外往返数据库以检索查询参数的元数据。
- 调用列主密钥存储以访问列主密钥。

本部分介绍在 Microsoft JDBC Driver for SQL Server 和可以如何控制上述两个因素对性能的影响的内置性能优化。

### <a name="controlling-round-trips-to-retrieve-metadata-for-query-parameters"></a>控制为了检索查询参数的元数据而往返的次数
如果为连接启用始终加密，默认情况下该驱动程序将调用[sys.sp_describe_parameter_encryption](../../relational-databases/system-stored-procedures/sp-describe-parameter-encryption-transact-sql.md)对于每个参数化查询，将查询语句 （不带任何参数值） 传递到 SQL Server。 [sys.sp_describe_parameter_encryption](../../relational-databases/system-stored-procedures/sp-describe-parameter-encryption-transact-sql.md)分析查询语句，以找出如果任何参数需要加密，并且如果是这样，为每个一个它返回与加密相关的信息，将允许要对参数值进行加密的驱动程序。 此行为确保掩蔽了客户端应用程序的高级别。 只要应用程序使用参数来传递面向加密的列于驱动程序的值，应用程序 （和应用程序开发人员） 不需要知道哪些查询在访问加密的列。

### <a name="setting-always-encrypted-at-the-query-level"></a>在查询级别设置始终加密
若要控制检索参数化查询的加密元数据的性能影响，你可以启用始终加密的单个查询而不是将其设置为连接。 这样可以确保该 sys.sp_describe_parameter_encryption 仅调用你知道具有面向加密的列的参数的查询。 但是，请注意，通过这样做减少的加密的透明性： 如果更改数据库列的加密属性时，你可能需要更改你的应用程序符合架构更改的代码。

若要控制单个查询的始终加密行为，你需要配置单独的语句对象通过传递枚举，SQLServerStatementColumnEncryptionSetting，指定将如何发送和接收时读取和写入数据适用于该特定语句的加密的列。 下面是一些有用的指导原则：
- 如果客户端应用程序通过数据库连接发送的大多数查询访问加密的列，使用这些指南：
    - 设置**columnEncryptionSetting**到连接字符串关键字**已启用**。
    - 设置 SQLServerStatementColumnEncryptionSetting.Disabled 不访问任何加密的列的单个查询。 此设置将禁止调用 sys.sp_describe_parameter_encryption 以及尝试解密结果集内的任何值。
    - 设置 SQLServerStatementColumnEncryptionSetting.ResultSet 的单个查询，没有任何参数需要加密但会从加密列检索数据。 此设置将禁止调用 sys.sp_describe_parameter_encryption 和参数加密。 查询将能够解密来自加密列的结果。
- 如果客户端应用程序通过数据库连接发送的大多数查询不访问加密的列，使用这些指南：
    - 设置**columnEncryptionSetting**到连接字符串关键字**禁用**。
    - 设置 SQLServerStatementColumnEncryptionSetting.Enabled 的单个查询，具有需要加密任何参数。 此设置将允许调用 sys.sp_describe_parameter_encryption 以及解密从加密列中检索到任何查询结果。
    - 没有任何参数需要进行加密，但从加密列检索数据的查询，设置 SQLServerStatementColumnEncryptionSetting.ResultSet。 此设置将禁止调用 sys.sp_describe_parameter_encryption 和参数加密。 查询将能够解密来自加密列的结果。

SQLServerStatementColumnEncryptionSetting 设置不能用于绕过加密以及获取纯文本数据的访问权限。 有关如何在一个语句上配置列加密的详细信息，请参阅[始终加密 API 参考 JDBC 驱动程序](../../connect/jdbc/always-encrypted-api-reference-for-the-jdbc-driver.md)。  

在下面的示例中，为数据库连接禁用始终加密。 查询的应用程序问题有一个面向未加密的 LastName 列的参数。 该查询从已加密的 SSN 和 BirthDate 列中检索数据。 在这种情况下，不需要调用 sys.sp_describe_parameter_encryption 来检索加密元数据。 但是，查询结果解密需要来启用，以便应用程序可以从两个加密列接收纯文本值。 SQLServerStatementColumnEncryptionSetting.ResultSet 设置用于确保。

```
// Assumes the same table definition as in Section "Retrieving and modifying data in encrypted columns"
// where only SSN and BirthDate columns are encrypted in the database.
String connectionUrl = "jdbc:sqlserver://localhost;databaseName=ae;user=sa;password=******;"
        + "keyStoreAuthentication=JavaKeyStorePassword;"
        + "keyStoreLocation=" + keyStoreLocation + ";"
        + "keyStoreSecret=******;";
SQLServerConnection connection = (SQLServerConnection) DriverManager.getConnection(connectionString);

String filterRecord="SELECT FirstName, LastName, SSN, BirthDate FROM " + tblName + " WHERE LastName = ?";
PreparedStatement selectStatement = connection.prepareStatement(
        filterRecord,
        ResultSet.TYPE_FORWARD_ONLY,
        ResultSet.CONCUR_READ_ONLY,
        connection.getHoldability(),
        SQLServerStatementColumnEncryptionSetting.ResultSetOnly);
selectStatement.setString(1, "Abel");
ResultSet rs = selectStatement.executeQuery();
while(rs.next()) {
    System.out.println("First name: " + rs.getString("FirstName"));
    System.out.println("Last name: " + rs.getString("LastName"));
    System.out.println("SSN: " + rs.getString("SSN"));
    System.out.println("Date of Birth: " + rs.getDate("BirthDate"));
}
rs.close();
selectStatement.close();
connection.close();
```

### <a name="column-encryption-key-caching"></a>列加密密钥缓存
若要减少的列主密钥存储的调用，以解密列加密密钥数，Microsoft JDBC Driver for SQL Server 将缓存在内存中的纯文本列加密密钥。 从数据库元数据收到加密的列加密密钥值之后, 该驱动程序首先尝试查找与加密密钥值相对应的纯文本列加密密钥。 驱动程序将调用密钥库包含列主密钥，仅当在缓存中找不到加密的列加密密钥值。

你可以在 SQLServerConnection 类中使用的 API，setColumnEncryptionKeyCacheTtl()，缓存中配置列加密密钥条目的生存时间值。 在缓存中的列加密密钥条目的默认生存时间值为两个小时。 若要关闭缓存，请使用值为 0。 若要设置的任何生存时间值，请使用以下 API:

```
SQLServerConnection.setColumnEncryptionKeyCacheTtl (int columnEncryptionKeyCacheTTL, TimeUnit unit)
```

例如，若要设置 10 分钟的生存时间值，使用：

```
SQLServerConnection.setColumnEncryptionKeyCacheTtl (10, TimeUnit.MINUTES)
```

天、 小时、 分钟或秒的时间单位为支持。  

## <a name="copying-encrypted-data-using-sqlserverbulkcopy"></a>复制使用 SQLServerBulkCopy 的加密的数据
SQLServerBulkCopy，你可以复制已加密，并不解密数据存储到另一个表的一个表中的数据。 为此：

- 请确保目标表的加密配置与源表的配置完全相同。 具体而言，这两个表必须具有相同的列加密，并且必须使用相同的加密类型和相同的加密密钥加密列。 如果任何目标列不同于其相应的源列已加密，你将无法解密后的复制操作的目标表中的数据。 数据将损坏。
- 不支持始终加密配置这两个数据库连接到源表和目标表。
- 设置 allowEncryptedValueModifications 选项。 有关详细信息，请参阅[使用 JDBC 驱动程序使用大容量复制](../../connect/jdbc/using-bulk-copy-with-the-jdbc-driver.md)。

> [!NOTE]
> 此选项可能会导致损坏数据库，因为 Microsoft JDBC Driver for SQL Server 不会检查确实已加密数据是否正确加密使用相同的加密指定 AllowEncryptedValueModifications 时要格外小心类型、 算法和密钥与目标列。

## <a name="see-also"></a>另请参阅
[始终加密（数据库引擎）](../../relational-databases/security/encryption/always-encrypted-database-engine.md)
