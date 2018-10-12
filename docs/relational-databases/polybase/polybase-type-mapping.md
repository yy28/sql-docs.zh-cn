---
title: PolyBase 的类型映射 | Microsoft Docs
ms.custom: ''
ms.date: 09/24/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: polybase
ms.topic: conceptual
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 9839c46f477fe31d29214eed10dce0d673c9fd00
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47732597"
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
| NCHAR         | String<br /><br /> Char[] | string         | text                  |
| NVARCHAR      | String<br /><br /> Char[] | string         | 文本                  |
| char          | String<br /><br /> Char[] | string         | 文本                  |
| varchar       | String<br /><br /> Char[] | string         | 文本                  |
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

| Oracle 数据类型              | SQL Server 类型 |
| ----------------------------- | --------------- |
| float                         | float           |
| Decimal                       | Decimal         |
| smallint                           | smallint             |
| Long                          | Ntext           |
| Binary Float                  | Real            |
| Char                          | Nchar           |
| Varchar2                      | nvarchar        |
| Raw                           | Varbinary       |
| Long Raw                      | 图像           |
| Bfile                         | 图像           |
| Blob                          | 图像           |
| Clob                          | 图像           |
| Rowid                         | Varchar         |
| date                          | Datetime2       |
| 时间戳                     | Datetime2       |
| Timestamp with local timezone | Datetime2       |

### <a name="type-mismatch-float"></a>类型不匹配 (Float)

Oracle 支持的浮点精度为 126，低于 SQL Server 支持的精度 (53)。 因此，可以直接映射 Float (1-53)，但除此之外，截断会导致数据丢失。

### <a name="type-mismatch-character-types"></a>类型不匹配（Character 类型）

对于诸如 Long 和 Bfile 的类型，Oracle 支持的数据类型大小为 4 GB。 SQL Server 支持的大小为 2 GB。 同样，对于 oracle 数据类型 Blob 和 clob，Oracle 最多可支持的大小为 128 TB，而 SQL Server LONGVARBINARY 或 WLONGVARBINARY 支持的大小不超过 2 GB。 数据类型大小超过 2 GB 的映射类型可能导致数据截断。  

### <a name="type-mismatch-timestamp"></a>类型不匹配 (Timestamp)

Oracle 中的 Timestamp 和 Timestamp with local timezone 支持 9 秒小数精度。 SQL Server DateTime2 支持 7 秒小数精度。

此外，Simba 将 Date、Timestamp 和 Timestamp with local zone 映射到 ODBC 类型 SQL_TIMESTAMP，并最终映射到 SQL Server 类型 Timestamp。 Timestamp 是自动生成的唯一行 ID。理想情况下，SQL_TIMESTAMP 应映射到 SQL Server 类型 DateTime/DateTime2 或 Oracle 类型 Date、Timestamp 和 Timestamp with local zone 应映射到 ODBC 类型 SQL_TYPE_TIMESTAMP。

### <a name="driver-configuration-option"></a>驱动程序配置选项

Long/LOB 列的默认缓冲区大小为 1024 KB（可配置）。

## <a name="mongo-type-mapping-reference"></a>Mongo 类型映射引用

| BSON 数据类型     | SQL Server 类型 |
| ------------------ | --------------- |
| 双精度             | float           |
| String             | nvarchar        |
| Object             |
| Array              |
| Binary data        | nvarchar        |
| 对象 ID          | nvarchar        |
| Boolean            | bit             |
| date               | Datetime2       |
| 32-bit integer     | smallint             |
| 时间戳          | nvarchar        |
| 64-bit integer     | BigInt          |
| DBPointer          | nvarchar        |
| Javascript         | nvarchar        |
| Max Key            | nvarchar        |
| Min Key            | nvarchar        |
| 符号             | nvarchar        |
| Regular Expression | nvarchar        |
| Undefined/NULL     | nvarchar        |

### <a name="javascript-with-scope"></a>Javascript (with scope)

驱动程序将该值作为包含“Unsupported Javascript with scope”的字符串返回。

### <a name="type-mismatch-string"></a>类型不匹配 (string)

MongoDB 字符串转换为 SQL_WVARCHAR 类型，默认列大小为 255。 此列大小可作为驱动程序配置的一部分进行调整。 虽然能够进行配置，但 SQL_WVARCHAR 或 SQL Server 类型 Varchar 最多仅支持 2 GB，而 MongoDB 最多可以容纳 4 GB 的数据。 这可能会导致数据截断。

### <a name="mongodb-driver-options"></a>MongoDB 驱动程序选项

- 启用双缓冲：默认选中。
- 每个块获取的文档：默认值 4096。
- 将字符串公开为 SQL_WVARCHAR：默认选中。 如果未选中，则将字符串公开为 SQL_VARCHAR。
- String 列大小：默认值 255。
- 将 Binary 公开为 SQL_LONGVARBINARY：默认选中。 如果未选中，则将 Binary 将公开为 SQL_VARBINARY。
- Binary 列大小：默认值 32767。
- 启用传递：默认选中。

### <a name="schema-related-driver-configurations"></a>与架构相关的驱动程序配置

- LoadMetadataTable：数据库的默认值。 要求驱动程序从指定的J SON 文件加载架构定义。
- LocalMetadataFile：如果从文件读取，则必须指定完整路径。
- 抽样方法：  
  - 默认向前：驱动程序从第一条记录中采样数据。
  - 向后：驱动程序从最后一条记录开始采样数据。
- SamplingLimit：默认值 100（驱动程序可以采样以生成临时架构定义的最大记录数）。 设置为 0 时，驱动程序对每个文档进行采样。
- SamplingStepSize：默认值 1（扫描数据库以生成临时架构定义时驱动程序采样记录的时间间隔）。 例如，设置为 2 时，它会对数据库中其他每条记录进行采样。

## <a name="teradata-type-mapping-reference"></a>Teradata 类型映射引用

| Teradata 数据类型               | SQL Server 类型 |
| -------------------------------- | --------------- |
| smallint                              | smallint             |
| Small Int                        | SmallInt        |
| Big Int                          | BigInt          |
| Byte Int                         | TinyInt         |
| Decimal                          | Decimal         |
| float                            | float           |
| Byte                             | 二进制          |
| Varbyte                          | Varbinary       |
| Blob                             | 图像           |
| Char                             | Nchar           |
| Clob                             | Ntext           |
| Varchar                          | nvarchar        |
| Graphic                          | Nchar           |
| JSON                             | Ntext           |
| Vargraphic                       | nvarchar        |
| date                             | date            |
| Time                             | Time            |
| Time with Time Zone              | Time            |
| 时间戳                        | Datetime2       |
| Interval Year                    |
| Interval year to month           |
| Interval Month                   |
| Interval Day                     |
| Interval Day to Hour             |
| Interval Day to Minute           |
| Interval Day to Second           |
| Interval Hour                    |
| Interval Hour to Minute          |
| Interval Hour to Second          |
| Interval Minute                  |
| Interval Minute to Second        |
| Interval Second                  |
| Period (DATE)                    |
| Period (TIME)                    |
| Period (TIME with Timezone)      |
| Period (Timestamp)               |
| Period (Timestamp with Timezone) |

### <a name="period-data-type"></a>Period 数据类型

Period 数据类型表示由开始边界和结束边界标记的持续时间。 从本质上讲，它是一个元组。 Period 没有等效的 SQL Server 类型。

### <a name="time-with-time-zone-and-timestamp"></a>Time with Time Zone 和 Timestamp

Time with Time Zone 和 Timestamp 包含会在转换期间丢失的时差。 如果将 SQL_Type_Time/SQL_Type_Timestamp 映射到 datetimeoffset 而不是 Time/DateTime2，则可以修复此问题。

### <a name="byteint"></a>ByteInt

Simba 将 Teradata 类型 ByteInt （可包含 0 到 255 之间的值）映射到可包含 -127 到 127 之间的值的 TinyInt。 这可能导致截断。  

### <a name="clob"></a>CLOB

带有 LATIN 字符集的 CLOB 数据类型应该能够接受 2097088000 个字符。 但是，超过 1073741823，缓冲区大小会变成负数。  

### <a name="driver-configuration-options"></a>驱动程序配置选项

- 对 TIMESTAMP 参数使用 DATE 数据。
- 为 2.X 应用程序启用自定义目录模式。
- 为 SQL_TIMESTAMP 返回 CREATE_PARAMS 列中的空字符串。
- 返回最大值。 CHAR/VARCHAR 长度为 32 K。

::: moniker-end

## <a name="next-steps"></a>后续步骤

有关如何使用它的更多信息，请参阅 [CREATE EXTERNAL TABLE](../../t-sql/statements/create-external-table-transact-sql.md) 的 Transact-SQL 参考文章。
