---
title: "CREATE EXTERNAL TABLE (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE_EXTERNAL_TABLE
- CREATE EXTERNAL TABLE
- PolyBase, T-SQL
dev_langs: TSQL
helpviewer_keywords:
- External
- External, table create
- PolyBase, external table
ms.assetid: 6a6fd8fe-73f5-4639-9908-2279031abdec
caps.latest.revision: "30"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 802122cb7c0902c731b0fcc7d8522901ad7ea044
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="create-external-table-transact-sql"></a>CREATE EXTERNAL TABLE (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  创建引用的 Hadoop 群集或 Azure blob 存储中存储的数据的 PolyBase 外部表。 此外可以用于创建外部表的[弹性数据库查询](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-overview/)。  
  
 使用外部表设置为：  
  
-   查询 Hadoop 或 Azure blob 存储数据和[!INCLUDE[tsql](../../includes/tsql-md.md)]语句。  
  
-   导入和存储数据从 Hadoop 或 Azure blob 存储到你[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库。  
  
-   使用弹性数据库创建用于外部表  
     查询。  
     
- 导入并将从 Azure 数据湖存储的数据存储到 Azure SQL 数据仓库
  
 另请参阅[创建外部数据源 &#40;Transact SQL &#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)和[DROP EXTERNAL TABLE &#40;Transact SQL &#41;](../../t-sql/statements/drop-external-table-transact-sql.md).  
  
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
    | REJECT_TYPE = value | percentage  
    | REJECT_VALUE = reject_value  
    | REJECT_SAMPLE_VALUE = reject_sample_value  
  
}  
```  
  
## <a name="arguments"></a>参数  
 *database_name* 。 [schema_name]。 |schema_name。 ] *table_name*  
 一个到三个部分组成的要创建的表的名称。 为外部表，只是表元数据存储在 SQL 中以及有关文件和或者是在 Hadoop 或 Azure blob 存储中引用的文件夹的基本统计信息。 移动实际数据或将其存储在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  
  
 \<column_definition > [，... *n*  ] CREATE EXTERNAL TABLE 允许一个或多个列定义。 CREATE EXTERNAL TABLE 和 CREATE TABLE 可以用于相同的语法定义列。 与此异常，不能使用外部表上的默认约束。 有关列定义和其数据类型的完整详细信息，请参阅[CREATE TABLE &#40;Transact SQL &#41;](../../t-sql/statements/create-table-transact-sql.md)和[Azure SQL 数据库上的创建表](http://msdn.microsoft.com/library/d53c529a-1d5f-417f-9a77-64ccc6eddca1)。  
  
 列定义中，包括数据类型和列数必须与匹配的外部文件中的数据。 如果存在不匹配，在查询的实际数据时，将拒绝文件行。  
  
 对于引用外部数据源中的文件的外部表，列和类型定义必须映射到外部文件的确切架构。 定义引用 Hadoop/Hive 中存储的数据的数据类型，使用 SQL 和 Hive 数据类型之间的以下映射，然后选择从它时，强制转换为 SQL 数据类型的类型。 类型包括配置单元的所有版本，除非另有说明。  
  
|SQL 数据类型|.NET 数据类型|Hive 数据类型|Hadoop/Java 数据类型|注释|  
|-------------------|--------------------|--------------------|----------------------------|--------------|  
|tinyint|Byte|tinyint|ByteWritable|对于无符号的数字。|  
|smallint|Int16|smallint|ShortWritable||  
|int|Int32|int|IntWritable||  
|bigint|Int64|bigint|LongWritable||  
|bit|Boolean|boolean|BooleanWritable||  
|float|双精度|double|DoubleWritable||  
|real|Single|float|FloatWritable||  
|money|Decimal|double|DoubleWritable||  
|smallmoney|Decimal|double|DoubleWritable||  
|nchar|字符串<br /><br /> Char]|string|text||  
|nvarchar|字符串<br /><br /> Char]|string|Text||  
|char|字符串<br /><br /> Char]|string|Text||  
|varchar|字符串<br /><br /> Char]|string|Text||  
|binary|Byte[]|binary|BytesWritable|适用于 Hive 0.8 及更高版本。|  
|varbinary|Byte[]|binary|BytesWritable|适用于 Hive 0.8 及更高版本。|  
|date|DateTime|timestamp|TimestampWritable||  
|smalldatetime|DateTime|timestamp|TimestampWritable||  
|datetime2|DateTime|timestamp|TimestampWritable||  
|datetime|DateTime|timestamp|TimestampWritable||  
|time|TimeSpan|timestamp|TimestampWritable||  
|decimal|Decimal|decimal|BigDecimalWritable|适用于 Hive0.11 和更高版本。|  
  
 位置 = '*folder_or_filepath*  
 在 Hadoop 或 Azure blob 存储中指定文件夹或文件路径和实际数据的文件名称。 从根文件夹中; 开始的位置根文件夹是外部数据源中指定的数据位置。  
  
 如果你指定要为文件夹位置，从外部表中选择的 PolyBase 查询将检索文件从文件夹和所有子文件夹。 一样 Hadoop，PolyBase 不返回隐藏的文件夹。 它也不返回的文件的文件名称开头的下划线 (_) 或句点 （.）。  
  
 在此示例中，如果位置 ='/ webdata /'，PolyBase 查询将从 mydata.txt 和 mydata2.txt 返回行。  它不会返回 mydata3.txt，因为它是隐藏文件夹的子文件夹。 它不会返回 _hidden.txt，因为它是一个隐藏的文件。  
  
 ![外部表的递归数据](../../t-sql/statements/media/aps-polybase-folder-traversal.png "外部表的递归数据")  
  
 若要更改默认值和只读取从根文件夹，请将属性设置\<polybase.recursive.traversal > 为 'false' core-site.xml 配置文件中。 此文件位于`<SqlBinRoot>\Polybase\Hadoop\Conf with SqlBinRoot the bin root of SQl Server`。 例如， `C:\\Program Files\\Microsoft SQL Server\\MSSQL13.XD14\\MSSQL\\Binn`。  
  
 DATA_SOURCE = *external_data_source_name*  
 指定包含外部数据的位置的外部数据源的名称。 此位置是 Hadoop 或 Azure blob 存储。 若要创建外部数据源，使用[CREATE EXTERNAL DATA SOURCE &#40;Transact SQL &#41;](../../t-sql/statements/create-external-data-source-transact-sql.md).  
  
 FILE_FORMAT = *external_file_format_name*  
 指定将存储的外部数据的文件类型和压缩方法的外部文件格式对象的名称。 若要创建外部文件格式，使用[CREATE EXTERNAL FILE FORMAT &#40;Transact SQL &#41;](../../t-sql/statements/create-external-file-format-transact-sql.md).  
  
 拒绝选项  
 你可以指定拒绝参数，以确定 PolyBase 如何处理*脏*记录它从外部数据源的检索。 数据记录被视为脏是否它实际数据类型或列数与外部表的列定义不匹配。  
  
 当你不指定或更改拒绝值时，PolyBase 将使用默认值。 使用 CREATE EXTERNAL TABLE 语句创建外部表时，作为其他元数据存储的拒绝参数此信息。   在将来的 SELECT 语句或选择到 SELECT 语句从外部表中选择数据，PolyBase 将使用拒绝选项来确定的数值或百分比的实际查询在失败之前可以被拒绝的行。 实例时都提供 SQL Server 登录名。 该查询将返回 （部分） 结果，直到超出拒绝阈值;然后失败并出现相应的错误消息。  
  
 REJECT_TYPE =**值**| 百分比  
 阐明了是否 REJECT_VALUE 选项指定为文字值或百分比。  
  
 值  
 REJECT_VALUE 是文本值，而非百分比。 PolyBase 查询会失败的被拒绝的行数超过时*reject_value*。  
  
 例如，如果 REJECT_VALUE = 5 和 REJECT_TYPE = value，PolyBase SELECT 查询将失败后 5 行已被拒绝。  
  
 百分比  
 REJECT_VALUE 为百分比，而非文本值。 PolyBase 查询会失败时*百分比*的失败的行超过了*reject_value*。 按时间间隔计算失败行百分比。  
  
 REJECT_VALUE = *reject_value*  
 指定的值或的查询在失败之前可以被拒绝的行的百分比。  
  
 向 reject_type = value， *reject_value*必须是介于 0 和 2147483647 之间的整数。  
  
 向 reject_type = 百分比， *reject_value*必须是介于 0 和 100 之间的浮点数。  
  
 REJECT_SAMPLE_VALUE = *reject_sample_value*  
 此属性是必选项时指定 REJECT_TYPE = 百分比。 它确定要尝试检索在 PolyBase 重新计算的被拒绝的行百分比之前的行数。  
  
 *Reject_sample_value*参数必须是介于 0 和 2147483647 之间的整数。  
  
 例如，如果 REJECT_SAMPLE_VALUE = 1000，它已尝试从外部数据文件导入 1000年行后，PolyBase 将计算失败行百分比。 如果失败的行的百分比小于*reject_value*，PolyBase 将尝试检索另一个 1000年行。 它将继续在导入每个其他的 1000年行次尝试后重新计算失败行百分比。  
  
> [!NOTE]  
>  由于 PolyBase 间隔计算失败行百分比，失败的行的实际百分比可能会超过*reject_value*。  
  
 例如：  
  
 此示例演示三个拒绝选项如何相互交互。 例如，如果 REJECT_TYPE = 百分比，REJECT_VALUE = 30 和 REJECT_SAMPLE_VALUE = 100，可能出现以下方案：  
  
-   PolyBase 尝试检索的前 100 行;25 失败，而且 75 成功。  
  
-   失败行百分比将计算为 25%，这小于 30%的拒绝值。 因此，PolyBase 将继续从外部数据源检索数据。  
  
-   PolyBase 尝试加载的下一步 100 行;这一次 25 成功，并且 75 失败。  
  
-   50%是重新计算失败行百分比。 失败的行的百分比超过 30%拒绝值。  
  
-   尝试返回前 200 行后，PolyBase 查询失败与拒绝的 50%的行。 请注意，已在 PolyBase 查询之前返回匹配的行检测已超过拒绝阈值。  
  
 分片的外部表选项  
 指定外部数据源 （SQL Server 数据源） 和一个用于分发方法[弹性数据库查询](https://azure.microsoft.com/documentation/articles/sql-database-elastic-query-overview/)。  
  
 DATA_SOURCE  
 数据存储在 Hadoop 文件系统中，Azure blob 存储，如外部数据源或[分片映射管理器](https://azure.microsoft.com/documentation/articles/sql-database-elastic-scale-shard-map-management/)。  
  
 SCHEMA_NAME  
 SCHEMA_NAME 子句提供的功能将外部表定义映射到远程数据库上不同架构中的表。 用于消除存在于本地和远程数据库的架构之间的歧义。  
  
 OBJECT_NAME  
 OBJECT_NAME 子句提供的功能将外部表定义映射到具有远程数据库上的不同名称的表。 用于消除之间存在于本地和远程数据库的对象名称的歧义。  
  
 分发  
 可选。 这只是仅对数据库的类型于包含 SHARD_MAP_MANAGER 必需的。 此参数控制表被视为分片表或复制的表。 与**SHARDED** (*列名*) 表，不同的表中的数据不重叠。 **复制**指定表的每个分片上具有相同的数据。 **ROUND_ROBIN**指示应用程序特定的方法用于将数据分布。  
  
## <a name="permissions"></a>Permissions  
 需要以下用户权限：  
  
-   **CREATE TABLE**  
  
-   **更改任意架构**  
  
-   **更改任何外部数据源**  
  
-   **更改任何外部文件格式**  

-   **控制数据库**
  
 请注意，创建外部数据源的登录名必须有权对外部数据源，位于 Hadoop 或 Azure blob 存储中读取和写入。  


 > [!IMPORTANT]  

>  ALTER ANY EXTERNAL DATA SOURCE 权限授予任何主体能够创建和修改任何外部数据源对象，并因此，它还授予访问数据库上的所有数据库范围凭据的功能。 此权限必须被视为高特权级别，并因此必须被授予到受信任的主体仅在系统中。

## <a name="error-handling"></a>错误处理  
 正在执行的 CREATE EXTERNAL TABLE 语句，PolyBase 尝试连接到外部数据源。 如果连接尝试失败，该语句将失败，并且将不会创建外部表。 可能需要一分钟或更命令失败，因为 PolyBase 重试之前最终查询失败的连接。  
  
## <a name="general-remarks"></a>一般备注  
 在即席查询应用场景，即选择从外部表，PolyBase 存储从临时表中的外部数据源检索的行。 查询完成后，PolyBase 中删除，并删除临时表。 任何永久数据不存储在 SQL 表。  
  
 与此相反，在导入方案中，即选择到从外部表，PolyBase 存储作为永久性 SQL 表中的数据从外部数据源检索的行。 在查询执行期间创建了新表，当 Polybase 检索外部数据。  
  
 PolyBase 可以将某些查询计算推送到 Hadoop 以提高查询性能。 这称为谓词下推。 若要启用此功能，指定 Hadoop 中的资源管理器位置选项[CREATE EXTERNAL DATA SOURCE &#40;Transact SQL &#41;](../../t-sql/statements/create-external-data-source-transact-sql.md).  
  
 你可以创建大量引用相同或不同的外部数据源的外部表。  
  
## <a name="limitations-and-restrictions"></a>限制和局限  
 在 CTP2，导出功能不支持，即永久存储到外部数据源的 SQL 数据。 此功能将受到在 CTP3 中可用。  
  
 为外部表的数据位于关闭设备，因为它不是受控制的 PolyBase，和可以更改或删除任何时候通过外部进程。 因此，针对外部表的 uery 结果并非一定要确定性。 相同的查询可以在每次对外部表运行此脚本返回不同的结果。 同样，如果外部数据被删除或重新定位在查询可能会失败。  
  
 你可以创建每个引用不同的外部数据源的多个外部表。 但是，如果你同时针对不同的 Hadoop 数据源运行查询，每个 Hadoop 源必须使用相同的 'hadoop connectivity' 服务器配置设置。 例如，你不能同时运行查询，针对 Cloudera Hadoop 群集和 Hortonworks Hadoop 群集因为这些使用不同的配置设置。 配置设置和受支持的组合，请参阅[PolyBase 连接配置 &#40;Transact SQL &#41;](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md).  
  
 外部表上允许仅这些数据定义语言 (DDL) 语句：  
  
-   CREATE TABLE 和 DROP TABLE  
  
-   创建统计信息和 DROP STATISTICS  
  
-   创建视图和删除视图  
  
 构造并不支持的操作：  
  
-   外部表中的列的默认约束  
  
-   数据操作语言 (DML) 操作的删除、 插入和更新  
  
 查询的限制：  
  
 PolyBase 可以使用每个文件夹的 33 k 文件最的多 32 个并发的 PolyBase 查询运行时。 此最大的数字包括每个 HDFS 文件夹中文件和子文件夹。 如果并发程度，小于 32 的用户可以对包含多个 33 k 文件的 HDFS 中的文件夹运行 PolyBase 查询。 我们建议你保持短的外部文件路径，并每个 HDFS 文件夹使用不超过 30 万个文件。 当被引用的文件太多，Java 虚拟机 (JVM) 内存不足异常可能会出现。  

表宽度限制： SQL Server 2016 中的 PolyBase 有行宽度限制为 32 KB 的表定义基于单个有效行的最大大小。 如果列架构的总和大于 32 KB，PolyBase 不能查询数据。 

在 SQL 数据仓库中，此限制已增加到 1 MB。


## <a name="locking"></a>锁定  
 共享 SCHEMARESOLUTION 对象上的锁。  
  
## <a name="security"></a>安全性  
 外部表的数据文件存储在 Hadoop 或 Azure blob 存储中。 这些数据文件创建和管理你自己的进程。 它由你负责管理的外部数据的安全。  
  
## <a name="examples"></a>示例  
  
### <a name="a-create-an-external-table-with-data-in-text-delimited-format"></a>A. 创建外部表包含数据采用文本分隔的格式。  
 此示例显示创建外部表具有格式文本分隔文件中数据所需的所有步骤。 它定义外部数据源*mydatasource*和外部文件格式*myfileformat*。 然后 CREATE EXTERNAL TABLE 语句中引用这些数据库级别对象。 有关详细信息，请参阅[CREATE EXTERNAL DATA SOURCE &#40;Transact SQL &#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)和[创建外部文件格式 &#40;Transact SQL &#41;](../../t-sql/statements/create-external-file-format-transact-sql.md).  
  
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
  
### <a name="b-create-an-external-table-with-data-in-rcfile-format"></a>B. RCFile 格式中的数据创建外部表。  
 此示例显示创建外部表具有格式 RCFiles 数据所需的所有步骤。 它定义外部数据源*mydatasource_rc*和外部文件格式*myfileformat_rc*。 然后 CREATE EXTERNAL TABLE 语句中引用这些数据库级别对象。 有关详细信息，请参阅[CREATE EXTERNAL DATA SOURCE &#40;Transact SQL &#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)和[创建外部文件格式 &#40;Transact SQL &#41;](../../t-sql/statements/create-external-file-format-transact-sql.md).  
  
```  
  
CREATE EXTERNAL DATA SOURCE mydatasource_rc  
WITH (  
    TYPE = HADOOP,  
    LOCATION = 'hdfs://xxx.xxx.xxx.xxx:8020'  
)  
  
CREATE EXTERNAL FILE FORMAT myfileformat_rc  
WITH (  
    FORMAT = RCFILE,  
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
  
### <a name="c-create-an-external-table-with-data-in-orc-format"></a>C. 使用 ORC 格式的数据创建外部表。  
 此示例显示创建外部表具有作为 ORC 文件格式数据所需的所有步骤。 它定义外部数据源 mydatasource_orc 和外部文件格式 myfileformat_orc。 然后 CREATE EXTERNAL TABLE 语句中引用这些数据库级别对象。 有关详细信息，请参阅[CREATE EXTERNAL DATA SOURCE &#40;Transact SQL &#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)和[创建外部文件格式 &#40;Transact SQL &#41;](../../t-sql/statements/create-external-file-format-transact-sql.md).  
  
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
 点击流是连接到 employee.tbl 分隔符的文本文件的 Hadoop 群集上的外部表。 下面的查询只是类似于针对标准表的查询。 但是，此查询从 Hadoop 检索数据，然后计算多次。  
  
```  
SELECT TOP 10 (url) FROM ClickStream WHERE user_ip = 'xxx.xxx.xxx.xxx'  
;  
```  
  
### <a name="e-join-hadoop-data-with-sql-data"></a>E. 加入 Hadoop 数据和 SQL 数据  
 此查询会在两个 SQL 表一样标准联接。 区别是 PolyBase 从 Hadoop 检索点击流数据，然后将其联接到 UrlDescription 表。 一个表是一个外部表，另一个是标准的 SQL 表。  
  
```  
SELECT url.description  
FROM ClickStream cs  
JOIN UrlDescription url ON cs.url = url.name  
WHERE cs.url = 'msdn.microsoft.com'  
;  
```  
  
### <a name="f-import-data-from-hadoop-into-a-sql-table"></a>F. 将数据从 Hadoop 导入 SQL 表  
 此示例将创建新的 SQL 表 ms_user 永久存储之间的标准的 SQL 表的联接的结果*用户*和外部表*点击流*。  
  
```  
SELECT DISTINCT user.FirstName, user.LastName  
INTO ms_user  
FROM user INNER JOIN (  
    SELECT * FROM ClickStream WHERE cs.url = 'www.microsoft.com'  
    ) AS ms_user  
ON user.user_ip = ms.user_ip  
;  
  
```  
  
### <a name="g-create-an-external-table-for-a-sharded-data-source"></a>G. 创建外部表的分片的数据源  
 此示例重新映射到外部表使用 SCHEMA_NAME 和 OBJECT_NAME 子句远程 DMV。  
  
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
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>示例：[!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="h-importing-data-from-adls-into-azure-includessdwincludesssdw-mdmd"></a>H. 将数据从 ADLS 导入 Azure[!INCLUDE[ssDW](../../includes/ssdw-md.md)]  
 
  
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
WITH ( FORMATTYPE = DELIMITEDTEXT 
     , FORMATOPTIONS ( FIELDTERMINATOR = '|' 
                     , STRINGDELIMITER = '' 
                     , DATEFORMAT = 'yyyy-MM-dd HH:mm:ss.fff' 
                     , USETYPE_DEFAULT = FALSE 
                     ) 
    )


CREATE EXTERNAL TABLE [dbo].[DimProductexternal] 
( [ProductKey] [int] NOT NULL, 
  [ProductLabel] nvarchar NULL, 
  [ProductName] nvarchar NULL ) 
WITH ( LOCATION='/DimProduct/' , 
       DATA_SOURCE = AzureDataLakeStore , 
       FILE_FORMAT = TextFileFormat , 
       REJECT_TYPE = VALUE ,
       REJECT_VALUE = 0 ) ;


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
  
### <a name="j-join-hdfs-data-with-pdw-data"></a>J. 加入 HDFS 数据与 PDW 数据  
  
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
  
### <a name="l-import-row-data-from-hdfs-into-a-replicated-pdw-table"></a>L. 从 HDFS 的行数据导入到复制的 PDW 表  
  
```  
CREATE TABLE ClickStream_PDW  
WITH ( DISTRIBUTION = REPLICATE )  
AS SELECT url, event_date, user_ip   
FROM ClickStream  
;  
```  
  
## <a name="see-also"></a>另请参阅  
 [常见的元数据查询示例 (SQL Server PDW)](http://msdn.microsoft.com/en-us/733fc99b-b9f6-4a29-b085-a1bd4f09f2ed)   
 [CREATE EXTERNAL DATA SOURCE (Transact-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md)   
 [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](../../t-sql/statements/create-external-file-format-transact-sql.md)   
 [创建外部 TABLE AS SELECT &#40;Transact SQL &#41;](../../t-sql/statements/create-external-table-as-select-transact-sql.md)   
 [创建 TABLE AS SELECT &#40;Azure SQL 数据仓库 &#41;](../../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)  
  
  



