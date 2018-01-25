---
title: "创建外部文件格式 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 12/08/2017
ms.prod: sql-non-specified
ms.prod_service: sql-data-warehouse, pdw, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE EXTERNAL FILE FORMAT
- CREATE_EXTERNAL_FILE_FORMAT
dev_langs: TSQL
helpviewer_keywords:
- External
- External, file format
- PolyBase, external file format
ms.assetid: abd5ec8c-1a0e-4d38-a374-8ce3401bc60c
caps.latest.revision: "25"
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: ab389a5c811f915ff497057a5daf12374f1cedb7
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="create-external-file-format-transact-sql"></a>创建外部文件格式 (Transact SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  创建存储在 Hadoop、 Azure blob 存储或 Azure 数据湖存储的外部数据的 PolyBase 外部文件格式定义。 创建外部文件格式是用于创建 PolyBase 外部表的先决条件。 通过创建外部文件格式，你可以指定所引用的外部表数据的实际布局。  
  
 PolyBase 支持以下文件格式：
  
-   带分隔符的文本  
  
-   Hive RCFile  
  
-   Hive ORC
  
-   Parquet  
  
 若要创建外部表，请参阅[CREATE EXTERNAL TABLE &#40;Transact SQL &#41;](../../t-sql/statements/create-external-table-transact-sql.md).
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法
  
```
-- Create an external file format for PARQUET files.  
CREATE EXTERNAL FILE FORMAT file_format_name  
WITH (  
    FORMAT_TYPE = PARQUET  
     [ , DATA_COMPRESSION = {  
        'org.apache.hadoop.io.compress.SnappyCodec'  
      | 'org.apache.hadoop.io.compress.GzipCodec'      }  
    ]);  
  
--Create an external file format for ORC files.  
CREATE EXTERNAL FILE FORMAT file_format_name  
WITH (  
    FORMAT_TYPE = ORC  
     [ , DATA_COMPRESSION = {  
        'org.apache.hadoop.io.compress.SnappyCodec'  
      | 'org.apache.hadoop.io.compress.DefaultCodec'      }  
    ]);  
  
--Create an external file format for RCFILE.  
CREATE EXTERNAL FILE FORMAT file_format_name  
WITH (  
    FORMAT_TYPE = RCFILE,  
    SERDE_METHOD = {  
        'org.apache.hadoop.hive.serde2.columnar.LazyBinaryColumnarSerDe'  
      | 'org.apache.hadoop.hive.serde2.columnar.ColumnarSerDe'  
    }  
    [ , DATA_COMPRESSION = 'org.apache.hadoop.io.compress.DefaultCodec' ]);  
  
--Create an external file format for DELIMITED TEXT files.  
CREATE EXTERNAL FILE FORMAT file_format_name  
WITH (  
    FORMAT_TYPE = DELIMITEDTEXT  
    [ , FORMAT_OPTIONS ( <format_options> [ ,...n  ] ) ]  
    [ , DATA_COMPRESSION = {  
           'org.apache.hadoop.io.compress.GzipCodec'  
         | 'org.apache.hadoop.io.compress.DefaultCodec'  
        }  
     ]);  
  
<format_options> ::=  
{  
    FIELD_TERMINATOR = field_terminator  
    | STRING_DELIMITER = string_delimiter  
    | DATE_FORMAT = datetime_format  
    | USE_TYPE_DEFAULT = { TRUE | FALSE } 
    | Encoding = {'UTF8' | 'UTF16'} 
}  
```  
  
## <a name="arguments"></a>参数  
 *file_format_name*  
 指定外部文件格式的名称。
  
 FORMAT_TYPE 指定外部数据的格式。
  
 PARQUET 指定 Parquet 格式。
  
 ORC  
 指定优化行纵栏表 (ORC) 格式。 此选项需要 Hive 0.11 或外部的 Hadoop 群集上更高版本。 在 Hadoop 中 ORC 文件格式提供更好的压缩和性能比 RCFILE 文件格式。
  
 RCFILE (结合 SERDE_METHOD = *SERDE_method*) 指定记录纵栏表文件格式 (RcFile)。 此选项需要你指定的 Hive 序列化程序和反序列化程序 (SerDe) 方法。 如果在 Hadoop 中使用 Hive/HiveQL 查询 RC 文件，此要求是相同的。 请注意，SerDe 方法是区分大小写。
  
 使用 PolyBase 支持两种 SerDe 方法指定 RCFile 示例。
  
-   FORMAT_TYPE = RCFILE, SERDE_METHOD = 'org.apache.hadoop.hive.serde2.columnar.LazyBinaryColumnarSerDe'
  
-   FORMAT_TYPE = RCFILE, SERDE_METHOD = 'org.apache.hadoop.hive.serde2.columnar.ColumnarSerDe'
  
 DELIMITEDTEXT 指定以文本格式使用列分隔符，也称为字段终止符。
  
 FIELD_TERMINATOR = *field_terminator*仅适用于带分隔符的文本文件。 字段终止符文本分隔文件中指定一个或多个标记每个字段 （列） 的末尾的字符。 默认值为管道字符 ꞌ | ꞌ。 要获得有保证的支持，我们建议使用一个或多个 ascii 字符。
  
  
 示例：  
  
-   FIELD_TERMINATOR = |  
  
-   FIELD_TERMINATOR =  
  
-   FIELD_TERMINATOR = ꞌ\tꞌ  
  
-   FIELD_TERMINATOR = ~ | ~  
  
 STRING_DELIMITER = *string_delimiter*  
 在文本分隔文件中指定的字符串类型的数据的字段终止符。 字符串分隔符的长度的一个或多个字符，并且用单引号括起来。 默认值为空字符串""。 要获得有保证的支持，我们建议使用一个或多个 ascii 字符。
 
  
 示例：  

-   STRING_DELIMITER ="

-   STRING_DELIMITER ="0x22"-双引号十六进制
  
-   STRING_DELIMITER = *  
  
-   STRING_DELIMITER = Ꞌ，Ꞌ  
  
-   STRING_DELIMITER ="0x7E0x7E"-两个颚化符 (例如，~ ~)
  
 日期\_格式 = *datetime_format*指定分隔的文本文件可能会出现的所有日期和时间数据的自定义格式。 如果源文件使用默认日期时间格式，则不需要此选项。 只有一个自定义 datetime 格式允许每个文件中。 不能指定每个文件的多个自定义 datetime 格式。 但是，你可以使用多个日期时间格式，如果每个外部表定义中其各自的数据类型的默认格式。

PolyBase 仅用于自定义日期格式将数据导入。 它不将数据写入到外部文件使用自定义格式。

 当 DATE_FORMAT 未指定或为空字符串时，PolyBase 将使用以下默认格式：
  
-   日期时间: yyyy-月-日 hh: mm:  
  
-   SmallDateTime: ' yyyy-月-日 hh: mm  
  
-   日期: ' yyyy-月-日  
  
-   DateTime2: ' yyyy-月-日 hh: mm:  
  
-   DateTimeOffset: ' yyyy-月-日 hh: mm:  
  
-   时间: hh: mm:  
  
 **示例日期格式**下表中。  
  
 有关表的说明：  
  
-   年、 月和日可以具有多种格式和订单。 下表仅显示**ymd**格式。 月可以有 1 个或 2 的数字，或者 3 个字符。 天可以有 1 或 2 个数字。 年份可具有 2 个或 4 位数。
  
-   毫秒 (fffffff) 不是必需的。
  
-   Am，pm (tt) 不是必需的。 默认值为 AM。
  
|日期类型|示例|Description|  
|---------------|-------------|-----------------|  
|DateTime|DATE_FORMAT = 'yyyy-MM-dd HH:mm:ss.fff'|除了年、 月和日，此日期格式包括 00-24 小时，00-59 分钟，00-59 秒和毫秒的 3 个数字。|  
|DateTime|DATE_FORMAT = yyyy-月-日 hh:mm:ss.ffftt|除了年、 月和日，此日期格式包括 00-12 小时，00-59 分钟，00-59 秒、 毫秒，和 AM，3 个数字 am，PM 或 pm。 |  
|SmallDateTime|DATE_FORMAT =  'yyyy-MM-dd HH:mm'|除了年、 月和日，此日期格式包括 00-23 小时数，00-59 分钟。|  
|SmallDateTime|DATE_FORMAT = yyyy-月-日 hh:mmtt|除了年、 月和日，此日期格式包括 00-11 时间的操作、 00-59 分钟，没有秒，和 AM、 am、 PM，或 pm。|  
|日期|DATE_FORMAT = yyyy-月-日|年、 月和日。 时间元素不是包含。|  
|日期|DATE_FORMAT = yyyy-MMM-'dd '|年、 月和日。 月被指定为 3 分钟，输入的值时，一项或年 1 月、 年 2 月、 日、 Apr、 可能、 六月、 七月、 日，9 月、 年 10 月、 年 11 月或年 12 月的字符串。|  
|datetime2|DATE_FORMAT = 'yyyy-MM-dd HH:mm:ss.fffffff'|除了年、 月和日，此日期格式包括 00-23 小时数，00-59 分钟，00-59 秒和毫秒的 7 位。|  
|datetime2|DATE_FORMAT = yyyy-月-日 hh:mm:ss.ffffffftt|除了年、 月和日，此日期格式包括 00-11 小时数，00-59 分钟，00-59 秒、 毫秒，和 AM 7 位 am，PM 或 pm。|  
|DateTimeOffset|DATE_FORMAT = 'yyyy-MM-dd HH:mm:ss.fffffff zzz'|除了年、 月和日，此日期格式包括 00-23 小时数，00-59 分钟，00-59 秒和毫秒为单位，和的时区偏移量作为输入文件中放置的 7 位`{+&#124;-}HH:ss`。 例如，而无需夏时制的洛杉矶以来节省了 8 小时后面 UTC，值为-08:00 输入文件中的指定洛杉矶的时区。|  
|DateTimeOffset|DATE_FORMAT = yyyy-月-日 hh:mm:ss.ffffffftt zzz|除了年、 月和日，此日期格式包括 00-11 小时数，00-59 分钟，00-59 秒、 毫秒、 （上午、 am、 PM，或下午），7 位和时区偏移量。 请参阅前一行中的说明。|  
|Time|DATE_FORMAT = 'HH:mm:ss'|没有日期值，仅 00-23 小时数，00-59 分钟和 00-59 秒。|  
  
 所有支持的日期格式：
  
|datetime|smalldatetime|date|datetime2|datetimeoffset|  
|--------------|-------------------|----------|---------------|--------------------|  
|[M[M]]M-[d]d-[yy]yy HH:mm:ss[.fff]|[M[M]]M-[d]d-[yy]yy HH:mm[:00]|[M[M]]M-[d]d-[yy]yy|[M[M]]M-[d]d-[yy]yy HH:mm:ss[.fffffff]|[M[M]]M-[d]d-[yy]yy HH:mm:ss[.fffffff] zzz|  
|[M[M]]M-[d]d-[yy]yy hh:mm:ss[.fff][tt]|[M[M]]M-[d]d-[yy]yy hh:mm[:00][tt]||[M[M]]M-[d]d-[yy]yy hh:mm:ss[.fffffff][tt]|[M[M]]M-[d]d-[yy]yy hh:mm:ss[.fffffff][tt] zzz|  
|[M[M]]M-[yy]yy-[d]d HH:mm:ss[.fff]|[M[M]]M-[yy]yy-[d]d HH:mm[:00]|[M[M]]M-[yy]yy-[d]d|[M[M]]M-[yy]yy-[d]d HH:mm:ss[.fffffff]|[M[M]]M-[yy]yy-[d]d HH:mm:ss[.fffffff] zzz|  
|[M[M]]M-[yy]yy-[d]d hh:mm:ss[.fff][tt]|[M [M]]M-[yy] yy-[d] d hh: mm [: 00] [tt]||[M[M]]M-[yy]yy-[d]d hh:mm:ss[.fffffff][tt]|[M[M]]M-[yy]yy-[d]d hh:mm:ss[.fffffff][tt] zzz|  
|[yy]yy-[M[M]]M-[d]d HH:mm:ss[.fff]|[yy]yy-[M[M]]M-[d]d HH:mm[:00]|[yy]yy-[M[M]]M-[d]d|[yy]yy-[M[M]]M-[d]d HH:mm:ss[.fffffff]|[yy]yy-[M[M]]M-[d]d HH:mm:ss[.fffffff]  zzz|  
|[yy]yy-[M[M]]M-[d]d hh:mm:ss[.fff][tt]|[yy] yy-[M [M]] M-[d] d hh: mm [: 00] [tt]||[yy]yy-[M[M]]M-[d]d hh:mm:ss[.fffffff][tt]|[yy]yy-[M[M]]M-[d]d hh:mm:ss[.fffffff][tt] zzz|  
|[yy]yy-[d]d-[M[M]]M HH:mm:ss[.fff]|[yy]yy-[d]d-[M[M]]M HH:mm[:00]|[yy]yy-[d]d-[M[M]]M|[yy]yy-[d]d-[M[M]]M HH:mm:ss[.fffffff]|[yy]yy-[d]d-[M[M]]M HH:mm:ss[.fffffff]  zzz|  
|[yy]yy-[d]d-[M[M]]M hh:mm:ss[.fff][tt]|[yy]yy-[d]d-[M[M]]M hh:mm[:00][tt]||[yy]yy-[d]d-[M[M]]M hh:mm:ss[.fffffff][tt]|[yy]yy-[d]d-[M[M]]M hh:mm:ss[.fffffff][tt] zzz|  
|[d]d-[M[M]]M-[yy]yy HH:mm:ss[.fff]|[d]d-[M[M]]M-[yy]yy HH:mm[:00]|[d]d-[M[M]]M-[yy]yy|[d]d-[M[M]]M-[yy]yy HH:mm:ss[.fffffff]|[d]d-[M[M]]M-[yy]yy HH:mm:ss[.fffffff] zzz|  
|[d]d-[M[M]]M-[yy]yy hh:mm:ss[.fff][tt]|[d]d-[M[M]]M-[yy]yy hh:mm[:00][tt]||[d]d-[M[M]]M-[yy]yy hh:mm:ss[.fffffff][tt]|[d]d-[M[M]]M-[yy]yy hh:mm:ss[.fffffff][tt] zzz|  
|[d]d-[yy]yy-[M[M]]M HH:mm:ss[.fff]|[d]d-[yy]yy-[M[M]]M HH:mm[:00]|[d]d-[yy]yy-[M[M]]M|[d]d-[yy]yy-[M[M]]M HH:mm:ss[.fffffff]|[d]d-[yy]yy-[M[M]]M HH:mm:ss[.fffffff]  zzz|  
|[d]d-[yy]yy-[M[M]]M hh:mm:ss[.fff][tt]|[d]d-[yy]yy-[M[M]]M hh:mm[:00][tt]||[d]d-[yy]yy-[M[M]]M hh:mm:ss[.fffffff][tt]|[d]d-[yy]yy-[M[M]]M hh:mm:ss[.fffffff][tt] zzz|  
  
 详细信息︰  
  
-   若要分隔月、 日和年的值，可以使用 –'，'/'，或。 '. 为简单起见，表使用仅 – 分隔符。
  
-   若要以文本格式指定月份，使用三个或多个字符。 月使用 1 或 2 个字符被解释为数字。
  
-   若要分隔时间值，请使用: 符号。
  
-   用方括号括起来的字母是可选的。
  
-   字母 tt 指定 [AM |PM | 是 | pm]。 AM 是默认设置。 当指定 tt 时，(hh) 的小时值必须在 0 到 12 范围内。
  
-   字母 zzz 指定系统的格式的当前时区的时区偏移量 {+ |-} HH:ss]。
  
 USE_TYPE_DEFAULT = {TRUE |**FALSE** } 指定如何处理缺失值分隔的文本文件中，当 PolyBase 从文本文件中检索数据。
  
 从文本文件中，检索数据的外部表定义中的相应列的数据类型使用默认值存储每个缺失值，则为 TRUE。 例如，将缺失值替换：  
  
-   如果列定义为数字列，则为 0。
  
-   空字符串""如果列是字符串列。
  
-   1900-01-01 如果列是日期列。
  
 FALSE 存储所有缺失值，则为 NULL。 通过使用带分隔符的文本文件中的单词 NULL 存储任何 NULL 值作为字符串 NULL 导入。
  
   编码 = {'UTF8' |UTF16} 中 Azure SQL 数据仓库、 PolyBase 可以读取 UTF8 和 UTF16 LE 编码带分隔符的文本文件。 在 SQL Server 和 PDW 中，PolyBase 不支持读取 UTF16 编码文件。
  
 DATA_COMPRESSION = *data_compression_method*指定外部数据的数据压缩方法。 如果不指定 DATA_COMPRESSION，默认值为未压缩的数据。
 若要正常工作，Gzip 压缩文件必须具有".gz"文件扩展名。
 
 DELIMITEDTEXT 格式类型支持这些压缩方法：
  
-   DATA COMPRESSION = 'org.apache.hadoop.io.compress.DefaultCodec'
  
-   DATA COMPRESSION = 'org.apache.hadoop.io.compress.GzipCodec'

 RCFILE 格式类型支持此压缩方法：
  
-   DATA COMPRESSION = 'org.apache.hadoop.io.compress.DefaultCodec'
  
 ORC 文件格式类型支持这些压缩方法：
  
-   DATA COMPRESSION = 'org.apache.hadoop.io.compress.DefaultCodec'
  
-   DATA COMPRESSION = 'org.apache.hadoop.io.compress.SnappyCodec'
  
 PARQUET 文件格式类型支持 folliwing 压缩方法：
  
-   DATA COMPRESSION = 'org.apache.hadoop.io.compress.GzipCodec'
  
-   DATA COMPRESSION = 'org.apache.hadoop.io.compress.SnappyCodec'
  
## <a name="permissions"></a>权限  
 需要 ALTER ANY EXTERNAL FILE FORMAT 权限。
  
## <a name="general-remarks"></a>一般备注
 数据库作用域中的外部文件格式是[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]。 服务器作用域中它是[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]。  
  
 格式选项都是可选项，并仅适用于带分隔符的文本文件。  
  
 当数据存储在压缩的格式之一时，PolyBase 首先在返回的数据记录之前解压缩数据。
  
## <a name="limitations-and-restrictions"></a>限制和局限
  
 Hadoop 的 LineRecordReader 必须支持行分隔符分隔文本文件中。 也就是说，它必须是 '\r'、 \n 或 \r\n。 这些分隔符不是用户可配置的。
  
 受支持的 SerDe 方法 RCFiles，进行组合和支持的数据压缩方法本文前面列出。 支持所有形式的组合。
  
 并发的 PolyBase 查询的最大数目为 32。 当运行 32 并发查询时，每个查询可以从外部文件位置读取 33,000 文件的最多。 根文件夹，并且每个子文件夹还为文件计数。 如果并发程度，小于 32 的外部文件位置可以包含拥有超过 33000 名的文件。
  
 对外部表中的文件数的限制，因此我们建议将小于 30000 文件存储在根和外部文件位置的子文件夹。 此外，我们建议你保留成数量较少的根目录下的子文件夹的数量。 当被引用的文件太多，Java 虚拟机的内存不足异常可能会出现。
  
  将数据导出到 Hadoop 或 Azure Blob 存储通过 PolyBase，仅将数据导出时，不列 names(metadata) CREATE EXTERNAL TABLE 命令中定义。

## <a name="locking"></a>锁定  
 外部文件格式对象上采用共享的锁。
  
## <a name="performance"></a>性能
 始终使用压缩的文件会作出权衡，即之间同时增加 CPU 使用率来压缩和解压缩数据的外部数据源和 SQL Server 之间传输更少的数据。
  
 Gzip 压缩文本文件不是可拆分的。 若要提高 Gzip 压缩的文本文件的性能，我们建议生成所有外部数据源中的同一目录中存储的多个文件。 这允许 PolyBase 来读取和使用多个读取器和解压缩进程解压缩数据的速度快。 理想的压缩的文件数是每个计算节点的数据读取器过程的最大数目。 在[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]，数据读取器进程的最大数目为每个节点在当前版本的 8。 在[!INCLUDE[ssSDW](../../includes/sssdw-md.md)]，每个节点的数据读取器进程的最大数因 SLO。 请参阅[加载模式和策略的 Azure SQL 数据仓库](https://blogs.msdn.microsoft.com/sqlcat/2016/02/06/azure-sql-data-warehouse-loading-patterns-and-strategies/)有关详细信息。  
  
## <a name="examples"></a>示例  
  
### <a name="a-create-a-delimitedtext-external-file-format"></a>A. 创建 DELIMITEDTEXT 外部文件格式  
 此示例将创建名为外部文件格式*textdelimited1*文本分隔文件。 格式列出这些选项\_选项指定应该使用竖线分隔文件中的字段 |。 文本文件也是使用 Gzip 编解码器压缩的。 如果数据\_压缩未指定，该文本文件为未压缩。
  
 对于带分隔符的文本文件，数据压缩方法可以是默认编解码器、 org.apache.hadoop.io.compress.DefaultCodec 或 Gzip 编解码器，org.apache.hadoop.io.compress.GzipCodec。
  
```  
CREATE EXTERNAL FILE FORMAT textdelimited1  
WITH (  
    FORMAT_TYPE = DELIMITEDTEXT,  
    FORMAT_OPTIONS (  
        FIELD_TERMINATOR = '|',  
        DATE_FORMAT = 'MM/dd/yyyy' ),  
    DATA_COMPRESSION = 'org.apache.hadoop.io.compress.GzipCodec'
);  
```  
  
### <a name="b-create-an-rcfile-external-file-format"></a>B. 创建 RCFile 外部文件格式  
 此示例为使用序列化/反序列化方法 org.apache.hadoop.hive.serde2.columnar.LazyBinaryColumnarSerDe RCFile 创建外部文件格式。 它还指定默认编解码器用于数据压缩方法。 如果不指定 DATA_COMPRESSION，默认为无压缩。
  
```  
CREATE EXTERNAL FILE FORMAT rcfile1  
WITH (  
    FORMAT_TYPE = RCFILE,  
    SERDE_METHOD = 'org.apache.hadoop.hive.serde2.columnar.LazyBinaryColumnarSerDe',  
    DATA_COMPRESSION = 'org.apache.hadoop.io.compress.DefaultCodec'  
);  
```  
  
### <a name="c-create-an-orc-external-file-format"></a>C. 创建 ORC 外部文件格式  
 此示例创建外部文件格式使用 org.apache.io.compress.SnappyCodec 数据压缩方法压缩的数据的 ORC 文件。 如果不指定 DATA_COMPRESSION，默认为无压缩。
  
```  
CREATE EXTERNAL FILE FORMAT orcfile1  
WITH (  
    FORMAT_TYPE = ORC,  
    DATA_COMPRESSION = 'org.apache.hadoop.io.compress.SnappyCodec'  
);  
```  
  
### <a name="d-create-a-parquet-external-file-format"></a>D. 创建 PARQUET 外部文件格式  
 此示例创建使用 org.apache.io.compress.SnappyCodec 数据压缩方法压缩的数据的 Parquet 文件外部文件格式。 如果不指定 DATA_COMPRESSION，默认为无压缩。  
  
```  
CREATE EXTERNAL FILE FORMAT parquetfile1  
WITH (  
    FORMAT_TYPE = PARQUET,  
    DATA_COMPRESSION = 'org.apache.hadoop.io.compress.SnappyCodec'  
);  
```  
  
## <a name="see-also"></a>另请参阅
 [CREATE EXTERNAL DATA SOURCE (Transact-SQL)](../../t-sql/statements/create-external-data-source-transact-sql.md)   
 [CREATE EXTERNAL TABLE (Transact-SQL)](../../t-sql/statements/create-external-table-transact-sql.md)   
 [创建外部 TABLE AS SELECT &#40;Transact SQL &#41;](../../t-sql/statements/create-external-table-as-select-transact-sql.md)   
 [创建 TABLE AS SELECT &#40;Azure SQL 数据仓库 &#41;](../../t-sql/statements/create-table-as-select-azure-sql-data-warehouse.md)   
 [sys.external_file_formats (Transact-SQL)](../../relational-databases/system-catalog-views/sys-external-file-formats-transact-sql.md)  
