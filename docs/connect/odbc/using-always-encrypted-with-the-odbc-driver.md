---
title: 在适用于 SQL Server 的 ODBC 驱动程序中使用 Always Encrypted | Microsoft Docs
ms.custom: ''
ms.date: 09/01/2018
ms.prod: sql
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 02e306b8-9dde-4846-8d64-c528e2ffe479
ms.author: v-chojas
manager: craigg
author: MightyPen
ms.openlocfilehash: dfe1777044234ec43c13f738fa1b0de896f96616
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47828265"
---
# <a name="using-always-encrypted-with-the-odbc-driver-for-sql-server"></a>在适用于 SQL Server 的 ODBC 驱动程序中使用 Always Encrypted
[!INCLUDE[Driver_ODBC_Download](../../includes/driver_odbc_download.md)]

### <a name="applicable-to"></a>适用于

- ODBC Driver 13.1 for SQL Server
- ODBC Driver 17 for SQL Server

### <a name="introduction"></a>简介

本文提供有关如何开发使用 ODBC 应用程序信息[Always Encrypted （数据库引擎）](../../relational-databases/security/encryption/always-encrypted-database-engine.md)并[适用于 SQL Server 的 ODBC 驱动程序](../../connect/odbc/microsoft-odbc-driver-for-sql-server.md)。

始终加密允许客户端应用程序对敏感数据进行加密，并且永远不向 SQL Server 或 Azure SQL 数据库显示该数据或加密密钥。 启用了 Always Encrypted 的驱动程序（例如适用于 SQL Server 的 ODBC 驱动程序）通过在客户端应用程序中以透明方式对敏感数据进行加密和解密来实现此目标。 该驱动程序自动确定哪些查询参数与敏感数据库列（使用始终加密进行保护）相对应，并对这些参数的值进行加密，然后再将数据传递到 SQL Server 或 Azure SQL 数据库。 同样，该驱动程序以透明方式对查询结果中从加密数据库列检索到的数据进行解密。 有关详细信息，请参阅 [始终加密（数据库引擎）](../../relational-databases/security/encryption/always-encrypted-database-engine.md)。

### <a name="prerequisites"></a>必备条件

在数据库中配置始终加密。 这涉及为选定数据库列预配始终加密密钥和设置加密。 如果还没有配置了始终加密的数据库，请按照 [始终加密入门](../../relational-databases/security/encryption/always-encrypted-database-engine.md#getting-started-with-always-encrypted)中的说明操作。 具体而言，数据库应包含列主密钥 (CMK)、 列加密密钥 (CEK)，以及包含一个或多个使用该 CEK 加密的列的表的元数据定义。

### <a name="enabling-always-encrypted-in-an-odbc-application"></a>在 ODBC 应用程序中启用始终加密

若要启用参数加密和解密加密的结果集列的最简单方法是通过设置的值`ColumnEncryption`到连接字符串关键字**已启用**。 以下是启用 Always Encrypted 的连接字符串示例：

```
SQLWCHAR *connString = L"Driver={ODBC Driver 13 for SQL Server};Server={myServer};Trusted_Connection=yes;ColumnEncryption=Enabled;";
```

可能还会启用了始终加密使用的相同的键和值 （该值将重写通过设置连接字符串，如果存在），在 DSN 配置或以编程方式使用`SQL_COPT_SS_COLUMN_ENCRYPTION`预连接属性。 将其设置这种方式重写中的连接字符串或 DSN 设置的值：

```
 SQLSetConnectAttr(hdbc, SQL_COPT_SS_COLUMN_ENCRYPTION, (SQLPOINTER)SQL_COLUMN_ENCRYPTION_ENABLE, 0);
```

为连接启用后，可能会为单个查询调整的始终加密行为。 请参阅[控制性能影响的 Always Encrypted](#controlling-the-performance-impact-of-always-encrypted)下面有关详细信息。

请注意，启用始终加密是不够的加密或解密成功;此外需要确保：

- 应用程序具有 *查看任意列主密钥定义* 和 *查看任意列加密密钥定义* 数据库权限，这是访问数据库中始终加密密钥的相关元数据所必需的权限。 有关详细信息，请参阅[数据库权限](../../relational-databases/security/encryption/always-encrypted-database-engine.md#database-permissions)。

- 应用程序可以访问保护查询加密列 Cek 的 CMK。 这是依赖于存储 CMK 的密钥存储提供程序。 请参阅[使用的列主密钥存储](#working-with-column-master-key-stores)有关详细信息。

### <a name="retrieving-and-modifying-data-in-encrypted-columns"></a>检索和修改加密列中的数据

一旦在连接上启用始终加密，就可以使用标准 ODBC Api (请参阅[ODBC 示例代码](https://code.msdn.microsoft.com/windowsapps/ODBC-sample-191624ae/sourcecode?fileId=51137&pathId=1980325953)或[ODBC 程序员参考](https://msdn.microsoft.com/library/ms714177(v=vs.85).aspx)) 来检索或修改加密的数据库列中的数据。 假设你的应用程序具有所需数据库权限和可以访问列主密钥，驱动程序将对任何查询参数，它面向加密的列并解密从加密列，以透明方式行为对检索到的数据进行加密应用程序，如同未加密的列。

如果未启用 Always Encrypted，具有面向加密列的参数的查询将失败。 只要查询没有面向加密列的参数，就仍然可以从加密列中检索数据。 但是，该驱动程序将不会尝试任何解密并且应用程序将收到二进制加密的数据 （作为字节数组）。

下表概述了查询的行为，具体取决于是否启用了 Always Encrypted：

|查询特征 | 启用了始终加密，并且应用程序可以访问密钥和密钥元数据|启用了始终加密，但应用程序无法访问密钥或密钥元数据 | 禁用了始终加密|
|:---|:---|:---|:---|
| 面向加密的列的参数。 | 以透明方式加密参数值。 | 错误 | 错误|
| 从加密列中检索数据，且没有面向加密列的参数。| 以透明方式解密来自加密列的结果。 应用程序接收纯文本列的值。 | 错误 | 不解密来自加密列的结果。 应用程序收到字节数组形式的加密值。

以下示例说明如何检索和修改加密列中的数据。 这些示例假定具有以下架构的表。 请注意，SSN 和 BirthDate 列已加密。

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
 PRIMARY KEY CLUSTERED ([PatientId] ASC) ON [PRIMARY] )
 GO
```

#### <a name="data-insertion-example"></a>数据插入示例

此示例向 Patients 表插入一行。 请注意以下事项：

- 对于示例代码中的加密，没有什么特定的注意事项。 该驱动程序会自动检测并加密 SSN 和日期参数，面向加密的列的值。 这使得加密操作对应用程序而言是透明的。

- 插入到数据库列（包括加密列）中的值将作为绑定参数传递（请参阅 [SQLBindParameter 函数](https://msdn.microsoft.com/library/ms710963(v=vs.85).aspx)）。 在将值发送到非加密列时，可以选择使用参数（强烈建议使用它，因为它有助于防止 SQL 注入），而在发送面向加密列的值时，必须使用该参数。 如果插入到 SSN 或 BirthDate 列中的值作为查询语句中嵌入的文本传递，查询会失败，因为该驱动程序不会尝试加密或其他处理查询中的文本。 因此，服务器会因为与加密列不兼容而拒绝它们。

- 插入到 SSN 列的参数的 SQL 类型设置为 SQL_CHAR，映射到**char** SQL Server 数据类型 (`rc = SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, 11, 0, (SQLPOINTER)SSN, 0, &cbSSN);`)。 如果参数的类型设置为 SQL_WCHAR，映射到**nchar**，查询将失败，因为始终加密不支持从加密的 nchar 值为加密的 char 值的服务器端转换。 请参阅[ODBC 程序员参考-附录 d： 数据类型](https://msdn.microsoft.com/library/ms713607.aspx)有关的数据类型映射信息。

```
    SQL_DATE_STRUCT date;
    SQLLEN cbdate;   // size of date structure  

    SQLCHAR SSN[12];
    strcpy_s((char*)SSN, _countof(SSN), "795-73-9838");

    SQLWCHAR* firstName = L"Catherine";
    SQLWCHAR* lastName = L"Abel";
    SQLINTEGER cbSSN = SQL_NTS, cbFirstName = SQL_NTS, cbLastName = SQL_NTS;

    // Initialize the date structure  
    date.day = 10;
    date.month = 9;
    date.year = 1996;

    // Size of structures   
    cbdate = sizeof(SQL_DATE_STRUCT);

    SQLRETURN rc = 0;

    string queryText = "INSERT INTO [dbo].[Patients] ([SSN], [FirstName], [LastName], [BirthDate]) VALUES (?, ?, ?, ?) ";

    rc = SQLPrepare(hstmt, (SQLCHAR *)queryText.c_str(), SQL_NTS);

    //SSN
    rc = SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, 11, 0, (SQLPOINTER)SSN, 0, &cbSSN);
    //FirstName
    rc = SQLBindParameter(hstmt, 2, SQL_PARAM_INPUT, SQL_C_WCHAR, SQL_WCHAR, 50, 0, (SQLPOINTER)firstName, 0, &cbFirstName);
    //LastName
    rc = SQLBindParameter(hstmt, 3, SQL_PARAM_INPUT, SQL_C_WCHAR, SQL_WCHAR, 50, 0, (SQLPOINTER)lastName, 0, &cbLastName);
    //BirthDate
    rc = SQLBindParameter(hstmt, 4, SQL_PARAM_INPUT, SQL_C_TYPE_DATE, SQL_TYPE_DATE, 10, 0, (SQLPOINTER)&date, 0, &cbdate);

    rc = SQLExecute(hstmt);
```

#### <a name="plaintext-data-retrieval-example"></a>纯文本数据检索示例

以下示例演示如何根据加密值筛选数据，以及从加密列中检索纯文本数据。 请注意以下事项：

- WHERE 子句中用于筛选 SSN 列的值需要使用 SQLBindParameter 进行传递，以便驱动程序可以在将其发送到数据库之前以透明方式对其加密。

- 程序打印的所有值均为纯文本形式，因为驱动程序将以透明方式解密从 SSN 和 BirthDate 列中检索到的数据。

> [!NOTE]
> 仅当加密是确定性的查询可以对加密列执行相等比较。 有关详细信息，请参阅[选择确定性加密或随机加密](../../relational-databases/security/encryption/always-encrypted-database-engine.md#selecting--deterministic-or-randomized-encryption)。

```
SQLCHAR SSN[12];
strcpy_s((char*)SSN, _countof(SSN), "795-73-9838");

SQLWCHAR* firstName = L"Catherine";
SQLWCHAR* lastName = L"Abel";
SQLINTEGER cbSSN = SQL_NTS, cbFirstName = SQL_NTS, cbLastName = SQL_NTS;

SQLRETURN rc = 0;
string empty = "";
string queryText = "SELECT [SSN], [FirstName], [LastName], [BirthDate] " + empty +
    "FROM  [dbo].[Patients]" +
    "WHERE " +
    "[SSN] = ? ";

rc = SQLPrepare(hstmt, (SQLCHAR *)queryText.c_str(), SQL_NTS);

//SSN
rc = SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, 11, 0, (SQLPOINTER)SSN, 0, &cbSSN);

rc = SQLExecute(hstmt);
HandleDiagnosticRecord(hstmt, SQL_HANDLE_STMT, rc);

SQL_DATE_STRUCT dateVal;
SQLWCHAR firstNameVal[50];
SQLWCHAR lastNameVal[50];
SQLCHAR SSNVal[12];
SQLLEN cbdate;   // size of date structure  

int rowcount = 0;
while (SQL_SUCCEEDED(SQLFetch(hstmt)))
{
    rowcount++;
    SQLGetData(hstmt, 1, SQL_C_CHAR, &SSNVal, 11, &cbSSN);
    SQLGetData(hstmt, 2, SQL_C_WCHAR, &firstNameVal, 50, &cbFirstName);
    SQLGetData(hstmt, 3, SQL_C_WCHAR, &lastNameVal, 50, &cbLastName);
    SQLGetData(hstmt, 4, SQL_C_TYPE_DATE, &dateVal, 10, &cbdate);        
}
```

#### <a name="ciphertext-data-retrieval-example"></a>密码文本数据检索示例

如果未启用始终加密，只要查询没有面向加密列的参数，就仍然可以从加密列中检索数据。

以下示例说明如何从加密列中检索二进制加密数据。 请注意以下事项：

- 由于未在连接字符串中启用始终加密，因此，查询将以字节数组的形式返回 SSN 和 BirthDate 的加密值（程序会将值转换为字符串）。
- 如果禁用始终加密，从加密列中检索数据的查询可以有参数，但前提是所有参数均不面向加密列。 上述查询按未在数据库中加密的 LastName 进行筛选。 如果查询按 SSN 或 BirthDate 进行筛选，则将失败。


```
SQLCHAR SSN[12];
strcpy_s((char*)SSN, _countof(SSN), "795-73-9838");

SQLWCHAR* firstName = L"Catherine";
SQLWCHAR* lastName = L"Abel";
SQLINTEGER cbSSN = SQL_NTS, cbFirstName = SQL_NTS, cbLastName = SQL_NTS;

SQLRETURN rc = 0;
string empty = "";
string queryText = "SELECT [SSN], [FirstName], [LastName], [BirthDate] " + empty +
    "FROM  [dbo].[Patients]" +
    "WHERE " +
    "[LastName] = ?";

rc = SQLPrepare(hstmt, (SQLCHAR *)queryText.c_str(), SQL_NTS);

//LastName
rc = SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_WCHAR, SQL_WCHAR, 50, 0, (SQLPOINTER)lastName, 0, &cbLastName);

rc = SQLExecute(hstmt);
HandleDiagnosticRecord(hstmt, SQL_HANDLE_STMT, rc);

SQL_DATE_STRUCT dateVal;
SQLWCHAR firstNameVal[50];
SQLWCHAR lastNameVal[50];
SQLCHAR SSNVal[12];
SQLLEN cbdate;   // size of date structure  

int rowcount = 0;
while (SQL_SUCCEEDED(SQLFetch(hstmt)))
{
    rowcount++;
    SQLGetData(hstmt, 1, SQL_C_CHAR, &SSNVal, 11, &cbSSN);
    SQLGetData(hstmt, 2, SQL_C_WCHAR, &firstNameVal, 50, &cbFirstName);
    SQLGetData(hstmt, 3, SQL_C_WCHAR, &lastNameVal, 50, &cbLastName);
    SQLGetData(hstmt, 4, SQL_C_TYPE_DATE, &dateVal, 10, &cbdate);        
}
```

#### <a name="avoiding-common-problems-when-querying-encrypted-columns"></a>避免查询加密列时的常见问题

本节介绍从 ODBC 应用程序查询加密列时的常见错误类别，以及有关如何避免这些错误的若干指导。

##### <a name="unsupported-data-type-conversion-errors"></a>不支持的数据类型转换错误

始终加密支持对加密数据类型进行若干种转换。 有关受支持类型转换的详细列表，请参阅 [Always Encrypted（数据库引擎）](../../relational-databases/security/encryption/always-encrypted-database-engine.md)。 若要避免数据类型转换错误，请确保具有面向加密的列的参数使用 SQLBindParameter 时观察到以下几点：

- 支持从 SQL 类型转换为列的类型或参数的 SQL 类型也是完全与目标列的类型相同。

- 对于面向列的 `decimal` 和 `numeric` SQL Server 数据类型的参数，其精度和小数位数与为目标列配置的精度和小数位数相同。

- 在用于修改目标列的查询中，面向列的 `datetime2`、`datetimeoffset` 或 `time` SQL Server 数据类型的参数的精度不大于目标列的精度。  

##### <a name="errors-due-to-passing-plaintext-instead-of-encrypted-values"></a>由于传递纯文本而非加密值而发生的错误

需要发送到服务器之前将其加密任何面向加密的列的值。 尝试插入、修改或者按纯文本值筛选加密列将导致错误。 为防止发生此类错误，请确保：

- 启用始终加密 (在 DSN 中，连接字符串中之前连接通过设置`SQL_COPT_SS_COLUMN_ENCRYPTION`的特定连接的连接属性或`SQL_SOPT_SS_COLUMN_ENCRYPTION`特定语句的语句属性)。

- 使用 SQLBindParameter 发送面向加密列的数据。 以下示例显示了一个查询，该查询按文本/常量对加密列 (SSN) 进行错误筛选，而不是将文本作为参数传递到 SQLBindParameter。

```
string queryText = "SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE SSN='795-73-9838'";
```

### <a name="precautions-when-using-sqlsetpos-and-sqlmoreresults"></a>使用 SQLSetPos 和 SQLMoreResults 时的注意事项

#### <a name="sqlsetpos"></a>SQLSetPos

`SQLSetPos` API 允许应用程序更新中使用的绑定与 SQLBindCol 和以前插入的行提取的数据缓冲区了结果集的行。 由于已加密的固定长度类型的非对称的填充行为，就可以在行中的其他列上执行更新时意外更改这些列的数据。 AE，具有固定的长度字符值将填充值是否小于缓冲区大小。

若要缓解此问题，请使用`SQL_COLUMN_IGNORE`标志来忽略将不会更新作为的一部分的列`SQLBulkOperations`以及何时使用`SQLSetPos`游标基于更新。  应忽略不会被直接修改应用程序的所有列，同时性能并避免截断的列绑定到一个缓冲区*较小*比其实际 (DB) 大小。 有关详细信息，请参阅[SQLSetPos 函数引用](https://msdn.microsoft.com/library/ms713507(v=vs.85).aspx)。

#### <a name="sqlmoreresults--sqldescribecol"></a>SQLMoreResults & SQLDescribeCol

应用程序可以调用[SQLDescribeCol](https://msdn.microsoft.com/library/ms716289(v=vs.85).aspx)在预定义语句中返回有关列的元数据。  启用始终加密后，调用`SQLMoreResults`*之前*调用`SQLDescribeCol`导致[sp_describe_first_result_set](../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md)调用，这不会正确返回纯文本加密列的元数据。 若要避免此问题，请调用`SQLDescribeCol`上预定义语句*之前*调用`SQLMoreResults`。

## <a name="controlling-the-performance-impact-of-always-encrypted"></a>控制 Always Encrypted 对性能的影响

Always Encrypted 是一种客户端加密技术，因此，大部分性能开销发生在客户端，而不是数据库中。 除加密和解密操作的成本之外，客户端上的其他性能开销来源包括：

- 额外往返数据库以检索查询参数的元数据。

- 调用列主密钥存储以访问列主密钥。

本节介绍适用于 SQL Server 的 ODBC 驱动程序中的内置性能优化，以及如何控制上述两个因素对性能的影响。

### <a name="controlling-round-trips-to-retrieve-metadata-for-query-parameters"></a>控制为了检索查询参数的元数据而往返的次数

如果为连接启用了 Always Encrypted，默认情况下，驱动程序将为每个参数化查询调用 [sys.sp_describe_parameter_encryption](../../relational-databases/system-stored-procedures/sp-describe-parameter-encryption-transact-sql.md)，并将查询语句（不带任何参数值）传递到 SQL Server。 此存储的过程分析查询语句，以找出，如果任何参数需要加密，并且如果是这样，将返回每个参数，以允许要进行加密的驱动程序的与加密相关信息。 以上行为可确保高级别的客户端应用程序的透明度： 应用程序 （和应用程序开发人员） 不需要知道哪些查询在访问加密的列，只要面向加密的列的值传递给参数中的驱动程序。

### <a name="per-statement-always-encrypted-behavior"></a>每个语句始终加密行为

若要控制检索参数化查询的加密元数据的性能影响，可以更改单个查询的始终加密行为，如果在连接上启用了。 这样一来，您可以确保`sys.sp_describe_parameter_encryption`仅针对你知道的查询具有面向加密的列的参数调用。 但请注意，这样做会降低加密的透明度：如果加密数据库中的其他列，可能需要更改应用程序代码，使其与架构更改保持一致。

若要控制语句的始终加密行为，请调用 SQLSetStmtAttr 设置`SQL_SOPT_SS_COLUMN_ENCRYPTION`语句属性设置为以下值之一：

|ReplTest1|描述|
|-|-|
|`SQL_CE_DISABLED` (0)|禁用了始终加密语句|
|`SQL_CE_RESULTSETONLY` (1)|仅解密。 结果集和返回值解密的、 和未加密的参数|
|`SQL_CE_ENABLED` (3) | 始终加密已启用并使用参数和结果|

从使用始终加密的连接创建的新语句句柄启用到 SQL_CE_ENABLED 的默认设置。 创建从与之连接禁用默认为 SQL_CE_DISABLED （和不能在其上启用始终加密。）

如果大多数查询的客户端应用程序访问加密的列，建议执行以下操作：

- 将 `ColumnEncryption` 连接字符串关键字设置为 `Enabled`。

- 设置`SQL_SOPT_SS_COLUMN_ENCRYPTION`属性为`SQL_CE_DISABLED`不访问任何加密的列的语句。 这将禁用这两个调用`sys.sp_describe_parameter_encryption`以及尝试解密结果中的任何值设置。
    
- 设置`SQL_SOPT_SS_COLUMN_ENCRYPTION`属性为`SQL_CE_RESULTSETONLY`上没有任何参数需要加密但会从加密列检索数据的语句。 这将禁用调用`sys.sp_describe_parameter_encryption`和参数加密。 包含加密的列的结果将继续进行解密。

## <a name="always-encrypted-security-settings"></a>始终加密的安全设置

### <a name="force-column-encryption"></a>强制列加密

若要强制实施参数的加密，请设置`SQL_CA_SS_FORCE_ENCRYPT`实现参数描述符 (IPD) 字段通过 SQLSetDescField 函数调用。 一个非零值会导致驱动程序相关联的参数返回加密元数据，则返回错误。

```
SQLHDESC ipd;
SQLGetStmtAttr(hStmt, SQL_ATTR_IMP_PARAM_DESC, &ipd, 0, 0);
SQLSetDescField(ipd, paramNum, SQL_CA_SS_FORCE_ENCRYPT, (SQLPOINTER)TRUE, SQL_IS_SMALLINT);   
```

如果 SQL Server 告知驱动程序参数不需加密，则使用该参数的查询会失败。 这提供针对安全攻击的额外保护，这些攻击涉及受损 SQL Server 向客户端提供不正确的加密元数据，这可能会导致数据泄漏。

### <a name="column-encryption-key-caching"></a>列加密密钥缓存

若要减少调用列主密钥存储解密列加密密钥的次数，该驱动程序将缓存在内存中的纯文本 Cek。 CEK 缓存是全局的驱动程序，而不与任何一个连接相关联。 从数据库元数据收到 ECEK 之后, 该驱动程序首先尝试查找纯文本 CEK 相对应的缓存中的加密密钥值。 该驱动程序将调用包含仅当它不能在缓存中找到相应的纯文本 CEK 的 CMK 的密钥存储。

> [!NOTE]
> 在 SQL Server 的 ODBC 驱动程序，在两个小时的超时被收回缓存中的条目。 这意味着，对于给定的 ECEK，驱动程序将在生存期内的应用程序或每隔两小时联系一次的密钥存储，小者为准。

适用于 SQL Server ODBC 驱动程序 17.1 从开始，CEK 缓存超时可以调整使用`SQL_COPT_SS_CEKCACHETTL`连接属性，指定的 CEK 将保留在缓存中的秒数。 由于缓存的全局特性，可以从任何有效的驱动程序的连接句柄调整此属性。 当的缓存 TTL 减小时，现有 Cek 将超过新的 TTL 还被逐出。 如果该值为 0，会缓存没有 Cek。

### <a name="trusted-key-paths"></a>可信密钥路径

从 SQL Server 的 ODBC 驱动程序 17.1`SQL_COPT_SS_TRUSTEDCMKPATHS`连接属性允许应用程序，以便始终加密操作仅使用指定的 Cmk，由其密钥路径标识列表。 默认情况下，此属性为 NULL，这意味着该驱动程序接受任何注册表项路径。 若要使用此功能，设置`SQL_COPT_SS_TRUSTEDCMKPATHS`以指向列出了允许的密钥路径的 null 分隔、 以 null 终止宽字符字符串。 在加密或解密操作使用的连接句柄在其设置它---在其驱动程序将检查指定的服务器元数据的 CMK 路径不区分大小写是否在此期间，此属性指向的内存必须保持有效列表。 如果 CMK 路径不在列表中，则操作将失败。 应用程序可以更改此属性指向，而无需再次设置该属性更改受信任的 Cmk，其列表的内存的内容。

## <a name="working-with-column-master-key-stores"></a>使用列主密钥存储

若要加密或解密数据，该驱动程序需要获取为目标列配置的 CEK。 Cek 存储在数据库元数据中的加密形式 (ECEKs) 中。 每个 CEK 具有相应 CMK 用来对其进行加密。 [数据库元数据](../../t-sql/statements/create-column-master-key-transact-sql.md)不存储 CMK 本身; 它仅包含的密钥存储和密钥存储可用于查找 CMK 的信息的名称。

若要获取 ECEK 的纯文本值，该驱动程序，首先获取有关该 CEK 和其相应的 CMK，元数据，然后它使用此信息与密钥存储包含 CMK 联系并请求该证书来解密 ECEK。 该驱动程序与使用密钥存储提供程序密钥存储进行通信。

### <a name="built-in-keystore-providers"></a>内置密钥存储提供程序

SQL Server 的 ODBC 驱动程序附带以下内置密钥存储提供程序：

| 名称 | 描述 | 提供程序 （元数据） 的名称 |可用性|
|:---|:---|:---|:---|
|Azure Key Vault |在 Azure Key Vault 中存储 Cmk | `AZURE_KEY_VAULT` |Windows、 macOS、 Linux|
|Windows 证书存储|Windows 密钥存储在本地存储 Cmk| `MSSQL_CERTIFICATE_STORE`|Windows|

- 你（或你的 DBA）需要确保列主密钥元数据中配置的提供程序名称正确，并且列主密钥路径符合对于给定提供程序的密钥路径格式。 建议你使用诸如 SQL Server Management Studio 之类的工具来配置密钥，这类工具在发出 [CREATE COLUMN MASTER KEY (Transact-SQL)](../../t-sql/statements/create-column-master-key-transact-sql.md) 语句时会自动生成有效的提供程序名称和密钥路径。

- 需要确保应用程序可以访问密钥存储中的密钥。 这可能涉及向应用程序授予对密钥和/或密钥存储的访问权限（具体取决于密钥存储），或执行其他特定于密钥存储的配置步骤。 例如，若要访问 Azure Key Vault，需要提供密钥存储到正确的凭据。

### <a name="using-the-azure-key-vault-provider"></a>使用 Azure Key Vault 提供程序

Azure 密钥保管库便于存储和管理用于始终加密的列主密钥（尤其是当应用程序在 Azure 中托管时）。 Linux、 macOS 和 Windows 上的 SQL Server ODBC 驱动程序包括 Azure 密钥保管库的内置列主密钥存储提供程序。 请参阅[Azure Key Vault-Step by Step](https://blogs.technet.microsoft.com/kv/2015/06/02/azure-key-vault-step-by-step/)，[开始使用 Key Vault](https://azure.microsoft.com/documentation/articles/key-vault-get-started/)，并[Azure 密钥保管库中创建列主密钥的密钥](https://msdn.microsoft.com/library/mt723359.aspx#Anchor_2)有关配置 Azure 密钥的详细信息保管库的 Always Encrypted。

> [!NOTE]
> 在 Linux 和 macOS，驱动程序版本 17.2 及更高版本上`libcurl`需要使用此提供程序，但并不显式依赖关系，因为使用驱动程序的其他操作不需要它。 如果您遇到的错误有关`libcurl`，确保已安装。

该驱动程序支持对 Azure 密钥保管库中使用下列凭据类型进行身份验证：

- 用户名/密码 – 使用此方法时，凭据是 Azure Active Directory 用户和其密码的名称。

- 客户端 ID/机密 – 使用此方法的凭据是应用程序客户端 ID 和应用程序密码。

若要允许使用 Cmk 存储在 AKV 中的列加密的驱动程序，请使用以下的仅限连接字符串关键字：

|凭据类型| `KeyStoreAuthentication` |`KeyStorePrincipalId`| `KeyStoreSecret` |
|-|-|-|-|
|用户名/密码| `KeyVaultPassword`|用户主体名称|Password|
|客户端 ID/机密| `KeyVaultClientSecret`|客户端 ID|机密|

#### <a name="example-connection-strings"></a>连接字符串示例

以下连接字符串演示如何为 Azure 密钥保管库将使用两种凭据类型的进行身份验证：

**ClientID/机密**:

```
DRIVER=ODBC Driver 13 for SQL Server;SERVER=myServer;Trusted_Connection=Yes;DATABASE=myDB;ColumnEncryption=Enabled;KeyStoreAuthentication=KeyVaultClientSecret;KeyStorePrincipalId=<clientId>;KeyStoreSecret=<secret>
```

**用户名/密码**

```
DRIVER=ODBC Driver 13 for SQL Server;SERVER=myServer;Trusted_Connection=Yes;DATABASE=myDB;ColumnEncryption=Enabled;KeyStoreAuthentication=KeyVaultPassword;KeyStorePrincipalId=<username>;KeyStoreSecret=<password>
```

任何其他 ODBC 应用程序更改所不需的 CMK 存储使用 AKV。

### <a name="using-the-windows-certificate-store-provider"></a>使用 Windows 证书存储提供程序

Windows 上的 SQL Server ODBC 驱动程序包含名为 Windows 证书存储的内置列主密钥存储提供程序`MSSQL_CERTIFICATE_STORE`。 （此提供程序不是在 macOS 或 Linux 上可用。）与此提供程序，客户端计算机上本地存储 CMK 和应用程序无额外配置才可使用的驱动程序。 但是，应用程序必须具有对证书和私钥的访问的存储中。 有关详细信息，请参阅[创建并存储列主密钥 (Always Encrypted)](https://docs.microsoft.com/sql/relational-databases/security/encryption/create-and-store-column-master-keys-always-encrypted)。

### <a name="using-custom-keystore-providers"></a>使用自定义密钥存储提供程序

SQL Server 的 ODBC 驱动程序还支持使用 CEKeystoreProvider 接口的自定义第三方密钥存储提供程序。 这允许应用程序加载查询，并配置密钥存储提供程序，以便它们可用于驱动程序访问加密的列。 应用程序可能还直接与密钥存储提供程序，以便为 SQL Server 中存储加密 Cek 和执行其任务之外访问加密的列使用 ODBC; 交互有关详细信息，请参阅[自定义密钥存储提供程序](../../connect/odbc/custom-keystore-providers.md)。

两个连接属性用于与自定义密钥存储提供程序进行交互。 它们分别是：

- `SQL_COPT_SS_CEKEYSTOREPROVIDER`

- `SQL_COPT_SS_CEKEYSTOREDATA`

前者用于加载和枚举加载的密钥存储提供程序，而后者使应用程序提供程序通信。 在任何时候，可能会使用这些连接属性之前, 或之后建立的连接，因为应用程序提供程序交互不涉及与 SQL Server 的通信。 但是，因为尚未加载该驱动程序，设置和连接之前获取这些属性将导致由驱动程序管理器中，处理它们，并且可能不会产生预期的结果。

#### <a name="loading-a-keystore-provider"></a>正在加载密钥存储提供程序

设置`SQL_COPT_SS_CEKEYSTOREPROVIDER`连接属性允许客户端应用程序加载提供程序库，使其中包含的密钥存储提供程序可供使用。

```
SQLRETURN SQLSetConnectAttr( SQLHDBC ConnectionHandle, SQLINTEGER Attribute, SQLPOINTER ValuePtr, SQLINTEGER StringLength);
```
| 参数 | 描述 |
|:---|:---|
|`ConnectionHandle`|[输入]连接句柄。 必须是有效的连接句柄，但通过一个连接句柄加载提供程序是从在同一进程中任何其他可访问。|
|`Attribute`|[输入]要设置属性：`SQL_COPT_SS_CEKEYSTOREPROVIDER`常量。|
|`ValuePtr`|[输入]指定的提供程序库文件名的以 null 结尾的字符字符串指针。 对于 SQLSetConnectAttrA，这是 ANSI （多字节） 字符串。 对于 SQLSetConnectAttrW，这是 Unicode (wchar_t) 字符串。|
|`StringLength`|[输入]ValuePtr 字符串或 sql_nts; 的长度。|

驱动程序将尝试加载使用加载机制的平台定义的动态库 ValuePtr 参数所标识的库 (`dlopen()`在 Linux 和 macOS 上`LoadLibrary()`在 Windows 上)，并将添加到的列表定义其中任何提供程序已知的驱动程序的提供程序。 可能会出现以下错误：

| 错误 | 描述 |
|:--|:--|
|`CE203`|无法加载动态库。|
|`CE203`|在库中找不到"CEKeyStoreProvider"导出符号。|
|`CE203`|库中的一个或多个提供程序已加载。|

`SQLSetConnectAttr` 返回的常见错误或成功值和其他信息是可用于通过标准 ODBC 诊断机制所发生任何错误。

> [!NOTE]
> 应用程序编程人员必须确保任何自定义提供程序加载之前通过任何连接发送无任何查询。 如果没有这样做，会导致错误：

| 错误 | 描述 |
|:--|:--|
|`CE200`|密钥存储提供程序 %1 找不到。 请确保已加载适当的密钥存储提供程序库。|

> [!NOTE]
> 密钥存储提供程序实现器应避免使用`MSSQL`其自定义提供程序的名称。 此术语保留仅供 Microsoft 使用并且可能导致冲突与未来的内置提供程序。 使用此术语的自定义提供的名称可能会导致 ODBC 警告。

#### <a name="getting-the-list-of-loaded-providers"></a>获取加载提供程序的列表

获取此连接属性使客户端应用程序以确定当前加载的驱动程序 （包括内置的。） 中的密钥存储提供程序这可以仅在连接后。

```
SQLRETURN SQLGetConnectAttr( SQLHDBC ConnectionHandle, SQLINTEGER Attribute, SQLPOINTER ValuePtr, SQLINTEGER BufferLength, SQLINTEGER * StringLengthPtr);
```
| 参数 | 描述 |
|:---|:---|
|`ConnectionHandle`|[输入]连接句柄。 必须是有效的连接句柄，但通过一个连接句柄加载提供程序是从在同一进程中任何其他可访问。|
|`Attribute`|[输入]若要检索的属性：`SQL_COPT_SS_CEKEYSTOREPROVIDER`常量。|
|`ValuePtr`|[输出]指向用于返回下一步的加载提供程序名称的内存的指针。|
|`BufferLength`|[输入]ValuePtr 的缓冲区的长度。|
|`StringLengthPtr`|[输出]指向在其中返回的总字节数 （不包括 null 终止字符） 的缓冲区的指针可用于返回在\*ValuePtr。 如果 ValuePtr 是 null 指针，则返回没有长度限制。 如果属性值是一个字符串，并且可用来返回的字节数大于 null 终止的长度减去 BufferLength 字符中的数据\*ValuePtr 被截断为 BufferLength 减去的长度null 终止字符是由驱动程序以 null 结尾。|

若要允许检索整个列表，每个 Get 操作返回当前提供程序的名称，并递增到下一个内部计数器。 此计数器达到结束列表中，空字符串 ("") 返回，和的计数器重置;后续的 Get 操作然后继续执行再次从列表开头。

### <a name="communicating-with-keystore-providers"></a>与密钥存储提供程序通信

`SQL_COPT_SS_CEKEYSTOREDATA`连接属性使客户端应用程序与加载的密钥存储提供程序通信配置其他参数，密钥材料，等等。客户端应用程序和提供程序之间的通信都遵循简单的请求-响应协议，基于 Get 和 Set 请求使用此连接属性。 仅由客户端应用程序启动的通信。

> [!NOTE]
> 由于 ODBC 调用 CEKeyStoreProvider 的响应 (SQLGet/SetConnectAttr)，ODBC 接口唯一支持的连接上下文的分辨率设置数据。

应用程序与通过 CEKeystoreData 结构通过驱动程序的密钥存储提供程序进行通信：

```
typedef struct CEKeystoreData {
wchar_t *name;
unsigned int dataSize;
char data[];
} CEKEYSTOREDATA;
```
| 参数 | 描述 |
|:---|:---|
|`name`|[输入]在集，提供程序的名称时将数据发送到。 在 Get 时被忽略。 以 null 结尾的宽字符字符串。|
|`dataSize`|[输入]以下结构的数据数组的大小。|
|`data`|[InOut]在组中，要发送到提供程序的数据。 这可能是任意数据;该驱动程序不会尝试将其解释。 在 Get，要接收的数据的缓冲区读取从提供程序。|

#### <a name="writing-data-to-a-provider"></a>将数据写入到提供程序

一个`SQLSetConnectAttr`调用使用`SQL_COPT_SS_CEKEYSTOREDATA`属性向指定的密钥存储提供程序写入数据的"数据包"。
```
SQLRETURN SQLSetConnectAttr( SQLHDBC ConnectionHandle, SQLINTEGER Attribute, SQLPOINTER ValuePtr, SQLINTEGER StringLength);
```
| 参数 | 描述 |
|:---|:---|
|`ConnectionHandle`| [输入]连接句柄。 必须是有效的连接句柄，但通过一个连接句柄加载提供程序是从在同一进程中任何其他可访问。|
|`Attribute`|[输入]要设置属性：`SQL_COPT_SS_CEKEYSTOREDATA`常量。|
|`ValuePtr`|[输入]指向 CEKeystoreData 结构的指针。 结构的名称字段标识提供程序所针对的数据。|
|`StringLength`|[输入]SQL_IS_POINTER 常量|

可通过获取其他详细的错误信息[SQLGetDiacRec](https://msdn.microsoft.com/library/ms710921(v=vs.85).aspx)。

> [!NOTE]
> 提供程序可用于连接句柄关联到特定的连接，写入的数据如果需要。 这可用于实现每个连接配置。 它还可以忽略连接上下文并处理相同而不考虑用于发送数据的连接的数据。 请参阅[上下文关联](../../connect/odbc/custom-keystore-providers.md#context-association)有关详细信息。

#### <a name="reading-data-from-a-provider"></a>从提供程序读取数据

调用`SQLGetConnectAttr`使用`SQL_COPT_SS_CEKEYSTOREDATA`属性读取的数据，"数据包"*最后一个写入-到*提供程序。 如果没有，则会发生函数序列错误。 建议以支持"dummy"的写入而不会导致其他负面影响，选择用于读取操作的提供程序，它会比较有利，若要执行此操作的方式的 0 字节的密钥存储提供程序实施者。

```
SQLRETURN SQLGetConnectAttr( SQLHDBC ConnectionHandle, SQLINTEGER Attribute, SQLPOINTER ValuePtr, SQLINTEGER BufferLength, SQLINTEGER * StringLengthPtr);
```
| 参数 | 描述 |
|:---|:---|
|`ConnectionHandle`|[输入]连接句柄。 必须是有效的连接句柄，但通过一个连接句柄加载提供程序是从在同一进程中任何其他可访问。|
|`Attribute`|[输入]若要检索的属性：`SQL_COPT_SS_CEKEYSTOREDATA`常量。|
|`ValuePtr`|[输出]指向在其中放置从提供程序读取的数据的 CEKeystoreData 结构的指针。|
|`BufferLength`|[输入]SQL_IS_POINTER 常量|
|`StringLengthPtr`|[输出]指向用于返回 BufferLength 缓冲区的指针。 如果 * ValuePtr 为 null 指针，则返回没有长度限制。|

调用方必须确保要写入的提供程序，会分配给以下 CEKEYSTOREDATA 结构的足够长的缓冲区。 在返回时，其 dataSize 字段已更新从提供程序读取的数据的实际长度。 可通过获取其他详细的错误信息[SQLGetDiacRec](https://msdn.microsoft.com/library/ms710921(v=vs.85).aspx)。

此接口上的应用程序和密钥存储提供程序之间传输的数据格式将没有其他要求。 每个提供程序可以定义其自己的协议/数据格式，具体取决于其需求。

实现自己的密钥存储提供程序的示例，请参阅[自定义密钥存储提供程序](../../connect/odbc/custom-keystore-providers.md)

## <a name="limitations-of-the-odbc-driver-when-using-always-encrypted"></a>ODBC 驱动程序使用始终加密时的限制

### <a name="asynchronous-operations"></a>异步操作
虽然 ODBC 驱动程序将允许使用[异步操作](../../relational-databases/native-client/odbc/creating-a-driver-application-asynchronous-mode-and-sqlcancel.md)借助 Always Encrypted，没有对性能产生影响的操作时启用了始终加密。 在调用`sys.sp_describe_parameter_encryption`确定加密元数据中的语句阻止并会导致驱动程序等待服务器返回的元数据返回前`SQL_STILL_EXECUTING`。

### <a name="retrieve-data-in-parts-with-sqlgetdata"></a>在使用 SQLGetData 部件中检索数据
ODBC Driver 17 for SQL Server 加密前字符和二进制列不能检索使用 SQLGetData 部件中。 SQLGetData 对只有一个调用可以进行，具有足够长以包含整个列的数据的缓冲区。

### <a name="send-data-in-parts-with-sqlputdata"></a>在使用 SQLPutData 部件中发送数据
不能使用 SQLPutData 部件中发送数据插入或比较。 SQLPutData 只有一个调用可以进行，使用包含整个数据的缓冲区。 对于将长数据插入到加密列中，使用大容量复制 API，包含一个输入的数据文件中下一节中所述。

### <a name="encrypted-money-and-smallmoney"></a>加密的 money 和 smallmoney
加密**资金**或**smallmoney**列不能为目标的参数，因为没有不特定 ODBC 数据类型映射到这些类型，从而导致操作数类型冲突错误。

## <a name="bulk-copy-of-encrypted-columns"></a>大容量复制加密列

利用[SQL 大容量复制函数](../../relational-databases/native-client-odbc-bulk-copy-operations/performing-bulk-copy-operations-odbc.md)并**bcp**实用程序使用始终加密自 ODBC Driver 17 for SQL Server 支持。 纯文本 （加密上的插入和已解密上检索） 和已加密文本 （按原样传输） 可以插入和检索使用大容量复制 （bcp_ *） Api 并**bcp**实用程序。

- 若要检索已加密文本 （例如，对于大容量加载到不同的数据库） 的 varbinary （max） 形式，而无需连接`ColumnEncryption`选项 (或将其设置为`Disabled`)，并且执行 BCP OUT 操作。

- 若要插入和检索纯文本，并让驱动程序以透明方式执行加密和解密作为必需的设置`ColumnEncryption`到`Enabled`就足够了。 BCP API 的功能在其他方面不变。

- 要将已加密文本插入 varbinary （max） 的形式 （例如上面检索到），请将`BCPMODIFYENCRYPTED`选项设为 TRUE，并且执行 BCP IN 操作。 为了使生成的数据以便进行解密，请确保目标列的 CEK 是与最初从其获取已加密文本相同。

使用时**bcp**实用程序： 控制`ColumnEncryption`设置，请使用-D 选项并指定包含所需的值的 DSN。 若要插入已加密文本，请确保`ALLOW_ENCRYPTED_VALUE_MODIFICATIONS`启用的用户的设置。

操作对加密列时下, 表提供的操作的摘要：

|`ColumnEncryption`|BCP 方向|描述|
|----------------|-------------|-----------|
|`Disabled`|OUT （到客户端）|检索已加密文本。 观察到的数据类型是**varbinary （max)**。|
|`Enabled`|OUT （到客户端）|检索纯文本。 该驱动程序将解密列数据。|
|`Disabled`|IN （到服务器）|将插入已加密文本。 这被适用于以不透明形式而不需要它移动加密的数据进行解密。 如果该操作将失败`ALLOW_ENCRYPTED_VALUE_MODIFICATIONS`选项未设置了用户，或连接句柄中未设置 BCPMODIFYENCRYPTED。 有关详细信息，请参阅下文。|
|`Enabled`|IN （到服务器）|将插入纯文本。 该驱动程序将对列数据进行加密。|

### <a name="the-bcpmodifyencrypted-option"></a>BCPMODIFYENCRYPTED 选项

为了防止数据损坏，服务器通常不允许直接将已加密文本插入加密列，并且因此尝试执行此操作将失败;但是，对于使用 BCP API、 设置的加密数据的大容量加载`BCPMODIFYENCRYPTED` [bcp_control](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/bcp-control.md)选项为 TRUE 将允许已加密文本直接插入并减少了通过设置损坏的加密的数据的风险`ALLOW_ENCRYPTED_VALUE_MODIFICATIONS`的用户帐户上的选项。 尽管如此，密钥必须匹配数据，而且很大容量插入后且在进一步使用之前执行插入的数据的一些只读检查一个好办法。

有关详细信息，请参阅[迁移通过 Always Encrypted 保护的敏感数据](../../relational-databases/security/encryption/migrate-sensitive-data-protected-by-always-encrypted.md)。

## <a name="always-encrypted-api-summary"></a>始终加密 API 摘要

### <a name="connection-string-keywords"></a>连接字符串关键字

|名称|描述|  
|----------|-----------------|  
|`ColumnEncryption`|接受的值是`Enabled` / `Disabled`。<br>`Enabled` - 启用或针对连接的 Always Encrypted 功能。<br>`Disabled` - 禁用针对连接的 Always Encrypted 功能。 <br><br>默认值为 `Disabled`。|  
|`KeyStoreAuthentication` | 有效值：`KeyVaultPassword`、`KeyVaultClientSecret` |
|`KeyStorePrincipalId` | 当`KeyStoreAuthentication`  =  `KeyVaultPassword`，将此值设置为有效的 Azure Active Directory 用户主体名称。 <br>当`KeyStoreAuthetication`  =  `KeyVaultClientSecret`将此值设置为有效 Azure Active Directory 应用程序客户端 ID |
|`KeyStoreSecret` | 当`KeyStoreAuthentication`  =  `KeyVaultPassword`将此值设置为相应的用户名的密码。 <br>当`KeyStoreAuthentication`  =  `KeyVaultClientSecret`将此值设置为与有效 Azure Active Directory 应用程序客户端 ID 关联的应用程序机密|

### <a name="connection-attributes"></a>连接属性

|名称|类型|描述|  
|----------|-------|----------|  
|`SQL_COPT_SS_COLUMN_ENCRYPTION`|预连接|`SQL_COLUMN_ENCRYPTION_DISABLE` (0)--禁用始终加密 <br>`SQL_COLUMN_ENCRYPTION_ENABLE` (1)--启用始终加密|
|`SQL_COPT_SS_CEKEYSTOREPROVIDER`|后连接|[设置]尝试加载 CEKeystoreProvider<br>[获取]返回 CEKeystoreProvider 名称|
|`SQL_COPT_SS_CEKEYSTOREDATA`|后连接|[设置]将数据写入到 CEKeystoreProvider<br>[获取]从 CEKeystoreProvider 读取数据|
|`SQL_COPT_SS_CEKCACHETTL`|后连接|[设置]CEK 缓存 TTL 设置<br>[获取]获取当前 CEK 缓存 TTL|
|`SQL_COPT_SS_TRUSTEDCMKPATHS`|后连接|[设置]设置受信任的 CMK 路径指针<br>[获取]获取当前受信任的 CMK 路径指针|

### <a name="statement-attributes"></a>语句属性

|名称|描述|  
|----------|-----------------|  
|`SQL_SOPT_SS_COLUMN_ENCRYPTION`|`SQL_CE_DISABLED` (0)--语句禁用了 always Encrypted <br>`SQL_CE_RESULTSETONLY` (1)--仅解密。 结果集和返回值解密的、 和未加密的参数 <br>`SQL_CE_ENABLED` (3)--始终加密已启用并使用参数和结果|

### <a name="descriptor-fields"></a>描述符字段

|IPD 字段|大小/类型|默认值|描述|
|-|-|-|-|  
|`SQL_CA_SS_FORCE_ENCRYPT` (1236)|WORD （2 个字节）|0|当 0 （默认值）：决定加密此参数由加密元数据的可用性。<br><br>当非零值： 如果此参数加密元数据不可用，则被加密。 否则，请求将失败，错误 [CE300] 为参数指定了 [Microsoft] [ODBC Driver 13 for SQL Server] 强制加密，但通过服务器提供的加密元数据。|

### <a name="bcpcontrol-options"></a>bcp_control 选项

|选项名称|默认值|描述|
|-|-|-|
|`BCPMODIFYENCRYPTED` (21)|FALSE|为 TRUE 时，允许 varbinary (max) 值插入到加密列。 为 FALSE 时，阻止插入，除非提供正确的类型和加密元数据。|

## <a name="see-also"></a>另请参阅

- [Always Encrypted（数据库引擎）](../../relational-databases/security/encryption/always-encrypted-database-engine.md)
- [始终加密博客](http://blogs.msdn.com/b/sqlsecurity/archive/tags/always-encrypted/)

