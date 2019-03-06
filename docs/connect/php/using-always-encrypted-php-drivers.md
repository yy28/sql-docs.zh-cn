---
title: 在适用于 SQL Server 的 PHP 驱动程序中使用 Always Encrypted | Microsoft Docs
ms.date: 01/08/2018
ms.prod: sql
ms.prod_service: connectivity
ms.custom: ''
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
manager: mbarwin
ms.openlocfilehash: 5c82c32922712b377fd732b6745b1761e9f32a82
ms.sourcegitcommit: afc0c3e46a5fec6759fe3616e2d4ba10196c06d1
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2019
ms.locfileid: "55889998"
---
# <a name="using-always-encrypted-with-the-php-drivers-for-sql-server"></a>在适用于 SQL Server 的 PHP 驱动程序中使用 Always Encrypted
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

## <a name="applicable-to"></a>适用于
 -   Microsoft Drivers 5.2 for PHP for SQL Server
 
## <a name="introduction"></a>简介

本文提供有关如何开发 PHP 应用程序使用的信息[Always Encrypted （数据库引擎）](../../relational-databases/security/encryption/always-encrypted-database-engine.md)并[适用于 SQL Server PHP 驱动程序](../../connect/php/Microsoft-php-driver-for-sql-server.md)。

始终加密允许客户端应用程序对敏感数据进行加密，并且永远不向 SQL Server 或 Azure SQL 数据库显示该数据或加密密钥。 启用了 Always Encrypted 的驱动程序（如适用于 SQL Server 的 ODBC 驱动程序）在客户端应用程序中以透明方式对敏感数据进行加密和解密。 该驱动程序自动确定哪些查询参数与敏感数据库列（使用始终加密进行保护）相对应，并对这些参数的值进行加密，然后再将数据传递到 SQL Server 或 Azure SQL 数据库。 同样，该驱动程序以透明方式对查询结果中从加密数据库列检索到的数据进行解密。 有关详细信息，请参阅 [始终加密（数据库引擎）](../../relational-databases/security/encryption/always-encrypted-database-engine.md)。 SQL Server PHP 驱动程序使用 ODBC 驱动程序用于加密敏感数据的 SQL Server。

## <a name="prerequisites"></a>必备条件

 -   在数据库中配置始终加密。 此配置涉及为选定数据库列预配 Always Encrypted 密钥和设置加密。 如果还没有配置了始终加密的数据库，请按照 [始终加密入门](../../relational-databases/security/encryption/always-encrypted-database-engine.md#getting-started-with-always-encrypted)中的说明操作。 具体而言，数据库应包含列主密钥 (CMK)、 列加密密钥 (CEK)，以及包含一个或多个使用该 CEK 加密的列的表的元数据定义。
 -   请确保在开发计算机上安装 SQL Server 版本 17 或更高版本的 ODBC 驱动程序。 有关详细信息，请参阅[ODBC Driver for SQL Server](../../connect/odbc/microsoft-odbc-driver-for-sql-server.md)。

## <a name="enabling-always-encrypted-in-a-php-application"></a>在 PHP 应用程序中启用始终加密

若要对面向加密列的参数启用加密，以及对查询结果启用解密，最简单的方法是将 `ColumnEncryption` 连接字符串关键字的值设置为 `Enabled`。 SQLSRV 和 PDO_SQLSRV 驱动程序中启用始终加密示例如下：

SQLSRV:
```
$connectionInfo = array("Database"=>$databaseName, "UID"=>$uid, "PWD"=>$pwd, "ColumnEncryption"=>"Enabled");
$conn = sqlsrv_connect($server, $connectionInfo);
```

PDO_SQLSRV:
```
$connectionInfo = "Database = $databaseName; ColumnEncryption = Enabled;";
$conn = new PDO("sqlsrv:server = $server; $connectionInfo", $uid, $pwd);
```

启用始终加密是不够的加密或解密成功;此外需要确保：
 -   应用程序具有“查看任意列主密钥定义”和“查看任意列加密密钥定义”数据库权限，这是访问数据库中 Always Encrypted 密钥的相关元数据所必需的权限。 有关详细信息，请参阅[数据库的权限](../../relational-databases/security/encryption/always-encrypted-database-engine.md#database-permissions)。
 -   应用程序可以访问可保护查询加密列 Cek 的 CMK。 此要求是依赖于存储 CMK 的密钥存储提供程序。 有关详细信息，请参阅[使用的列主密钥存储](#working-with-column-master-key-stores)。

## <a name="retrieving-and-modifying-data-in-encrypted-columns"></a>检索和修改加密列中的数据

一旦在连接上启用始终加密，就可以使用标准 SQLSRV Api (请参阅[SQLSRV 驱动程序 API 参考](../../connect/php/sqlsrv-driver-api-reference.md)) 或 PDO_SQLSRV Api (请参阅[PDO_SQLSRV 驱动程序 API 参考](../../connect/php/pdo-sqlsrv-driver-reference.md)) 来检索或修改数据在加密的数据库列。 假设你的应用程序具有所需的数据库的权限，并且可以访问列主密钥，则驱动程序加密面向加密的列和解密从加密列，以透明方式行为检索到的数据的任何查询参数应用程序，如同未加密的列。

如果未启用 Always Encrypted，具有面向加密列的参数的查询将失败。 只要查询没有面向加密列的参数，就仍然可以从加密列中检索数据。 但是，该驱动程序不会尝试任何解密和应用程序收到二进制加密的数据 （作为字节数组）。

下表概述了查询的行为，具体取决于是否启用了 Always Encrypted：

|查询特征|启用了始终加密，并且应用程序可以访问密钥和密钥元数据|启用了始终加密，但应用程序无法访问密钥或密钥元数据|禁用了始终加密|
|---|---|---|---|
|面向加密的列的参数。|以透明方式加密参数值。|错误|错误|
|从加密列中检索数据，且没有面向加密列的参数。|以透明方式解密来自加密列的结果。 应用程序接收纯文本列的值。 |错误|不解密来自加密列的结果。 应用程序收到字节数组形式的加密值。|
 
以下示例说明如何检索和修改加密列中的数据。 这些示例假定具有以下架构的表。 SSN 和 BirthDate 列已加密。
```
CREATE TABLE [dbo].[Patients](
 [PatientId] [int] IDENTITY(1,1),
 [SSN] [char](11) COLLATE Latin1_General_BIN2
 ENCRYPTED WITH (ENCRYPTION_TYPE = DETERMINISTIC,
 ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256',
 COLUMN_ENCRYPTION_KEY = CEK1) NOT NULL,
 [FirstName] [nvarchar](50) NULL,
 [LastName] [nvarchar](50) NULL,
 [BirthDate] [date]
 ENCRYPTED WITH (ENCRYPTION_TYPE = RANDOMIZED,
 ALGORITHM = 'AEAD_AES_256_CBC_HMAC_SHA_256',
 COLUMN_ENCRYPTION_KEY = CEK1) NOT NULL
 PRIMARY KEY CLUSTERED ([PatientId] ASC) ON [PRIMARY])
 GO
```

### <a name="data-insertion-example"></a>数据插入示例

以下示例演示如何使用 SQLSRV 和 PDO_SQLSRV 驱动程序患者表中插入一行。 请注意以下几点：
 -   对于示例代码中的加密，没有什么特定的注意事项。 该驱动程序会自动检测并加密 SSN 和 BirthDate 参数，面向加密的列的值。 该机制使得加密操作对应用程序而言是透明的。
 -   插入到数据库列（包括加密列）中的值将作为绑定参数传递。 在将值发送到非加密列时，可以选择使用参数（强烈建议使用它，因为它有助于防止 SQL 注入），而在发送面向加密列的值时，必须使用该参数。 如果插入到 SSN 或 BirthDate 列中的值作为查询语句中嵌入的文本传递，查询会失败，因为该驱动程序不会尝试加密或其他处理查询中的文本。 因此，服务器会因为与加密列不兼容而拒绝它们。
 -   在插入时使用的绑定参数的值，则 SQL 类型与目标列的数据类型相同或者支持将其转换为目标列的数据类型必须传递到数据库。 此要求是因为 Always Encrypted 支持几个类型转换 (有关详细信息，请参阅[Always Encrypted （数据库引擎）](../../relational-databases/security/encryption/always-encrypted-database-engine.md))。 两个 PHP 驱动程序，SQLSRV 和 PDO_SQLSRV，每个都有一种机制来帮助用户确定值的 SQL 类型。 因此，用户不必显式提供的 SQL 类型。
  -   SQLSRV 驱动程序，用户有两个选项：
   -   依赖 PHP 驱动程序，以确定并设置正确的 SQL 类型。 在这种情况下，用户必须使用`sqlsrv_prepare`和`sqlsrv_execute`来执行参数化的查询。
   -   显式设置的 SQL 类型。
  -   PDO_SQLSRV 驱动程序，用户没有显式设置参数的 SQL 类型的选项。 PDO_SQLSRV 驱动程序会自动可帮助用户确定绑定参数时的 SQL 类型。
 -   有关驱动程序来确定 SQL 类型，有一些限制：
  -   SQLSRV 驱动程序：
   -   如果用户想要确定已加密列的 SQL 类型的驱动程序，则用户必须使用`sqlsrv_prepare`和`sqlsrv_execute`。
   -   如果`sqlsrv_query`是首选，用户负责指定所有参数的 SQL 类型。 指定的 SQL 类型必须包含字符串类型的字符串长度和小数位数和精度的十进制类型。
  -   PDO_SQLSRV 驱动程序：
   -   语句属性`PDO::SQLSRV_ATTR_DIRECT_QUERY`不支持参数化查询中。
   -   语句属性`PDO::ATTR_EMULATE_PREPARES`不支持参数化查询中。
   
SQLSRV 驱动程序和[sqlsrv_prepare](../../connect/php/sqlsrv-prepare.md):
```
// insertion into encrypted columns must use a parameterized query
$query = "INSERT INTO [dbo].[Patients] ([SSN], [FirstName], [LastName], [BirthDate]) VALUES (?, ?, ?, ?)";
$ssn = "795-73-9838";
$firstName = "Catherine";
$lastName = "Abel;
$birthDate = "1996-10-19";
$params = array($ssn, $firstName, $lastName, $birthDate);
// during sqlsrv_prepare, the driver determines the SQL types for each parameter and pass them to SQL server
$stmt = sqlsrv_prepare($conn, $query, $params);
sqlsrv_execute($stmt);
```

SQLSRV 驱动程序和[sqlsrv_query](../../connect/php/sqlsrv-query.md):
```
// insertion into encrypted columns must use a parameterized query
$query = "INSERT INTO [dbo].[Patients] ([SSN], [FirstName], [LastName], [BirthDate]) VALUES (?, ?, ?, ?)";
$ssn = "795-73-9838";
$firstName = "Catherine";
$lastName = "Abel";
$birthDate = "1996-10-19";
// need to provide the SQL types for ALL parameters  
// note the SQL types (including the string length) have to be the same at the column definition
$params = array(array(&$ssn, null, null, SQLSRV_SQLTYPE_CHAR(11)),
                array(&$firstName, null, null, SQLSRV_SQLTYPE_NVARCHAR(50)),
                array(&$lastName, null, null, SQLSRV_SQLTYPE_NVARCHAR(50)),
                array(&$birthDate, null, null, SQLSRV_SQLTYPE_DATE));
sqlsrv_query($conn, $query, $params);
```

PDO_SQLSRV 驱动程序和[pdo:: prepare](../../connect/php/pdo-prepare.md):
```
// insertion into encrypted columns must use a parameterized query
$query = "INSERT INTO [dbo].[Patients] ([SSN], [FirstName], [LastName], [BirthDate]) VALUES (?, ?, ?, ?)";
$ssn = "795-73-9838";
$firstName = "Catherine";
$lastName = "Able";
$birthDate = "1996-10-19";
// during PDO::prepare, the driver determines the SQL types for each parameter and pass them to SQL server
$stmt = $conn->prepare($query);
$stmt->bindParam(1, $ssn);
$stmt->bindParam(2, $firstName);
$stmt->bindParam(3, $lastName);
$stmt->bindParam(4, $birthDate);
$stmt->execute();
```

### <a name="plaintext-data-retrieval-example"></a>纯文本数据检索示例

下面的示例演示如何根据加密的值和从使用 SQLSRV 和 PDO_SQLSRV 驱动程序的加密列中检索纯文本数据的筛选数据。 请注意以下几点：
 -   WHERE 子句中用于筛选 SSN 列的值需要使用 bind 参数进行传递，以便驱动程序可以在将其发送到数据库之前以透明方式对其加密。
 -   执行带有绑定参数的查询，PHP 驱动程序将自动确定用户的 SQL 类型，除非用户明确指定的 SQL 类型时使用 SQLSRV 驱动程序。
 -   程序打印的所有值均为纯文本形式，因为驱动程序将以透明方式解密从 SSN 和 BirthDate 列中检索到的数据。
 
注意：仅当加密是确定性的查询可以对加密列执行相等比较。 有关详细信息，请参阅[选择确定性加密或随机加密](../../relational-databases/security/encryption/always-encrypted-database-engine.md#selecting--deterministic-or-randomized-encryption)。

SQLSRV:
```
// since SSN is an encrypted column, need to pass the value in the WHERE clause through bind parameter
$query = "SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE [SSN] = ?";
$ssn = "795-73-9838";
$stmt = sqlsrv_prepare($conn, $query, array(&$ssn));
// during sqlsrv_execute, the driver encrypts the ssn value and passes it to the database
sqlsrv_execute($stmt);
// fetch like usual
$row = sqlsrv_fetch_array($stmt);
```

PDO_SQLSRV:
```
// since SSN is an encrypted column, need to pass the value in the WHERE clause through bind parameter
$query = "SELET [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE [SSN] = ?";
$ssn = "795-73-9838";
$stmt = $conn->prepare($query);
$stmt->bindParam(1, $ssn);
// during PDOStatement::execute, the driver encrypts the ssn value and passes it to the database
$stmt->execute();
// fetch like usual
$row = $stmt->fetch();
```

### <a name="ciphertext-data-retrieval-example"></a>密码文本数据检索示例

如果未启用始终加密，只要查询没有面向加密列的参数，就仍然可以从加密列中检索数据。

以下示例说明了从使用 SQLSRV 和 PDO_SQLSRV 驱动程序的加密列中检索二进制加密的数据。 请注意以下几点：
 -   由于未在连接字符串中启用 Always Encrypted，因此，查询将以字节数组的形式返回 SSN 和 BirthDate 的加密值（程序会将值转换为字符串）。
 -   如果禁用始终加密，从加密列中检索数据的查询可以有参数，但前提是所有参数均不面向加密列。 以下查询按未在数据库中加密的 LastName 进行筛选。 如果查询按 SSN 或 BirthDate 进行筛选，则查询将失败。
 
SQLSRV:
```
$query = "SELET [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE [LastName] = ?";
$lastName = "Abel";
$stmt = sqlsrv_prepare($conn, $query, array(&$lastName));
sqlsrv_execute($stmt);
$row = sqlsrv_fetch_array($stmt);
```

PDO_SQLSRV:
```
$query = "SELET [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE [LastName] = ?";
$lastName = "Abel";
$stmt = $conn->prepare($query);
$stmt->bindParam(1, $lastName);
$stmt->execute();
$row = $stmt->fetch();
```

### <a name="avoiding-common-problems-when-querying-encrypted-columns"></a>避免查询加密列时的常见问题

本节介绍从 PHP 应用程序查询加密列时的常见错误类别，以及有关如何避免这些错误的若干指导。

#### <a name="unsupported-data-type-conversion-errors"></a>不支持的数据类型转换错误

始终加密支持对加密数据类型进行若干种转换。 有关受支持类型转换的详细列表，请参阅 [Always Encrypted（数据库引擎）](../../relational-databases/security/encryption/always-encrypted-database-engine.md)。 执行以下操作可避免数据类型转换错误：
 -   使用 SQLSRV 驱动程序使用时`sqlsrv_prepare`和`sqlsrv_execute`自动确定 SQL 类型，以及列的大小和参数的小数位数。
 -   当使用 PDO_SQLSRV 驱动程序来执行查询时，还会自动确定列大小和参数的小数位数的 SQL 类型
 -   使用 SQLSRV 驱动程序和时`sqlsrv_query`来执行查询：
  -   支持从 SQL 类型转换为列的类型或参数的 SQL 类型也是完全与目标列的类型相同。
  -   对于面向列的 `decimal` 和 `numeric` SQL Server 数据类型的参数，其精度和小数位数与为目标列配置的精度和小数位数相同。
  -   在用于修改目标列的查询中，面向列的 `datetime2`、`datetimeoffset` 或 `time` SQL Server 数据类型的参数的精度不大于目标列的精度。
 -   不使用 PDO_SQLSRV 语句属性`PDO::SQLSRV_ATTR_DIRECT_QUERY`或`PDO::ATTR_EMULATE_PREPARES`中参数化查询
 
#### <a name="errors-due-to-passing-plaintext-instead-of-encrypted-values"></a>由于传递纯文本而非加密值而发生的错误

需要发送到服务器之前将其加密任何面向加密的列的值。 尝试插入、修改或者按纯文本值筛选加密列会导致错误。 为防止发生此类错误，请确保：
 -   启用始终加密 (连接字符串中设置`ColumnEncryption`关键字`Enabled`)。
 -   使用 bind 参数发送面向加密列的数据。 下面的示例显示了按文本/常量对加密列 (SSN) 进行错误筛选的查询：
```
$query = "SELET [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE SSN='795-73-9838'";
```

## <a name="controlling-performance-impact-of-always-encrypted"></a>控制始终加密对性能的影响

Always Encrypted 是一种客户端加密技术，因此，大部分性能开销发生在客户端，而不是数据库中。 除加密和解密操作的成本之外，客户端上的其他性能开销来源包括：
 -   额外往返数据库以检索查询参数的元数据。
 -   调用列主密钥存储以访问列主密钥。
 
### <a name="round-trips-to-retrieve-metadata-for-query-parameters"></a>为了检索查询参数的元数据而往返的次数

如果为连接启用了 Always Encrypted，默认情况下，ODBC 驱动程序将为每个参数化查询调用 [sys.sp_describe_parameter_encryption](../../relational-databases/system-stored-procedures/sp-describe-parameter-encryption-transact-sql.md)，并将查询语句（不带任何参数值）传递到 SQL Server。 此存储的过程分析查询语句，以找出，如果任何参数需要加密，并且如果是这样，将返回每个参数，以允许要进行加密的驱动程序的与加密相关信息。

由于 PHP 驱动程序允许用户将参数绑定在已准备的语句，而无需提供 SQL 中，键入，当一个参数绑定支持始终加密的连接中，PHP 驱动程序调用[SQLDescribeParam](../../odbc/reference/syntax/sqldescribeparam-function.md)上若要获取 SQL 类型、 列大小和小数位数的参数。 元数据然后用于调用[SQLBindParameter]( ../../odbc/reference/syntax/sqlbindparameter-function.md)。 这些额外`SQLDescribeParam`ODBC 驱动程序已具有客户端上存储信息的调用不需要额外的往返访问数据库时`sys.sp_describe_parameter_encryption`调用。

上述行为可确保出现最高的客户端应用程序 （和应用程序开发人员） 的透明度级别不需要只要面向加密的列的值传递给驱动程序中需要注意的哪些查询在访问加密的列参数。

与不同的 SQL Server 的 ODBC 驱动程序，在语句/查询级别启用始终加密是尚不支持的 PHP 驱动程序中。 

### <a name="column-encryption-key-caching"></a>列加密密钥缓存

若要减少对列主密钥存储调用，以解密列加密密钥 (CEK) 数，该驱动程序将缓存在内存中的纯文本 Cek。 从数据库元数据收到加密的 CEK (ECEK) 之后, 的 ODBC 驱动程序首先尝试查找纯文本 CEK 相对应的缓存中的加密密钥值。 该驱动程序将调用包含仅当它不能在缓存中找到相应的纯文本 CEK 的 CMK 的密钥存储。

注意：在 SQL Server 的 ODBC 驱动程序，在两个小时的超时被收回缓存中的条目。 此行为意味着，对于给定的 ECEK，驱动程序将在生存期内的应用程序或每隔两小时联系一次的密钥存储，小者为准。

## <a name="working-with-column-master-key-stores"></a>使用列主密钥存储

若要加密或解密数据，该驱动程序需要获取为目标列配置的 CEK。 Cek 存储在数据库元数据中的加密形式 (ECEKs) 中。 每个 CEK 具有相应 CMK 用来对其进行加密。 [数据库元数据](../../t-sql/statements/create-column-master-key-transact-sql.md)不存储 CMK 本身; 它仅包含的密钥存储和密钥存储可用于查找 CMK 的信息的名称。

若要获取 ECEK 的纯文本值，该驱动程序，首先获取有关该 CEK 和其相应的 CMK，元数据，然后它使用此信息来联系包含 CMK 的密钥存储并请求该证书来解密 ECEK。 与使用密钥存储提供程序的密钥存储通信，该驱动程序。

对于 Microsoft Driver 5.3.0 for PHP for SQL Server，支持仅 Windows 证书存储区提供程序和 Azure 密钥保管库。 尚不支持其他密钥存储提供程序支持的 ODBC 驱动程序 （自定义密钥存储提供程序）。

### <a name="using-the-windows-certificate-store-provider"></a>使用 Windows 证书存储提供程序

Windows 上的 SQL Server ODBC 驱动程序包含名为 Windows 证书存储的内置列主密钥存储提供程序`MSSQL_CERTIFICATE_STORE`。 （此提供程序不是在 macOS 或 Linux 上可用。）与此提供程序，客户端计算机上本地存储 CMK 和应用程序无额外配置才可使用的驱动程序。 但是，应用程序必须具有对证书和私钥的访问的存储中。 有关详细信息，请参阅 [创建并存储列主密钥 (Always Encrypted)](../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)。

### <a name="using-azure-key-vault"></a>使用 Azure Key Vault

Azure Key Vault 提供了一种方法来存储加密密钥、 密码和其他机密，使用 Azure，可以用于始终加密的存储密钥。 SQL Server （17 和更高版本） 的 ODBC 驱动程序包括 Azure 密钥保管库的内置主密钥存储提供程序。 以下连接选项处理 Azure Key Vault 配置： `KeyStoreAuthentication`， `KeyStorePrincipalId`，和`KeyStoreSecret`。 
 -   `KeyStoreAuthentication` 可以采用两个可能的字符串值之一：`KeyVaultPassword`和`KeyVaultClientSecret`。 这些值控制与其他两个关键字一起使用哪种身份验证凭据。
 -   `KeyStorePrincipalId` 采用一个表示查找来访问 Azure Key Vault 的帐户的标识符的字符串。 
     -   如果`KeyStoreAuthentication`设置为`KeyVaultPassword`，然后`KeyStorePrincipalId`必须是与 Azure active Directory 用户的名称。
     -   如果`KeyStoreAuthentication`设置为`KeyVaultClientSecret`，然后`KeyStorePrincipalId`必须是应用程序客户端 id。
 -   `KeyStoreSecret` 采用一个字符串，表示凭据机密。 
     -   如果`KeyStoreAuthentication`设置为`KeyVaultPassword`，然后`KeyStoreSecret`必须是用户的密码。 
     -   如果 `KeyStoreAuthentication` 设置为 `KeyVaultClientSecret`，则 `KeyStoreSecret` 必须是与应用程序客户端 ID 相关联的应用程序机密。

所有三个选项中必须存在要使用 Azure 密钥保管库的连接字符串。 此外，`ColumnEncryption`必须设置为`Enabled`。 如果`ColumnEncryption`设置为`Disabled`但 Azure 密钥保管库选项都存在，该脚本将继续而不进行错误但会执行任何加密。

以下示例演示如何连接到 SQL Server 使用 Azure 密钥保管库。

SQLSRV:

使用 Azure Active Directory 帐户：
```
$connectionInfo = array("Database"=>$databaseName, "UID"=>$uid, "PWD"=>$pwd, "ColumnEncryption"=>"Enabled", "KeyStoreAuthentication"=>"KeyVaultPassword", "KeyStorePrincipalId"=>$AADUsername, "KeyStoreSecret"=>$AADPassword);
$conn = sqlsrv_connect($server, $connectionInfo);
```
使用 Azure 应用程序客户端 ID 和机密：
```
$connectionInfo = array("Database"=>$databaseName, "UID"=>$uid, "PWD"=>$pwd, "ColumnEncryption"=>"Enabled", "KeyStoreAuthentication"=>"KeyVaultClientSecret", "KeyStorePrincipalId"=>$applicationClientID, "KeyStoreSecret"=>$applicationClientSecret);
$conn = sqlsrv_connect($server, $connectionInfo);
```

PDO_SQLSRV:使用 Azure Active Directory 帐户：
```
$connectionInfo = "Database = $databaseName; ColumnEncryption = Enabled; KeyStoreAuthentication = KeyVaultPassword; KeyStorePrincipalId = $AADUsername; KeyStoreSecret = $AADPassword;";
$conn = new PDO("sqlsrv:server = $server; $connectionInfo", $uid, $pwd);
```
使用 Azure 应用程序客户端 ID 和机密：
```
$connectionInfo = "Database = $databaseName; ColumnEncryption = Enabled; KeyStoreAuthentication = KeyVaultClientSecret; KeyStorePrincipalId = $applicationClientID; KeyStoreSecret = $applicationClientSecret;";
$conn = new PDO("sqlsrv:server = $server; $connectionInfo", $uid, $pwd);
```

## <a name="limitations-of-the-php-drivers-when-using-always-encrypted"></a>PHP 驱动程序使用始终加密时的限制

SQLSRV 和 PDO_SQLSRV:
 -   Linux/macOS 不支持 Windows 证书存储区提供程序
 -   强制实施参数加密
 -   启用始终加密在语句级别 
 -   使用始终加密功能和非 UTF8 区域设置在 Linux 和 macOS （例如"en_US。ISO-8859-1")，除非已在系统上安装的代码页 1252年将 null 数据或空字符串插入到加密的 char （n） 列可能无法工作
 
仅 SQLSRV:
 -   使用`sqlsrv_query`而无需指定 SQL 类型的绑定参数
 -   使用`sqlsrv_prepare`为一批 SQL 语句中的绑定参数  
 
只有用于 PDO_SQLSRV:
 -   `PDO::SQLSRV_ATTR_DIRECT_QUERY` 参数化查询中指定的语句属性
 -   `PDO::ATTR_EMULATE_PREPARE` 参数化查询中指定的语句属性
 -   一批 SQL 语句中的绑定参数
 
PHP 驱动程序还将继承通过 ODBC 驱动程序为 SQL Server 和数据库规定的限制。 请参阅[的 ODBC 驱动程序使用 Always Encrypted 时限制](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md)并[始终加密功能的详细信息](../../relational-databases/security/encryption/always-encrypted-database-engine.md#feature-details)。  
  
## <a name="see-also"></a>另请参阅  
[PHP SQL 驱动程序的编程指南](../../connect/php/programming-guide-for-php-sql-driver.md)
[SQLSRV 驱动程序 API 参考](../../connect/php/sqlsrv-driver-api-reference.md)  
[PDO_SQLSRV 驱动程序 API 参考](../../connect/php/pdo-sqlsrv-driver-reference.md)  
  
