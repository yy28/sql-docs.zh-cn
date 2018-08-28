---
title: CREATE EXTERNAL TABLE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 6/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- CREATE_EXTERNAL_TABLE
- CREATE EXTERNAL TABLE
- PolyBase, T-SQL
dev_langs:
- TSQL
helpviewer_keywords:
- External
- External, table create
- PolyBase, external table
ms.assetid: 6a6fd8fe-73f5-4639-9908-2279031abdec
caps.latest.revision: 30
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f30febe9ab31ac58bbdd993a3e5034e5abcb427c
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2018
ms.locfileid: "43077301"
---
# <a name="create-external-table-transact-sql"></a>CREATE EXTERNAL TABLE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  为 PolyBase 或弹性数据库查询创建外部表。 根据具体方案，语法存在显著差异。 为 PolyBase 创建的外部表不能用于弹性数据库查询。  同样，为弹性数据库查询创建的外部表不能用于 PolyBase 等。 
  
> [!NOTE]  
>  仅在 SQL Server 2016（或更高版本）、Azure SQL 数据仓库和并行数据仓库上支持 PolyBase。 仅在 Azure SQL 数据库 v12 或更高版本上支持弹性数据库查询。  


- [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用外部表访问存储在 Hadoop 群集或 Azure blob 存储中的数据（引用存储在 Hadoop 群集或 Azure blob 存储中的数据的 PolyBase 外部表）。 还可以用于为[弹性数据库查询](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-overview/)创建外部表。  
  
 使用外部表可：  
  
-   通过 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句查询 Hadoop 或 Azure blob 存储数据。  
  
-   将数据从 Hadoop 或 Azure blob 存储导入并存储到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库中。  
  
-   创建外部表以用于弹性数据库  
     查询。  
     
- 将数据从 Azure Data Lake Store 导入并存储到 Azure SQL 数据仓库中
  
 另请参阅 [CREATE EXTERNAL DATA SOURCE (Transact-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md) 和 [DROP EXTERNAL TABLE (Transact-SQL)](../../t-sql/statements/drop-external-table-transact-sql.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  

```  
-- Syntax for SQL Server 
  
-- Create a new external table  
CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name   
    ( <column_definition> [ ,...n ] )  
    WITH (   
        LOCATION = 'folder_or_filepath',  
        DATA_SOURCE = external_data_source_name,  
        FILE_FORMAT = external_file_format_name  
        [ , <reject_options> [ ,...n ] ]  
    )  
[;]  
  
<reject_options> ::=  
{  
    | REJECT_TYPE = value | percentage  
    | REJECT_VALUE = reject_value  
    | REJECT_SAMPLE_VALUE = reject_sample_value  
  
}  
  
-- Create a table for use with Elastic Database query  
CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name   
    ( <column_definition> [ ,...n ] )  
    WITH ( <sharded_external_table_options> )  
[;]  
  
<sharded_external_table_options> ::=  
        DATA_SOURCE = external_data_source_name,   
        SCHEMA_NAME = N'nonescaped_schema_name',  
        OBJECT_NAME = N'nonescaped_object_name',  
        [DISTRIBUTION  = SHARDED(sharding_column_name) | REPLICATED | ROUND_ROBIN]]  
    )  
[;]  
```  

```  
-- Syntax for Azure SQL Database
  
-- Create a table for use with Elastic Database query  
CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name   
    ( <column_definition> [ ,...n ] )  
    WITH ( <sharded_external_table_options> )  
[;]  
  
<sharded_external_table_options> ::=  
        DATA_SOURCE = external_data_source_name,   
        SCHEMA_NAME = N'nonescaped_schema_name',  
        OBJECT_NAME = N'nonescaped_object_name',  
        [DISTRIBUTION  = SHARDED(sharding_column_name) | REPLICATED | ROUND_ROBIN]]  
    )  
[;]  
```  


```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
-- Create a new external table in SQL Server PDW  
CREATE EXTERNAL TABLE [ database_name . [ schema_name ] . | schema_name. ] table_name   
    ( <column_definition> [ ,...n ] )  
    WITH (   
        LOCATION = 'hdfs_folder_or_filepath',  
        DATA_SOURCE = external_data_source_name,  
        FILE_FORMAT = external_file_format_name  
        [ , <reject_options> [ ,...n ] ]  
    )  
[;]  
  
<reject_options> ::=  
{  
    | REJECT_TYPE = value | percentage,  
    | REJECT_VALUE = reject_value,  
    | REJECT_SAMPLE_VALUE = reject_sample_value,
    | REJECTED_ROW_LOCATION = '\REJECT_Directory'
  
}  
```  
  
## <a name="arguments"></a>参数  
 database_name . [ schema_name ] . | schema_name. ] *table_name*  
 要创建的表的一到三部分名称。 对于外部表，只有表元数据以及有关 Hadoop 或 Azure blob 存储中引用的文件和/或文件夹的基本统计信息才存储在 SQL 中。 在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 中不移动或存储任何实际数据。  
  
 \<column_definition> [ ,...n ] CREATE EXTERNAL TABLE 允许使用一个或多个列定义。 CREATE EXTERNAL TABLE 和 CREATE TABLE 可以使用相同语法定义列。 对于此点有一个例外，不能对外部表使用 DEFAULT CONSTRAINT。 有关列定义及其数据类型的完整详细信息，请参阅 [CREATE TABLE (Transact-SQL)](../../t-sql/statements/create-table-transact-sql.md) 和 [Azure SQL 数据库上的 CREATE TABLE](http://msdn.microsoft.com/library/d53c529a-1d5f-417f-9a77-64ccc6eddca1)。  
  
 列定义（包括数据类型和列数）必须与外部文件中的数据匹配。 如果存在不匹配，则在查询实际数据时会拒绝文件行。  
  
 对于引用外部数据源中的文件的外部表，列和类型定义必须映射到外部文件的确切架构。 定义引用 Hadoop/Hive 中存储的数据的数据类型时，可在 SQL 与 Hive 数据类型之间使用以下映射，并在从中进行选择时将类型强制转换为 SQL 数据类型。 除非另有说明，否则类型包括 Hive 的所有版本。

> [!NOTE]  
>  在任何转换中，SQL Server 都不支持 Hive 无穷大数据值。 PolyBase 会失败，并出现数据类型转换错误。


|SQL 数据类型|.NET 数据类型|Hive 数据类型|Hadoop/Java 数据类型|注释|  
|-------------------|--------------------|--------------------|----------------------------|--------------|  
|TINYINT|Byte|TINYINT|ByteWritable|仅用于无符号数字。|  
|SMALLINT|Int16|SMALLINT|ShortWritable||  
|ssNoversion|Int32|ssNoversion|IntWritable||  
|BIGINT|Int64|BIGINT|LongWritable||  
|bit|Boolean|boolean|BooleanWritable||  
|FLOAT|双精度|double|DoubleWritable||  
|REAL|Single|FLOAT|FloatWritable||  
|money|Decimal|double|DoubleWritable||  
|SMALLMONEY|Decimal|double|DoubleWritable||  
|NCHAR|String<br /><br /> Char[]|string|text||  
|NVARCHAR|String<br /><br /> Char[]|string|文本||  
|char|String<br /><br /> Char[]|string|文本||  
|varchar|String<br /><br /> Char[]|string|文本||  
|BINARY|Byte[]|BINARY|BytesWritable|适用于 Hive 0.8 及更高版本。|  
|varbinary|Byte[]|BINARY|BytesWritable|适用于 Hive 0.8 及更高版本。|  
|日期|DateTime|TIMESTAMP|TimestampWritable||  
|smalldatetime|DateTime|TIMESTAMP|TimestampWritable||  
|datetime2|DateTime|TIMESTAMP|TimestampWritable||  
|DATETIME|DateTime|TIMESTAMP|TimestampWritable||  
|time|TimeSpan|TIMESTAMP|TimestampWritable||  
|Decimal|Decimal|Decimal|BigDecimalWritable|适用于 Hive 0.11 及更高版本。|  
  
 LOCATION =  'folder_or_filepath'  
 为 Hadoop 或 Azure blob 存储中的实际数据指定文件夹或文件路径和文件名。 位置从根文件夹开始；根文件夹是外部数据源中指定的数据位置。  


在 SQL Server 中，如果路径和文件夹不存在，CREATE EXTERNAL TABLE 语句会进行创建。 然后，可使用 INSERT INTO 将数据从本地 SQL Server 表导出到外部数据源。 有关详细信息，请参阅 [Polybase 查询](/sql/relational-databases/polybase/polybase-queries)。 

在 SQL 数据仓库和分析平台系统中，如果路径和文件夹不存在，[CREATE EXTERNAL TABLE AS SELECT](create-external-table-as-select-transact-sql.md) 语句会进行创建。 在这两个产品，CREATE EXTERNAL TABLE 不会创建路径和文件夹。

  
 如果将 LOCATION 指定为一个文件夹，则从外部表中进行选择的 PolyBase 查询会从该文件夹及其所有子文件夹中检索文件。 正如 Hadoop 一样，PolyBase 不返回隐藏文件夹。 它也不返回文件名以下划线 (_) 或句点 (.) 开头的文件。  
  
 在此示例中，如果 LOCATION='/webdata/'，则 PolyBase 查询会从 mydata.txt 和 mydata2.txt 返回行。  它不会返回 mydata3.txt，因为它是隐藏文件夹的子文件夹。 它不会返回 _hidden.txt，因为它是隐藏文件。  
  
 ![外部表的递归数据](../../t-sql/statements/media/aps-polybase-folder-traversal.png "外部表的递归数据")  
  
 若要更改默认值并且只从根文件夹进行读取，请在 core-site.xml 配置文件中将属性 \<polybase.recursive.traversal> 为“false”。 此文件位于 `<SqlBinRoot>\Polybase\Hadoop\Conf with SqlBinRoot the bin root of SQl Server` 下。 例如， `C:\\Program Files\\Microsoft SQL Server\\MSSQL13.XD14\\MSSQL\\Binn`。  
  
 DATA_SOURCE = *external_data_source_name*  
 指定包含外部数据位置的外部数据源的名称。 此位置是 Hadoop 或 Azure blob 存储。 若要创建外部数据源，请使用 [CREATE EXTERNAL DATA SOURCE (Transact-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md)。  
  
 FILE_FORMAT = *external_file_format_name*  
 指定为外部数据存储文件类型和压缩方法的外部文件格式对象的名称。 若要创建外部文件格式，请使用 [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](../../t-sql/statements/create-external-file-format-transact-sql.md)。  
  
 拒绝选项  
 可以指定用于确定 PolyBase 如何处理它从外部数据源检索的脏记录的拒绝参数。 如果实际数据类型或列数与外部表的列定义不匹配，则数据记录被视为“脏”记录。  
  
 未指定或更改拒绝值时，PolyBase 会使用默认值。 使用 CREATE EXTERNAL TABLE 语句创建外部表时，有关拒绝参数的此信息会存储为附加元数据。   在将来的 SELECT 语句或 SELECT INTO SELECT 语句从外部表中选择数据时，PolyBase 会使用拒绝选项确定在实际查询失败之前可以拒绝的行的数量或百分比。 实例时都提供 SQL Server 登录名。 查询会返回（部分）结果，直到超出拒绝阈值；它随后会失败，并出现相应的错误消息。  
  
 REJECT_TYPE = **value** | percentage  
 说明 REJECT_VALUE 选项是指定为文本值还是百分比。  
  
 值  
 REJECT_VALUE 是文本值，而非百分比。 当拒绝的行数超过 reject_value 时，PolyBase 查询会失败。  
  
 例如，如果 REJECT_VALUE = 5 并且 REJECT_TYPE = value，则 PolyBase SELECT 查询会在拒绝了 5 行之后失败。  
  
 percentage  
 REJECT_VALUE 是百分比，而非文本值。 当失败行的百分比超过 reject_value 时，PolyBase 查询会失败。 每隔一段时间计算失败行的百分比。  
  
 REJECT_VALUE = *reject_value*  
 指定在查询失败之前可以拒绝的行数的值或百分比。  
  
 对于 REJECT_TYPE = value，reject_value 必须是介于 0 与 2,147,483,647 之间的整数。  
  
 对于 REJECT_TYPE = percentage，reject_value 必须是介于 0 与 100 之间的浮点数。  
  
 REJECT_SAMPLE_VALUE = *reject_sample_value*  
 当指定 REJECT_TYPE = percentage 时，此属性是必需的。 它确定在 PolyBase 重新计算拒绝的行的百分比之前要尝试检索的行数。  
  
 Reject_sample_value 参数必须是介于 0 与 2,147,483,647 之间的整数。  
  
 例如，如果 REJECT_SAMPLE_VALUE = 1000，则 PolyBase 会在尝试从外部数据文件导入 1000 行后计算失败行的百分比。 如果失败行的百分比小于 reject_value，则 PolyBase 会尝试检索另外 1000 行。 它在尝试导入每个另外 1000 行后会继续重新计算失败行的百分比。  
  
> [!NOTE]  
>  由于 PolyBase 按间隔计算失败行的百分比，因此失败行的实际百分比可能会超过 reject_value。  
  

例如：  
  
 此示例演示三个 REJECT 选项相互之间如何交互。 例如，如果 REJECT_TYPE = percentage、REJECT_VALUE = 30、REJECT_SAMPLE_VALUE = 100，可能出现以下情况：  
  
-   PolyBase 尝试检索前 100 行；25 行失败，75 行成功。  
  
-   失败行的百分比计算结果为 25%，小于 30% 的拒绝值。 因此，PolyBase 会继续从外部数据源检索数据。  
  
-   PolyBase 尝试加载下一个 100 行；这次 25 行成功，75 行失败。  
  
-   重新计算的失败行的百分比为 50%。 失败行的百分比已超过 30% 的拒绝值。  
  
-   在尝试返回前 200 行之后，PolyBase 查询失败，拒绝的行为 50%。 请注意，在 PolyBase 查询检测到超过拒绝阈值之前已返回了匹配行。  
  
REJECTED_ROW_LOCATION = 目录位置
  
  指定应该写入拒绝行和对应错误文件的外部数据源中的目录。
如果指定的路径不存在，PolyBase 将代你创建一个。 创建的子目录的名称为“_rejectedrows”。除非在位置参数中明确命名，否则，“_”字符将确保对该目录转义以进行其他数据处理。 在此目录中，存在根据负荷提交时间创建的文件夹，采用 YearMonthDay -HourMinuteSecond 格式（例如， 20180330-173205）。 在此文件夹中，将写入两种文件类型，_原因文件和数据文件。 

原因文件和数据文件均包含与 CTAS 语句关联的 queryID。 因为数据和原因位于单独的文件中，相应的文件具有匹配的后缀。 
  
 分片外部表选项  
 为[弹性数据库查询](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-overview/)指定外部数据源（非 SQL Server 数据源）和分发方法。  
  
 DATA_SOURCE  
 外部数据源，如存储在 Hadoop 文件系统、Azure blob 存储或[分片映射管理器](https://azure.microsoft.com/documentation/articles/sql-database-elastic-scale-shard-map-management/)中的数据。  
  
 SCHEMA_NAME  
 通过 SCHEMA_NAME 子句可以将外部表定义映射到远程数据库上不同架构中的表。 使用此子句可消除本地和远程数据库上存在的架构之间的歧义。  
  
 OBJECT_NAME  
 通过 OBJECT_NAME 子句可以将外部表定义映射到远程数据库上具有不同名称的表。 使用此子句可消除本地和远程数据库上存在的对象名称之间的歧义。  
  
 分发  
 可选。 只有 SHARD_MAP_MANAGER 类型的数据库才需要此参数。 此参数控制表是被视为分片表还是复制表。 使用 **SHARDED** (column name) 表时，来自不同表的数据不会重叠。 **REPLICATED** 指定表在每个分片上具有相同数据。 **ROUND_ROBIN** 指示将特定于应用程序的方法用于分发数据。  
  
## <a name="permissions"></a>Permissions  
 需要以下用户权限：  
  
-   **CREATE TABLE**  
  
-   **ALTER ANY SCHEMA**  
  
-   **ALTER ANY EXTERNAL DATA SOURCE**  
  
-   **ALTER ANY EXTERNAL FILE FORMAT**  

-   **CONTROL DATABASE**
  
 请注意，创建外部数据源的登录名必须有权对位于 Hadoop 或 Azure blob 存储中的外部数据源进行读取和写入。  


 > [!IMPORTANT]  

>  ALTER ANY EXTERNAL DATA SOURCE 权限授予任何主体创建和修改任何外部数据源对象的权限，还授予访问数据库上所有数据库作用域凭据的权限。 必须将此权限视为高度特权，因此必须仅授予系统中受信任的主体。

## <a name="error-handling"></a>错误处理  
 执行 CREATE EXTERNAL TABLE 语句时，PolyBase 会尝试连接到外部数据源。 如果连接尝试失败，则该语句会失败且不会创建外部表。 由于 PolyBase 在使查询最终失败之前会重新尝试连接，因此命令需要一分钟或更多时间才会失败。  
  
## <a name="general-remarks"></a>一般备注  
 在即席查询方案（即 SELECT FROM EXTERNAL TABLE）中，PolyBase 会将从外部数据源检索的行存储在临时表中。 查询完成之后，PolyBase 会移除并删除临时表。 任何永久数据都不会存储在 SQL 表中。  
  
 相反，在导入方案（即 SELECT INTO FROM EXTERNAL TABLE）中，PolyBase 会将从外部数据源检索的行作为永久数据存储在 SQL 表中。 当 Polybase 检索外部数据时，会在查询执行期间创建新表。  
  
 PolyBase 可以将某些查询计算推送到 Hadoop 以提高查询性能。 这称为谓词下推。 若要启用此功能，请在 [CREATE EXTERNAL DATA SOURCE (Transact-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md) 中指定 Hadoop 资源管理器位置选项。  
  
 可以创建大量引用相同或不同外部数据源的外部表。  
  
## <a name="limitations-and-restrictions"></a>限制和局限  
 在 CTP2 中，导出功能不受支持，即将 SQL 数据永久存储到外部数据源中。 CTP3 中会支持此功能。  
  
 由于外部表的数据不在设备上，因此它不受 PolyBase 控制，可以随时由外部进程进行更改或删除。 因此，针对外部表的查询结果不保证具有确定性。 相同查询可能会在每次针对外部表运行时返回不同结果。 同样，如果外部数据已删除或重定位，则查询可能会失败。  
  
 可以创建各自引用不同外部数据源的多个外部表。 但是，如果同时针对不同 Hadoop 数据源运行查询，则每个 Hadoop 源都必须使用相同的“hadoop 连接”服务器配置设置。 例如，不能同时针对 Cloudera Hadoop 群集和 Hortonworks Hadoop 群集运行查询，因为这些群集使用不同的配置设置。 有关配置设置和受支持的组合，请参阅 [PolyBase 连接配置 (Transact-SQL)](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md)。  
  
 外部表上仅允许使用以下这些数据定义语言 (DDL) 语句：  
  
-   CREATE TABLE 和 DROP TABLE  
  
-   CREATE STATISTICS 和 DROP STATISTICS  
注意：Azure SQL 数据库中不支持外部表上的 CREATE 和 DROP STATISTICS。 
  
-   CREATE VIEW 和 DROP VIEW  
  
 不支持构造和操作：  
  
-   外部表列上的 DEFAULT 约束  
  
-   删除、插入和更新的数据操作语言 (DML) 操作  
  
 查询限制：  
  
 运行 32 个并发 PolyBase 查询时，每个文件夹中 PolyBase 最多可使用 33000 个文件。 此最大数量包括每个 HDFS 文件夹中的文件和子文件夹。 如果并发程度小于 32，用户可以针对 HDFS 中包含超过 33000 个文件的文件夹运行 PolyBase 查询。 建议保持外部文件路径简短，并且每个 HDFS 文件夹不超过 30000 个文件。 当引用太多文件时，可能会发生 Java 虚拟机 (JVM) 内存不足异常。  

表宽度限制：SQL Server 2016 中的 PolyBase 基于表定义中单个有效行的最大大小，具有 32KB 的行宽度限制。 如果列架构的总和大于 32KB，则 PolyBase 无法查询数据。 

在 SQL 数据仓库中，此限制已提高到 1MB。


## <a name="locking"></a>锁定  
 SCHEMARESOLUTION 对象上的共享锁。  
  
## <a name="security"></a>Security  
 外部表的数据文件存储在 Hadoop 或 Azure blob 存储中。 这些数据文件由你自己的进程进行创建和管理。 由你负责管理外部数据的安全。  
  
## <a name="examples"></a>示例  
  
### <a name="a-create-an-external-table-with-data-in-text-delimited-format"></a>A. 创建外部表，其中包含采用带分隔符的文本格式的数据。  
 此示例演示创建包含采用带分隔符的文本文件设置格式的数据的外部表所需的所有步骤。 它定义外部数据源 mydatasource 和外部文件格式 myfileformat。 这些数据库级别对象随后会在 CREATE EXTERNAL TABLE 语句中进行引用。 有关详细信息，请参阅 [CREATE EXTERNAL DATA SOURCE (Transact-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md) 和 [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](../../t-sql/statements/create-external-file-format-transact-sql.md)。  
  
```  
  
CREATE EXTERNAL DATA SOURCE mydatasource  
WITH (  
    TYPE = HADOOP,  
    LOCATION = 'hdfs://xxx.xxx.xxx.xxx:8020'  
)  
  
CREATE EXTERNAL FILE FORMAT myfileformat  
WITH (  
    FORMAT_TYPE = DELIMITEDTEXT,   
    FORMAT_OPTIONS (FIELD_TERMINATOR ='|')  
);  
  
CREATE EXTERNAL TABLE ClickStream (   
    url varchar(50),  
    event_date date,  
    user_IP varchar(50)  
)  
WITH (  
        LOCATION='/webdata/employee.tbl',  
        DATA_SOURCE = mydatasource,  
        FILE_FORMAT = myfileformat  
    )  
;  
  
```  
  
### <a name="b-create-an-external-table-with-data-in-rcfile-format"></a>B. 创建外部表，其中包含采用 RCFile 格式的数据。  
 此示例演示创建包含格式为 RCFile 的数据的外部表所需的所有步骤。 它定义外部数据源 mydatasource_rc 和外部文件格式 myfileformat_rc。 这些数据库级别对象随后会在 CREATE EXTERNAL TABLE 语句中进行引用。 有关详细信息，请参阅 [CREATE EXTERNAL DATA SOURCE (Transact-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md) 和 [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](../../t-sql/statements/create-external-file-format-transact-sql.md)。  
  
```  
  
CREATE EXTERNAL DATA SOURCE mydatasource_rc  
WITH (  
    TYPE = HADOOP,  
    LOCATION = 'hdfs://xxx.xxx.xxx.xxx:8020'  
)  
  
CREATE EXTERNAL FILE FORMAT myfileformat_rc  
WITH (  
    FORMAT_TYPE = RCFILE,  
    SERDE_METHOD = 'org.apache.hadoop.hive.serde2.columnar.LazyBinaryColumnarSerDe'  
)  
;  
  
CREATE EXTERNAL TABLE ClickStream_rc (   
    url varchar(50),  
    event_date date,  
    user_ip varchar(50)  
)  
WITH (  
        LOCATION='/webdata/employee_rc.tbl',  
        DATA_SOURCE = mydatasource_rc,  
        FILE_FORMAT = myfileformat_rc  
    )  
;  
  
```  
  
### <a name="c-create-an-external-table-with-data-in-orc-format"></a>C. 创建外部表，其中包含采用 ORC 格式的数据。  
 此示例演示创建包含格式为 ORC 的数据的外部表所需的所有步骤。 它定义外部数据源 mydatasource_orc 和外部文件格式 myfileformat_orc。 这些数据库级别对象随后会在 CREATE EXTERNAL TABLE 语句中进行引用。 有关详细信息，请参阅 [CREATE EXTERNAL DATA SOURCE (Transact-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md) 和 [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](../../t-sql/statements/create-external-file-format-transact-sql.md)。  
  
```  
  
CREATE EXTERNAL DATA SOURCE mydatasource_orc  
WITH (  
    TYPE = HADOOP,  
    LOCATION = 'hdfs://xxx.xxx.xxx.xxx:8020'  
)  
  
CREATE EXTERNAL FILE FORMAT myfileformat_orc  
WITH (  
    FORMAT = ORC,  
    COMPRESSION = 'org.apache.hadoop.io.compress.SnappyCodec'  
)  
;  
  
CREATE EXTERNAL TABLE ClickStream_orc (   
    url varchar(50),  
    event_date date,  
    user_ip varchar(50)  
)  
WITH (  
        LOCATION='/webdata/',  
        DATA_SOURCE = mydatasource_orc,  
        FILE_FORMAT = myfileformat_orc  
    )  
;  
  
```  
  
### <a name="d-querying-hadoop-data"></a>D. 查询 Hadoop 数据  
 Clickstream 是连接到 Hadoop 群集上带分隔符的文本文件 employee.tbl 的外部表。 下面的查询看上去如同针对标准表的查询。 但是，此查询从 Hadoop 检索数据，然后计算结果。  
  
```  
SELECT TOP 10 (url) FROM ClickStream WHERE user_ip = 'xxx.xxx.xxx.xxx'  
;  
```  
  
### <a name="e-join-hadoop-data-with-sql-data"></a>E. 将 Hadoop 数据与 SQL 数据联接  
 此查询看上去如同两个 SQL 表上的标准 JOIN。 区别在于，PolyBase 从 Hadoop 检索 Clickstream 数据，然后将它联接到 UrlDescription 表。 一个表是外部表，另一个表是标准 SQL 表。  
  
```  
SELECT url.description  
FROM ClickStream cs  
JOIN UrlDescription url ON cs.url = url.name  
WHERE cs.url = 'msdn.microsoft.com'  
;  
```  
  
### <a name="f-import-data-from-hadoop-into-a-sql-table"></a>F. 将数据从 Hadoop 导入 SQL 表中  
 此示例创建新 SQL 表 ms_user，它永久存储在标准 SQL 表 user 与外部表 ClickStream 之间进行联接的结果。  
  
```  
SELECT DISTINCT user.FirstName, user.LastName  
INTO ms_user  
FROM user INNER JOIN (  
    SELECT * FROM ClickStream WHERE cs.url = 'www.microsoft.com'  
    ) AS ms_user  
ON user.user_ip = ms.user_ip  
;  
  
```  
  
### <a name="g-create-an-external-table-for-a-sharded-data-source"></a>G. 为分片数据源创建外部表  
 此示例使用 SCHEMA_NAME 和 OBJECT_NAME 子句将远程 DMV 重映射到外部表。  
  
```  
CREATE EXTERNAL TABLE [dbo].[all_dm_exec_requests]([session_id] smallint NOT NULL,  
  [request_id] int NOT NULL,  
  [start_time] datetime NOT NULL,   
  [status] nvarchar(30) NOT NULL,  
  [command] nvarchar(32) NOT NULL,  
  [sql_handle] varbinary(64),  
  [statement_start_offset] int,  
  [statement_end_offset] int,  
  [cpu_time] int NOT NULL)  
WITH  
(  
  DATA_SOURCE = MyExtSrc,  
  SCHEMA_NAME = 'sys',  
  OBJECT_NAME = 'dm_exec_requests',  
  DISTRIBUTION=ROUND_ROBIN  
);   
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] 和 [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="h-importing-data-from-adls-into-azure-includessdwincludesssdw-mdmd"></a>H. 将数据从 ADLS 导入 Azure [!INCLUDE[ssDW](../../includes/ssdw-md.md)]  
 
  
```  

-- These values come from your Azure Active Directory Application used to authenticate to ADLS
CREATE DATABASE SCOPED CREDENTIAL ADLUser 
WITH IDENTITY = '<clientID>@\<OAuth2.0TokenEndPoint>',
SECRET = '<KEY>' ;


CREATE EXTERNAL DATA SOURCE AzureDataLakeStore
WITH (TYPE = HADOOP,
      LOCATION = 'adl://pbasetr.azuredatalakestore.net'
)



CREATE EXTERNAL FILE FORMAT TextFileFormat 
WITH
(
    FORMAT_TYPE = DELIMITEDTEXT 
    , FORMAT_OPTIONS ( FIELDTERMINATOR = '|' 
                     , STRINGDELIMITER = '' 
                     , DATEFORMAT = 'yyyy-MM-dd HH:mm:ss.fff' 
                     , USETYPE_DEFAULT = FALSE 
                     ) 
)


CREATE EXTERNAL TABLE [dbo].[DimProductexternal] 
( [ProductKey] [int] NOT NULL, 
  [ProductLabel] nvarchar NULL, 
  [ProductName] nvarchar NULL ) 
WITH
(
    LOCATION='/DimProduct/' , 
    DATA_SOURCE = AzureDataLakeStore , 
    FILE_FORMAT = TextFileFormat , 
    REJECT_TYPE = VALUE ,
    REJECT_VALUE = 0
) ;


CREATE TABLE [dbo].[DimProduct] 
WITH (DISTRIBUTION = HASH([ProductKey] ) ) 
AS SELECT * FROM 
[dbo].[DimProduct_external] ; 
     
```  
  
### <a name="i-join-external-tables"></a>I. 联接外部表  
  
```  
SELECT url.description  
FROM ClickStream cs  
JOIN UrlDescription url ON cs.url = url.name  
WHERE cs.url = 'msdn.microsoft.com'  
;  
```  
  
### <a name="j-join-hdfs-data-with-pdw-data"></a>J. 将 HDFS 数据与 PDW 数据联接  
  
```  
SELECT cs.user_ip FROM ClickStream cs  
JOIN User u ON cs.user_ip = u.user_ip  
WHERE cs.url = 'www.microsoft.com'  
;  
  
```  
  
### <a name="k-import-row-data-from-hdfs-into-a-distributed-pdw-table"></a>K. 将行数据从 HDFS 导入分布式 PDW 表  
  
```  
CREATE TABLE ClickStream_PDW  
WITH ( DISTRIBUTION = HASH (url) )  
AS SELECT url, event_date, user_ip FROM ClickStream  
;  
```  
  
### <a name="l-import-row-data-from-hdfs-into-a-replicated-pdw-table"></a>L. 将行数据从 HDFS 导入复制 PDW 表  
  
```  
CREATE TABLE ClickStream_PDW  
WITH ( DISTRIBUTION = REPLICATE )  
AS SELECT url, event_date, user_ip   
FROM ClickStream  
;  
```  
  
## <a name="see-also"></a>另请参阅  
 [常见元数据查询示例 (SQL Server PDW)](http://msdn.microsoft.com/en-us/733fc99b-b9f6-4a29-b085-a1bd4f09f2ed)   
 [CREATE EXTERNAL DATA SOURCE (Transact-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md)   
 [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](../../t-sql/statements/create-external-file-format-transact-sql.md)   
 [CREATE EXTERNAL TABLE AS SELECT (Transact-SQL)](../../t-sql/statements/create-external-table-as-select-transact-sql.md)   
 [CREATE TABLE AS SELECT（Azure SQL 数据仓库）](../../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)  
  
  



