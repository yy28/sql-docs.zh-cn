---
title: PolyBase 的类型映射 | Microsoft Docs
ms.date: 09/24/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: polybase
ms.topic: conceptual
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 490b00717d16e4ca101ea591c22e71a2d228e659
ms.sourcegitcommit: d5cd4a5271df96804e9b1a27e440fb6fbfac1220
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2019
ms.locfileid: "64774970"
---
# <a name="type-mapping-with-polybase"></a>PolyBase 的类型映射

[!INCLUDE[appliesto-ss-xxxx-asdw-pdw-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文介绍 PolyBase 外部数据源与 SQL Server 之间的映射。 可以使用此信息通过 [CREATE EXTERNAL TABLE](../../t-sql/statements/create-external-table-transact-sql.md) Transact-SQL 命令正确定义外部表。

## <a name="overview"></a>概述

使用 PolyBase 创建外部表时，列定义（包括数据类型和列数）必须与外部文件中的数据匹配。 如果存在不匹配，则在查询实际数据时会拒绝文件行。  
  
对于引用外部数据源中的文件的外部表，列和类型定义必须映射到外部文件的确切架构。 定义引用 Hadoop/Hive 中存储的数据的数据类型时，可在 SQL 与 Hive 数据类型之间使用以下映射，并在从中进行选择时将类型强制转换为 SQL 数据类型。 除非另有说明，否则类型包括 Hive 的所有版本。

> [!NOTE]  
> 在任何转换中，SQL Server 都不支持 Hive 无穷大数据值。 PolyBase 会失败，并出现数据类型转换错误。

## <a name="hadoop-type-mapping-reference"></a>Hadoop 类型映射引用

| SQL 数据类型 | .NET 数据类型            | Hive 数据类型 | Hadoop/Java 数据类型 | 注释                       |
| ------------- | ------------------------- | -------------- | --------------------- | ------------------------------ |
| TINYINT       | Byte                      | TINYINT        | ByteWritable          | 仅用于无符号数字。     |
| SMALLINT      | Int16                     | SMALLINT       | ShortWritable         |
| ssNoversion           | Int32                     | ssNoversion            | IntWritable           |
| BIGINT        | Int64                     | BIGINT         | LongWritable          |
| bit           | Boolean                   | boolean        | BooleanWritable       |
| FLOAT         | 双精度                    | double         | DoubleWritable        |
| REAL          | Single                    | FLOAT          | FloatWritable         |
| money         | Decimal                   | double         | DoubleWritable        |
| SMALLMONEY    | Decimal                   | double         | DoubleWritable        |
| NCHAR         | String<br /><br /> Char[] | string         | Varchar               |
| NVARCHAR      | String<br /><br /> Char[] | string         | Varchar               |
| char          | String<br /><br /> Char[] | string         | Varchar               |
| varchar       | String<br /><br /> Char[] | string         | Varchar               |
| BINARY        | Byte[]                    | BINARY         | BytesWritable         | 适用于 Hive 0.8 及更高版本。 |
| varbinary     | Byte[]                    | BINARY         | BytesWritable         | 适用于 Hive 0.8 及更高版本。 |
| 日期          | DateTime                  | TIMESTAMP      | TimestampWritable     |
| smalldatetime | DateTime                  | TIMESTAMP      | TimestampWritable     |
| datetime2     | DateTime                  | TIMESTAMP      | TimestampWritable     |
| DATETIME      | DateTime                  | TIMESTAMP      | TimestampWritable     |
| time          | TimeSpan                  | TIMESTAMP      | TimestampWritable     |
| Decimal       | Decimal                   | Decimal        | BigDecimalWritable    | 适用于 Hive 0.11 及更高版本。 |

<!--SQL Server 2019-->
::: moniker range=">= sql-server-ver15 || =sqlallproducts-allversions"

## <a name="oracle-type-mapping-reference"></a>Oracle 类型映射引用

| Oracle 数据类型 | SQL Server 类型 | 
| -------------    | --------------- |
|float             |float            |
|NUMBER            |Decimal          |
|LONG              |nvarchar         |
|BINARY_FLOAT      |Real             | 
|BINARY_DOUBLE     |float            | 
|CHAR              |Char             |
|VARCHAR2          |Varchar          | 
|NVARCHAR2         |nvarchar         | 
|RAW               |Varbinary        |
|LONG RAW          |Varbinary        | 
|BLOB              |Varbinary        |
|CLOB              |Varchar          |
|NCLOB             | nvarchar        | 
|ROWID             |Varchar          |
|UROWID            |Varchar          | 
|DATE              |Datetime2        |
|timestamp         |Datetime2        | 

类型不匹配 

Float：Oracle 支持的浮点精度为 126，低于 SQL Server 支持的精度 (53)。 因此，可以直接映射 Float (1-53)，但除此之外，截断会导致数据丢失。

时间戳：Oracle 中的时间戳和具有当地时区的时间戳支持 0.9 秒的精度，而 SQL Server DateTime2 仅支持 0.7 秒的精度。 




## <a name="mongodb-type-mapping"></a>MongoDB 类型映射

| BSON 数据类型     | SQL Server 类型 |
| ------------------ | --------------- |
| 双精度             | float           |
| String             | nvarchar        |
| Binary data        | nvarchar        |
| 对象 ID          | nvarchar        |
| Boolean            | bit             |
| date               | Datetime2       |
| 32-bit integer     | smallint             |
| 时间戳          | nvarchar        |
| 64-bit integer     | BigInt          |
|Decimal 128         | Decimal         | 
| DBPointer          | nvarchar        |
| Javascript         | nvarchar        |
| Max Key            | nvarchar        |
| Min Key            | nvarchar        |
| 符号             | nvarchar        |
| Regular Expression | nvarchar        |
| Undefined/NULL     | nvarchar        |


MongoDB 使用 BSON 文档来存储数据记录。 与之前的方案不同，BSON 是无架构的，并且支持在其他文档中嵌入文档和数组。 这为用户提供了灵活性。 


## <a name="teradata-type-mapping-reference"></a>Teradata 类型映射引用

| Teradata 数据类型 | SQL Server 类型 | 
| -------------      | -------------   |
|整数             |smallint              |
|SMALLINT            |SmallInt         |
|bigint              |BigInt           |
|BYTEINT             |SmallInt         |
|DECIMAL             |Decimal          |
|FLOAT               |Decimal          |
|BYTE                |二进制           |
|VARBYTE             |Varbinary        |
|BLOB                |varbinary        |
|CHAR                |Nchar            |
|CLOB                |nvarchar         |
|VARCHAR             |nvarchar         |
|Graphic             |Nchar            |
|JSON                |nvarchar         |
|VARGRAPHIC          |nvarchar         |
|DATE                |date             |
|timestamp           |Datetime2        |
|TIME                |Time             |
|TIME WITH TIME ZONE |Time             |
|TIMESTAMP WITH TIME ZONE|Time         |

::: moniker-end

## <a name="next-steps"></a>后续步骤

有关如何使用它的更多信息，请参阅 [CREATE EXTERNAL TABLE](../../t-sql/statements/create-external-table-transact-sql.md) 的 Transact-SQL 参考文章。
