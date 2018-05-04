---
title: 使用始终加密的 PHP 驱动程序适用于 SQL Server |Microsoft 文档
ms.date: 01/08/2018
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: php
ms.suite: sql
ms.custom: ''
ms.technology:
- drivers
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
manager: mbarwin
ms.openlocfilehash: cc5ccc20d4a1a4324933ea64b9126f10df66dd26
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="using-always-encrypted-with-the-php-drivers-for-sql-server"></a>使用始终加密的 PHP 驱动程序适用于 SQL Server
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

## <a name="applicable-to"></a>适用于
 -   Microsoft Drivers 5.2 for PHP for SQL Server
 
## <a name="introduction"></a>简介

本文提供有关如何开发 PHP 应用程序使用信息[始终加密 （数据库引擎）](../../relational-databases/security/encryption/always-encrypted-database-engine.md)和[的 SQL Server PHP 驱动程序](../../connect/php/Microsoft-php-driver-for-sql-server.md)。

始终加密允许客户端应用程序对敏感数据进行加密，并且永远不向 SQL Server 或 Azure SQL 数据库显示该数据或加密密钥。 始终加密启用驱动程序，如 ODBC Driver for SQL Server，以透明方式进行加密和解密在客户端应用程序中的敏感数据。 该驱动程序自动确定哪些查询参数与敏感数据库列（使用始终加密进行保护）相对应，并对这些参数的值进行加密，然后再将数据传递到 SQL Server 或 Azure SQL 数据库。 同样，该驱动程序以透明方式对查询结果中从加密数据库列检索到的数据进行解密。 有关详细信息，请参阅 [始终加密（数据库引擎）](../../relational-databases/security/encryption/always-encrypted-database-engine.md)。 SQL Server PHP 驱动程序利用 ODBC Driver for SQL Server 来加密敏感数据。

## <a name="prerequisites"></a>必要條件

 -   在数据库中配置始终加密。 此配置涉及预配始终加密密钥和设置所选的数据库列的加密。 如果还没有配置了始终加密的数据库，请按照 [始终加密入门](../../relational-databases/security/encryption/always-encrypted-database-engine.md#getting-started-with-always-encrypted)中的说明操作。 具体而言，你的数据库应包含列主密钥 (CMK)、 列加密密钥 (CEK) 及包含一个或多个使用该 CEK 加密的列的表的元数据定义。
 -   确保在你的开发计算机上安装 ODBC Driver for SQL Server 17 或更高版本。 有关详细信息，请参阅[ODBC Driver for SQL Server](../../connect/odbc/microsoft-odbc-driver-for-sql-server.md)。

## <a name="enabling-always-encrypted-in-a-php-application"></a>在 PHP 应用程序中启用始终加密

启用面向加密的列中和的查询结果解密的参数加密的最简单方法是通过设置的值`ColumnEncryption`到连接字符串关键字`Enabled`。 SQLSRV 和 PDO_SQLSRV 驱动程序中启用始终加密的示例如下：

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

启用始终加密不足以加密或解密才能成功;你还需要确保：
 -   该应用程序查看任意列主密钥定义和查看任意列加密密钥定义数据库，所需的权限来访问有关数据库中的始终加密密钥的元数据。 有关详细信息，请参阅[数据库权限](../../relational-databases/security/encryption/always-encrypted-database-engine.md#database-permissions)。
 -   应用程序可以访问 CMK 保护查询加密列 Cek。 这是依赖于存储 CMK 密钥存储提供程序。 有关详细信息，请参阅[使用列主密钥存储](#working-with-column-master-key-stores)。

## <a name="retrieving-and-modifying-data-in-encrypted-columns"></a>检索和修改加密列中的数据

一旦在连接上启用始终加密，你可以使用标准 SQLSRV Api (请参阅[SQLSRV 驱动程序 API 参考](../../connect/php/sqlsrv-driver-api-reference.md)) 或 PDO_SQLSRV Api (请参阅[PDO_SQLSRV 驱动程序 API 参考](../../connect/php/pdo-sqlsrv-driver-reference.md)) 来检索或修改数据在加密的数据库列。 假设你的应用程序具有所需的数据库权限，并且可以访问列主密钥，驱动程序加密面向加密的列和解密从加密列，以透明方式为行为检索的数据的任何查询参数应用程序，就像未加密的列。

如果未启用始终加密，具有面向加密的列的参数的查询失败。 只要查询没有面向加密的列的参数，则仍可以从加密列检索数据。 但是，该驱动程序不会尝试任何解密和应用程序收到二进制加密的数据 （作为字节数组）。

下表总结了查询，具体取决于是否启用始终加密或不的行为：

|查询特征 |启用了始终加密以及应用程序可以访问密钥和密钥元数据 |启用了始终加密和应用程序无法访问密钥或密钥元数据 |禁用了始终加密 | |面向加密的列的参数。 |以透明方式加密参数值。 |错误 |错误 | |检索数据从加密列，而不面向加密的列的参数。 |从加密列的结果将是以透明方式解密。 应用程序收到的纯文本列的值。 |错误 |不解密从加密列的结果。 应用程序收到字节数组形式的加密的值。 |
 
以下示例说明如何检索和修改加密列中的数据。 这些示例假定具有以下架构的表。 SSN 和 BirthDate 列进行加密。
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

下面的示例演示如何使用 SQLSRV 和 PDO_SQLSRV 驱动程序以将行插入患者的表。 请注意以下几点：
 -   对于示例代码中的加密，没有什么特定的注意事项。 该驱动程序会自动检测并加密的 SSN 和 BirthDate 参数，面向加密的列的值。 此机制透明使向加密对应用程序。
 -   插入到数据库列，包括加密的列的值作为绑定参数传递。 时将值发送到非加密列，（尽管它强烈建议，因为它有助于防止 SQL 注入） 时使用的参数是可选的它是必要条件面向加密的列的值。 如果插入 SSN 或 BirthDate 列中的值作为查询语句中嵌入的文本传递，查询将失败，因为该驱动程序不会尝试加密或其他方式处理在查询中的文本。 因此，服务器会因为与加密列不兼容而拒绝它们。
 -   在插入时使用的绑定参数的值，则 SQL 类型与目标列的数据类型完全相同或支持其转换为目标列的数据类型必须传递到数据库。 此要求是因为始终加密支持若干种类型转换 (有关详细信息，请参阅[始终加密 （数据库引擎）](../../relational-databases/security/encryption/always-encrypted-database-engine.md))。 两个 PHP 驱动程序，SQLSRV 和 PDO_SQLSRV，每个具有一种机制来帮助用户确定的 SQL 类型的值。 因此，用户不必显式提供的 SQL 类型。
  -   SQLSRV 驱动程序，对于用户拥有两个选项：
   -   依赖于要确定并设置正确的 SQL 类型的 PHP 驱动程序。 在这种情况下，用户必须使用`sqlsrv_prepare`和`sqlsrv_execute`来执行参数化的查询。
   -   显式设置的 SQL 类型。
  -   对于 PDO_SQLSRV 驱动程序，用户没有显式设置参数的 SQL 类型的选项。 PDO_SQLSRV 驱动程序自动帮助用户确定 SQL 类型时将参数绑定。
 -   要确定 SQL 类型的驱动程序，适用于一些限制：
  -   SQLSRV 驱动程序：
   -   如果用户想要确定加密列的 SQL 类型的驱动程序，则用户必须使用`sqlsrv_prepare`和`sqlsrv_execute`。
   -   如果`sqlsrv_query`是首选，用户将负责指定所有参数的 SQL 类型。 指定的 SQL 类型必须包括字符串类型的字符串长度和小数位数和精度的十进制类型。
  -   PDO_SQLSRV 驱动程序：
   -   语句属性`PDO::SQLSRV_ATTR_DIRECT_QUERY`参数化查询中不支持。
   -   语句属性`PDO::ATTR_EMULATE_PREPARES`参数化查询中不支持。
   
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
 -   在 WHERE 子句来筛选 SSN 列需要用于传递使用绑定参数，以便该驱动程序可以以透明方式对其进行加密发送到服务器之前的值。
 -   执行带有绑定参数的查询，PHP 驱动程序将自动确定用户的 SQL 类型，除非用户在使用 SQLSRV 驱动程序时显式指定的 SQL 类型。
 -   程序打印的所有值都是以纯文本形式，因为该驱动程序以透明方式解密从 SSN 和 BirthDate 列中检索的数据。
 
注意： 查询可以执行相等比较对加密列才是确定性加密。 有关详细信息，请参阅[选择确定性或随机加密](../../relational-databases/security/encryption/always-encrypted-database-engine.md#selecting--deterministic-or-randomized-encryption)。

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

### <a name="ciphertext-data-retrieval-example"></a>已加密文本数据检索示例

如果未启用始终加密，只要查询没有面向加密列的参数，就仍然可以从加密列中检索数据。

下面的示例说明了从使用 SQLSRV 和 PDO_SQLSRV 驱动程序的加密列中检索二进制加密的数据。 请注意以下几点：
 -   连接字符串中未启用始终加密，因为查询 （该程序将值转换为字符串） 的字节数组形式返回 SSN 和 BirthDate 的加密的值。
 -   如果禁用始终加密，从加密列中检索数据的查询可以有参数，但前提是所有参数均不面向加密列。 按姓氏，未加密数据库中的以下查询筛选器。 如果查询按 SSN 或 BirthDate 进行筛选，查询将失败。
 
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

查询从 PHP 应用程序和几个指导说明了如何避免它们的加密的列时，本部分介绍常见错误的类别。

#### <a name="unsupported-data-type-conversion-errors"></a>不支持的数据类型转换错误

始终加密支持对加密数据类型进行若干种转换。 请参阅[始终加密 （数据库引擎）](../../relational-databases/security/encryption/always-encrypted-database-engine.md)有关受支持的类型转换的详细列表。 执行以下操作可避免数据类型转换错误：
 -   使用 SQLSRV 驱动程序与时`sqlsrv_prepare`和`sqlsrv_execute`自动确定 SQL 类型，以及列大小和参数的十进制数字个数。
 -   当使用 PDO_SQLSRV 驱动程序来执行查询时，还会自动确定具有列大小和数量的参数的十进制数字的 SQL 类型
 -   使用 SQLSRV 驱动程序与时`sqlsrv_query`来执行查询：
  -   支持从 SQL 类型转换为列的类型或参数的 SQL 类型也是完全与目标列的类型相同。
  -   精度和小数位数为面向的列的参数`decimal`和`numeric`精度和小数位数为目标列配置与 SQL Server 数据类型都将是相同。
  -   面向的列的参数的精度`datetime2`， `datetimeoffset`，或`time`SQL Server 数据类型不是大于修改目标列的查询中的目标列的精度。
 -   不使用 PDO_SQLSRV 语句特性`PDO::SQLSRV_ATTR_DIRECT_QUERY`或`PDO::ATTR_EMULATE_PREPARES`中参数化查询
 
#### <a name="errors-due-to-passing-plaintext-instead-of-encrypted-values"></a>由于传递纯文本而非加密值而发生的错误

任何面向加密的列的值必须发送到服务器之前加密。 尝试插入、 修改或筛选加密的列导致错误纯文本值。 若要防止此类错误，请确保：
 -   启用了始终加密 (在连接字符串中，设置`ColumnEncryption`关键字`Enabled`)。
 -   绑定参数用于将发送面向加密的列的数据。 下面的示例演示通过文本/常量对加密列 (SSN) 进行错误筛选的查询：
```
$query = "SELET [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE SSN='795-73-9838'";
```

## <a name="controlling-performance-impact-of-always-encrypted"></a>控制始终加密对性能的影响

由于始终加密是客户端加密技术，则会将大部分性能开销观察到在客户端，不是数据库中。 除加密和解密操作的成本，性能开销在客户端的其他来源是：
 -   额外往返数据库以检索查询参数的元数据。
 -   调用列主密钥存储以访问列主密钥。
 
### <a name="round-trips-to-retrieve-metadata-for-query-parameters"></a>若要检索查询参数的元数据的往返

如果为连接启用始终加密，ODBC 驱动程序将默认情况下，调用[sys.sp_describe_parameter_encryption](../../relational-databases/system-stored-procedures/sp-describe-parameter-encryption-transact-sql.md)对于每个参数化查询，将查询语句 （不带任何参数值） 传递到 SQL Server. 此存储的过程分析查询语句，以找出，如果任何参数需要加密，并且如果是这样，则返回的每个参数，以允许要加密的驱动程序与加密相关的信息。

由于 PHP 驱动程序允许用户将参数绑定在已准备的语句，而无需提供 SQL 中，键入，当将参数绑定支持始终加密的连接中，PHP 驱动程序调用[SQLDescribeParam](../../odbc/reference/syntax/sqldescribeparam-function.md)上若要获取 SQL 类型、 列大小和十进制数字的参数。 元数据然后用于调用[SQLBindParameter]( ../../odbc/reference/syntax/sqlbindparameter-function.md)。 这些额外`SQLDescribeParam`调用 ODBC 驱动程序具有已存储在客户端上的信息不需要额外往返访问数据库时`sys.sp_describe_parameter_encryption`调用。

前面的行为可确保高程度的透明性向客户端应用程序 （和应用程序开发人员） 不需要注意的哪些查询在访问加密的列，只要面向加密的列的值传递到中的驱动程序参数。

与 ODBC Driver for SQL Server 中，不同的级别语句/查询启用始终加密尚不支持的 PHP 驱动程序中。 

### <a name="column-encryption-key-caching"></a>列加密密钥缓存

为了减少对列主密钥存储调用，以解密列加密密钥 (CEK) 的数量，该驱动程序缓存在内存中的纯文本 Cek。 从数据库元数据收到加密 CEK (ECEK) 后, 的 ODBC 驱动程序首先尝试查找纯文本 CEK 对应于缓存中的加密密钥值。 该驱动程序调用包含 CMK，仅当在缓存中找不到相应的纯文本 CEK 的密钥存储。

注意： 在 ODBC Driver for SQL Server 中，缓存中的项被逐出在两小时超时后。 此行为意味着为给定 ECEK，驱动程序生存期的应用程序或每隔两小时联系一次的密钥存储，小者为准。

## <a name="working-with-column-master-key-stores"></a>使用列主密钥存储

若要加密或解密数据，该驱动程序必须获取配置为目标列 CEK。 Cek 存储在数据库元数据中的加密形式 (ECEKs)。 每个 CEK 具有相应 CMK 用来对其进行加密。 [数据库元数据](../../t-sql/statements/create-column-master-key-transact-sql.md)不会存储 CMK 本身; 它仅包含的密钥存储和密钥存储可用于查找 CMK 的信息的名称。

若要获取 ECEK 的纯文本值，该驱动程序，首先获取有关此 CEK 和其相应 CMK 的元数据，然后它使用此信息来联系包含 CMK 的密钥存储并请求，则以解密 ECEK。 与使用密钥存储提供程序的密钥存储通信的驱动程序。

对于 Microsoft Driver 5.2.0 for PHP for SQL Server，支持仅 Windows 证书存储区提供程序。 尚不支持两个其他 Keystore 提供程序支持的 ODBC 驱动程序 （Azure 密钥保管库和自定义密钥存储提供程序）。

### <a name="using-the-windows-certificate-store-provider"></a>使用 Windows 证书存储区提供程序

在 Windows 上的 SQL Server ODBC 驱动程序包括用于 Windows 证书存储中，名为的内置列主密钥存储提供程序`MSSQL_CERTIFICATE_STORE`。 （此提供程序不可用在 macOS 或 Linux。）与此提供程序，客户端计算机上本地存储 CMK 和不使用该驱动程序所必需的附加配置应用程序。 但是，应用程序必须具有访问证书和其私钥存储区中。 有关详细信息，请参阅 [创建并存储列主密钥 (Always Encrypted)](../../relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted.md)。

## <a name="limitations-of-the-php-drivers-when-using-always-encrypted"></a>使用始终加密时的 PHP 驱动程序的限制

SQLSRV 和 PDO_SQLSRV:
 -   Linux/MacOS 支持
  -   Windows 证书存储区提供程序并且该父级是 PHP 驱动程序当前支持仅 Keystore 提供程序不支持 Linux/MacOS
 -   强制参数加密
 -   启用始终加密级别的语句 
 
仅 SQLSRV:
 -   使用`sqlsrv_query`而无需指定 SQL 类型的绑定参数
 -   使用`sqlsrv_prepare`用于绑定参数的 SQL 语句的批处理中  
 
仅 PDO_SQLSRV:
 -   `PDO::SQLSRV_ATTR_DIRECT_QUERY` 在指定了参数化查询语句属性
 -   `PDO::ATTR_EMULATE_PREPARE` 在指定了参数化查询语句属性
 -   一批 SQL 语句中的绑定参数
 
PHP 驱动程序还将继承为 SQL Server 和数据库规定的 ODBC 驱动程序的限制。 请参阅[的 ODBC 驱动程序使用始终加密时限制](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md)和[始终加密功能详细信息](../../relational-databases/security/encryption/always-encrypted-database-engine.md#feature-details)。  
  
## <a name="see-also"></a>另请参阅  
[PHP SQL 驱动程序的编程指南](../../connect/php/programming-guide-for-php-sql-driver.md)
[SQLSRV 驱动程序 API 参考](../../connect/php/sqlsrv-driver-api-reference.md)  
[PDO_SQLSRV 驱动程序 API 参考](../../connect/php/pdo-sqlsrv-driver-reference.md)  
  
